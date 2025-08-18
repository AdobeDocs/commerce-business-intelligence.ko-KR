---
title: 견적 테이블
description: Quote 표로 작업하는 방법을 알아봅니다.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# 견적 테이블

`quote` 테이블(M1의 `sales_flat_quote`)에는 스토어에서 만든 모든 장바구니에 대한 레코드가 중단되었거나 구매로 변환되었는지 여부에 관계없이 들어 있습니다. 각 행은 하나의 장바구니를 나타냅니다. 이 테이블의 잠재적 크기 때문에 Adobe에서는 60일 이상 된 전환되지 않은 장바구니가 있는 경우와 같이 특정 기준이 충족되는 경우 레코드를 주기적으로 삭제할 것을 권장합니다.

>[!NOTE]
>
>`quote` 테이블에서 레코드를 삭제하지 않는 경우에만 중단된 이전 장바구니를 분석할 수 있습니다. 레코드를 삭제하면 데이터베이스에서 아직 제거되지 않은 장바구니만 표시됩니다.

## 일반 기본 열

| **열 이름** | **설명** |
|---|---|
| `base_currency_code` | `base_*` 필드(즉, `base_grand_total`, `base_subtotal` 등)에 캡처된 모든 값의 통화입니다. 이는 일반적으로 Commerce 스토어의 기본 통화를 반영합니다 |
| `base_grand_total` | 모든 세금, 배송 및 할인이 적용된 후 장바구니에 대해 고객에게 견적된 최종 가격입니다. 정확한 계산을 사용자 지정할 수 있지만 일반적으로 `base_grand_total`은(는) `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount`로 계산됩니다 |
| `base_subtotal` | 장바구니에 포함된 모든 항목의 총 상품 가치. 세금, 배송, 할인 등은 포함되지 않습니다 |
| `created_at` | UTC로 로컬에 저장된 장바구니의 생성 타임스탬프. [!DNL Commerce Intelligence]의 구성에 따라 이 타임스탬프가 데이터베이스 시간대와 다른 [!DNL Commerce Intelligence]의 보고 시간대로 변환될 수 있습니다. |
| `customer_email` | 장바구니를 만든 고객의 이메일 주소 |
| `customer_id` | 고객이 등록된 경우 `Foreign key`이(가) `customer_entity` 테이블에 연결되어 있습니다. `customer_entity.entity_id`에 참여하여 장바구니를 만든 사용자와 관련된 고객 특성을 확인하십시오. 장바구니가 게스트 체크아웃을 통해 만들어진 경우 이 필드는 `NULL`입니다. |
| `entity_id`(PK) | 테이블에 대한 고유 식별자로, Commerce 인스턴스 내의 다른 테이블에 대한 조인에 일반적으로 사용됩니다. |
| `is_active` | 고객이 장바구니를 만들고 아직 주문으로 전환하지 않은 경우 &quot;1&quot;을 반환하는 부울 필드. 변환된 장바구니 또는 관리자를 통해 만든 장바구니에 대해 &quot;0&quot;을 반환합니다. |
| `items_qty` | 장바구니에 포함된 모든 항목의 총 수량 합계 |
| `reserved_order_id` | `Foreign key`이(가) `sales_order` 테이블에 연결되어 있습니다. `sales_order.increment_id`에 참여하여 전환된 장바구니와 연결된 주문 세부 정보를 확인합니다. 전환된 주문과 연결되어 있지 않은 장바구니의 경우 `reserved_order_id`은(는) `NULL` 상태로 유지됩니다. |
| `store_id` | `Foreign key`이(가) `store` 테이블에 연결되어 있습니다. `store`에 참가합니다.장바구니와 연결된 Commerce 스토어 보기를 확인하는 `store_id` |

{style="table-layout:auto"}

## 공통 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Order date` | 전환된 장바구니의 주문 생성 날짜를 반영하는 타임스탬프. `quote.reserved_order_id`에 `sales_order.increment_id`을(를) 조인하고 `sales_order.created_at` 필드를 반환하여 계산됨 |
| `Seconds between cart creation and order` | 장바구니 생성과 주문 생성 사이의 경과 시간. `created_at`에서 `Order date`을(를) 빼서 계산했으며 정수로 반환됩니다. |
| `Seconds since cart creation` | 장바구니 생성일과 현재 사이의 경과 시간. 쿼리가 실행될 때 서버 타임스탬프에서 `created_at`을(를) 빼서 계산되며, 정수로 반환됩니다. 장바구니 나이를 식별하는 데 가장 일반적으로 사용됨 |
| `Store name` | 이 주문과 연계된 Commerce 스토어 이름. `quote.store_id`에 `store.store_id`을(를) 조인하고 `name` 필드를 반환하여 계산됨 |

{style="table-layout:auto"}

## 일반 지표

| **지표 이름** | **설명** | **구성** |
|---|---|---|
| `Number of abandoned carts` | 특정 &quot;포기&quot; 조건을 충족하는 장바구니 수 | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>필터:<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x. 여기서 &quot;x&quot;는 장바구니 만들기 이후 장바구니가 중단된 것으로 간주되는 경과 시간(초)에 해당합니다 |
| `Avg time to cart conversion` | 전환된 장바구니에 대한 장바구니 생성과 주문 생성 사이의 평균 시간 | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | 수익이 `base_grand_total` 필드로 정의되는 총 포기한 장바구니 잠재적 수익의 합계 | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>필터:<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x. 여기서 &quot;x&quot;는 장바구니 만들기 이후 장바구니가 중단된 것으로 간주되는 경과 시간(초)에 해당합니다 |

{style="table-layout:auto"}

## 외래 키 조인 경로

`customer_entity`

* `customer_entity` 테이블에 연결하여 장바구니를 만든 고객과 연결된 새 고객 수준 열을 만드십시오.
   * 경로: `quote.customer_id`(많음) => `customer_entity.entity_id`(하나)

`sales_order`

* `sales_order` 테이블에 연결하여 전환된 장바구니와 연결된 주문 세부 정보를 반환하는 열을 만드십시오.
   * 경로:`quote.reserved_order_id`(많음) => `sales_order.increment_id`(하나)

`store`

* `store` 테이블에 연결하여 장바구니와 연결된 Commerce 스토어와 관련된 세부 정보를 반환하는 열을 만듭니다.
   * 경로: `quote.store_id`(많음) => `store.store_id`(하나)
