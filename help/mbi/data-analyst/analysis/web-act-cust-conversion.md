---
title: 웹 사이트 활동 및 고객 전환율 분석
description: 페이지 보기 수, 세션 및 사용자를 포함하여 웹 사이트 활동 및 시간에 따른 고객 전환율을 추적하는 대시보드를 설정하는 방법에 대해 알아봅니다.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# 웹 사이트 활동 분석

[!DNL Adobe Commerce Intelligence]을(를) 사용하면 광고 비용 데이터를 나머지 데이터와 쉽게 통합할 수 있습니다. 이를 통해 웹 사이트 활동을 이해할 수 있을 뿐만 아니라, 등록된 사용자가 되거나 구매하는 웹 사이트 방문자의 비율을 도출할 수 있습니다.

이 항목에서는 페이지 보기 수, 세션 및 사용자를 포함하여 웹 사이트 활동 및 시간에 따른 고객 전환율을 추적하는 대시보드를 설정하는 방법을 보여 줍니다.

## 사전 요구 사항

**광고 비용 데이터를 가져옵니다** - [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md)을(를) [!DNL Adobe Commerce Intelligence]에 연결합니다. 이렇게 하면 [!DNL AdWords] 지출이 Commerce Intelligence에서 자동으로 동기화됩니다.

**사용자 확보 채널 데이터 추적** - [!DNL Google AdWords] 데이터를 데이터베이스의 특정 주문에 연결하려면 [을(를) 통해 ](../analysis/google-track-user-acq.md)사용자 확보 추적[!DNL Google Analytics E-commerce]해야 합니다. 이렇게 하면 각 주문을 utm 소스 및 미디어와 연결할 수 있습니다.

## 사용자 확보 캠페인

이 보고서 컬렉션은 다음을 사용하여 작성됩니다.

* [!DNL Google AdWords] 데이터를 연결할 때 자동으로 생성되는 지표
* `Number of orders` 및 `New users`과(와) 같이 계정에서 이미 사용할 수 있는 기본 지표
* [!DNL Google Analytics Ecommerce] 데이터를 데이터베이스에 연결할 때 만들어지는 차원입니다(예: 주문의 utm 소스 및 주문의 utm 미디어). 현재 계정에서 이러한 필드를 사용할 수 없는 경우 지원 팀에 문의하십시오

## 보고서 작성

**시간 경과에 따른 페이지 보기, 세션 및 사용자 수를 표시하는 보고서를 만들어 시작합니다.**

1. 보고서를 만듭니다.
1. **[!UICONTROL Add Metric]**&#x200B;을(를) 클릭한 다음 드롭다운 아래의 [!DNL Google Analytics] 섹션 위로 마우스를 가져간 후 `Page Views`을(를) 선택합니다.
1. 다른 지표를 추가하고 다시 [!DNL Google Analytics] 섹션 위로 마우스를 가져간 후 이번에는 `Sessions`을(를) 선택합니다.
1. 세 번째 지표를 추가하고 다시 [!DNL Google Analytics] 섹션 위로 마우스를 가져갑니다. 이번에는 `Users`을(를) 선택합니다.
1. 이제 31일 전부터 1일 전까지의 이동 범위로 기간을 변경하고 시간 간격을 `by day`(으)로 조정하십시오.
1. 보고서에 이름을 지정하고(예: `Page views, sessions and users by day`) **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

**두 번째 보고서는 지난 1년 동안의 페이지 보기 횟수를 살펴봅니다.**

1. 보고서를 만듭니다.
1. **[!UICONTROL Add Metric]**&#x200B;을(를) 클릭하고 드롭다운 아래의 [!DNL Google Analytics] 섹션 위로 마우스를 가져간 후 _페이지 보기_&#x200B;를 선택합니다.
1. 13개월 전부터 1개월 전까지 기간을 이동 범위로 변경하고 시간 간격을 `by month`(으)로 조정합니다.
1. 보고서에 이름을 지정하십시오(예: `Page views by month,`). **[!UICONTROL Save]**&#x200B;을(를) 클릭하십시오.

**세 번째 차트는 지난 1년 동안의 바운스 비율을 보여 줍니다.**

