---
title: Adobe Commerce에 데이터 저장
description: 데이터가 생성되는 방법, 새 행이 삽입되는 원인 및 Adobe Commerce 데이터베이스에 작업이 기록되는 방법에 대해 알아봅니다.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# 데이터 저장 [!DNL Adobe Commerce]

다음 [!DNL Adobe Commerce] 플랫폼은 수백 개의 테이블에 걸쳐 중요한 다양한 상거래 데이터를 기록하고 구성합니다. 이 항목에서는 다음을 설명합니다.

* 데이터 생성 방법
* 새 행이 다음 중 하나에 삽입되는 이유 [Core Commerce 표](../data-warehouse-mgr/common-mage-tables.md)
* 구매 또는 계정 생성과 같은 작업을 [!DNL Adobe Commerce] 데이터베이스

이러한 개념에 대해 논의하려면 다음 예를 참조하십시오.

`Clothes4U` 은 온라인 및 오프라인 매장 모두를 갖춘 의류 소매업체입니다. 다음을 사용합니다 [!DNL Magento Open Source] 웹 사이트 뒤쪽에서 데이터를 수집하고 구성합니다.

## `catalog\_product\_entity`

9월 22일이고, `Clothes4U` 은(는) 가을 라인으로 세 개의 새 항목을 롤아웃합니다. `Throwback Bellbottoms`, `Straight Leg Jeans`, 및 `V-Neck T-Shirts`. A `Clothes4U` 직원이 상거래 관리자를 열고 클릭 수 **[!UICONTROL Add Product]**&#x200B;및 의 모든 정보를 입력합니다. `Throwback Bellbottoms`.

