---
title: sales_order_item 테이블
description: sales_order_item 테이블을 사용하여 작업하는 방법을 알아봅니다.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# `sales_order_item` 테이블

`sales_order_item` 테이블(M1의 `sales_flat_order_item`)에는 주문에서 구입한 모든 제품의 레코드가 들어 있습니다. 각 행은 주문에 포함된 고유한 `sku`을(를) 나타냅니다. 특정 `sku`에 대해 구입한 장치의 수량은 대개 `qty_ordered` 필드에 표시됩니다.

## 제품 유형

`sales_order_item`은(는) 구매한 모든 [제품 유형](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types)에 대한 세부 정보를 캡처합니다. [!DNL Adobe Commerce]의 일반적인 방법은 구성 가능한 제품, 즉 크기, 색상 및 기타 제품 특성에 따라 사용자 지정할 수 있는 제품을 제공하는 것입니다. 구성 가능한 제품에는 고유한 `sku`이(가) 있지만 각 단순 제품이 고유한 제품 구성을 나타내는 여러 단순 제품과 관련될 수 있습니다. 자세한 내용은 [제품 구성](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/)을 참조하세요.

예를 들어 티셔츠와 같이 구성 가능한 제품을 고려해 보십시오. 고객이 체크아웃할 때 색상 및 크기를 변경하는 옵션을 선택합니다. 고객이 `blue`의 색상과 `small`의 크기를 선택하면 `t-shirt`의 상위 제품과 다시 연결된 `t-shirt-blue-small`과(와) 같은 간단한 제품을 구매하게 됩니다.

