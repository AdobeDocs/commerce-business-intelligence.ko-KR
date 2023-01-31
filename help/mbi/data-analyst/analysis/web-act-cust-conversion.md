---
title: 웹 사이트 활동 및 고객 전환율 분석
description: 페이지 보기 수, 세션 및 사용자를 포함하여 웹 사이트 활동을 추적할 대시보드와 시간 경과에 따른 고객 전환율을 추적하는 대시보드를 설정하는 방법을 알아봅니다.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# 웹 사이트 활동 분석

[!DNL MBI] 를 사용하면 광고 비용 데이터를 나머지 데이터와 쉽게 통합할 수 있습니다. 이를 통해 웹 사이트 활동을 이해할 수 있을 뿐만 아니라 등록된 사용자가 되거나 구매를 수행하는 웹 사이트의 방문자 비율을 도출할 수 있습니다.

이 문서에서는 페이지 보기 수, 세션 및 사용자를 비롯하여 시간에 따른 고객 전환율과 같은 웹 사이트 활동을 추적하는 대시보드를 설정하는 방법을 보여줍니다.

## 전제 조건

**광고 비용 데이터 가져오기** - 연결 [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) to [!DNL MBI] - 자동으로 동기화됩니다. [!DNL AdWords] BI에 쓰세요.

**사용자 획득 채널 데이터 추적** - [!DNL Google AdWords] 데이터베이스의 특정 주문에 데이터를 할당하려면 [사용자 획득 추적](../analysis/google-track-user-acq.md) via [!DNL Google Analytics E-commerce]각 주문을 utm 소스 및 미디어와 연결할 수 있습니다.

## 사용자 획득 캠페인

이 보고서 컬렉션은 다음을 사용하여 작성됩니다.

* 연결할 때 자동으로 생성되는 지표 [!DNL Google AdWords] 데이터
* 과 같이 계정에 이미 사용할 수 있어야 하는 기본 지표 `Number of orders` 및 `New users`
* 가입할 때 생성된 Dimension [!DNL Google Analytics Ecommerce] 주문의 utm 소스 및 주문 utm 미디어와 같이 데이터베이스에 데이터를 추가할 수 있습니다. 현재 해당 필드를 계정에서 사용할 수 없는 경우 지원 팀에 문의하십시오

## 보고서 작성

**먼저 시간에 따른 페이지 보기, 세션 및 사용자 수를 표시하는 보고서를 만듭니다.**

1. 새 보고서를 만듭니다.
1. 클릭 **[!UICONTROL Add Metric]**&#x200B;를 마우스로 가리킨 다음 [!DNL Google Analytics] 드롭다운 하단의 섹션에서 을(를) 선택하고 을(를) 선택합니다 `Page Views`.
1. 다른 지표를 추가하고 다시 마우스로 [!DNL Google Analytics] 섹션, 이번에는 선택 `Sessions`.
1. 세 번째 지표를 추가하고 다시 마우스로 [!DNL Google Analytics] 섹션, 이번에는 선택 `Users`.
1. 이제 기간을 31일 전에서 1일 전까지로 변경하고 시간 간격을 로 조정합니다 `by day`.
1. 보고서에 이름을 지정합니다(예: `Page views, sessions and users by day`). **[!UICONTROL Save]**.

**두 번째 보고서는 지난 한 해 동안의 페이지 보기 수를 확인할 것입니다.**

1. 새 보고서를 만듭니다.
1. 클릭 **[!UICONTROL Add Metric]**, 마우스 위로 [!DNL Google Analytics] 드롭다운 하단의 섹션에서 을(를) 선택하고 을(를) 선택합니다 _페이지 보기 수_.
1. 기간을 13개월 전에서 1개월 전까지의 이동 범위로 변경하고 시간 간격을 로 조정합니다 `by month`.
1. 보고서에 다음과 같은 이름을 지정합니다. `Page views by month,` 을 클릭하고 **[!UICONTROL Save]**.

**세 번째 차트는 지난 해에 대한 바운스 비율을 볼 것입니다.**