의 모든 설정에 만족함 `Throwback Bellbottoms`, 직원이 클릭 **[!UICONTROL Save]**: 아래에 있는 첫 번째 줄을 `catalog_product_entity` 테이블. 직원이 프로세스를 반복하여 다른 Commerce 제품을 만듭니다. `Straight Leg Jeans`, 그리고 다음에 대한 세 번째 `V-Neck T-Shirt`, 아래의 두 번째 및 세 번째 줄을 `catalog_product_entity` 표:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id` - 의 기본 키입니다 `catalog_product_entity` 테이블, 즉, 테이블의 모든 행에 다른 값이 있어야 합니다. `entity_id`. 각 `entity_id` 이 테이블의 제품은 하나의 제품에만 연결될 수 있으며 각 제품은 하나의 제품에만 연결될 수 있습니다. `entity_id`
   * 위 표의 맨 위 줄 `entity_id` = 205, 는 &quot;Throwback Bellbottom&quot;에 대해 생성된 새 행입니다. 어디서나 `entity_id` = 205는 상거래 플랫폼에 나타나며 &quot;Throwback Bellbottom&quot; 제품을 나타냅니다.
* `entity_type_id` - Commerce에는 여러 범주의 객체(예: 고객, 주소 및 제품)가 있으며 이 열은 이 특정 행이 속한 범주를 나타내는 데 사용됩니다.
   * 이 은(는) 입니다. `catalog_product_entity` 테이블의 각 행에는 동일한 엔티티 유형(제품)이 있습니다. Adobe Commerce에서 `entity_type_id` for product는 4이므로 새로 만든 세 가지 제품 모두 이 열에 대해 return 4를 사용합니다.
* `attribute_set_id` - 속성 세트는 설명자와 동일한 제품을 식별하는 데 사용됩니다.
   * 표의 위쪽 두 행은 입니다. `Throwback Bellbottoms` 및 `Straight Leg Jeans` 둘 다 바지인 제품들입니다. 이러한 제품은 동일한 설명자(예: 이름, 인심, 허리 라인)를 가지므로 동일한 설명자를 갖습니다 `attribute_set_id`. 세 번째 항목, `V-Neck T-Shirt` 다른 항목 있음 `attribute_set_id` 왜냐하면 그것은 바지와 같은 설명자를 가지고 있지 않을 것이기 때문이다; 셔츠는 허리띠나 인솔선이 없다.
* `sku` - Adobe Commerce에서 제품을 만들 때 사용자가 각 제품에 할당한 고유한 값입니다.
* `created_at` - 이 열은 각 제품이 만들어진 시점의 타임스탬프를 반환합니다.

## `customer\_entity`

새로운 고객인 세 가지 신제품이 추가된 직후 `Sammy Customer`, 방문 횟수 `Clothes4U`의 웹 사이트가 처음으로 추가되었습니다. 다음 이후 `Clothes4U` 은(는) 게스트 주문을 허용하지 않습니다. `Sammy Customer` 먼저 웹 사이트에서 계정을 만들어야 합니다. 고객이 필요한 자격 증명을 입력하고 제출 을 클릭하여 [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - 앞의 테이블처럼 `entity_id` 는 의 기본 키입니다. `customer_entity` 테이블.
   * 날짜 `Sammy Customer` 이(가) 계정을 만들었고 위의 행이 `customer_entity` 테이블, 고객이 할당됨 `entity_id` = 214. 모든 테이블에서 고객은 `entity_id` = 214는 항상 사용자 Sammy 고객을 나타냅니다.
* `entity_type_id` - 이 열은 이 테이블에 나열되는 엔티티 유형을 식별하며 에서와 동일한 방식으로 작동합니다. `catalog_product_entity` 표
   * 의 모든 행 `customer_entity` 테이블은 고객이고 Commerce는 고객을 다음과 같이 정의합니다. `entity_type_id` 기본적으로 1개
* `email` - 이 필드는 새 고객이 계정을 만들 때 입력하는 이메일로 채워집니다.
* `created_at` - 이 열은 각 사용자가 가입한 시점의 타임스탬프를 반환합니다.

## `sales\_flat\_order (or Sales\_order` 다음을 보유한 경우 [!DNL Adobe Commerce 2.x]

계정 생성이 완료되고 `Sammy Customer` 구매를 시작할 준비가 되었습니다. 웹 사이트에서 고객은 `Throwback Bellbottoms` 및 1 `V-Neck T-Shirt` 장바구니에. 선택에 만족하면 고객이 체크아웃으로 이동하여 주문을 제출하고 [판매 플랫 주문 테이블](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id` - 의 기본 키입니다. `sales_flat_order` 테이블.
   * Sammy 고객이 이 주문을 하고 위의 행이 `sales_flat_order` 테이블, 주문이 할당되었습니다. `entity_id` = 227.
* `customer_id` - 이 열은 해당 특정 주문을 한 고객의 고유 식별자입니다.
   * 다음 `customer_id` 해당 주문과 연계된 주문은 214로, Sammy Customer&#39;s `entity_id` 다음에 있음 `customer_entity` 테이블.
* `subtotal` - 이 열은 주문에 대해 고객에게 청구된 총 금액입니다.
   * &#39;트로우백 벨바텀&#39;과 &#39;브이넥 티셔츠&#39; 두 켤레의 가격은 총 94.85달러였다
* `created_at` - 이 열은 각 순서가 생성된 시기에 대한 타임스탬프를 반환합니다.

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(Commerce 2.0 이상이 있는 경우)

의 단일 행 외에도 `Sales\_flat\_order` 테이블, 조건 `Sammy Customer` 주문을 제출하면 해당 주문의 각 고유 항목에 대한 행이 [`sales\_flat\_order\_item` 표](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id` - 이 열은 `sales_flat_order_item` 표
   * `Sammy Customer`주문에 두 개의 고유 제품이 포함되어 있으므로 의 주문은 이 테이블에 두 개의 라인을 생성했습니다.
* `name` - 이 열은 제품 이름입니다.
* `product_id` - 이 열은 이 행이 참조하는 제품에 대한 고유 식별자입니다.
   * 위의 첫 번째 행에 이 있습니다. `product_id` = 205 이유 `Throwback Bellbottoms` 다음 권한 보유 `entity_id` / 205 의 `catalog_product_entity` 표
* `order_id` - 이 열은 `entity_id` 이러한 특정 주문 항목을 포함하는 주문
   * 위의 두 행 모두 `order_id` = 227. 두 값 모두 다음에 의해 배치된 주문의 일부이기 때문입니다. `Sammy Customer`, , `entity_id` = 227( `sales_flat_order` 표
* `qty_ordered` - 이 열은 이 특정 주문에 포함된 제품의 단위 수입니다.
   * `Sammy Customer`의 주문에는 다음 두 쌍이 포함되어 있습니다. `Throwback Bellbottoms`
* `price` - 이 열은 주문 품목의 단일 단위 가격입니다.
   * 다음 `subtotal` 출처: `Sammy Customer`의 순서 `sales_flat_order` 표는 두 쌍의 합인 94.85였다. `Throwback Bellbottoms` 각각 $39.95이고 1입니다 `V-Neck T-Shirt` 14.95달러입니다.