구성 가능한 제품이 주문에 포함된 경우 `sales_order_item` 테이블에 [simple](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku`과(와) [configurable](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) 상위 항목에 대한 두 개의 행이 생성됩니다. `sales_order_item` 테이블의 이 두 레코드는 다음 조인을 통해 서로 연결될 수 있습니다.

* (단순) `sales_order_item.parent_item_id` => (구성 가능) `sales_order_item.item_id`

따라서 단순 수준 또는 구성 가능한 수준에서 제품 판매에 대해 보고할 수 있습니다. 기본적으로 [!DNL Commerce Intelligence]의 모든 표준 `order-item-level` 지표는 간단한 제품을 제외하도록 구성되어 있으며 *only* 보고서에서 구성 가능한 버전을 보고합니다. 이 작업은 `parent_item_id`이(가) `NULL`인 상태에서 필터링하는 `Ordered products we count` 필터 집합을 통해 수행됩니다.

## 공통 열

| **열 이름** | **설명** |
|----|----|
| `base_price` | [카탈로그 가격 규칙, 계층별 할인 및 특별 가격](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html)이 적용된 후 그리고 세금, 배송 또는 장바구니 할인이 적용되기 전에 판매 시점의 개별 제품 단가. 이 값은 스토어의 기본 통화로 표시됩니다. |
| `created_at` | UTC로 로컬에 저장된 주문 항목의 생성 타임스탬프. [!DNL Commerce Intelligence]의 구성에 따라 이 타임스탬프가 데이터베이스 시간대와 다른 [!DNL Commerce Intelligence]의 보고 시간대로 변환될 수 있습니다. |
| `item_id`(PK) | 테이블에 대한 고유 식별자. |
| `name` | 주문 항목의 텍스트 이름. |
| `order_id` | `Foreign key`이(가) `sales_order` 테이블에 연결되어 있습니다. 주문 항목과 연결된 주문 특성을 확인하려면 `sales_order.entity_id`에 참가하십시오. |
| `parent_item_id` | 단순 제품을 상위 번들 또는 구성 가능한 제품과 연결하는 `Foreign key`. `sales_order_item.item_id`에 연결하여 간단한 제품과 관련된 상위 제품 특성을 확인하십시오. 상위 주문 항목(즉, 번들 또는 구성 가능한 제품 유형)의 경우 `parent_item_id`은(는) `NULL`입니다. |
| `product_id` | `Foreign key`이(가) `catalog_product_entity` 테이블에 연결되어 있습니다. 주문 항목과 연결된 제품 특성을 확인하려면 `catalog_product_entity.entity_id`에 참가하십시오. |
| `product_type` | 판매된 제품의 유형입니다. [제품 유형](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types)에는 단순, 구성 가능, 그룹화, 가상, 번들 및 다운로드 가능한 유형이 포함될 수 있습니다. |
| `qty_ordered` | 판매 시 특정 주문 품목에 대해 장바구니에 포함된 단위 수량. |
| `sku` | 구매한 주문 항목에 대한 고유 식별자. |
| `store_id` | `Foreign key`이(가) `store` 테이블에 연결되어 있습니다. 주문 항목과 연결된 Commerce 스토어 보기를 확인하려면 `store.store_id`에 참가하십시오. |

{style="table-layout:auto"}

## 공통 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Customer's email` | 주문 고객의 이메일 주소. `sales_order.entity_id`에 `sales_order_item.order_id`을(를) 조인하고 `customer_email` 필드를 반환하여 계산되었습니다. |
| `Customer's lifetime number of orders` | 이 고객이 수행한 총 주문 수. `sales_order.entity_id`에 `sales_order_item.order_id`을(를) 조인하고 `Customer's lifetime number of orders` 필드를 반환하여 계산되었습니다. |
| `Customer's lifetime revenue` | 이 고객이 수행한 모든 주문에 대한 총 매출액 합계. `sales_order.entity_id`에 `sales_order_item.order_id`을(를) 조인하고 `Customer's lifetime revenue` 필드를 반환하여 계산되었습니다. |
| `Customer's order number` | 해당 고객 주문에 대한 순차적 주문 등급. `sales_order.entity_id`에 `sales_order_item.order_id`을(를) 조인하고 `Customer's order number` 필드를 반환하여 계산되었습니다. |
| `Order item total value (quantity * price)` | [카탈로그 가격 규칙, 계층별 할인 및 특별 가격](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html)이 적용된 후 세금, 배송 또는 장바구니 할인이 적용되기 전에 판매 시점의 주문 항목의 총 값입니다. `qty_ordered`에 `base_price`을(를) 곱하여 계산됩니다. |
| `Order's coupon_code` | 주문에 적용되는 쿠폰입니다. `sales_order.entity_id`에 `sales_order_item.order_id`을(를) 조인하고 `coupon_code` 필드를 반환하여 계산되었습니다. |
| `Order's increment_id` | 주문에 대한 고유 식별자. `sales_order.entity_id`에 `sales_order_item.order_id`을(를) 조인하고 `increment_id` 필드를 반환하여 계산되었습니다. |
| `Order's status` | 주문 상태. `sales_order.entity_id`에 `sales_order_item.order_id`을(를) 조인하고 `status` 필드를 반환하여 계산되었습니다. |
| `Store name` | 주문 항목과 연결된 Commerce 스토어의 이름입니다. `store.store_id`에 `sales_order_item.store_id`을(를) 조인하고 `name` 필드를 반환하여 계산되었습니다. |

{style="table-layout:auto"}

## 일반 지표

| **지표 이름** | **설명** | **구성** |
|---|---|---|
| `Products ordered` | 판매 시 장바구니에 포함된 제품의 총 수량 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | 카탈로그 가격 규칙, 계층별 할인 및 특별 가격 적용이 끝나고 세금, 배송 또는 장바구니 할인이 적용되기 전 판매 시 장바구니에 포함된 제품의 총 금액 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key`개 조인 경로

`catalog_product_entity`

* `catalog_product_entity` 테이블에 연결하여 주문 항목과 연결된 제품 특성을 반환하는 열을 만드십시오.
   * 경로: `sales_order_item.product_id`(많음) => `catalog_product_entity.entity_id`(하나)

`sales_order`

* `sales_order` 테이블에 연결하여 주문 항목과 연결된 새 주문 수준 열을 만드십시오.
   * 경로: `sales_order_item.order_id`(많음) => `sales_order.entity_id`(하나)

`sales_order_item`

* 상위 구성 가능 또는 번들 SKU의 세부 정보를 간단한 제품과 연결하는 열을 만들려면 `sales_order_item`에 참가하십시오. Data Warehouse 관리자에서 빌드하는 경우 이러한 계산을 구성하는 데 도움이 필요하면 [지원팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)하십시오.
   * 경로: `sales_order_item.parent_item_id`(많음) => `sales_order_item.item_id`(하나)

`store`

* `store` 테이블에 연결하여 주문 항목과 연결된 Commerce 스토어와 관련된 세부 정보를 반환하는 열을 만드십시오.
   * 경로: `sales_order_item.store_id`(많음) => `store.store_id`(하나)
