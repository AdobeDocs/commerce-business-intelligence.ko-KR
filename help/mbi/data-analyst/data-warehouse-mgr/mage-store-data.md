---
title: Adobe Commerce에 데이터 저장
description: 데이터가 생성되는 방법, 새 행이 삽입되는 원인 및 Adobe Commerce 데이터베이스에 작업이 기록되는 방법에 대해 알아봅니다.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# [!DNL Adobe Commerce]에 데이터 저장 중

[!DNL Adobe Commerce] 플랫폼은 수백 개의 테이블에 걸쳐 중요한 다양한 상거래 데이터를 기록하고 구성합니다. 이 항목에서는 다음을 설명합니다.

* 데이터 생성 방법
* 이유 때문에 새 행이 [핵심 Commerce 표](../data-warehouse-mgr/common-mage-tables.md) 중 하나에 삽입됩니다.
* 구매 또는 계정 만들기와 같은 작업을 [!DNL Adobe Commerce] 데이터베이스에 기록하는 방법

이러한 개념에 대해 논의하려면 다음 예를 참조하십시오.

`Clothes4U`은(는) 온라인 및 오프라인 매장 모두를 보유한 의류 소매점입니다. 웹 사이트 뒤에 있는 [!DNL Magento Open Source]을(를) 사용하여 데이터를 수집하고 구성합니다.

## `catalog\_product\_entity`

9월 22일이며 `Clothes4U`이(가) 가을 라인으로 세 개의 새 항목 `Throwback Bellbottoms`, `Straight Leg Jeans`, `V-Neck T-Shirts`을(를) 롤아웃합니다. `Clothes4U` 직원이 Commerce 관리자를 열고 **[!UICONTROL Add Product]**&#x200B;을(를) 클릭한 다음 `Throwback Bellbottoms`에 대한 모든 정보를 입력합니다.

