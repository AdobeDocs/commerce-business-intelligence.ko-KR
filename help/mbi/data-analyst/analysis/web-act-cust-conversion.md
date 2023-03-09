---
title: 웹 사이트 활동 및 고객 전환율 분석
description: 페이지 보기 수, 세션 및 사용자를 포함하여 웹 사이트 활동 및 시간에 따른 고객 전환율을 추적하는 대시보드를 설정하는 방법에 대해 알아봅니다.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# 웹 사이트 활동 분석

[!DNL MBI] 를 사용하면 광고 비용 데이터를 나머지 데이터와 쉽게 통합할 수 있습니다. 이를 통해 웹 사이트 활동을 이해할 수 있을 뿐만 아니라, 등록된 사용자가 되거나 구매하는 웹 사이트 방문자의 비율을 도출할 수 있습니다.

이 문서에서는 페이지 보기 수, 세션 및 사용자를 포함하여 웹 사이트 활동 및 시간에 따른 고객 전환율을 추적하는 대시보드를 설정하는 방법을 보여 줍니다.

## 전제 조건

**광고 비용 데이터 가져오기** - 연결 [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) 끝 [!DNL MBI] - 이렇게 하면 [!DNL AdWords] MBI에서 시간을 보내십시오.

**사용자 획득 채널 데이터 추적** - 을 묶습니다. [!DNL Google AdWords] 데이터베이스의 특정 주문에 대한 데이터입니다. [사용자 획득 추적](../analysis/google-track-user-acq.md) 경유 [!DNL Google Analytics E-commerce]. 이렇게 하면 각 주문을 utm 소스 및 미디어와 연결할 수 있습니다.

## 사용자 확보 캠페인

이 보고서 컬렉션은 다음을 사용하여 작성됩니다.

* 에 연결할 때 자동으로 생성되는 지표 [!DNL Google AdWords] 데이터
* 다음과 같이 계정에서 이미 사용할 수 있는 기본 지표 `Number of orders` 및 `New users`
* 가입 시 생성된 Dimension [!DNL Google Analytics Ecommerce] 주문의 utm 소스 및 주문의 utm 미디어와 같은 데이터베이스에 대한 데이터입니다. 현재 계정에서 이러한 필드를 사용할 수 없는 경우 지원 팀에 문의하십시오

## 보고서 작성

**먼저 시간 경과에 따른 페이지 보기, 세션 및 사용자 수를 표시하는 보고서를 만듭니다.**

1. 보고서를 만듭니다.
1. 클릭 **[!UICONTROL Add Metric]**, 마우스를 위에 놓기 [!DNL Google Analytics] 드롭다운 하단에 있는 섹션에서 을(를) 선택합니다. `Page Views`.
1. 다른 지표를 추가하고 다시 마우스를 위에 놓기 [!DNL Google Analytics] 섹션, 이번에 선택 `Sessions`.
1. 세 번째 지표를 추가하고 다시 마우스를 위에 놓습니다. [!DNL Google Analytics] 섹션, 이번에 선택 `Users`.
1. 이제 기간을 31일 전에서 1일 전으로 이동 범위로 변경하고 시간 간격을 로 조정합니다. `by day`.
1. 보고서에 이름을 지정하십시오(예: `Page views, sessions and users by day`), 클릭 **[!UICONTROL Save]**.

**두 번째 보고서는 지난 해 동안의 페이지 보기 수를 살펴봅니다.**

1. 보고서를 만듭니다.
1. 클릭 **[!UICONTROL Add Metric]**, 마우스를 위에 놓기 [!DNL Google Analytics] 드롭다운 하단에 있는 섹션에서 을(를) 선택합니다. _페이지 보기 수_.
1. 13개월 전부터 1개월 전까지 기간을 이동 범위로 변경하고 시간 간격을 다음으로 조정 `by month`.
1. 보고서에 다음과 같은 이름을 지정합니다. `Page views by month,` 및 클릭 **[!UICONTROL Save]**.

**세 번째 차트는 지난 해 동안의 바운스 비율을 보여 줍니다.**

