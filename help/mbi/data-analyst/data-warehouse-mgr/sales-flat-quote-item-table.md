---
title: quote_item 테이블
description: quote_item 테이블을 사용하여 작업하는 방법을 알아봅니다.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# quote_item 테이블

`quote_item` 테이블(M1의 `sales_flat_quote_item`)에는 장바구니가 중단되었거나 구매로 전환되었는지에 관계없이 장바구니에 추가된 모든 항목에 대한 레코드가 포함되어 있습니다. 각 행은 하나의 장바구니 항목을 나타냅니다. 이 테이블의 잠재적 크기 때문에 Adobe에서는 60일 이상 된 전환되지 않은 장바구니가 있는 경우와 같이 특정 기준이 충족되는 경우 레코드를 주기적으로 삭제할 것을 권장합니다.

>[!NOTE]
>
>`quote` 및 `quote_item` 테이블에서 레코드를 삭제하지 않는 경우에만 중단된 이전 장바구니를 분석할 수 있습니다. 레코드를 삭제하면 데이터베이스에서 아직 제거되지 않은 장바구니만 표시됩니다.

## 일반 기본 열

| **열 이름** | **설명** |
|---|---|
| `base_price` | [카탈로그 가격 규칙, 계층별 할인 및 특별 가격](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=ko)이 적용된 후 세금, 배송 또는 장바구니 할인이 적용되기 전에 품목이 장바구니에 추가된 시점의 개별 제품 단가입니다. 이 값은 스토어의 기본 통화로 표시됩니다. |
| `created_at` | 로컬에 UTC로 저장된 장바구니 항목의 생성 타임스탬프. [!DNL Commerce Intelligence]의 구성에 따라 이 타임스탬프가 데이터베이스 시간대와 다른 [!DNL Commerce Intelligence]의 보고 시간대로 변환될 수 있습니다. |
| `item_id`(PK) | 테이블에 대한 고유 식별자 |
| `name` | 주문 항목의 텍스트 이름 |
| `parent_item_id` | 단순 제품을 상위 번들 또는 구성 가능한 제품과 연결하는 `Foreign key`. `quote_item.item_id`에 연결하여 간단한 제품과 관련된 상위 제품 특성을 확인하십시오. 상위 장바구니 항목(번들 또는 구성 가능한 제품 유형)의 경우 `parent_item_id`은(는) `NULL`입니다. |
| `product_id` | `Foreign key`이(가) `catalog_product_entity` 테이블에 연결되어 있습니다. 주문 항목과 연결된 제품 특성을 확인하려면 `catalog_product_entity.entity_id`에 참가하십시오. |
| `product_type` | 장바구니에 추가된 제품의 유형입니다. [제품 유형](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=ko#product-types)에는 단순, 구성 가능, 그룹화, 가상, 번들 및 다운로드 가능한 제품이 포함됩니다. |
| `qty` | 특정 장바구니 품목에 대해 장바구니에 포함된 단위 수량 |
| `quote_id` | `Foreign key`이(가) `quote` 테이블에 연결되어 있습니다. 장바구니 항목과 연결된 장바구니 특성을 확인하려면 `quote.entity_id`에 참가하십시오. |
| `sku` | 장바구니 항목에 대한 고유 식별자 |
| `store_id` | `store` 테이블에 연결된 외래 키입니다. 장바구니 항목과 연결된 Commerce 스토어 보기를 확인하려면 `store.store_id`에 참가하십시오. |

{style="table-layout:auto"}

## 공통 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Cart creation date` | 장바구니 생성 날짜와 연계된 타임스탬프. `quote_item.quote_id`을(를) `quote.entity_id`에 조인하고 `created_at` 타임스탬프를 반환하여 계산됨 |
| `Cart is active? (1/0)` | 고객이 장바구니를 만들고 아직 주문으로 전환하지 않은 경우 &quot;1&quot;을 반환하는 부울 필드. 변환된 장바구니 또는 관리자를 통해 만든 장바구니에 대해 &quot;0&quot;을 반환합니다. `quote_item.quote_id`에 `quote.entity_id`을(를) 조인하고 `is_active` 필드를 반환하여 계산됨 |
| `Cart item total value (qty * base_price)` | [카탈로그 가격 규칙, 계층화된 할인 및 특별 가격](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=ko)이 적용된 후 세금, 배송 또는 장바구니 할인이 적용되기 전에 장바구니에 항목을 추가한 시점의 총 항목 값입니다. `qty`에 `base_price`을(를) 곱하여 계산됨 |
| `Seconds since cart creation` | 장바구니 생성일과 현재 사이의 경과 시간. `quote_item.quote_id`에 `quote.entity_id`을(를) 조인하고 `Seconds since cart creation` 필드를 반환하여 계산됨 |
| `Store name` | 주문 항목과 연결된 Commerce 스토어의 이름입니다. `sales_order_item.store_id`에 `store.store_id`을(를) 조인하고 `name` 필드를 반환하여 계산됨 |

{style="table-layout:auto"}

## 일반 지표

| **지표 이름** | **설명** | **구성** |
|---|---|---|
| `Number of abandoned cart items` | 특정 &quot;포기&quot; 조건을 충족하는 장바구니에 추가된 항목의 총 수량 | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>필터:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x. 여기서 &quot;x&quot;는 장바구니 만들기 이후 장바구니가 중단된 것으로 간주되는 경과 시간(초)에 해당합니다 |
| `Abandoned cart item value` | 특정 &quot;포기&quot; 조건을 충족하는 장바구니와 관련된 총 매출의 합계 | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>필터:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x. 여기서 &quot;x&quot;는 장바구니 만들기 이후 장바구니가 중단된 것으로 간주되는 경과 시간(초)에 해당합니다 |

{style="table-layout:auto"}

## 외래 키 조인 경로

`catalog_product_entity`

* `catalog_product_entity` 테이블에 연결하여 장바구니 항목과 연결된 제품 특성을 반환하는 열을 만드십시오.
   * 경로: `quote_item.product_id`(많음) => `catalog_product_entity.entity_id`(하나)

`quote`

* `quote` 테이블에 연결하여 장바구니 항목과 연결된 새 장바구니 수준 열을 만드십시오.
   * 경로: `quote_item.quote_id`(많음) => `quote.entity_id`(하나)

`quote_item`

* 상위 구성 가능 또는 번들 SKU의 세부 정보를 간단한 제품과 연결하는 열을 만들려면 `quote_item`에 참가하십시오. Data Warehouse 관리자에 빌드하는 경우 이러한 계산을 구성하는 데 도움이 필요하면 [지원팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ko)하십시오.
   * 경로: `quote_item.parent_item_id`(많음) => `quote_item.item_id`(하나)

`store`

* `store` 테이블에 연결하여 장바구니 항목과 연결된 Commerce 스토어와 관련된 세부 정보를 반환하는 열을 만드십시오.
   * 경로: `quote_item.store_id`(많음) => `store.store_id`(하나)