1. 새 보고서를 만듭니다.
1. 클릭 **[!UICONTROL Add Metric]**, 마우스 위로 [!DNL Google Analytics] 드롭다운 하단의 섹션에서 을(를) 선택하고 을(를) 선택합니다 _바운스 비율_.
1. 기간을 13개월 전에서 1개월 전까지의 이동 범위로 변경하고 시간 간격을 로 조정합니다 `by month`.
1. 보고서에 다음과 같은 이름을 지정합니다. `Bounce rate by month`, 을 클릭한 다음 **[!UICONTROL Save]**.

**이제 재방문자와 비교하여 새 방문자의 평균 세션 길이를 확인합니다.**

1. 새 보고서를 만듭니다.
1. 클릭 **UICONTROL 지표 추가**, 마우스 위로 [!DNL Google Analytics] 드롭다운 하단의 섹션에서 을(를) 선택하고 을(를) 선택합니다 `Average Session Length`.
1. 기간을 13개월 전에서 1개월 전까지의 이동 범위로 변경하고 시간 간격을 로 조정합니다 `by month`?
1. 추가 `Group by` 을(를) 선택합니다. `New or returning visitor`.  을(를) 확인합니다. `Show All` box; 을 클릭한 다음 **[!UICONTROL Apply]**.
1. 보고서에 다음과 같은 이름을 지정합니다. `Average session length`, 을 클릭한 다음 **[!UICONTROL Save]**.

**그런 다음 지난 30일 동안 주요 참조 도메인을 살펴보십시오.**

1. 새 보고서를 만듭니다.
1. 클릭 **[!UICONTROL Add Metric]**, 마우스 위로 [!DNL Google Analytics] 드롭다운 하단의 섹션에서 을(를) 선택하고 을(를) 선택합니다 `Sessions`.
1. 기간을 31일 전에서 1일 전까지로 변경하고 시간 간격을 로 조정합니다 `none`.
1. 추가 `Group by` 을(를) 선택합니다. `ga:source`.  을(를) 확인합니다. _모두 표시_ box; 을 클릭한 다음 **[!UICONTROL Apply]**.
1. 다른 추가 `group by` 을(를) 선택합니다. `ga:medium`. 다시 한 번, `Show All` box; 을 클릭한 다음 **[!UICONTROL Apply]**.
1. 보고서에 다음과 같은 이름을 지정합니다. `Top 20 Referring Domains, 30 Days`를 클릭하고 **[!UICONTROL Save]**.

**마지막으로 전환을 확인합니다.**

1. 새 보고서를 만듭니다.
1. 다음 지표를 추가합니다.

* `New users`
   * 클릭 **[!UICONTROL Hide]** 지표 이름 아래

* `Number of orders`
   * 다음에 대한 필터 추가 `Customer's order number` = 1 및 클릭 **[!UICONTROL Apply]**
   * 지표 이름을 클릭하고 이를 호출하여 지표 이름을 변경합니다 `Number of first orders`을 클릭한 다음 **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** 지표

* `Users`
   * **[!UICONTROL Hide]** 지표
   * 기간을 로 변경합니다. `24 months ago to now`, 및 시간 간격을 `by month`.
   * 다음 공식을 눌러 추가합니다 **[!UICONTROL Formula]**.
   * A/D 를 클릭한 다음 **[!UICONTROL Apply]**
   * 수식 이름 바꾸기 `Registration conversion`
   * B/D 를 클릭한 다음 **[!UICONTROL Apply]**
   * 수식 이름 바꾸기 `First order conversion`
   * C/D 를 클릭한 다음 **[!UICONTROL Apply]**
   * 수식 이름 바꾸기 `Any order conversion`

* 이제 보고서 이름을 다음과 같이 지정합니다. `Conversion by month`를 클릭한 다음 **[!UICONTROL Save]**.

## 다음 단계

이제 웹 트래픽 및 전환율에 대한 데이터에 액세스할 수 있으므로 비즈니스 의사 결정을 내리기 위해 이 정보를 파악할 수 있습니다. 사이트로 트래픽을 유도하는 데 가장 좋은 사이트는 무엇입니까?  높은 라이프타임 값으로 고객을 확보하는 데 가장 효과적인 캠페인이 무엇입니까?

광고 지출 및 마케팅 전략을 조정하면서 결과를 계속 추적할 수 있습니다. [!DNL MBI], 회사의 진화하는 우선순위를 충족하기 위해 이 대시보드를 반복합니다.
