---
title: Enterprise_Rma_Item_Entity 테이블
description: 요청된 반품에서 특정 항목에 대한 정보를 분석하는 방법에 대해 알아봅니다.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/jBMtEluq3XNIzItebuvDQ43PAuW6mAsyG7RkHn8URJ4
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 08a466710b782238003c6bdb8cefacd07134291c
workflow-type: tm+mt
source-wordcount: 269
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
| `entity_id` | 테이블에 대한 고유 식별자. 각 `entity_id`은(는) 반환이 요청된 항목을 나타냅니다. |
| `rma_entity_id` | `enterprise_rma` 테이블에 연결된 외래 키입니다. |
| `status` | 항목 반환의 상태입니다. 값에는 &quot;받음&quot;, &quot;보류 중&quot;, &quot;인증됨&quot; 등이 포함됩니다. 이 상태의 값은 전체 반환 상태의 값과 일치하지 않을 수 있습니다. |
| `qty_requested` | 고객이 반품을 요청하는 수량입니다. |
| `qty_approved` | 반품이 승인된 수량입니다. |
| `qty_returned` | 반환된 수량입니다. |
| `order_item_id` | `sales_flat_order_item` 테이블에 연결된 외래 키입니다. |
| `product_sku` | 반환되는 sku. |

{style="table-layout:auto"}

## 공통 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Return date_requested` | 고객이 반환을 요청한 날짜입니다. |
| `Item price` | 항목의 가격입니다. |
| `Return item's total value (qty_returned * price)` | 반환된 항목의 총 통화 가치입니다. `enterprise_rma` 테이블의 총 반환 금액을 계산하는 데 사용됩니다. |

{style="table-layout:auto"}

## 일반 지표

| **지표 이름** | **설명** | **구성** |
|---|---|---|
| `Number of items returned` | 반환되는 항목의 수입니다. | 작업 열: 수량 반환<br>작업: 합계<br>타임스탬프 열: 반환 날짜 요청 |
| `Returned items' total value` | 반환된 금액입니다. | 공정 열: 반품 품목의 총 값(반품 수량 * 가격)<br>공정: 합계<br>타임스탬프 열: 반품 요청 일자 |

{style="table-layout:auto"}

## 다른 테이블에 대한 연결

`enterprise_rma`

* 다음 조인을 통해 `Return date_requested` 테이블에 `enterprise_rma_item_entity`과(와) 같은 조인된 열을 만듭니다.
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id `(많음) => `enterprise_rma.entity_id`(하나)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id `(많음) => `magento_rma.entity_id`(하나)

`sales_flat_order_item`

* 에 조인된 열 만들기  다음 조인을 통해 `enterprise_rma_item_entity` 테이블:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id `(많음) => `sales_flat_order_item.item_id`(하나)
* Commerce 2.x: `magento_rma_item_entity.order_item_id `(많음) => `sales_order_item.item_id`(하나)
