---
title: quote_item 테이블
description: quote_item 테이블을 사용하여 작업하는 방법을 알아봅니다.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---

# quote_item 테이블

다음 `quote_item` 표 (`sales_flat_quote_item` - m1) 1)에는 장바구니에 추가된 모든 항목에 대한 레코드(장바구니가 중단되었는지 또는 구매로 전환되었는지 여부)가 포함됩니다. 각 행은 하나의 장바구니 항목을 나타냅니다. Adobe 이 테이블의 잠재적 크기 때문에 60일 이상 된 전환되지 않은 장바구니가 있는 경우와 같이 특정 기준이 충족되는 경우 레코드를 정기적으로 삭제하는 것이 좋습니다.

>[!NOTE]
>
>중단된 내역 장바구니를 분석하는 것은 `quote` 및 `quote_item` 테이블. 레코드를 삭제하면 데이터베이스에서 아직 제거되지 않은 장바구니만 표시됩니다.

## 일반 기본 열

| **열 이름** | **설명** |
|---|---|
| `base_price` | 이후에 품목이 장바구니에 추가된 시점의 개별 제품 단가 [카탈로그 가격 규칙, 계층형 할인 및 특별 가격](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 세금, 배송 또는 장바구니 할인이 적용되기 전에 적용됩니다. 이 값은 스토어의 기본 통화로 표시됩니다. |
| `created_at` | 로컬에 UTC로 저장된 장바구니 항목의 생성 타임스탬프. 의 구성에 따라 [!DNL MBI], 이 타임스탬프는에서 보고 시간대로 변환될 수 있습니다. [!DNL MBI] 데이터베이스 시간대와 다릅니다. |
| `item_id` (PK) | 테이블에 대한 고유 식별자 |
| `name` | 주문 항목의 텍스트 이름 |
| `parent_item_id` | `Foreign key` 단순 제품을 상위 번들 또는 구성 가능한 제품과 연결합니다. 가입 대상 `quote_item.item_id` 간단한 제품과 연관된 상위 제품 속성을 확인합니다. 상위 장바구니 항목(번들 또는 구성 가능한 제품 유형)의 경우 `parent_item_id` 은(는) `NULL` |
| `product_id` | `Foreign key` 과(와) 연계됨 `catalog_product_entity` 테이블. 가입 대상 `catalog_product_entity.entity_id` 주문 품목과 연관된 제품 속성 결정 |
| `product_type` | 장바구니에 추가된 제품의 유형입니다. 잠재적 [제품 유형](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 단순, 구성 가능, 그룹화, 가상, 번들 및 다운로드 가능한 기능이 포함됩니다. |
| `qty` | 특정 장바구니 품목에 대해 장바구니에 포함된 단위 수량 |
| `quote_id` | `Foreign key` 과(와) 연계됨 `quote` 테이블. 가입 대상 `quote.entity_id` 장바구니 항목과 연결된 장바구니 속성을 확인하려면 |
| `sku` | 장바구니 항목에 대한 고유 식별자 |
| `store_id` | 와(과) 연결된 외래 키 `store` 테이블. 가입 대상 `store.store_id` 장바구니 항목과 연결된 상거래 스토어 보기를 확인하려면 |

{style="table-layout:auto"}

## 공통 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Cart creation date` | 장바구니 생성 날짜와 연계된 타임스탬프. 조인으로 계산됨 `quote_item.quote_id` 끝 `quote.entity_id` 및 반환 `created_at` timestamp |
| `Cart is active? (1/0)` | 고객이 장바구니를 만들고 아직 주문으로 전환하지 않은 경우 &quot;1&quot;을 반환하는 부울 필드. 변환된 장바구니 또는 관리자를 통해 만든 장바구니에 대해 &quot;0&quot;을 반환합니다. 조인으로 계산됨 `quote_item.quote_id` 끝 `quote.entity_id` 및 반환 `is_active` 필드 |
| `Cart item total value (qty * base_price)` | 항목이 장바구니에 추가된 시점의 다음 항목 총 값 [카탈로그 가격 규칙, 계층형 할인 및 특별 가격](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 세금, 배송 또는 장바구니 할인이 적용되기 전에 적용됩니다. 다음을 곱하여 계산됨 `qty` 작성자 `base_price` |
| `Seconds since cart creation` | 장바구니 생성일과 현재 사이의 경과 시간. 조인으로 계산됨 `quote_item.quote_id` 끝 `quote.entity_id` 및 반환 `Seconds since cart creation` 필드 |
| `Store name` | 주문 항목과 연결된 상거래 저장소의 이름입니다. 조인으로 계산됨 `sales_order_item.store_id` 끝 `store.store_id` 및 반환 `name` 필드 |

{style="table-layout:auto"}

## 일반 지표

| **지표 이름** | **설명** | **구성** |
|---|---|---|
| `Number of abandoned cart items` | 특정 &quot;포기&quot; 조건을 충족하는 장바구니에 추가된 항목의 총 수량 | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>필터:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x이고, 여기서 &quot;x&quot;는 장바구니가 생성된 후 장바구니가 포기한 것으로 간주되는 경과 시간(초)에 해당합니다 |
| `Abandoned cart item value` | 특정 &quot;포기&quot; 조건을 충족하는 장바구니와 관련된 총 매출의 합계 | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>필터:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x이고, 여기서 &quot;x&quot;는 장바구니가 생성된 후 장바구니가 포기한 것으로 간주되는 경과 시간(초)에 해당합니다 |

{style="table-layout:auto"}

## 외래 키 조인 경로

`catalog_product_entity`

* 가입 대상 `catalog_product_entity` 표를 사용하여 장바구니 항목과 연결된 제품 속성을 반환하는 열을 만들 수 있습니다.
   * 경로: `quote_item.product_id` (다) => `catalog_product_entity.entity_id` (1)

`quote`

* 가입 대상 `quote` 테이블 - 장바구니 항목과 연결된 새 장바구니 수준 열을 만들 수 있습니다.
   * 경로: `quote_item.quote_id` (다) => `quote.entity_id` (1)

`quote_item`

* 가입 대상 `quote_item` 상위 구성 가능 또는 번들 SKU의 세부 정보를 간단한 제품과 연결하는 열을 만듭니다. [지원 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) Data Warehouse 관리자에서 빌드하는 경우 이러한 계산을 구성하는 데 도움이 됩니다.
   * 경로: `quote_item.parent_item_id` (다) => `quote_item.item_id` (1)

`store`

* 가입 대상 `store` 테이블을 사용하여 장바구니 항목과 연결된 상거래 저장소 관련 세부 정보를 반환하는 열을 만들 수 있습니다.
   * 경로: `quote_item.store_id` (다) => `store.store_id` (1)
