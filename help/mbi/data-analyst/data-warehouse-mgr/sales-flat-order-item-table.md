---
title: sales_order_item 테이블
description: sales_order_item 테이블을 사용하여 작업하는 방법을 알아봅니다.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# `sales_order_item` 표

다음 `sales_order_item` 테이블 (`sales_flat_order_item` M1 1에서)에는 주문으로 구매한 모든 제품의 레코드가 포함되어 있습니다. 각 행은 고유한 `sku` 주문에 포함되어 있습니다. 특정 항목에 대해 구매한 단위 수량 `sku` 는 `qty_ordered` 필드.

## 제품 유형

다음 `sales_order_item` 모든 [제품 유형](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 구입한 것입니다. Commerce의 일반적인 방법은 구성 가능한 제품 또는 크기, 색상 및 기타 제품 속성에 따라 사용자 지정할 수 있는 제품을 제공하는 것입니다. 구성 가능한 제품에는 자체 제품이 있지만 `sku`과 관련된 것으로, 각 간단한 제품은 고유한 제품 구성을 나타냅니다. 을(를) 참조하십시오. [제품 구성](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) 추가 정보.

예를 들어 티셔츠와 같은 구성 가능한 제품을 고려해 보십시오. 고객이 체크 아웃하면 색상과 크기를 변경할 옵션을 선택합니다. 고객이 색을 선택하는 경우 `blue`, 크기 `small`과 같은 간단한 제품을 구입하게 됩니다 `t-shirt-blue-small` 의 상위 제품과 관련된 `t-shirt`.

구성 가능한 제품이 주문에 포함되면, `sales_order_item` 표: 하나 [단순](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku`, 및 [구성 가능](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) 상위 이 두 레코드는 `sales_order_item` 테이블은 다음 조인을 통해 서로 관련될 수 있습니다.

* (단순) `sales_order_item.parent_item_id` => (구성 가능) `sales_order_item.item_id`

따라서 단순 레벨 또는 구성 가능한 레벨에서 제품의 판매를 보고할 수 있습니다. 기본적으로 모든 표준 `order-item-level` 지표 [!DNL MBI] 단순 제품을 제외하도록 구성되었으며, *전용* 구성 가능한 버전에 대해 보고합니다. 이 작업은 `Ordered products we count` 필터 세트: `parent_item_id` is `NULL`.

## 공통 열

| **열 이름** | **설명** |
|----|----|
| `base_price` | 판매 후 제품의 개별 단위 가격 [카탈로그 가격 규칙, 계층형 할인 및 특별 가격](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 세금, 배송 또는 장바구니 할인이 적용되기 전에 저장소의 기본 통화로 표시됩니다 |
| `created_at` | 주문 항목의 생성 타임스탬프이며, 일반적으로 UTC에 로컬로 저장됩니다. 의 구성에 따라 [!DNL MBI]로 지정하는 경우 이 타임스탬프가 [!DNL MBI] 데이터베이스 시간대와 다른 |
| `item_id` (PK) | 테이블의 고유 식별자 |
| `name` | 주문 항목의 텍스트 이름 |
| `order_id` | `Foreign key` 관련 `sales_order` 테이블. 가입 대상 `sales_order.entity_id` 주문 품목과 연관된 주문 속성을 확인하려면 |
| `parent_item_id` | `Foreign key` 단순 제품과 상위 번들 또는 구성 가능한 제품 간의 연관성이 있습니다. 가입 대상 `sales_order_item.item_id` 단순 제품과 연관된 상위 제품 속성을 판별하는 데 사용됩니다. 상위 주문 품목(즉, 번들 또는 구성 가능한 제품 유형)의 경우 `parent_item_id` 다음 `NULL` |
| `product_id` | `Foreign key` 관련 `catalog_product_entity` 테이블. 가입 대상 `catalog_product_entity.entity_id` 주문 품목과 연관된 제품 속성을 확인하려면 |
| `product_type` | 판매된 제품의 유형입니다. 잠재적 [제품 유형](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 포함: 간단하고 구성 가능하고 그룹화된 가상, 번들 및 다운로드 가능 |
| `qty_ordered` | 판매 시 특정 주문 품목의 장바구니에 포함된 단위 수량 |
| `sku` | 구매한 주문 품목의 고유 식별자입니다 |
| `store_id` | `Foreign key` 관련 `store` 테이블. 가입 대상 `store.store_id` 주문 항목과 연관된 상거래 스토어 보기를 확인하려면 |

{style=&quot;table-layout:auto&quot;}

## 일반적인 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Customer's email` | 주문하는 고객의 이메일 주소입니다. 가입으로 계산됨 `sales_order_item.order_id` to `sales_order.entity_id` 재방문 `customer_email` 필드 |
| `Customer's lifetime number of orders` | 이 고객이 수행한 총 주문 수입니다. 가입으로 계산됨 `sales_order_item.order_id` to `sales_order.entity_id` 재방문 `Customer's lifetime number of orders` 필드 |
| `Customer's lifetime revenue` | 이 고객이 수행한 모든 주문에 대한 총 매출액. 가입으로 계산됨 `sales_order_item.order_id` to `sales_order.entity_id` 재방문 `Customer's lifetime revenue` 필드 |
| `Customer's order number` | 이 고객의 주문에 대한 순차적 순서 등급입니다. 가입으로 계산됨 `sales_order_item.order_id` to `sales_order.entity_id` 재방문 `Customer's order number` 필드 |
| `Order item total value (quantity * price)` | 판매 후 주문 품목의 합계 값 [카탈로그 가격 규칙, 계층형 할인 및 특별 가격](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 세금, 배송 또는 장바구니 할인이 적용되기 전에 적용됩니다. 에 를 곱하여 계산됩니다. `qty_ordered` 기준 `base_price` |
| `Order's coupon_code` | 주문에 적용된 쿠폰입니다. 가입으로 계산됨 `sales_order_item.order_id` to `sales_order.entity_id` 재방문 `coupon_code` 필드 |
| `Order's increment_id` | 주문의 고유 식별자입니다. 가입으로 계산됨 `sales_order_item.order_id` to `sales_order.entity_id` 재방문 `increment_id` 필드 |
| `Order's status` | 주문 상태입니다. 가입으로 계산됨 `sales_order_item.order_id` to `sales_order.entity_id` 재방문 `status` 필드 |
| `Store name` | 주문 항목과 연결된 상거래 저장소의 이름입니다. 가입으로 계산됨 `sales_order_item.store_id` to `store.store_id` 재방문 `name` 필드 |

{style=&quot;table-layout:auto&quot;}

## 일반 지표

| **지표 이름** | **설명** | **건설** |
|---|---|---|
| `Products ordered` | 판매 시 장바구니에 포함된 제품의 총 수량 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | 카탈로그 가격 규칙, 계층형 할인 및 특별 가격 적용 후 판매 시 장바구니에 포함된 제품의 총 가격 및 세금, 배송 또는 장바구니 할인이 적용되기 전 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style=&quot;table-layout:auto&quot;}

## `Foreign Key` 경로 결합

`catalog_product_entity`

* 가입 대상 `catalog_product_entity` 표 를 사용하여 주문 항목과 연관된 제품 속성을 반환하는 새 열을 만들 수 있습니다.
   * 경로: `sales_order_item.product_id` (다) => `catalog_product_entity.entity_id` (1)

`sales_order`

* 가입 대상 `sales_order` 테이블: 주문 품목과 연관된 신규 주문 레벨 열을 생성합니다.
   * 경로: `sales_order_item.order_id` (다) => `sales_order.entity_id` (1)

`sales_order_item`

* 가입 대상 `sales_order_item` 상위 구성 가능 또는 번들 SKU의 세부 정보를 단순 제품과 연결하는 새 열을 만들 수 있습니다. 다음을 수행해야 합니다 [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) Data Warehouse 관리자에서 작성하는 경우 이러한 계산을 구성하는 데 도움이 됩니다.
   * 경로: `sales_order_item.parent_item_id` (다) => `sales_order_item.item_id` (1)

`store`

* 가입 대상 `store` 주문 항목과 연결된 상거래 저장소와 관련된 세부 사항을 반환하는 새 열을 만들 수 있습니다.
   * 경로: `sales_order_item.store_id` (다) => `store.store_id` (1)
