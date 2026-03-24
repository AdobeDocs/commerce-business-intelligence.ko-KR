---
title: enterprise_rma 테이블
description: 특정 반환 요청에 대한 정보를 분석하는 방법에 대해 알아봅니다.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/ofPlk5xNr8aspjFlpzEtDtjcOPm9DrQFYX9-vPDfK6w
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 0%

---

# enterprise_rma 테이블

`enterprise_rma` 테이블의 각 행(Adobe Commerce 2.x에서는 `magento_rma`이라고도 하지만 이름을 사용자 지정할 수 있음)에는 특정 반환 요청에 대한 정보가 포함되어 있습니다.

>[!NOTE]
>
>이 테이블은 `Enterprise Edition` 또는 `Enterprise Cloud Edition` 고객인 경우에만 Adobe Commerce 계정과 함께 제공됩니다.

## 일반 기본 열

| **열 이름** | **설명** |
|---|---|
| `entity\_id` | 테이블에 대한 고유 식별자. 각 `entity\_id`은(는) 반환 요청을 나타냅니다. |
| `date\_requested` | 반환 요청 날짜. |
| `status` | 반환 상태. 값에는 &quot;받음&quot;, &quot;보류 중&quot;, &quot;인증됨&quot; 등이 포함됩니다. |
| `order\_id` | `sales\_flat\_order` 테이블에 연결된 외래 키입니다. |
| `customer\_id` | `customer\_entity` 테이블에 연결된 외래 키입니다. |

{style="table-layout:auto"}

## 공통 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Order's created\_at` | 원래 주문한 날짜입니다. 주문과 반환 요청 사이의 시간을 구하는 데 사용할 수 있습니다. |
| `Customer's order number` | 원래 주문과 연관된 고객의 주문 번호입니다. |
| `Seconds between order's created\_at and return's date\_requested` | 주문 날짜부터 반환 요청까지의 시간(초). |
| `Return's total value` | 이는 반환되는 총 금액입니다. 각 반품 항목의 개별 반품 금액의 합계입니다. |

{style="table-layout:auto"}

## 일반 지표

| **지표 이름** | **설명** | **구성** |
|---|---|---|
| `Number of returns` | 요청한 반환 횟수입니다. | `Operation` 열: `entity id`<br>`Operation`: `Count`<br>`Timestamp` 열: `date requested` |
| `Total returned amount` | 반환된 총 금액. | `Operation `열: `Return's total value`<br>`Operation`: 합계<br>`Timestamp` 열: 요청한 날짜 |
| `Average returned amount` | 반환된 평균 금액입니다. | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` 열: `date requested` |
| `Average time to return` | 주문에서 반환까지의 평균 시간. | `Operation` 열: 주문에서 만든 날짜와 요청한 반환 날짜 사이의 초<br>`Operation`: `Average`<br>`Timestamp` 열: `date requested` |

{style="table-layout:auto"}

## 다른 테이블에 대한 연결

`sale_flat_order`

* 다음 조인을 통해 `enterprise_rma` 테이블의 순서 수준 특성을 세분화하고 필터링할 조인된 열을 만듭니다.
   * Commerce 1.x: `enterprise_rma.order_id`(많음) => `sales_flat_order.entity_id`(하나)
   * Commerce 2.x: `magento_rma.order_id`(많음) => `sales_order.entity_id`(하나)

`enterprise_rma_item_entity`

* 다음 조인을 통해 `Return's total value` 테이블에 `enterprise_rma`과(와) 같은 다대일 열을 만듭니다.
   * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id`(많음) => `enterprise_rma.entity_id`(하나)
   * Commerce 2.x: `magento_rma_item_entity.rma_entity_id `(많음) => `magento_rma.entity_id`(하나)
