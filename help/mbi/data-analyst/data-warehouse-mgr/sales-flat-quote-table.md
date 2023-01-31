---
title: 견적 테이블
description: 견적 테이블로 작업하는 방법을 알아봅니다.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# 견적 테이블

다음 `quote` 테이블 (`sales_flat_quote` m1)에는 스토어에서 생성된 모든 장바구니에 대한 레코드(포기 또는 구매로 변환되었는지 여부)가 포함되어 있습니다. 각 행은 하나의 장바구니를 나타냅니다. 이 테이블의 잠재적 크기로 인해 60일 이상 오래된 전환되지 않은 장바구니가 있는 경우와 같이 특정 기준이 충족되는 경우 레코드를 주기적으로 삭제하는 것이 좋습니다.

>[!NOTE]
>
>기록을 목록에서 삭제하지 않는 경우에만 기록 포기 카트를 분석할 수 있습니다 `quote` 테이블. 레코드를 삭제하는 경우, 데이터베이스에서 아직 제거되지 않은 장바구니만 볼 수 있습니다.

## 공통 기본 열

| **열 이름** | **설명** |
|---|---|
| `base_currency_code` | 캡처된 모든 값에 대한 통화 `base_*` 필드(즉, `base_grand_total`, `base_subtotal`, 등). 일반적으로 상거래 저장소의 기본 통화를 반영합니다 |
| `base_grand_total` | 모든 세금, 배송 및 할인이 적용된 후 장바구니에 대한 고객에게 견적 최종 가격입니다. 정확한 계산은 일반적으로 사용자 지정할 수 있지만 `base_grand_total` 는 `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | 장바구니에 포함된 모든 항목의 총 상품 값입니다. 세금, 배송, 할인 등은 포함되지 않습니다 |
| `created_at` | 장바구니의 생성 타임스탬프이며, 일반적으로 UTC에 로컬로 저장됩니다. 의 구성에 따라 [!DNL MBI]로 지정하는 경우 이 타임스탬프가 [!DNL MBI] 데이터베이스 시간대와 다른 |
| `customer_email` | 장바구니를 만든 고객의 이메일 주소입니다 |
| `customer_id` | `Foreign key` 관련 `customer_entity` 테이블(고객이 등록된 경우) 가입 대상 `customer_entity.entity_id` 를 클릭하여 장바구니를 만든 사용자와 연결된 고객 속성을 확인합니다. 게스트 체크아웃을 통해 장바구니를 만든 경우, 이 필드는 `NULL` |
| `entity_id` (PK) | 테이블의 고유 식별자이며, 상거래 인스턴스 내의 다른 테이블에 대한 조인에 일반적으로 사용됩니다 |
| `is_active` | 고객이 장바구니를 만들고 아직 주문으로 전환하지 않은 경우 &quot;1&quot;을 반환하는 부울 필드입니다. 전환된 장바구니 또는 관리자를 통해 생성된 장바구니에 대해 &quot;0&quot;을 반환합니다 |
| `items_qty` | 장바구니에 포함된 모든 항목의 총 수량 합계 |
| `reserved_order_id` | `Foreign key` 관련 `sales_order` 테이블. 가입 대상 `sales_order.increment_id` 를 입력하여 변환된 장바구니와 연관된 주문 세부 사항을 결정합니다. 변환된 주문과 연관되지 않은 카트의 경우 `reserved_order_id` 계속 `NULL` |
| `store_id` | `Foreign key` 관련 `store` 테이블. 가입 대상 `store`.`store_id` 장바구니와 연결된 상거래 스토어 보기를 확인하려면 |

{style=&quot;table-layout:auto&quot;}

## 일반적인 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Order date` | 전환된 장바구니에 대한 주문 생성 날짜를 반영하는 타임스탬프입니다. 가입으로 계산됨 `quote.reserved_order_id` to `sales_order.increment_id` 재방문 `sales_order.created_at` 필드 |
| `Seconds between cart creation and order` | 장바구니 만들기와 주문 작성 사이의 경과 시간입니다. 빼서 계산됨 `created_at` 변환 전: `Order date`: 초 단위의 정수 수로 반환됩니다 |
| `Seconds since cart creation` | 장바구니의 생성 날짜와 현재 사이의 경과 시간입니다. 빼서 계산됨 `created_at` 쿼리 실행 시 서버 타임스탬프에서 정수(초)로 반환됩니다. 가장 일반적으로 장바구니의 날짜를 식별하는 데 사용됩니다 |
| `Store name` | 이 주문과 연결된 상거래 저장소의 이름입니다. 가입으로 계산됨 `quote.store_id` to `store.store_id` 재방문 `name` 필드 |

{style=&quot;table-layout:auto&quot;}

## 일반 지표

| **지표 이름** | **설명** | **건설** |
|---|---|---|
| `Number of abandoned carts` | 특정 &quot;포기&quot; 조건을 충족하는 장바구니 수 | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>필터:<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x. 여기서 &quot;x&quot;는 장바구니를 포기한 것으로 간주되는 장바구니 작성 이후 경과된 시간(초)에 해당합니다 |
| `Avg time to cart conversion` | 변환된 장바구니에 대한 장바구니 생성과 주문 생성 사이의 평균 시간입니다 | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | 매출이 다음과 같이 정의된 총 포기한 장바구니 잠재적 수익의 합계 `base_grand_total` 필드 | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>필터:<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x. 여기서 &quot;x&quot;는 장바구니를 포기한 것으로 간주되는 장바구니 작성 이후 경과된 시간(초)에 해당합니다 |

{style=&quot;table-layout:auto&quot;}

## 외래 키 연결 경로

`customer_entity`

* 가입 대상 `customer_entity` 장바구니를 만든 고객과 연결된 새 고객 수준 열을 만드는 표입니다.
   * 경로: `quote.customer_id` (다) => `customer_entity.entity_id` (1)

`sales_order`

* 가입 대상 `sales_order` 변환된 장바구니와 관련된 주문 세부 사항을 반환하는 새 열을 만들 수 있습니다.
   * 경로:`quote.reserved_order_id` (다) => `sales_order.increment_id` (1)

`store`

* 가입 대상 `store` 장바구니와 연결된 상거래 스토어와 관련된 세부 사항을 반환하는 새 열을 만드는 표입니다.
   * 경로: `quote.store_id` (다) => `store.store_id` (1)
