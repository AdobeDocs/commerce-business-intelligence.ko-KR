---
title: 전자 상거래 이탈
description: 전자 상거래 이탈 비율을 생성하고 분석하는 방법을 알아봅니다.
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# 이탈률

이 주제에서는 **이탈률** 에 대해 **상거래 고객**. SaaS 또는 기존 구독 회사와 달리, 상거래 고객은 일반적으로 구체적인 것이 없습니다 **&quot;churn 이벤트&quot;** 는 활성 고객에게 더 이상 계산되지 않아야 함을 나타냅니다. 이러한 이유로, 아래 지침에 따라 마지막 주문 이후 경과된 일정 시간을 기반으로 고객을 &quot;대량&quot;으로 정의할 수 있습니다.

![](../../assets/Churn_rate_image.png)

많은 고객이 다음을 개념화하기 시작하는 데 대한 지원을 원합니다 **일정** 데이터를 기반으로 사용해야 합니다. 이전 고객 행동을 사용하여 이를 정의하려면 **이탈 일정**&#x200B;를 사용하는 경우 [이탈 정의](../analysis/define-cust-churn.md) 문서. 그런 다음 아래 지침에 따라 이탈률 수식의 결과를 사용할 수 있습니다.

## 계산된 열

만들 열

* **`customer_entity`** 표
* **`Customer's last order date`**
   * 선택 [!UICONTROL definition]: `Max`
   * 선택 [!UICONTROL table]: `sales_flat_order`
   * 선택 [!UICONTROL column]: `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * 선택 [!UICONTROL definition]: `Age`
   * 선택 [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>다음을 확인하십시오 [새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에

## 지표

* **신규 고객(최초 주문 일자별)**
   * Adobe가 계산하는 고객

>[!NOTE]
>
>이 지표는 계정에 이미 있을 수 있습니다.

* 에서 **`customer_entity`** 표
* 이 지표는 다음을 수행합니다 **카운트**
* 설정 **`entity_id`** 열
* 정렬 기준 **`Customer's first order date`** timestamp
* [!UICONTROL Filter]:

* **새 고객(마지막 주문 날짜별)**
   * Adobe가 계산하는 고객

>[!NOTE]
>
>이 지표는 계정에 이미 있을 수 있습니다.

* 에서 **`customer_entity`** 표
* 이 지표는 다음을 수행합니다 **카운트**
* 설정 **`entity_id`** 열
* 정렬 기준 **`Customer's last order date`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>다음을 확인하십시오 [새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에

## 보고서

* **이탈률**
   * [!UICONTROL Metric]: 신규 고객(최초 주문 일자별)
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * 고객의 마지막 주문 날짜 이후 시간(초) >= [대량 고객에 대한 자체 정의 마감&#x200B;]**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]: `(B / ((A + B) - C)`
   * 

      [!UICONTROL Format]: Percentage

* *지표 `A`:`New customers cumulative`*
* *지표 `B`:`Churned customers by last order date`*
* *지표 `C`:`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

다음은 몇 가지 일반적인 월 > 두 번째 전환이지만, google에서는 찾을 수 있는 사용자 지정 값에 대한 주 > 초 변환을 포함하여 다른 값을 제공합니다.

| **개월** | **초** |
|---|---|
| 3 | 7,776,000 |
| 6 | 15,552,000 |
| 9 | 23,328,000 |
| 12 | 31,104,000 |

모든 보고서를 컴파일한 후 대시보드에서 원하는 대로 구성할 수 있습니다. 최종 결과는 위의 샘플 대시보드와 비슷합니다.
