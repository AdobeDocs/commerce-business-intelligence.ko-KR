---
title: 고객 이탈 정의
description: 트랜잭션 고객을 위한 이탈을 정의하는 데 도움이 되는 대시보드를 설정하는 방법을 알아봅니다.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
source-git-commit: 3557e6370fae637cd74550b2806847bebe61d5d3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 트랜잭션 고객 이탈

이 문서에서는 트랜잭션 고객을 위한 이탈을 정의하는 데 도움이 되는 대시보드를 설정하는 방법을 보여줍니다.

![](../../assets/churn-deashboard.png)

이 분석에는 다음이 포함됩니다 [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md).

## 계산된 열

만들 열

* `customer_entity` 표
* `Customer's lifetime number of orders`
* 정의를 선택합니다. `Count`
* 선택 [!UICONTROL table]: `sales_flat_order`
* 선택 [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* 주문 수

* `sales_flat_order` 표
* `Customer's lifetime number of orders`
* 정의를 선택합니다. 조인된 열
* 선택 [!UICONTROL table]: `customer_entity`
* 선택 [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* 정의를 선택합니다. `Age`
* 선택 [!UICONTROL column]: `created_at`

* **`Customer's order number`** 분석가가 의 일부로 **[이탈 정의]** 티켓
* **`Is customer's last order`** 분석가가 의 일부로 **[이탈 정의]** 티켓
* **`Seconds since previous order`** 분석가가 의 일부로 **[이탈 정의]** 티켓
* **`Months since order`** 분석가가 의 일부로 **[이탈 정의]** 티켓
* **`Months since previous order`** 분석가가 의 일부로 **[이탈 정의]** 티켓

## 지표

새 지표가 없습니다!

>[!NOTE]
>
>다음을 확인하십시오 [새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에

## 보고서

* **초기 반복 순서 확률**
* 지표 A: 모든 시간 반복 주문
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 지표 B: 모든 시간 주문
* [!UICONTROL Metric]: 주문 수

* [!UICONTROL Formula]: 초기 반복 순서 확률
* 
   [[!UICONTROL 공식]: `A/B`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart type]: `Scalar`

* **주문 이후 개월 동안 반복 주문 가능성**
* 지표 A: 이전 주문 이후 개월별로 주문 반복(숨기기)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 지표 B: 주문 이후 개월별 마지막 주문(숨기기)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 지표 C: 모든 시간 반복 주문(숨기기)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 

   [[!UICONTROL 그룹]: `Independent`

* 지표 D: 마지막 주문 시간(숨기기)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 

   [[!UICONTROL 그룹]: `Independent`

* [!UICONTROL Formula]: 초기 반복 순서 확률
* 
   [[!UICONTROL 공식]: `(C-A)/(C+D-A-B)`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* top.bottom 표시: 카테고리 이름별로 정렬된 상위 24개 카테고리

* 

   [!UICONTROL Chart type]: `Line`

초기 반복 주문 확률 보고서는 총 반복 주문 / 총 주문 수를 나타냅니다. 모든 주문은 재주문을 할 수 있는 기회이다. 반복 주문 수는 실제로 수행하는 주문의 하위 집합입니다.

우리가 사용하는 공식은 (X개월 이후에 발생한 총 반복 주문 수)/ (X개월 이상인 총 주문)로 단순화됩니다. 이는 지금까지 주문 이후 X개월이라는 점을 감안할 때 사용자가 다른 주문을 제출할 가능성이 Y%라는 것을 보여줍니다.

대시보드를 구축한 후 가장 일반적인 질문은 다음과 같습니다. 이탈 임계값을 결정하려면 어떻게 해야 합니까?

**이것에 대한 &quot;하나의 옳은 대답&quot;은 없다.** 그러나 선이 초기 반복 확률 비율의 절반인 값을 교차하는 지점을 찾는 것이 좋습니다. 이것이 우리가 &quot;사용자가 반복적인 주문을 하려고 한다면, 그들은 아마 지금쯤 그것을 했을 것입니다&quot;라고 말할 수 있는 지점입니다. 궁극적으로 목표는 &quot;유지&quot;에서 &quot;재활성화&quot; 노력으로 전환하는 것이 적절할 수 있는 임계값을 선택하는 것입니다.

모든 보고서를 컴파일한 후 대시보드에서 원하는 대로 구성할 수 있습니다. 최종 결과는 페이지 맨 위의 이미지와 같을 수 있습니다

이 분석을 작성하는 동안 질문이 있거나 전문 서비스 팀에 참여하려는 경우 [연락처 지원](../../guide-overview.md).
