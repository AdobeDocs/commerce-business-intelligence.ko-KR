---
title: Enterprise_Rma_Item_Entity 테이블
description: 요청된 리턴에서 특정 항목에 대한 정보를 분석하는 방법을 알아봅니다.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# enterprise_rma_item_entity 테이블

의 각 행 `enterprise_rma_item_entity` 테이블(종종 `magento_rma_item_entity` commerce 2.x에서는 이름을 사용자 지정할 수 있지만, 요청된 반환의 특정 항목에 대한 정보가 포함됩니다.

>[!NOTE]
>
>이 테이블은 상거래 계정을 사용하는 경우에만 표준이 됩니다 `Enterprise Edition` 또는 `Enterprise Cloud Edition` 고객.

## 공통 기본 열

| **열 이름** | **설명** |
|---|---|
| `entity\_id` | 테이블의 고유 식별자입니다. 각 `entity\_id` 반환이 요청된 항목을 나타냅니다. |
| `rma\_entity\_id` | 와 연결된 외부 키 `enterprise\_rma` 테이블. |
| `status` | 항목의 반환 상태입니다. 값에는 &#39;received&#39;, &#39;pending&#39;, &#39;authorized&#39; 등이 포함됩니다. 이 상태의 값은 전체 반환 상태의 값과 반드시 일치하지 않습니다. |
| `qty\_requested` | 고객이 반품을 요청하는 수량입니다. |
| `qty\_approved` | 반품을 위해 승인된 수량. |
| `qty\_returned` | 실제로 반환된 양입니다. |
| `order\_item\_id` | 와 연결된 외부 키 `sales\_flat\_order\_item` 테이블. |
| `product\_sku` | 반환되는 sku입니다. |

{style=&quot;table-layout:auto&quot;}

## 일반적인 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Return date\_requested` | 고객이 반품을 요청한 날짜입니다. |
| `Item price` | 품목 가격입니다. |
| `Return item's total value (qty\_returned * price)` | 반환되는 항목의 총 통화 값입니다. 이 값은 `enterprise\_rma` 테이블. |

{style=&quot;table-layout:auto&quot;}

## 일반 지표

| **지표 이름** | **설명** | **건설** |
|---|---|---|
| `Number of items returned` | 반환되는 항목의 수입니다. | 작업 열: 반환된 수량<br>작업: 합계<br>타임스탬프 열: 요청한 반환 날짜 |
| `Returned items' total value` | 반환된 통화량입니다. | 작업 열: 반품 품목의 총 값(반환된 수량 * 가격)<br>작업: 합계<br>타임스탬프 열: 요청한 반환 날짜 |

{style=&quot;table-layout:auto&quot;}

## 다른 테이블에 연결

`enterprise_rma`

* 다음과 같은 연결된 열 만들기 `Return date\_requested` on `enterprise_rma_item_entity` 다음 조인을 통한 표:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (다) => `enterprise_rma.entity_id` (1)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (다) => `magento_rma.entity_id` (1)

`sales_flat_order_item`

* 에 연결된 열 만들기  `enterprise_rma_item_entity` 다음 조인을 통한 표:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (다) => `sales_flat_order_item.item_id` (1)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (다) => `sales_order_item.item_id` (1)
