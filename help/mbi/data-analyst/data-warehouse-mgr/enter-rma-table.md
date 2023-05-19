---
title: enterprise_rma 테이블
description: 특정 반환 요청에 대한 정보를 분석하는 방법에 대해 알아봅니다.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# enterprise_rma 테이블

의 각 행 `enterprise_rma` 테이블(종종 호출됨) `magento_rma` Adobe Commerce 2.x에서 이름을 사용자 지정할 수 있습니다)에는 특정 반환 요청에 대한 정보가 포함되어 있습니다.

>[!NOTE]
>
>이 테이블은 다음과 같은 경우에만 Adobe Commerce 계정과 함께 제공됩니다. `Enterprise Edition` 또는 `Enterprise Cloud Edition` 고객.

## 일반 기본 열

| **열 이름** | **설명** |
|---|---|
| `entity\_id` | 테이블에 대한 고유 식별자. 각 `entity\_id` 반환 요청을 나타냅니다. |
| `date\_requested` | 반환 요청 날짜. |
| `status` | 반환 상태. 값에는 &quot;받음&quot;, &quot;보류 중&quot;, &quot;인증됨&quot; 등이 포함됩니다. |
| `order\_id` | 와(과) 연결된 외래 키 `sales\_flat\_order` 테이블. |
| `customer\_id` | 와(과) 연결된 외래 키 `customer\_entity` 테이블. |

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
| `Number of returns` | 요청한 반환 횟수입니다. | `Operation` 열: `entity id`<br>`Operation`: `Count`<br>`Timestamp` 열: `date requested` |
| `Total returned amount` | 반환된 총 금액. | `Operation `열: `Return's total value`<br>`Operation`: Sum<br>`Timestamp` 열: 요청한 날짜 |
| `Average returned amount` | 반환된 평균 금액입니다. | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` 열: `date requested` |
| `Average time to return` | 주문에서 반환까지의 평균 시간. | `Operation` 열: 주문 생성일과 반환 요청 날짜 사이의 초<br>`Operation`: `Average`<br>`Timestamp` 열: `date requested` |

{style="table-layout:auto"}

## 다른 테이블에 대한 연결

`sale_flat_order`

* 세그먼트화할 조인 열을 만들고, 의 주문 수준 속성별로 필터링 `enterprise_rma` 다음 조인을 통한 테이블:
   * Commerce 1.x: `enterprise_rma.order_id` (다) => `sales_flat_order.entity_id` (1)
   * Commerce 2.x: `magento_rma.order_id` (다) => `sales_order.entity_id` (1)

`enterprise_rma_item_entity`

* 다음과 같은 다대일 열 만들기 `Return's total value` 다음에 있음 `enterprise_rma` 다음 조인을 통한 테이블:
   * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id` (다) => `enterprise_rma.entity_id` (1)
   * Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (다) => `magento_rma.entity_id` (1)
