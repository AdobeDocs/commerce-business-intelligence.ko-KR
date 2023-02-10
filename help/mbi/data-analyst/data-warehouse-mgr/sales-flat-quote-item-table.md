---
title: quote_item 테이블
description: quote_item 테이블을 사용하는 방법을 알아봅니다.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 0%

---

# quote_item 테이블

다음 `quote_item` 테이블 (`sales_flat_quote_item` M1) 1) 장바구니에 추가된 모든 항목에 대한 레코드(장바구니가 포기 또는 구매로 변환되었는지 여부)를 포함합니다. 각 행은 하나의 장바구니 항목을 나타냅니다. 이 테이블의 잠재적 크기로 인해 60일 이상 오래된 전환되지 않은 장바구니가 있는 경우와 같이 특정 기준이 충족되는 경우 레코드를 주기적으로 삭제하는 것이 좋습니다.

>[!NOTE]
>
>기록을 목록에서 삭제하지 않는 경우에만 기록 포기 카트를 분석할 수 있습니다 `quote` 및 `quote_item` 테이블. 레코드를 삭제하는 경우, 데이터베이스에서 아직 제거되지 않은 장바구니만 볼 수 있습니다.

## 공통 기본 열

| **열 이름** | **설명** |
|---|---|
| `base_price` | 품목을 장바구니에 추가한 당시 제품의 개별 단위 가격, 이후 [카탈로그 가격 규칙, 계층형 할인 및 특별 가격](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 세금, 배송 또는 장바구니 할인이 적용되기 전에 저장소의 기본 통화로 표시됩니다 |
| `created_at` | 장바구니 항목의 생성 타임스탬프이며, 일반적으로 UTC에 로컬로 저장됩니다. 의 구성에 따라 [!DNL MBI]로 지정하는 경우 이 타임스탬프가 [!DNL MBI] 데이터베이스 시간대와 다른 |
| `item_id` (PK) | 테이블의 고유 식별자 |
| `name` | 주문 항목의 텍스트 이름 |
| `parent_item_id` | `Foreign key` 단순 제품과 상위 번들 또는 구성 가능한 제품 간의 연관성이 있습니다. 가입 대상 `quote_item.item_id` 단순 제품과 연관된 상위 제품 속성을 판별하는 데 사용됩니다. 상위 장바구니 항목(즉, 번들 또는 구성 가능한 제품 유형)의 경우, `parent_item_id` 다음 `NULL` |
| `product_id` | `Foreign key` 관련 `catalog_product_entity` 테이블. 가입 대상 `catalog_product_entity.entity_id` 주문 품목과 연관된 제품 속성을 확인하려면 |
| `product_type` | 장바구니에 추가된 제품 유형입니다. 잠재적 [제품 유형](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 포함: 간단하고 구성 가능하고 그룹화된 가상, 번들 및 다운로드 가능 |
| `qty` | 특정 장바구니 항목에 대한 장바구니에 포함된 단위 수량 |
| `quote_id` | `Foreign key` 관련 `quote` 테이블. 가입 대상 `quote.entity_id` 장바구니 항목과 연결된 장바구니 속성을 확인하려면 |
| `sku` | 장바구니 항목에 대한 고유 식별자입니다 |
| `store_id` | 와 연결된 외부 키 `store` 테이블. 가입 대상 `store.store_id` 장바구니 항목과 연결된 상거래 스토어 보기를 확인하려면 |

{style=&quot;table-layout:auto&quot;}

## 일반적인 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Cart creation date` | 장바구니 작성 날짜와 연결된 타임스탬프입니다. 가입으로 계산됨 `quote_item.quote_id` to `quote.entity_id` 재방문 `created_at` timestamp |
| `Cart is active? (1/0)` | 고객이 장바구니를 만들고 아직 주문으로 전환하지 않은 경우 &quot;1&quot;을 반환하는 부울 필드입니다. 전환된 장바구니 또는 관리자를 통해 생성된 장바구니에 대해 &quot;0&quot;을 반환합니다. 가입으로 계산됨 `quote_item.quote_id` to `quote.entity_id` 재방문 `is_active` 필드 |
| `Cart item total value (qty * base_price)` | 장바구니에 항목을 추가한 시간(이후)의 항목의 총 값 [카탈로그 가격 규칙, 계층형 할인 및 특별 가격](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 세금, 배송 또는 장바구니 할인이 적용되기 전에 적용됩니다. 에 를 곱하여 계산됩니다. `qty` 기준 `base_price` |
| `Seconds since cart creation` | 장바구니의 생성 날짜와 현재 사이의 경과 시간입니다. 가입으로 계산됨 `quote_item.quote_id` to `quote.entity_id` 재방문 `Seconds since cart creation` 필드 |
| `Store name` | 주문 항목과 연결된 상거래 저장소의 이름입니다. 가입으로 계산됨 `sales_order_item.store_id` to `store.store_id` 재방문 `name` 필드 |

{style=&quot;table-layout:auto&quot;}

## 일반 지표

| **지표 이름** | **설명** | **건설** |
|---|---|---|
| `Number of abandoned cart items` | 특정 &quot;포기&quot; 조건을 충족하는 장바구니에 추가된 총 품목 수량 | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>필터:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x. 여기서 &quot;x&quot;는 장바구니를 포기한 것으로 간주되는 장바구니 작성 이후 경과된 시간(초)에 해당합니다 |
| `Abandoned cart item value` | 특정 &quot;포기&quot; 조건을 충족하는 장바구니와 연결된 총 매출액의 합계입니다 | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>필터:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x. 여기서 &quot;x&quot;는 장바구니를 포기한 것으로 간주되는 장바구니 작성 이후 경과된 시간(초)에 해당합니다 |

{style=&quot;table-layout:auto&quot;}

## 외래 키 연결 경로

`catalog_product_entity`

* 가입 대상 `catalog_product_entity` 표 를 사용하여 장바구니 항목과 연결된 제품 속성을 반환하는 새 열을 만들 수 있습니다.
   * 경로: `quote_item.product_id` (다) => `catalog_product_entity.entity_id` (1)

`quote`

* 가입 대상 `quote` 표 를 사용하여 장바구니 항목과 연결된 새 장바구니 수준 열을 만들 수 있습니다.
   * 경로: `quote_item.quote_id` (다) => `quote.entity_id` (1)

`quote_item`

* 가입 대상 `quote_item` 상위 구성 가능 또는 번들 SKU의 세부 정보를 단순 제품과 연결하는 새 열을 만들 수 있습니다. 다음을 수행해야 합니다 [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) Data Warehouse 관리자에서 작성하는 경우 이러한 계산을 구성하는 데 도움이 됩니다.
   * 경로: `quote_item.parent_item_id` (다) => `quote_item.item_id` (1)

`store`

* 가입 대상 `store` 장바구니 항목과 연결된 상거래 스토어와 관련된 세부 사항을 반환하는 새 열을 만드는 표
   * 경로: `quote_item.store_id` (다) => `store.store_id` (1)