1. 보고서를 만듭니다.
1. 클릭 **[!UICONTROL Add Metric]**, 마우스를 위에 놓기 [!DNL Google Analytics] 드롭다운 하단에 있는 섹션에서 을(를) 선택합니다. _바운스 비율_.
1. 13개월 전부터 1개월 전까지 기간을 이동 범위로 변경하고 시간 간격을 다음으로 조정 `by month`.
1. 보고서에 다음과 같은 이름을 지정합니다. `Bounce rate by month`, 및 클릭 **[!UICONTROL Save]**.

**이제 재방문자와 비교하여 새 방문자의 평균 세션 길이를 살펴봅니다.**

1. 보고서를 만듭니다.
1. 클릭 **UICONTROL 지표 추가**, 마우스를 위에 놓기 [!DNL Google Analytics] 드롭다운 하단에 있는 섹션에서 을(를) 선택합니다. `Average Session Length`.
1. 13개월 전부터 1개월 전까지 기간을 이동 범위로 변경하고 시간 간격을 다음으로 조정 `by month`?
1. 추가 `Group by` 및 선택 `New or returning visitor`.  다음 확인: `Show All` 상자; 그런 다음 클릭 **[!UICONTROL Apply]**.
1. 보고서에 다음과 같은 이름을 지정합니다. `Average session length`, 및 클릭 **[!UICONTROL Save]**.

**그런 다음 지난 30일 동안의 상위 참조 도메인을 확인합니다.**

1. 보고서를 만듭니다.
1. 클릭 **[!UICONTROL Add Metric]**, 마우스를 위에 놓기 [!DNL Google Analytics] 드롭다운 하단에 있는 섹션에서 을(를) 선택합니다. `Sessions`.
1. 기간을 31일 전부터 1일 전까지 이동 범위로 변경하고 시간 간격을 다음으로 조정 `none`.
1. 추가 `Group by` 및 선택 `ga:source`.  다음 확인: _모두 표시_ 상자; 그런 다음 클릭 **[!UICONTROL Apply]**.
1. 다른 항목 추가 `group by` 및 선택 `ga:medium`. 다시 한 번 `Show All` 상자; 그런 다음 클릭 **[!UICONTROL Apply]**.
1. 보고서에 다음과 같은 이름을 지정합니다. `Top 20 Referring Domains, 30 Days`, 및 클릭 **[!UICONTROL Save]**.

**마지막으로 전환 을 살펴봅니다.**

1. 보고서를 만듭니다.
1. 다음 지표를 추가합니다.

* `New users`
   * 클릭 **[!UICONTROL Hide]** 지표 이름 아래에서

* `Number of orders`
   * 필터 추가 `Customer's order number` = 1 및 클릭 **[!UICONTROL Apply]**
   * 지표 이름을 클릭하고 호출하여 지표 이름을 변경합니다 `Number of first orders`을 클릭한 다음 을 클릭합니다 **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** 지표

* `Users`
   * **[!UICONTROL Hide]** 지표
   * 기간을 다음으로 변경 `24 months ago to now`, 및 시간 간격 조정 `by month`.
   * 을(를) 클릭하여 다음 공식을 추가합니다 **[!UICONTROL Formula]**.
   * A/D를 클릭한 다음 **[!UICONTROL Apply]**
   * 공식 이름 바꾸기 `Registration conversion`
   * B/D 를 클릭한 다음 **[!UICONTROL Apply]**
   * 공식 이름 바꾸기 `First order conversion`
   * C/D 를 클릭한 다음 **[!UICONTROL Apply]**
   * 공식 이름 바꾸기 `Any order conversion`

* 이제 보고서에 다음과 같은 이름을 지정합니다. `Conversion by month`을 클릭한 다음 을 클릭합니다 **[!UICONTROL Save]**.

## 다음 단계

이제 웹 트래픽 및 전환율의 데이터에 액세스할 수 있으므로 이를 활용하여 사이트로 트래픽을 유도하는 데 가장 적합한 사이트를 선정할 수 있습니다. 또는 라이프타임 값이 높은 고객을 확보하는 데 가장 효과적인 캠페인은 무엇입니까?

광고 지출과 마케팅 전략을 조정할 때 의 결과를 계속 추적할 수 있습니다. [!DNL MBI], 이 대시보드를 반복하여 회사의 변화하는 우선 순위를 충족합니다.