`Throwback Bellbottoms`에 대한 모든 설정에 만족하면 직원이 **[!UICONTROL Save]**&#x200B;을(를) 클릭하여 아래의 첫 번째 줄을 `catalog_product_entity` 테이블에 삽입합니다. 직원은 프로세스를 반복하여 `Straight Leg Jeans`에 대해 다른 Commerce 제품을 만든 다음 `V-Neck T-Shirt`에 대해 세 번째 라인을 만들고 아래의 두 번째 라인과 세 번째 라인을 `catalog_product_entity` 테이블에 삽입합니다.

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id` - `catalog_product_entity` 테이블의 기본 키입니다. 즉, 테이블의 모든 행에 다른 `entity_id`이(가) 있어야 합니다. 이 테이블의 각 `entity_id`은(는) 하나의 제품에만 연결할 수 있으며 각 제품은 하나의 `entity_id`에만 연결할 수 있습니다.
   * 위 표의 맨 위 줄 `entity_id` = 205는 &quot;Throwback Bellbottom&quot;에 대해 만들어진 새 행입니다. Commerce 플랫폼에 `entity_id` = 205가 나타나면 &quot;Throwback Bellbottom&quot; 제품을 참조합니다.
* `entity_type_id` - Commerce에는 여러 범주의 개체(예: 고객, 주소 및 제품 등)가 있으며, 이 열은 이 특정 행이 속한 범주를 나타내는 데 사용됩니다.
   * `catalog_product_entity` 테이블인 각 행에는 동일한 엔터티 형식(product)이 있습니다. Adobe Commerce에서 제품에 대한 `entity_type_id`은(는) 4입니다. 따라서 만들어진 세 개의 새 제품이 모두 이 열에 대해 4를 반환합니다.
* `attribute_set_id` - 특성 집합은 같은 설명자가 있는 제품을 식별하는 데 사용됩니다.
   * 테이블의 맨 위 두 행은 `Throwback Bellbottoms` 및 `Straight Leg Jeans` 제품이며 둘 다 바지입니다. 이러한 제품에는 동일한 설명자(예: 이름, 인심, 허리줄)가 있으므로 동일한 `attribute_set_id`이(가) 있습니다. 세 번째 항목 `V-Neck T-Shirt`에는 바지와 같은 설명자가 없으므로 다른 `attribute_set_id`이(가) 있습니다. 셔츠에는 허리선이나 인심이 없습니다.
* `sku` - Adobe Commerce에서 제품을 만들 때 사용자가 각 제품에 할당한 고유한 값입니다.
* `created_at` - 이 열은 각 제품이 만들어진 시점의 타임스탬프를 반환합니다.

## `customer\_entity`

새 제품 3개를 추가한 직후 새 고객 `Sammy Customer`이(가) 처음으로 `Clothes4U`의 웹 사이트를 방문합니다. `Clothes4U`이(가) 게스트 주문을 허용하지 않으므로 `Sammy Customer`은(는) 먼저 웹 사이트에서 계정을 만들어야 합니다. 고객이 필요한 자격 증명을 입력하고 제출을 클릭하여 [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md)에 다음과 같은 새 항목을 만듭니다.

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - 이전 테이블과 마찬가지로 `entity_id`은(는) `customer_entity` 테이블의 기본 키입니다.
   * `Sammy Customer`이(가) 계정을 만들고 위의 행을 `customer_entity` 테이블에 썼을 때 고객에게 `entity_id` = 214가 할당되었습니다. 모든 테이블에서 `entity_id` = 214로 식별된 고객은 항상 사용자 Sammy 고객을 참조합니다
* `entity_type_id` - 이 열은 이 테이블에 나열되는 엔터티 형식을 식별하며 `catalog_product_entity` 테이블과 동일한 방식으로 작동합니다
   * `customer_entity` 테이블의 모든 행은 고객이며 Commerce은 기본적으로 고객을 `entity_type_id` 1로 정의합니다
* `email` - 이 필드는 새 고객이 계정을 만들 때 입력한 전자 메일로 채워집니다.
* `created_at` - 이 열은 각 사용자가 가입했을 때의 타임스탬프를 반환합니다.

## [!DNL Adobe Commerce 2.x]이(가) 있는 경우 `sales\_flat\_order (or Sales\_order`

계정 생성이 완료되면 `Sammy Customer`이(가) 구매를 시작할 준비가 되었습니다. 웹 사이트에서 고객이 두 쌍의 `Throwback Bellbottoms`과(와) 한 쌍의 `V-Neck T-Shirt`을(를) 장바구니에 추가합니다. 선택에 만족하면 고객이 체크아웃으로 이동하여 주문을 제출하고 [sales flat order table](../data-warehouse-mgr/sales-flat-order-table.md)에 다음 항목을 만듭니다.

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id` - `sales_flat_order` 테이블의 기본 키입니다.
   * Sammy 고객이 이 주문을 하고 위의 행이 `sales_flat_order` 테이블에 작성되면 해당 주문이 `entity_id` = 227로 할당되었습니다.
* `customer_id` - 이 열은 이 특정 주문을 한 고객의 고유 식별자입니다.
   * 이 주문과 연결된 `customer_id`은(는) 214입니다. 이 값은 `customer_entity` 테이블에 있는 Sammy 고객의 `entity_id`입니다.
* `subtotal` - 이 열은 주문에 대해 고객에게 청구된 총 금액입니다.
   * &#39;트로우백 벨바텀&#39;과 &#39;브이넥 티셔츠&#39; 두 켤레의 가격은 총 94.85달러였다
* `created_at` - 이 열은 각 순서가 만들어진 시점의 타임스탬프를 반환합니다.

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(Commerce 2.0 이상이 있는 경우)

`Sales\_flat\_order` 테이블의 단일 행 외에 `Sammy Customer`이(가) 순서를 제출하면 해당 순서의 각 고유 항목에 대한 행이 [`sales\_flat\_order\_item` 테이블에 삽입됩니다](../data-warehouse-mgr/sales-flat-order-item-table.md).

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id` - 이 열은 `sales_flat_order_item` 테이블의 기본 키입니다.
   * `Sammy Customer`의 주문에 두 개의 개별 제품이 포함되어 있으므로 이 테이블에 두 개의 줄이 생성되었습니다.
* `name` - 이 열은 제품 이름입니다.
* `product_id` - 이 열은 이 행이 참조하는 제품의 고유 식별자입니다.
   * `catalog_product_entity` 테이블에 `Throwback Bellbottoms`의 `entity_id`이(가) 205이므로 위의 첫 번째 행에 `product_id` = 205가 있습니다.
* `order_id` - 이 열은 이러한 특정 주문 항목을 포함하는 주문의 `entity_id`입니다.
   * 위의 두 행은 모두 `sales_flat_order` 테이블에 `entity_id` = 227이 있는 `Sammy Customer`에서 수행한 주문의 일부이므로 `order_id` = 227이 있습니다
* `qty_ordered` - 이 열은 이 특정 주문에 포함된 제품의 단위 수입니다.
   * `Sammy Customer`의 주문에는 두 쌍의 `Throwback Bellbottoms`이(가) 포함되어 있습니다.
* `price` - 이 열은 주문 항목의 단일 단위 가격입니다.
   * `sales_flat_order` 테이블의 `Sammy Customer` 순서에서 `subtotal`은(는) 각각 $39.95에 있는 두 쌍의 `Throwback Bellbottoms`과(와) $14.95에 있는 한 쌍의 `V-Neck T-Shirt`을(를) 합한 94.85입니다.
