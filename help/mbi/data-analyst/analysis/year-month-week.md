---
title: 연간, 월별 및 주별 보고서
description: 시간 경과에 따른 트렌드를 쉽게 보고 비교할 수 있는 기간의 시점을 변경하는 방법을 알아봅니다.
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# 기간 보고

>[!NOTE]
>
>이 문서에는 원래 아키텍처와 새 아키텍처를 사용하는 클라이언트를 위한 지침이 포함되어 있습니다. 다음 단계에 있습니다. [새로운 아키텍처](../../administrator/account-management/new-architecture.md) 만약 _Data Warehouse 보기_ 선택 후 사용 가능한 섹션 `Manage Data` 기본 도구 모음에서 를 클릭합니다.

Report Builder를 사용하면 시간 경과에 따른 트렌드를 쉽게 보고 비교할 수 있는 기간에 대한 원근 변경을 수행할 수 있습니다. 이 문서에서, Adobe에서는 연도별 분석을 위해 주, 월, 매월 및 연도별 보고서를 만들 수 있도록 더 깊이 있게 대시보드를 설정하는 방법을 보여줍니다.

![](../../assets/Wow__mom__yoy.png)

시작하기 전에 보다 자세한 탐색 관점에 대해 숙지하고 싶을 수 있습니다 [여기](../../tutorials/using-visual-report-builder.md) 독립 시간 옵션 및 [여기](../../tutorials/time-options-visual-rpt-bldr.md).

이 분석에는 다음이 포함됩니다 [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md).

## 계산된 열

* **`Sales_flat_order`** 표
* **원래 아키텍처:** 아래 열은 분석가가 의 일부로 만듭니다. `[YoY WoW MoM ANALYSIS]` 티켓
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **새로운 아키텍처:** 이 계산을 만드는 방법에 대한 예제 사진과 함께 아래에 나열된 SQL입니다
   * `created_at (month-day)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-dd&#39;)**
   * `created_at (month)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-month&#39;)**
   * `created_at (day of the month)`&lt; [!UICONTROL Calculation]: **to_char(A, &#39;dd&#39;)**
   * `created_at (day of the week)` [!UICONTROL Calculation]: **to_char(A, &#39;d-Day&#39;)**
   * **`created_at (hour of the day)` [!UICONTROL Calculation]: **to_char(A, &#39;hh24&#39;)**

      ![](../../assets/new-arch-create-calc.png)

## 지표

없음.

>[!NOTE]
>
>다음을 확인하십시오 [새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에

## 보고서

* **YoY 차트**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 years ago to 1 year ago`

   * [!UICONTROL Show top/bottom]: 상위 100% 정렬 기준 **`created_at (month-day)`***

* 지표 `A`: `This year`
* 지표 `B`: `Last year`
* [!UICONTROL Time period]: `1 year ago to 0 years ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (month-day)`
* 
   [!UICONTROL Chart Type]: `Line`

* **MoM 차트**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 시간 옵션: `Time range (Custom)`: `2 months ago to 1 month ago`

   * 위쪽/아래쪽 표시: 상위 100% 정렬 기준 **`created_at (day of month)`***

* 지표 `A`: 이번 달*
* 지표 `B`: 지난 달*
* [!UICONTROL Time period]: 1개월 전 - 0개월 전
* 
   [!UICONTROL Interval]: None
* [!UICONTROL Group by]: `created_at (day of month)`
* 
   [!UICONTROL Chart Type]: Line

* **WoW 차트**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 weeks ago to 1 week ago`

   * [!UICONTROL Show top/bottom]: 상위 100% 정렬 기준 `created_at (day of week)`

* 지표 `A`: `This week`
* 지표 `B`: `Last week`
* [!UICONTROL Time period]: `1 week ago to 0 weeks ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (day of week)`
* 
   [!UICONTROL Chart Type]: `Line`

* **DoD 차트**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 days ago to 1 day ago`

   * [!UICONTROL Show top/bottom]: 상위 100% 정렬 기준 `created_at (hour of day)`

* 지표 `A`: `Today`
* 지표 B: `Yesterday`
* [!UICONTROL Time period]: `1 day ago to 0 days ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (hour of day)`
* 
   [!UICONTROL Chart Type]: `Line`

모든 보고서를 컴파일한 후 대시보드에서 원하는 대로 구성할 수 있습니다. 최종 결과는 이 페이지의 맨 위에 있는 이미지와 같을 수 있습니다.
