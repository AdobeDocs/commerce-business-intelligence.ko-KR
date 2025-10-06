---
title: Visual Report Builder에서 시간 옵션 사용
description: 특정 기간 동안 보고서의 데이터를 분석하는 방법에 대해 알아봅니다.
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 0%

---

# [!DNL Time]에서 [!DNL Visual Report Builder] 옵션 사용

[!DNL Visual Report Builder]의 기능 중 하나는 전역 `Time Range` 및 `Interval` 설정입니다. 이러한 설정을 사용하여 특정 기간 동안 보고서의 데이터를 분석할 수 있습니다.

그러나 일부 분석의 경우 동일한 보고서에서 서로 다른 시간 범위 또는 시간 간격을 고려해야 할 수 있습니다. 여기에서 `Time` 옵션이 제공됩니다. 보고서에서 `Time` 옵션을 사용하는 방법에 대한 더 나은 아이디어를 제공하기 위해 이 자습서에서는 다음 사용 사례를 다룹니다.

* [타임스탬프가 없는 지표 분석](#notimestamp)
* [한 지표에 독립적인 시간 간격 제공](#independenttimeinterval)
* [서로 다른 시간 범위에서 동일한 지표 비교](#difftimerange)

이 항목에서 설명한 몇 가지 샘플 보고서와 함께 사용하려면 계속하기 전에 [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md)을(를) 여십시오.

## 타임스탬프가 없는 지표 분석 {#notimestamp}

데이터가 관련 타임스탬프와 함께 수집되거나 저장되지 않아 일부 지표는 시간에 따른 트렌드를 단순히 파악할 수 없습니다. 예를 들어 인벤토리 테이블에는 각 SKU에 대해 하나의 행만 포함된 경우가 있습니다. 이 경우 타임스탬프를 지정하지 않고 [지표를 만듭니다](../data-user/reports/ess-manage-data-metrics.md).

보고서에서 이러한 지표를 사용할 때 이 지표를 보고서에 추가하면 독립적인 `Time Interval`(`None`)과 `Time Range`(`Global`)이(가) 자동으로 설정됩니다.

![시간 간격이 없음으로 설정되고 시간 범위가 전역으로 설정된 지표를 표시하는 보고서](../assets/Metrics_without_timestamps.gif)

## 한 지표에 독립적인 시간 간격 제공 {#independenttimeinterval}

`Time` 옵션을 사용하면 시간 기반 100% 차트를 만들어 특정 시간 범위 동안 가장 많은 가치를 제공한 일, 주, 월 또는 연도를 식별할 수 있습니다. 이 섹션에서는 한 해의 각 달에서 생성된 수입의 백분율을 보여 주는 차트를 만듭니다.

이 유형의 보고서는 연도별로 생성된 매출을 비교하려는 경우 유용할 수 있습니다. 예를 들어, 2015년 차트는 1월이 해당 연도 매출의 18%를 기여했다고 밝혔고 2016년 차트는 8%만을 보여주었다. 무슨 일이 일어났을지 조사를 시작할 수 있을 거야

1. 보고서에 `Revenue` 지표를 추가합니다.
1. 지표의 복사본을 만들려면 **[!UICONTROL Duplicate]**&#x200B;을(를) 클릭하십시오.
1. 전역 **[!UICONTROL Time Range]** 옵션을 클릭한 다음 **[!UICONTROL Moving Time Range]**&#x200B;을(를) 클릭합니다. `Last Year`(으)로 설정합니다.
1. 전역 **[!UICONTROL Time Interval]** 옵션을 클릭하고 `Monthly`(으)로 설정합니다.
1. Report Builder은 두 번째 지표에 대해 두 번째 Y축을 자동으로 추가합니다. `Multiple Y-Axes` 상자를 선택 취소합니다.
1. 그런 다음 첫 번째 지표에 독립 `Time Interval`을(를) 적용합니다. **[!UICONTROL Time Options]** 오른쪽에 있는 `first Revenue metric`(시계 아이콘)을 클릭합니다.
1. 보고서 위에 표시되는 확장된 창에서 **[!UICONTROL Time Options]**&#x200B;을(를) 클릭합니다.
1. 드롭다운에서 다음을 설정합니다.

   * `Time Interval`: `None`(으)로 설정합니다.

   * `Time Range`: 먼저 `Last Year`을(를) 클릭한 다음 **[!UICONTROL Custom]**&#x200B;을(를) 클릭하고 마지막으로 **[!UICONTROL Moving Range]** 옵션을 선택하여 `Last Year`(으)로 설정합니다.

   * **[!UICONTROL Apply]**&#x200B;을(를) 클릭하여 간격 및 범위 설정을 저장합니다. 이렇게 하면 이전 연도의 총 매출을 계산하는 지표가 만들어집니다. 그런 다음 이 지표를 수식에서 분모로 사용합니다.

   * 월별 매출의 백분율을 보려면 보고서에 공식을 추가해야 합니다. **[!UICONTROL Add Formula]**&#x200B;을(를) 클릭합니다.

   * 수식 필드에 `B/A`을(를) 입력하고 텍스트 필드 옆에 있는 드롭다운에서 `% Percent`을(를) 선택합니다. 이 공식은 작년 특정 월의 수익 금액을 지난해 총 수익 금액으로 나눕니다.

   * **[!UICONTROL Apply Changes]**&#x200B;을(를) 클릭합니다.

   * 두 입력 지표를 모두 숨기고 공식 이름을 변경합니다.

이제 각 달이 작년에 얼마나 영향을 미쳤는지 알 수 있습니다.

![이전 연도의 월별 매출액 비율을 보여 주는 차트](../assets/Independent_Time_Int.png)

## 서로 다른 시간 범위에서 동일한 지표 비교 {#difftimerange}

이 예제에서는 사용자 지정 차원 `Day number of the month`을(를) 사용합니다. 이 보고서를 만들려고 하는데 Data Warehouse에 이 차원이 없는 경우 [지원팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)하여 도움을 받으십시오.

이 범주에서 가장 일반적인 두 가지 예는 (1) 성장 지표 (전년 대비 또는 전월 대비 매출)를 비교하는 것과 (2) 최근 재고 또는 품목 판매 트렌드를 더 잘 이해하는 것입니다.

이 사용 사례를 보여주기 위해 전월 일일 매출액을 전년도의 같은 달과 비교하여 살펴보십시오. 2016년 1월 각 날의 매출을 확인하고 이를 2015년 1월, 2014년 1월 등과 비교한다고 가정해 보겠습니다. - 이 보고서에 이러한 결과가 표시됩니다.

1. 보고서에 `Revenue` 지표를 추가합니다.
1. 지표의 복사본을 만들려면 **[!UICONTROL Duplicate]**&#x200B;을(를) 클릭하십시오.
1. 첫 번째 지표의 이름을 `Items sold last 7 days`(으)로 바꾸고 두 번째 지표의 이름을 `Items sold last 28 days`(으)로 바꿉니다.
1. **[!UICONTROL Time Range]**&#x200B;을(를) 클릭한 다음 **[!UICONTROL Moving Time Range]**&#x200B;을(를) 클릭합니다. `Last Month`(으)로 설정합니다.
1. **[!UICONTROL Time Interval]**&#x200B;을(를) 클릭하고 `None`(으)로 설정합니다.
1. 두 번째 **[!UICONTROL Time Options]** 지표 옆에 있는 `Revenue`(시계 아이콘)을 클릭합니다.
1. 보고서 위에 표시되는 확장된 창에서 **[!UICONTROL Time Options]**&#x200B;을(를) 클릭합니다.
1. 드롭다운에서 다음을 설정합니다.

   * `Time Interval`: `None`(으)로 설정합니다.

   * `Time Range`: 먼저 `From 14 Months Ago To 13 Months Ago`을(를) 클릭한 후 **[!UICONTROL Custom]**&#x200B;을(를) 클릭하여 **[!UICONTROL Moving Range]**(으)로 설정합니다. 메뉴 상단에 있는 필드와 드롭다운을 사용하여 범위를 설정합니다. 이 설정을 사용하면 이전 달과 이전 연도의 매출을 볼 수 있습니다.

   지표가 보고서에서 사라지더라도 걱정하지 마십시오. 독립적인 시간 옵션을 설정하면 보고서에서 지표를 자동으로 숨깁니다. 다시 표시하려면 지표 옆에 있는 **[!UICONTROL Show]**&#x200B;을(를) 클릭합니다.

   ![보고서에서 지표에 대해 다른 시간 범위를 설정하는 데모](../assets/Different_Time_Ranges.gif)

   * **[!UICONTROL Apply]**&#x200B;을(를) 클릭하여 간격 및 범위 설정을 저장합니다.

   * 그런 다음 `Day number of the month`을(를) 클릭하고 차원을 선택하여 사용자 지정 **[!UICONTROL Group By]** 차원을 추가합니다. 이 경우 주문의 월 일 번호가 반환됩니다. 예를 들어 3월 2일에 수행한 주문은 `2`을(를) 반환합니다.

   * `Group By` 드롭다운에서 `Show All`을(를) 선택하고 **[!UICONTROL Apply]**&#x200B;을(를) 클릭합니다. 이렇게 하면 보고서에 대한 X축 값이 만들어집니다.

   ![일별로 그룹화된 매출액 비교를 보여 주는 보고서](../assets/TO4.png)

   * 지표 이름을 변경합니다. 이 예제에서 첫 번째 지표는 `Revenue - 2015`이고 두 번째 지표는 `Revenue - 2014`입니다.

사용자 지정 `Time Options`의 또 다른 일반적인 용도는 공급 주를 확인하는 것입니다. 특히 휴가철이나 특별 프로모션 기간에는 마지막 주, 월, 이전 프로모션 기간 동안 판매된 품목을 고려하여 정보에 입각한 구매 결정을 내릴 수 있습니다.

이 보고서를 직접 작성할 때 필요한 시간으로 시간 범위를 설정하는 것을 잊지 마십시오.

1. 보고서에 `Items Sold` 지표를 추가합니다.
1. 지표의 복사본을 만들려면 **[!UICONTROL Duplicate]**&#x200B;을(를) 클릭하십시오.
1. 지표 이름을 변경합니다. 동일한 이름을 사용하거나 다음과 유사한 이름을 사용할 수 있습니다.
   1. 첫 번째 지표의 이름을 `Items sold last 7 days`(으)로 바꿉니다.
   1. 두 번째 지표의 이름을 `Items sold last 28 days`(으)로 바꿉니다.
1. `Items sold last 7 days` 지표에서 전역 **[!UICONTROL Time Range]** 옵션을 클릭한 다음 **[!UICONTROL Moving Time Range]**&#x200B;을(를) 클릭합니다. 이 예제에서는 `Last 7 Days`(으)로 설정합니다.
1. **[!UICONTROL Time Interval]**&#x200B;을(를) 클릭하고 `None`(으)로 설정합니다.
1. 그런 다음 `Time Options` 지표에 대해 `Items sold last 28 days`을(를) 정의합니다. **[!UICONTROL Time Options]** 지표의 오른쪽에 있는 `second Items sold`(시계 아이콘)을 클릭합니다.
1. 보고서 위에 표시되는 확장된 창에서 **[!UICONTROL Time Options]**&#x200B;을(를) 클릭합니다.
1. 드롭다운에서 다음을 설정합니다.

   * `Time Interval`: `None`(으)로 설정합니다.
   * `Time Range`: 먼저 `From 29 days to 1 day ago`을(를) 클릭한 다음 **[!UICONTROL Custom]**&#x200B;을(를) 클릭하여 **[!UICONTROL Moving Range]**(으)로 설정합니다. 메뉴 상단에 있는 필드와 드롭다운을 사용하여 범위를 설정합니다.
   * **[!UICONTROL Apply]**&#x200B;을(를) 클릭하여 간격 및 범위 설정을 저장합니다.
   * `Items sold last 28 days` 지표를 복제하고 새 지표의 `Time Options`을(를) 엽니다. 옵션을 다음과 같이 설정합니다.

      * `Time Interval`: `None`(으)로 둡니다.
      * `Time Range`: **[!UICONTROL Specific Date Range]**&#x200B;을(를) 클릭한 다음 적절한 날짜를 입력하여 원하는 프로모션에 맞는 날짜 범위로 변경하십시오.
      * `Items sold during last promotion` 지표의 이름을 바꾸거나 비슷한 이름으로 바꾸십시오.
      * `Units on hand` 지표를 추가합니다.
      * 그런 다음 보고서에 포함하는 기간(`last 7 days`, `last 28 days` 및 `last promo`)에 대해 판매 추세를 고려하여 현재고 주를 보여 주는 계산을 추가해야 합니다. 각 기간에 대해 이 작업을 한 번 수행해야 합니다.

수식을 만들려면 **[!UICONTROL Add Formula]**&#x200B;을(를) 클릭합니다. 아래 공식을 입력하고 완료되면 **[!UICONTROL Apply Changes]**&#x200B;을(를) 클릭합니다. 다음 세 가지 기간에 대해 각각 이 작업을 반복합니다.

* `last 7 days time period`에 대해 `D / A` 필드에 `Formula`을(를) 입력하십시오.
* `last 28 days time period`에 대해 `D / (B/4)` 필드에 `Formula`을(를) 입력하십시오.

  >[!NOTE]
  >
  >여기에서 선택한 시간 범위를 정규화하는 것이 중요합니다. 이 예에서는 28일을 4주로 나눕니다. 수식에 다른 논리를 적용해야 할 수도 있습니다.

* `last promo period`에 대해 `D / C` 필드에 `Formula`을(를) 입력하십시오.

  ![서로 다른 기간에 대한 주별 공급 계산을 보여 주는 보고서](../assets/Different_Time_Ranges_2.png)

* 마지막으로 지표를 숨기고 `SKU` 또는 유사한 차원을 보고서에 `Group By`(으)로 추가하여 보고서를 사용자 지정합니다.

이 예는 현재 재고 수준이 제품 전체의 14일 판매에 적합하다는 것을 보여줍니다. 그러나 비교 가능한 판촉 기간을 추가하면 회사가 재고를 더 많이 주문하고 재고가 충분한 품목만 판촉하여 일부 변경을 할 필요가 있음을 시사합니다.

고객이 시간에 따라 다르게 동작하기 때문에 분석을 수행할 때 데이터에서 차이가 발생할 것으로 예상할 수 있습니다. 사용자 지정 시간 옵션을 설정하면 복잡한 분석을 신속하게 만들 수 있으므로 기록 추세를 결정하는 데이터 기반 결정을 가능하게 합니다.

