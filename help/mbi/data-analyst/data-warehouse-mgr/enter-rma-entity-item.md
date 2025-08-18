---
title: Enterprise_Rma_Item_Entity 테이블
description: 요청된 반품에서 특정 항목에 대한 정보를 분석하는 방법에 대해 알아봅니다.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# enterprise_rma_item_entity 테이블

`enterprise_rma_item_entity` 테이블의 각 행(Commerce 2.x에서는 `magento_rma_item_entity`이라고도 하지만 이름을 사용자 지정할 수 있음)에는 요청된 반환의 특정 항목에 대한 정보가 포함되어 있습니다.

>[!NOTE]
>
>이 테이블은 `Enterprise Edition` 또는 `Enterprise Cloud Edition` 고객인 경우에만 Commerce 계정과 함께 제공됩니다.

## 일반 기본 열

| **열 이름** | **설명** |
|---|---|
| `entity\_id` | 테이블에 대한 고유 식별자. 각 `entity\_id`은(는) 반환이 요청된 항목을 나타냅니다. |
| `rma\_entity\_id` | `enterprise\_rma` 테이블에 연결된 외래 키입니다. |
| `status` | 항목 반환의 상태입니다. 값에는 &quot;받음&quot;, &quot;보류 중&quot;, &quot;인증됨&quot; 등이 포함됩니다. 이 상태의 값은 전체 반환 상태의 값과 일치하지 않을 수 있습니다. |
| `qty\_requested` | 고객이 반품을 요청하는 수량입니다. |
| `qty\_approved` | 반품이 승인된 수량입니다. |
| `qty\_returned` | 반환된 수량입니다. |
| `order\_item\_id` | `sales\_flat\_order\_item` 테이블에 연결된 외래 키입니다. |
| `product\_sku` | 반환되는 sku. |

{style="table-layout:auto"}

## 공통 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Return date\_requested` | 고객이 반환을 요청한 날짜입니다. |
| `Item price` | 항목의 가격입니다. |
| `Return item's total value (qty\_returned * price)` | 반환된 항목의 총 통화 가치입니다. `enterprise\_rma` 테이블의 총 반환 금액을 계산하는 데 사용됩니다. |

{style="table-layout:auto"}

## 일반 지표

| **지표 이름** | **설명** | **구성** |
|---|---|---|
| `Number of items returned` | 반환되는 항목의 수입니다. | 작업 열: 수량 반환<br>작업: 합계<br>타임스탬프 열: 반환 날짜 요청 |
| `Returned items' total value` | 반환된 금액입니다. | 공정 열: 반품 품목의 총 값(반품 수량 * 가격)<br>공정: 합계<br>타임스탬프 열: 반품 요청 일자 |

{style="table-layout:auto"}

## 다른 테이블에 대한 연결

`enterprise_rma`

* 다음 조인을 통해 `Return date\_requested` 테이블에 `enterprise_rma_item_entity`과(와) 같은 조인된 열을 만듭니다.
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id `(많음) => `enterprise_rma.entity_id`(하나)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id `(많음) => `magento_rma.entity_id`(하나)

`sales_flat_order_item`

* 에 조인된 열 만들기  다음 조인을 통해 `enterprise_rma_item_entity` 테이블:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id `(많음) => `sales_flat_order_item.item_id`(하나)
* Commerce 2.x: `magento_rma_item_entity.order_item_id `(많음) => `sales_order_item.item_id`(하나)
