---
title: 예상 라이프타임 값(LTV) 분석(기본)
description: 현재 고객의 라이프타임 값을 파악하고 더 많은 주문으로 라이프타임 값이 어떻게 증가할 것인지 예측하는 분석을 만드는 방법을 알아봅니다.
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# 예상 라이프타임 값 분석

고객이 주문을 더 많이 할수록 고객의 라이프타임 가치를 예측하는 것은 모든 규모의 비즈니스에서 가장 중요한 측면 중 하나입니다.

다음은 현재 고객의 라이프타임 값을 파악하고 더 많은 주문으로 라이프타임 값이 어떻게 증가할 것인지 예측하는 분석을 만드는 단계입니다.

![예상 라이프타임 값](../../assets/expected_ltv_720.png)

## 지표 작성

첫 번째 단계는 다음 단계로 새 지표를 구성하는 것입니다.
* 다음으로 이동 **[!UICONTROL Manage Data > Metrics]**
   * 기존 보기 **[!UICONTROL Avg lifetime revenue]**.

   >[!NOTE]
   >
   >이 지표가 구성되는 테이블(아마도 `customer_entity` 또는 `sales_order` 게스트 체크아웃을 수락하는 사용자의 스토어 기능에 따라 다릅니다.

   * 클릭 **[!UICONTROL Create New Metric]** 그리고 위에서 표를 선택합니다.
   * 이 지표는 다음을 수행합니다 **중간값** on `Customer's lifetime revenue` 열, 정렬 기준 `created_at`.
      * [!UICONTROL Filters]:
         * 추가 `Customers we count (Saved Filter Set)` 또는 `Registered accounts we count`)
   * 지표에 다음과 같은 이름을 지정합니다. `Median lifetime revenue`.



## 대시보드 만들기

지표를 만들면 다음을 수행할 수 있습니다 **대시보드 만들기** 다음을 수행합니다.
* 다음으로 이동 **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* 대시보드에 다음과 같은 이름을 지정합니다. `Expected LTV`.

* 이 단계에서 모든 보고서를 만들고 추가합니다.

## 보고서 작성

* 아직 예약하지 않았다면 체크 아웃하십시오 [이 비디오](https://fast.wistia.net/embed/iframe/24zz7wmjrt) **[!UICONTROL Visual Report Builder] 차트, 테이블 및 스칼라 값을 만들려면

>[!NOTE]
>
>설정 **[!UICONTROL Time Period:]**, 각 보고서의 기간은 다음과 같이 나열됩니다 `All-time`. 분석 요구 사항에 맞게 자유롭게 변경할 수 있습니다. 이 대시보드의 모든 보고서는 다음과 같은 동일한 기간을 포함하는 것이 좋습니다 `All time`, `Year-to-date`, 또는 `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 추가 [!UICONTROL filters]:
         * [`A`] `Customer's group code` **같지 않음** `Not Logged In`
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
   * 선택을 취소합니다 `Multiple Y-Axes`

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
   >다음에 대한 값을 모두 추가하지 마십시오 `Customer's lifetime number of orders`대신 신규 고객 수가 적은 수에 도달하는 지점을 살펴보고 해당 지점에 각 고객의 라이프타임 주문 값을 수동으로 추가합니다. 예를 들어 한 번에 200명, 두 번에 75명, 세 시에 15명, 네 시에 3명이 있는 경우 *1, 2 및 3*.

* 기존 [!UICONTROL Avg customer lifetime revenue by cohort] 보고서 세트에 대해 설명합니다.

보고서를 작성한 후 대시보드에서 보고서를 구성하는 방법에 대해서는 이 항목 상단의 이미지를 참조하십시오.