1. 보고서를 만듭니다.
1. **[!UICONTROL Add Metric]**&#x200B;을(를) 클릭하고 드롭다운 아래의 [!DNL Google Analytics] 섹션 위로 마우스를 가져간 후 _바운스 비율_&#x200B;을 선택합니다.
1. 13개월 전부터 1개월 전까지 기간을 이동 범위로 변경하고 시간 간격을 `by month`(으)로 조정합니다.
1. 보고서에 `Bounce rate by month`과(와) 같은 이름을 지정하고 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

**이제 재방문자와 비교하여 새 방문자의 평균 세션 길이를 살펴봅니다.**

1. 보고서를 만듭니다.
1. 드롭다운 아래의 **섹션 위로 마우스를 가져간 후** UICONTROL 지표 추가[!DNL Google Analytics]를 클릭하고 `Average Session Length`을(를) 선택합니다.
1. 13개월 전부터 1개월 전까지 기간을 이동 범위로 변경하고 시간 간격을 `by month`(으)로 조정하시겠습니까?
1. `Group by`을(를) 추가하고 `New or returning visitor`을(를) 선택합니다.  `Show All` 상자를 선택한 다음 **[!UICONTROL Apply]**&#x200B;을(를) 클릭합니다.
1. 보고서에 `Average session length`과(와) 같은 이름을 지정하고 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

**다음 최근 30일 동안 추천 도메인을 살펴봅니다.**

1. 보고서를 만듭니다.
1. **[!UICONTROL Add Metric]**&#x200B;을(를) 클릭하고 드롭다운 아래의 [!DNL Google Analytics] 섹션 위로 마우스를 가져간 후 `Sessions`을(를) 선택합니다.
1. 31일 전부터 1일 전까지 이동 범위로 기간을 변경하고 시간 간격을 `none`(으)로 조정합니다.
1. `Group by`을(를) 추가하고 `ga:source`을(를) 선택합니다.  _모두 표시_ 상자를 선택한 다음 **[!UICONTROL Apply]**&#x200B;을(를) 클릭합니다.
1. 다른 `group by`을(를) 추가하고 `ga:medium`을(를) 선택합니다. 다시 `Show All` 상자를 선택한 다음 **[!UICONTROL Apply]**&#x200B;을(를) 클릭합니다.
1. 보고서에 `Top 20 Referring Domains, 30 Days`과(와) 같은 이름을 지정하고 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

**마지막으로 전환 확인:**

1. 보고서를 만듭니다.
1. 다음 지표를 추가합니다.

* `New users`
   * 지표 이름 아래의 **[!UICONTROL Hide]** 클릭

* `Number of orders`
   * `Customer's order number` = 1에 대한 필터를 추가하고 **[!UICONTROL Apply]** 클릭
   * 지표 이름을 클릭하고 `Number of first orders`을(를) 호출한 다음 **[!UICONTROL Hide]**&#x200B;을(를) 클릭하여 지표의 이름을 변경합니다.

* `Number of orders`
   * **[!UICONTROL Hide]** 지표

* `Users`
   * **[!UICONTROL Hide]** 지표
   * 기간을 `24 months ago to now`(으)로 변경하고 시간 간격을 `by month`(으)로 조정합니다.
   * **[!UICONTROL Formula]**&#x200B;을(를) 클릭하여 다음 수식을 추가하십시오.
   * A/D를 클릭한 다음 **[!UICONTROL Apply]** 클릭
   * 수식 이름 바꾸기 `Registration conversion`
   * B/D를 클릭한 다음 **[!UICONTROL Apply]** 클릭
   * 수식 이름 바꾸기 `First order conversion`
   * C/D를 클릭한 다음 **[!UICONTROL Apply]**&#x200B;을(를) 클릭합니다.
   * 수식 이름 바꾸기 `Any order conversion`

* 이제 보고서에 `Conversion by month`과(와) 같은 이름을 지정한 다음 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

## 다음 단계

이제 웹 트래픽 및 전환율의 데이터에 액세스할 수 있으므로 이를 활용하여 사이트로 트래픽을 유도하는 데 가장 적합한 사이트를 선정할 수 있습니다. 또는 라이프타임 값이 높은 고객을 확보하는 데 가장 효과적인 캠페인은 무엇입니까?

광고 지출과 마케팅 전략을 조정할 때 [!DNL Commerce Intelligence]에서 결과를 계속 추적할 수 있으며, 이 대시보드를 반복하여 회사의 진화하는 우선 순위를 충족할 수 있습니다.
