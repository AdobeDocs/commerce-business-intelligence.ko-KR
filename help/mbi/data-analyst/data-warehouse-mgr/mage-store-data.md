---
title: 상거래에 데이터 저장
description: 데이터 생성 방법, 새 행이 핵심 상거래 테이블 중 하나에 삽입되는 정확한 원인 및 상거래 데이터베이스에 데이터를 구매하거나 계정을 만드는 등의 작업을 알아봅니다.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 3%

---

# 데이터 저장 위치 [!DNL Adobe Commerce]

Adobe Commerce 플랫폼에서는 수백 개의 표에 다양한 중요한 상거래 데이터를 기록하고 구성합니다. 이 항목에서는 데이터가 생성되는 방법, 새 행이 삽입되는 원인이 무엇인지 알아봅니다 [코어 상거래 테이블](../data-warehouse-mgr/common-mage-tables.md), 그리고 를 사용하여 구매 또는 계정을 만드는 등의 작업을 전자 상거래 데이터베이스에 기록하는 방법입니다. 이러한 개념을 설명하려면 다음 예를 참조하십시오.

`Clothes4U` 온라인 및 오프라인 사이트를 보유한 의류 소매업체입니다. 웹 사이트 뒤에서 Magento Open Source을 사용하여 데이터를 수집하고 구성합니다.

## `catalog\_product\_entity`

9월 22일 `Clothes4U` 가을 상품 3개를 출시하고 있습니다. `Throwback Bellbottoms`, `Straight Leg Jeans`, 및 `V-Neck T-Shirts`. A `Clothes4U` 직원이 상거래 관리자를 열고, **[!UICONTROL Add Product]**, 및에 대한 모든 정보를 입력합니다. `Throwback Bellbottoms`.

