---
title: 예상 라이프타임 값(LTV) 분석(기본)
description: 분석을 생성하여 현재 고객의 라이프타임 값을 이해하고 더 많은 주문에 따라 라이프타임 값이 어떻게 증가하는지 예측하는 방법을 알아봅니다.
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# 예상 라이프타임 값 분석

더 많은 주문을 할수록 고객의 생애 가치를 예측하는 것은 모든 규모의 비즈니스에서 가장 중요한 측면 중 하나입니다.

다음은 현재 고객의 라이프타임 값을 파악하고 더 많은 주문에 따라 라이프타임 값이 어떻게 증가하는지 예측하기 위한 분석을 만드는 단계입니다.

![예상 라이프타임 값](../../assets/expected_ltv_720.png)

## 지표 작성

첫 번째 단계는 다음 단계로 새 지표를 구성하는 것입니다.
* 다음으로 이동 **[!UICONTROL Manage Data > Metrics]**
   * 기존 항목 보기 **[!UICONTROL Avg lifetime revenue]**.

   >[!NOTE]
   >
   >이 지표가 구성되는 테이블 (아마도 `customer_entity` 또는 `sales_order` 게스트 체크아웃을 수락하는 스토어의 기능에 따라 다릅니다.)

   * 클릭 **[!UICONTROL Create New Metric]** 위에서 표를 선택합니다.
   * 이 지표는 다음을 수행합니다. **중간값** 다음에 있음 `Customer's lifetime revenue` 열, 정렬 기준 `created_at`.
      * [!UICONTROL Filters]:
         * 추가 `Customers we count (Saved Filter Set)` (또는 `Registered accounts we count`)
   * 지표에 다음과 같은 이름을 지정합니다. `Median lifetime revenue`.



## 대시보드 만들기

지표가 만들어지면 다음 작업을 수행할 수 있습니다. **대시보드 만들기** 다음을 수행합니다.
* 다음으로 이동 **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* 대시보드에 다음과 같은 이름을 지정합니다. `Expected LTV`.

* 여기서 모든 보고서를 만들고 추가할 수 있습니다.

## 보고서 작성 중

>[!NOTE]
>
>날짜 **[!UICONTROL Time Period:]**, 각 보고서의 기간은 다음과 같이 나열됩니다. `All-time`. 분석 요구 사항에 맞게 자유롭게 변경하십시오. Adobe은 이 대시보드에 있는 모든 보고서가 동일한 기간을 다루는 것을 권장합니다. 예: `All time`, `Year-to-date`, 또는 `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 추가 [!UICONTROL filters]:
         * [`A`] `Customer's group code` **다음과 같지 않음** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **보다 큼**`0`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`


* **[!UICONTROL Average and Median LTV]**
   * 지표 `1`: `Avg lifetime revenue`
   * 지표 `2`: `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
      [!UICONTROL 차트 유형]: `Line`
   * 선택 취소 `Multiple Y-Axes`

* **라이프타임 주문 수별 LTV**
   * 지표 `1`: `Avg lifetime revenue`
   * 지표 `2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 간격]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 

      [!UICONTROL 차트 유형]: `Line`
   >[!NOTE]
   >
   >에 대한 모든 값을 추가하지 않음 `Customer's lifetime number of orders`. 대신 신규 고객 수가 적은 수에 도달하는 시점을 보고 각 고객의 라이프타임 주문 수 값을 해당 시점에 수동으로 추가합니다. 예를 들어, 한 주문에 200명의 고객이 있고, 두 주문에 75명, 세 주문에 15명, 네 주문에 3명이 있다면, 를 추가합니다 *1, 2 및 3*.

* 기존 항목 추가 [!UICONTROL Avg customer lifetime revenue by cohort] 보고서.

보고서를 작성한 후 대시보드에서 보고서를 구성하는 방법에 대한 자세한 내용은 이 항목 맨 위에 있는 이미지를 참조하십시오.
