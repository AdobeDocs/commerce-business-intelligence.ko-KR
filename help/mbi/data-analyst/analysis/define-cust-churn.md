---
title: 고객 이탈 정의
description: 트랜잭션 고객에 대한 이탈을 정의하는 데 도움이 되는 대시보드를 설정하는 방법에 대해 알아봅니다.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# 트랜잭션 고객 이탈

이 문서에서는 트랜잭션 고객에 대한 이탈을 정의하는 데 도움이 되는 대시보드를 설정하는 방법을 보여 줍니다.

![](../../assets/churn-deashboard.png)

이 분석에는 다음이 포함됩니다. [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md).

## 계산된 열

생성할 열

* `customer_entity` 표
* `Customer's lifetime number of orders`
* 정의 선택: `Count`
* 선택 [!UICONTROL table]: `sales_flat_order`
* 선택 [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* 계산되는 주문

* `sales_flat_order` 표
* `Customer's lifetime number of orders`
* 정의 선택: 조인된 열
* 선택 [!UICONTROL table]: `customer_entity`
* 선택 [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* 정의 선택: `Age`
* 선택 [!UICONTROL column]: `created_at`

* **`Customer's order number`** 는 분석가가 의 일부로 만듭니다. **[이탈 정의]** 티켓
* **`Is customer's last order`** 는 분석가가 의 일부로 만듭니다. **[이탈 정의]** 티켓
* **`Seconds since previous order`** 는 분석가가 의 일부로 만듭니다. **[이탈 정의]** 티켓
* **`Months since order`** 는 분석가가 의 일부로 만듭니다. **[이탈 정의]** 티켓
* **`Months since previous order`** 는 분석가가 의 일부로 만듭니다. **[이탈 정의]** 티켓

## 지표

새 지표가 없습니다!

>[!NOTE]
>
>다음을 확인하십시오. [새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에

## 보고서

* **초기 반복 순서 확률**
* 지표 A: 모든 시간 반복 주문
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 지표 B: 역대 주문
* [!UICONTROL Metric]: 주문 수

* [!UICONTROL Formula]: 초기 반복 순서 확률
* 
   [!UICONTROL 공식]: `A/B`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart type]: `Scalar`

* **주문 이후 주어진 개월 반복 주문 확률**
* 지표 A: 이전 주문 이후 매월 주문 반복(숨기기)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 지표 B: 주문 이후 개월별 마지막 주문(숨기기)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 지표 C: 모든 시간 반복 주문 (숨기기)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 

   [!UICONTROL 그룹 기준]: `Independent`

* 지표 D: 역대 마지막 주문 수(숨기기)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 

   [!UICONTROL 그룹 기준]: `Independent`

* [!UICONTROL Formula]: 초기 반복 순서 확률
* 
   [!UICONTROL 공식]: `(C-A)/(C+D-A-B)`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* Show top.bottom: 카테고리 이름별로 정렬된 상위 24개 카테고리

* 

   [!UICONTROL Chart type]: `Line`

초기 반복 주문 확률 보고서는 총 반복 주문 / 총 주문 수를 나타냅니다. 모든 주문은 반복 주문을 할 수 있는 기회입니다. 반복 주문 수는 실제로 실행되는 주문의 하위 집합입니다.

사용하는 공식은 (X개월 후에 발생한 총 반복 주문)/(최소 X개월 전의 총 주문)을 간소화합니다. 이는 주문 후 X개월이 지난 시점에서 사용자가 다른 주문을 할 가능성이 Y%라는 것을 보여 줍니다.

대시보드를 작성한 후 묻는 가장 일반적인 질문은 다음과 같습니다. 이탈 임계값을 결정하는 데 이 대시보드를 어떻게 사용합니까?

**이에 대한 &quot;하나의 정답&quot;은 없습니다.** 그러나 Adobe은 초기 반복 확률률의 절반인 값과 선이 교차하는 지점을 찾는 것을 추천한다. 이 점은 &quot;사용자가 반복 주문을 하려고 하면 지금쯤 완료했을 것&quot;이라고 말할 수 있는 지점입니다. 궁극적으로 목표는 &quot;유지&quot;에서 &quot;재활성화&quot; 노력으로 전환하는 것이 적절할 임계값을 선택하는 것입니다.

모든 보고서를 컴파일한 후 원하는 대로 대시보드에서 구성할 수 있습니다. 결과는 페이지 상단에 있는 이미지와 비슷할 수 있습니다

이 분석을 작성하는 동안 질문이 발생하거나 Professional Services 팀의 도움을 얻고자 하는 경우 [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