의 모든 설정에 만족함 `Throwback Bellbottoms`를 클릭하면 직원이 **[!UICONTROL Save]**: 아래의 첫 번째 줄을 `catalog_product_entity` 테이블. 직원이 프로세스를 반복하며 다음에 대한 새 상거래 제품을 만듭니다. `Straight Leg Jeans`, 다음에 세 번째 - `V-Neck T-Shirt`아래의 두 번째 줄과 세 번째 줄을 `catalog_product_entity` 표:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id` - 이 키가 `catalog_product_entity` 테이블, 즉 테이블의 모든 행은 서로 다른 `entity_id`. 각 `entity_id` 이 표에서 한 제품에만 연결할 수 있으며 각 제품은 한 제품에만 연결할 수 있습니다 `entity_id`
   * 위 테이블의 맨 윗줄에 `entity_id` = 205, 는 &quot;Throwback Bellbots&quot;에 대해 만들어진 새로운 행입니다. 어디든지 `entity_id` = 205는 상거래 플랫폼에 나타나며, &quot;Throwback Bellbots&quot; 제품을 참조하게 됩니다.
* `entity_type_id` - 상거래에 여러 가지 객체 카테고리가 있으며(예: 고객, 주소 및 제품 이름 지정) 이 열은 이 특정 행이 속하는 카테고리를 나타내는 데 사용됩니다.
   * 다음 `catalog_product_entity` 테이블, 각 행에는 동일한 엔티티 유형이 있습니다. 제품. Adobe Commerce에서 `entity_type_id` 제품의 경우 4이고, 이 때문에 생성된 3개의 새 제품 모두가 이 열에 대해 4를 반환합니다.
* `attribute_set_id` - 속성 세트는 설명자와 동일한 제품을 식별하는 데 사용됩니다.
   * 테이블의 상위 두 행은 다음과 같습니다 `Throwback Bellbottoms` 및 `Straight Leg Jeans` 두 가지 모두 팬티입니다 이러한 제품에는 동일한 설명자(예: 이름, inseam, waistline)가 있으므로 동일한 설명자가 있습니다 `attribute_set_id`. 세 번째 항목 `V-Neck T-Shirt` 은(는) 다릅니다 `attribute_set_id` 그것은 바지와 같은 설명자들을 가지고 있지 않기 때문입니다. 셔츠에는 허리줄이나 인센스가 없습니다
* `sku` - Adobe Commerce에서 새 제품을 만들 때 사용자가 각 제품에 할당한 고유 값입니다.
* `created_at` - 이 열은 각 제품을 만들 때의 타임스탬프를 반환합니다

## `customer\_entity`

새로운 3가지 제품을 추가한 직후 새로운 고객인 `Sammy Customer`, 방문 횟수 `Clothes4U`의 웹 사이트를 처음 방문합니다. 이후 `Clothes4U` 게스트 주문을 허용하지 않음, `Sammy Customer` 먼저 웹 사이트에서 계정을 만들어야 합니다. 자격 증명을 입력하고 제출을 클릭하면 [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - 이전 테이블처럼 `entity_id` 는 `customer_entity` 테이블.
   * When `Sammy Customer` 그녀의 계정을 만들고 위의 행이 `customer_entity` 테이블, 그녀가 `entity_id` = 214. 모든 테이블에서 고객이 `entity_id` = 214는 항상 사용자 Sammy Customer를
* `entity_type_id` - 이 열은 이 테이블에 나열되는 엔티티 유형을 식별하고, `catalog_product_entity` 표
   * 모든 행 `customer_entity` 표는 고객이 되고 상거래 는 고객을 `entity_type_id` 기본적으로 1개
* `email` - 이 필드는 새 고객이 계정을 만들 때 입력하는 이메일로 채워집니다
* `created_at` - 이 열은 각 사용자가 참여할 때 타임스탬프를 반환합니다

## `sales\_flat\_order (or Sales\_order` commerce 2.0 이상이 있는 경우)

계정 생성이 끝나면 `Sammy Customer` 이제 곧 구입을 시작할 겁니다 그녀는 웹사이트를 탐색할 때 `Throwback Bellbottoms` 하나 `V-Neck T-Shirt` 카트에 선택한 항목에 만족하여 체크아웃으로 이동하여 주문을 제출하면, [판매 플랫 주문 테이블](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**`**`subtotal`****`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id` - 이는 `sales_flat_order` 테이블.
   * Sammy Customer가 이 주문을 했을 때 위의 행이 `sales_flat_order` 테이블, 순서가 지정됨 `entity_id` = 227.
* `customer_id` - 이 열은 이 특정 순서를 지정한 고객의 고유 식별자입니다
   * 다음 `customer_id` 이 주문과 연관된 것은 214입니다. 새미 고객의 것입니다 `entity_id` on `customer_entity` 테이블.
* `subtotal` - 이 열은 주문에 대해 고객에게 부과된 총 금액입니다
   * &quot;투스롭백 하의&quot;와 &quot;V-Neck T-셔츠&quot; 두 쌍의 가격은 총 94.85달러였다
* `created_at` - 이 열은 각 주문이 작성되었을 때의 타임스탬프를 반환합니다

## `sales\_flat\_order\_item ( or Sales\_order\_item` commerce 2.0 이상이 있는 경우)

에 있는 단일 행 추가 `Sales\_flat\_order` 테이블 `Sammy Customer` 이 주문을 제출하면 해당 순서의 각 고유 항목에 대한 행이 [`sales\_flat\_order\_item` 표](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id` - 이 열은 `sales_flat_order_item` 표
   * `Sammy Customer`주문에 두 개의 개별 제품이 포함되어 있으므로 이 테이블에 두 개의 라인이 생성됩니다
* `name` - 이 열은 제품 이름입니다
* `product_id` - 이 열은 이 행이 참조하는 제품의 고유 식별자입니다
   * 위의 첫 번째 행은 다음과 같습니다 `product_id` = 205 `Throwback Bellbottoms` 있음 `entity_id` 205명 `catalog_product_entity` 표
* `order_id` - 이 열은 `entity_id` 이러한 특정 주문 항목이 포함된 주문
   * 위의 두 행은 모두 다음과 같습니다 `order_id` = 227이며, 둘 다 가 보낸 주문의 일부이므로 `Sammy Customer`: `entity_id` = 227 `sales_flat_order` 표
* `qty_ordered` - 이 열은 특정 순서에 포함된 제품 단위 수입니다
   * `Sammy Customer`의 순서대로 2쌍의 `Throwback Bellbottoms`
* `price` - 이 열은 주문 품목의 단일 단위 가격입니다
   * 다음 `subtotal` 변환 전: `Sammy Customer`주문 `sales_flat_order` 테이블은 94.85이며, 이 값은 두 쌍의 합입니다 `Throwback Bellbottoms` 각각 39.95달러 및 1 `V-Neck T-Shirt` 14달러 95센트입니다
