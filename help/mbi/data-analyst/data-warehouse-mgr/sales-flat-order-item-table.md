---
title: sales_order_item 테이블
description: sales_order_item 테이블을 사용하여 작업하는 방법을 알아봅니다.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# `sales_order_item` 표

다음 `sales_order_item` 표 (`sales_flat_order_item` (M1)에는 주문에서 구입한 모든 제품에 대한 기록이 들어 있습니다. 각 행은 고유한 을 나타냅니다 `sku` 주문에 포함됩니다. 특정 용도로 구입한 장치의 수량입니다 `sku` 는 다음과 같은 형식으로 표시되며, `qty_ordered` 필드.

## 제품 유형

다음 `sales_order_item` 모든 세부 정보 캡처 [제품 유형](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 구매되었습니다. 의 일반적인 관행 [!DNL Adobe Commerce] 는 구성 가능한 제품을 제공하는 것입니다. 즉, 크기, 색상 및 기타 제품 속성에 따라 사용자 정의할 수 있는 제품을 제공합니다. 구성 가능한 제품에는 고유한 가 있지만 `sku`, 각 단순 제품이 고유한 제품 구성을 나타내는 여러 단순 제품과 관련될 수 있습니다. 을(를) 참조하십시오 [제품 구성](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) 추가 정보.

예를 들어 티셔츠와 같이 구성 가능한 제품을 고려해 보십시오. 고객이 체크아웃할 때 색상 및 크기를 변경하는 옵션을 선택합니다. 고객이 색상을 선택한 경우 `blue`, 및 크기 `small`, 다음과 같은 간단한 제품을 구입하게 됩니다. `t-shirt-blue-small` 의 상위 제품과 다시 관련되어 있습니다. `t-shirt`.

구성 가능한 제품이 주문에 포함되면 `sales_order_item` 표: [단순](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku` 및 1개 [구성 가능](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) 상위. 의 다음 두 레코드 `sales_order_item` 다음 조인을 통해 테이블을 서로 연결할 수 있습니다.

* (단순) `sales_order_item.parent_item_id` => (구성 가능) `sales_order_item.item_id`

따라서 단순 수준 또는 구성 가능한 수준에서 제품 판매에 대해 보고할 수 있습니다. 기본적으로 모든 표준 `order-item-level` 의 지표 [!DNL Commerce Intelligence] 는 단순 제품을 제외하도록 구성되어 있으며, *전용* 구성 가능한 버전에 대해 보고합니다. 이는 다음을 통해 수행됩니다. `Ordered products we count` 필터 세트: 다음의 조건을 필터링합니다. `parent_item_id` 은(는) `NULL`.

## 공통 열

| **열 이름** | **설명** |
|----|----|
| `base_price` | 판매 후 제품의 개별 단위 가격 [카탈로그 가격 규칙, 계층형 할인 및 특별 가격](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 세금, 배송 또는 장바구니 할인이 적용되기 전에 적용됩니다. 이 값은 스토어의 기본 통화로 표시됩니다. |
| `created_at` | UTC로 로컬에 저장된 주문 항목의 생성 타임스탬프. 의 구성에 따라 [!DNL Commerce Intelligence], 이 타임스탬프는에서 보고 시간대로 변환될 수 있습니다. [!DNL Commerce Intelligence] 데이터베이스 시간대와 다릅니다. |
| `item_id` (PK) | 테이블에 대한 고유 식별자. |
| `name` | 주문 항목의 텍스트 이름. |
| `order_id` | `Foreign key` 과(와) 연계됨 `sales_order` 테이블. 가입 대상 `sales_order.entity_id` 주문 품목과 연관된 주문 속성을 결정합니다. |
| `parent_item_id` | `Foreign key` 단순 제품을 상위 번들 또는 구성 가능한 제품과 연결합니다. 가입 대상 `sales_order_item.item_id` 간단한 제품과 연관된 상위 제품 속성을 확인합니다. 상위 주문 품목(즉, 번들 또는 구성 가능한 제품 유형)의 경우 `parent_item_id` 은(는) `NULL`. |
| `product_id` | `Foreign key` 과(와) 연계됨 `catalog_product_entity` 테이블. 가입 대상 `catalog_product_entity.entity_id` 주문 품목과 연관된 제품 속성을 결정합니다. |
| `product_type` | 판매된 제품의 유형입니다. 잠재적 [제품 유형](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) include: 단순, 구성 가능, 그룹화, 가상, 번들 및 다운로드 가능 |
| `qty_ordered` | 판매 시 특정 주문 품목에 대해 장바구니에 포함된 단위 수량. |
| `sku` | 구매한 주문 항목에 대한 고유 식별자. |
| `store_id` | `Foreign key` 과(와) 연계됨 `store` 테이블. 가입 대상 `store.store_id` 주문 항목과 연결된 Commerce 스토어 보기를 확인할 수 있습니다. |

{style="table-layout:auto"}

## 공통 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Customer's email` | 주문 고객의 이메일 주소. 조인으로 계산됨 `sales_order_item.order_id` 끝 `sales_order.entity_id` 및 반환 `customer_email` 필드. |
| `Customer's lifetime number of orders` | 이 고객이 수행한 총 주문 수. 조인으로 계산됨 `sales_order_item.order_id` 끝 `sales_order.entity_id` 및 반환 `Customer's lifetime number of orders` 필드. |
| `Customer's lifetime revenue` | 이 고객이 수행한 모든 주문에 대한 총 매출액 합계. 조인으로 계산됨 `sales_order_item.order_id` 끝 `sales_order.entity_id` 및 반환 `Customer's lifetime revenue` 필드. |
| `Customer's order number` | 해당 고객 주문에 대한 순차적 주문 등급. 조인으로 계산됨 `sales_order_item.order_id` 끝 `sales_order.entity_id` 및 반환 `Customer's order number` 필드. |
| `Order item total value (quantity * price)` | 판매 후 주문 항목의 총 금액 [카탈로그 가격 규칙, 계층형 할인 및 특별 가격](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 세금, 배송 또는 장바구니 할인이 적용되기 전에 적용됩니다. 다음을 곱하여 계산됨 `qty_ordered` 작성자 `base_price`. |
| `Order's coupon_code` | 주문에 적용되는 쿠폰입니다. 조인으로 계산됨 `sales_order_item.order_id` 끝 `sales_order.entity_id` 및 반환 `coupon_code` 필드. |
| `Order's increment_id` | 주문에 대한 고유 식별자. 조인으로 계산됨 `sales_order_item.order_id` 끝 `sales_order.entity_id` 및 반환 `increment_id` 필드. |
| `Order's status` | 주문 상태. 조인으로 계산됨 `sales_order_item.order_id` 끝 `sales_order.entity_id` 및 반환 `status` 필드. |
| `Store name` | 주문 항목과 연결된 상거래 저장소의 이름입니다. 조인으로 계산됨 `sales_order_item.store_id` 끝 `store.store_id` 및 반환 `name` 필드. |

{style="table-layout:auto"}

## 일반 지표

| **지표 이름** | **설명** | **구성** |
|---|---|---|
| `Products ordered` | 판매 시 장바구니에 포함된 제품의 총 수량 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | 카탈로그 가격 규칙, 계층별 할인 및 특별 가격 적용이 끝나고 세금, 배송 또는 장바구니 할인이 적용되기 전 판매 시 장바구니에 포함된 제품의 총 금액 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` 패스 연결

`catalog_product_entity`

* 가입 대상 `catalog_product_entity` 주문 품목과 연관된 제품 속성을 반환하는 열을 생성하는 테이블입니다.
   * 경로: `sales_order_item.product_id` (다) => `catalog_product_entity.entity_id` (1)

`sales_order`

* 가입 대상 `sales_order` 주문 품목과 연관된 새 주문 레벨 열을 생성하는 테이블.
   * 경로: `sales_order_item.order_id` (다) => `sales_order.entity_id` (1)

`sales_order_item`

* 가입 대상 `sales_order_item` 상위 구성 가능 또는 번들 SKU의 세부 정보를 간단한 제품과 연결하는 열을 만듭니다. [지원 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) Data Warehouse 관리자에서 빌드하는 경우 이러한 계산을 구성하는 데 도움이 됩니다.
   * 경로: `sales_order_item.parent_item_id` (다) => `sales_order_item.item_id` (1)

`store`

* 가입 대상 `store` 주문 항목과 연결된 상거래 저장소 관련 세부 정보를 반환하는 열을 만드는 표입니다.
   * 경로: `sales_order_item.store_id` (다) => `store.store_id` (1)
