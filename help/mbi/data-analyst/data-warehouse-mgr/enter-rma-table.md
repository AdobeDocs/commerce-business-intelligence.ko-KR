---
title: enterprise_rma 테이블
description: 특정 반환 요청에 대한 정보를 분석하는 방법을 알아봅니다.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# enterprise_rma 테이블

의 각 행 `enterprise_rma` 테이블(종종 `magento_rma` commerce 2.x에서는 이름을 사용자 지정할 수 있지만, 특정 반환 요청에 대한 정보가 포함됩니다.

>[!NOTE]
>
>이 테이블은 상거래 계정을 사용하는 경우에만 표준이 됩니다 `Enterprise Edition` 또는 `Enterprise Cloud Edition` 고객.

## 공통 기본 열

| **열 이름** | **설명** |
|---|---|
| `entity\_id` | 테이블의 고유 식별자입니다. 각 `entity\_id` 반환 요청을 나타냅니다. |
| `date\_requested` | 반품이 요청된 날짜입니다. |
| `status` | 반환의 상태입니다. 값에는 &#39;received&#39;, &#39;pending&#39;, &#39;authorized&#39; 등이 포함됩니다. |
| `order\_id` | 와 연결된 외부 키 `sales\_flat\_order` 테이블. |
| `customer\_id` | 와 연결된 외부 키 `customer\_entity` 테이블. |

{style=&quot;table-layout:auto&quot;}

## 일반적인 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Order's created\_at` | 원래 주문 날짜입니다. 주문과 반환 요청 사이의 시간을 가져오는 데 사용할 수 있습니다. |
| `Customer's order number` | 최초 주문과 연관된 고객의 주문 번호입니다. |
| `Seconds between order's created\_at and return's date\_requested` | 주문 날짜에서 반환 요청까지의 시간(초)입니다. |
| `Return's total value` | 반환되는 총 통화량입니다. 이것은 각 반품 품목의 개별 반품 금액의 합계입니다. |

{style=&quot;table-layout:auto&quot;}

## 일반 지표

| **지표 이름** | **설명** | **건설** |
|---|---|---|
| `Number of returns` | 요청한 반환 수입니다. | `Operation` 열: `entity id`<br>`Operation`: `Count`<br>`Timestamp` 열: `date requested` |
| `Total returned amount` | 반환된 총 통화 금액입니다. | `Operation `열: `Return's total value`<br>`Operation`: 합계<br>`Timestamp` 열: 요청한 날짜 |
| `Average returned amount` | 반환된 평균 통화 금액입니다. | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` 열: `date requested` |
| `Average time to return` | 주문에서 반환까지의 평균 시간입니다. | `Operation` 열: 주문과 반환 날짜 사이의 시간(초)<br>`Operation`: `Average`<br>`Timestamp` 열: `date requested` |

{style=&quot;table-layout:auto&quot;}

## 다른 테이블에 연결

`sale_flat_order`

* 연결된 열을 만들어 세그먼트 및 필터링 `enterprise_rma` 다음 조인을 통한 표:
   * Commerce 1.x: `enterprise_rma.order_id` (다) => `sales_flat_order.entity_id` (1)
   * Commerce 2.x: `magento_rma.order_id` (다) => `sales_order.entity_id` (1)

`enterprise_rma_item_entity`

* 과 같은 일대일 열 만들기 `Return's total value` on `enterprise_rma` 다음 조인을 통한 표:
   * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id` (다) => `enterprise_rma.entity_id` (1)
   * Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (다) => `magento_rma.entity_id` (1)
