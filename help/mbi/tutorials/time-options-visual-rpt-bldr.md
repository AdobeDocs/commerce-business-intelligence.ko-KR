---
title: 시각적 Report Builder에서 시간 옵션 사용
description: 특정 기간 동안 보고서의 데이터를 분석하는 방법을 알아봅니다.
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 0%

---

# 사용 `Time` 옵션 `Visual Report Builder`

의 기능 중 하나 `Visual Report Builder` 은 글로벌 `Time Range` 및 `Interval` 설정. 이러한 설정을 사용하면 특정 기간 동안 보고서의 데이터를 분석할 수 있습니다.

그러나 일부 분석의 경우 동일한 보고서에서 다른 시간 범위 또는 시간 간격을 고려해야 할 수 있습니다. 여기에서 `Time` 옵션이 제공됩니다. 사용하는 방법에 대해 더 잘 알고 있습니다 `Time` 보고서의 옵션, 이 자습서에서는 다음 사용 사례를 다룹니다.

* [타임스탬프가 없는 지표 분석](#notimestamp)
* [한 지표에 독립 시간 간격 지정](#independenttimeinterval)
* [다른 시간 범위에서 동일한 지표 비교](#difftimerange)

이 항목에서 설명한 샘플 보고서 중 일부를 함께 따르려면 [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) 계속하기 전에

## 타임스탬프가 없는 지표 분석 {#notimestamp}

일부 지표는 데이터가 관련 타임스탬프와 함께 수집되거나 저장되지 않으므로 시간에 따른 트렌드를 표시할 수 없습니다. 예를 들어, 재고 테이블에는 각 SKU에 대해 하나의 행만 포함될 수 있습니다. 이 경우 다음을 수행해야 합니다 [지표 만들기](../data-user/reports/ess-manage-data-metrics.md) 타임스탬프를 지정하지 않고

보고서에서 이러한 지표를 사용할 때 보고서에 이 지표를 추가하면 자동으로 독립적 설정이 설정됩니다 `Time Interval` 의 `None` 및 `Time Range` 의 `Global`:

![](../assets/Metrics_without_timestamps.gif)

## 한 지표에 독립 시간 간격 지정 {#independenttimeinterval}

`Time` 선택 사항을 사용하면 특정 시간 범위 동안 가장 많은 가치를 기여한 일, 주, 월 또는 년을 식별하는 시간 기반 100% 차트를 만들 수 있습니다. 이 섹션에서는 1년의 각 달력에서 발생한 매출액의 비율을 보여주는 차트를 만듭니다.

이 유형의 보고서는 전년 대비 생성된 매출을 비교하려는 경우 유용합니다. 예를 들어, 2015년 한 차트에서 1월이 그 해의 수입의 18퍼센트를 기부했고 2016년에 한 명이 단지 8퍼센트만을 보여주었다고 밝혀진다면, 당신은 무엇이 일어났었을지 조사를 시작할 수 있습니다.

1. 추가 `Revenue` 지표를 생성합니다.
1. 클릭 **[!UICONTROL Duplicate]** 지표의 사본을 만듭니다.
1. 글로벌 클릭 **[!UICONTROL Time Range]** 옵션, **[!UICONTROL Moving Time Range]**. 을(를) (으)로 설정합니다. `Last Year`.
1. 글로벌 클릭 **[!UICONTROL Time Interval]** 옵션을 설정하고 `Monthly`.
1. Report Builder은 두 번째 지표에 대해 두 번째 Y축을 자동으로 추가합니다. 선택 취소 `Multiple Y-Axes` 상자.
1. 다음으로, 우리는 독립적인 `Time Interval` 첫 번째 지표에 대해 자세히 알아보십시오. 클릭 **[!UICONTROL Time Options]** (시계 아이콘) `first Revenue metric`.
1. 클릭 **[!UICONTROL Time Options]** 보고서 위에 표시되는 확장 창에서 클릭합니다.
1. 드롭다운에서 다음을 설정합니다.

   * `Time Interval`: 다음 설정 `None`.

   * `Time Range`: 다음 설정 `Last Year` 처음 클릭하기 **[!UICONTROL Custom]**, 그런 다음 **[!UICONTROL Moving Range]**, 마지막으로 선택 `Last Year` 선택 사항입니다.

   * 클릭 **[!UICONTROL Apply]** 간격 및 범위 설정을 저장하려면 을 클릭합니다. 이 경우 이전 연도의 총 매출액을 계산하는 지표를 만듭니다. 다음으로, 이 지표를 수식에서 분모로 사용합니다.

   * 매월 수입 비율을 보려면 보고서에 수식을 추가해야 합니다. 클릭 **[!UICONTROL Add Formula]**.

   * Enter 키 `B/A` 공식 필드에서 을(를) 선택하고 을(를) 선택합니다. `% Percent` 텍스트 필드 옆에 있는 드롭다운에서 을 클릭합니다. 이 공식은 작년 특정 월의 수입 금액을 작년 총 수입 금액으로 나눈 것입니다.

   * 클릭 **[!UICONTROL Apply Changes]**.

   * 입력 지표를 모두 숨기고 공식 이름을 변경합니다.

이제 우리는 매 달이 작년에 얼마나 중요했는지 알 수 있습니다.

![](../assets/Independent_Time_Int.png)

## 다른 시간 범위에서 동일한 지표 비교 {#difftimerange}

이 예제에서는 `Day number of the month`. 이 보고서를 만들고 Data Warehouse에 이 차원이 없는 경우, [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 지원 요청.

이 카테고리에서 가장 일반적인 두 가지 예는 (1) 성장 지표(전년 또는 월 대비)와 (2) 최근 재고 또는 품목 판매 트렌드를 더 잘 이해하는 것입니다.

이 사용 사례를 보여주기 위해 이전 달과 비교한 이전 달의 일별 매출액을 살펴보겠습니다. 2016년 1월 각 날의 매출을 확인한 다음 2015년 1월, 2014년 1월 등과 비교하려고 하며 이 보고서에는 해당 내용이 표시됩니다.

1. 추가 `Revenue` 지표를 생성합니다.
1. 클릭 **[!UICONTROL Duplicate]** 지표의 사본을 만듭니다.
1. 첫 번째 지표 이름을 다음으로 변경합니다. `Items sold last 7 days` 및에 두 번째 지표 `Items sold last 28 days`.
1. 클릭 **[!UICONTROL Time Range]**, 그런 다음 **[!UICONTROL Moving Time Range]**. 을(를) (으)로 설정합니다. `Last Month`.
1. 클릭 **[!UICONTROL Time Interval]** 다음으로 설정 `None`.
1. 클릭 **[!UICONTROL Time Options]** (시계 아이콘) 옆에 있는 두 번째 `Revenue` 지표.
1. 클릭 **[!UICONTROL Time Options]** 보고서 위에 표시되는 확장 창에서 클릭합니다.
1. 드롭다운에서 다음을 설정합니다.

   * `Time Interval`: 다음 설정 `None`.

   * `Time Range`: 다음 설정 `From 14 Months Ago To 13 Months Ago` 처음 클릭하기 **[!UICONTROL Custom]** 그런 다음 **[!UICONTROL Moving Range]**. 메뉴 상단의 필드 및 드롭다운을 사용하여 범위를 설정합니다. 이 설정을 사용하면 이전 월이나 이전 연도의 매출을 볼 수 있습니다.
   보고서에서 지표가 사라져도 걱정하지 마십시오. 독립 시간 옵션을 설정하면 보고서에서 지표가 자동으로 표시되지 않습니다. 다시 표시하려면 **[!UICONTROL Show]** 지표 옆에 표시됩니다.

   ![](../assets/Different_Time_Ranges.gif)

   * 클릭 **[!UICONTROL Apply]** 간격 및 범위 설정을 저장하려면 을 클릭합니다.

   * 다음으로, 사용자 지정 항목을 추가합니다 `Day number of the month` 을 클릭하여 차원을 **[!UICONTROL Group By]** 차원을 선택합니다. 주문 월의 일자 번호를 반환합니다. 예를 들어 3월 2일에 수행한 주문은 반환됩니다 `2`.

   * 에서 `Group By` 드롭다운, 선택 `Show All` 을(를) 클릭합니다. **[!UICONTROL Apply]**. 이렇게 하면 보고서에 대한 X축 값이 효과적으로 생성됩니다.

   ![](../assets/TO4.png)

   * 지표 이름을 변경합니다. 이 예제에서 첫 번째 지표는 다음과 같습니다 `Revenue - 2015` 두 번째는 `Revenue - 2014`.



사용자 지정의 또 다른 일반적인 사용 `Time Options` 는 몇 주 간의 공급 기간을 결정하는 것입니다. 특히 휴가 시즌 또는 특별 판촉 기간 동안 최근 주, 월 및 이전 판촉 기간에 걸쳐 판매되는 품목을 고려하여 현명한 구매 결정을 내릴 수 있습니다.

이 보고서를 직접 작성할 때 필요한 시간 범위를 설정해야 합니다.

1. 추가 `Items Sold` 지표를 생성합니다.
1. 클릭 **[!UICONTROL Duplicate]** 지표의 사본을 만듭니다.
1. 지표 이름을 변경합니다. 같은 이름을 사용하거나 유사한 이름을 사용할 수 있습니다.
   1. 첫 번째 지표 이름을 다음으로 변경합니다. `Items sold last 7 days`.
   1. 두 번째 지표의 이름을 다음으로 변경합니다. `Items sold last 28 days`.
1. 설정 `Items sold last 7 days` 지표를 클릭하고 글로벌 **[!UICONTROL Time Range]** 옵션을 선택한 후 **[!UICONTROL Moving Time Range]**. 이 예제에서는 을(를) (으)로 설정합니다. `Last 7 Days`.
1. 클릭 **[!UICONTROL Time Interval]** 다음으로 설정 `None`.
1. 다음으로, `Time Options` 대상 `Items sold last 28 days` 지표. 클릭 **[!UICONTROL Time Options]** (시계 아이콘) `second Items sold` 지표.
1. 클릭 **[!UICONTROL Time Options]** 보고서 위에 표시되는 확장 창에서 클릭합니다.
1. 드롭다운에서 다음을 설정합니다.

   * `Time Interval`: 다음 설정 `None`.
   * `Time Range`: 다음 설정 `From 29 days to 1 day ago` 처음 클릭하기 **[!UICONTROL Custom]**, 그런 다음 **[!UICONTROL Moving Range]**. 메뉴 상단의 필드 및 드롭다운을 사용하여 범위를 설정합니다.
   * 클릭 **[!UICONTROL Apply]** 간격 및 범위 설정을 저장하려면 을 클릭합니다.
   * 을(를) 복제합니다 `Items sold last 28 days` 지표 및 새 지표의 열기 `Time Options`. 옵션을 다음과 같이 설정합니다.

      * `Time Interval`: 다음 방법으로 `None`.
      * `Time Range`: 을 클릭하여 판촉에 맞는 날짜 범위로 변경합니다. **[!UICONTROL Specific Date Range]** 그런 다음 적절한 날짜를 입력합니다.
      * 지표 이름 변경 `Items sold during last promotion` 또는 이와 유사한 것을 의미합니다.
      * 추가 `Units on hand` 지표.
      * 다음으로, 기간(`last 7 days`, `last 28 days`, 및 `last promo` 기간) 보고서에 포함하겠습니다. 각 기간에 대해 한 번씩 이 작업을 수행해야 합니다.

공식을 만들려면 **[!UICONTROL Add Formula]**. 아래 공식을 입력하고 을(를) 클릭합니다 **[!UICONTROL Apply Changes]** 완료됨. 세 개의 기간 각각에 대해 이 과정을 반복합니다.

* 대상 `last 7 days time period`, 입력 `D / A` 에서 `Formula` 필드.
* 대상 `last 28 days time period`, 입력 `D / (B/4)` 에서 `Formula` 필드.

   >[!NOTE]
   >
   >선택한 시간 범위를 여기서 정규화하는 것이 중요합니다. 이 예에서 28일은 4주로 나누어져야 합니다. 수식에 다른 논리를 적용해야 할 수 있습니다.

* 대상 `last promo period`, 입력 `D / C` 에서 `Formula` 필드.

   ![](../assets/Different_Time_Ranges_2.png)

* 마지막으로, 지표를 숨기고 보고서를 사용자 지정합니다. `SKU` 또는 다음과 유사한 차원으로서 보고서에 대한 `Group By`.

이 예에서는 현재 재고 수준이 제품 전체 14일 판매에 매우 적합했음을 보여줍니다. 그러나 비교 가능한 판촉 기간을 추가하는 것은 회사가 더 많은 재고를 주문하고 충분히 재고가 있는 품목만 홍보함으로써, 몇 가지 변경이 필요하다고 제안합니다.

고객이 시간이 지남에 따라 다르게 동작하므로 분석을 수행할 때 데이터에서 차이를 볼 수 있습니다. 사용자 지정 시간 옵션을 설정하면 복잡한 분석을 신속하게 생성할 수 있으므로 기록 추세를 결정하는 데이터 중심 결정을 수행할 수 있습니다.

