---
title: 비날짜 기반 집단에 대한 집단 Report Builder
description: 유사한 활동 또는 속성별로 사용자를 그룹화하는 방법을 알아봅니다.
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# `Cohort Report Builder for Non-Date-Based Cohorts`

Adobe [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) 는 상인들이 시간이 지남에 따라 다양한 사용자 하위 세트가 어떻게 행동하는지 연구하는 데 큰 도움이 되었습니다. 과거에 `Cohort Report Builder` 는 주로 공통으로 사용자를 그룹화하는 데 최적화되었습니다 `cohort date` (예: 지정된 월에 첫 번째 구매를 한 모든 고객 세트). 다음 `Non-Date Based Cohort` 이제 이 기능을 통해 유사한 활동이나 속성으로 사용자를 그룹화할 수 있습니다. 이 기능에 대한 몇 가지 사용 사례를 살펴보십시오.

## 사용 사례

다음은 이 기능을 사용하여 수행할 수 있는 몇 가지 잠재적인 분석입니다.

* Analytics Standard에서 획득한 고객 [!DNL Google] 비교 [!DNL Facebook]
* 미국 및 캐나다에서 첫 구매를 한 고객 분석
* 다양한 광고 캠페인에서 획득한 고객의 행동을 살펴봅니다

## 분석을 만드는 방법

1. 클릭 **[!UICONTROL Report Builder]** 왼쪽 탭에서 또는 **[!UICONTROL Add Report** > **Create Report]** 아무 대시보드에서나 볼 수 있습니다.

1. 에서 `Report Builder Selection` 을 클릭하고 **[!UICONTROL Create Report]** 다음 `Visual Report Builder` 선택 사항입니다.

### 지표 추가

이제 우리가 `Report Builder`를 채울 지표를 추가합니다(예: `Revenue` 또는 `Orders`).

>[!NOTE]
>
>기본 [!DNL Google Analytics] 지표는 와 호환되지 않습니다 `Cohort Report Builder`. 이 예제의 목표는 서로 다른 GA 소스를 통해 취득한 최초 주문 고객에 대해 시간 경과에 따른 수익을 확인하는 것입니다.

### 전환 `Metric View` to `Cohort`

![지표 보기를 집단에 전환](../../assets/1-toggle-metric-view-to-cohort.png)

그러면 집단 보고서의 세부 사항을 구성할 수 있는 새 창이 열립니다.

집단 보고서를 만들려면 다음 5가지 사양이 필요합니다.

1. 집단을 그룹화하는 방법
1. 집단 선택
1. 작업 타임스탬프
1. 첫 번째 작업 시간 범위 집단
1. 집단 발생 후 시간 범위

![집단 그룹](../../assets/2-cohort-groups.png){: width=&quot;200&quot; height=&quot;224&quot;}

![coort-first-action-time-range](../../assets/3-cohort-first-action-time-range.png){: width=&quot;400&quot; height=&quot;554&quot;}

#### 1. 그룹화 `cohorts`

`Cohorts` 이 예제에서는 동작 특성별로 그룹화됩니다 `Customer's first order GA source`. 여기에서 사용할 수 있는 옵션은 이미 로 지정된 열입니다 `groupable` 참조하십시오.

#### 2. 집단 선택

지정된 특성에 대한 모든 결과를 표시하는 옵션이 있습니다. 이는 많은 수의 결과를 초래할 수 있으므로 `cohorts`특정 `cohorts` (이 값은 `Customer's first order GA source`)에 사용할 수 있습니다.

![집단 그룹](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. `Action timestamp`

이렇게 하면 지표를 만들 열 이외의 날짜 기반 열을 선택할 수 있습니다. 아래에서는 제공된 항목에 적용되는 시간 범위를 선택하는 것을 봅니다 `action timestamp`.

#### 4. `Cohort first action time range`

여기에서 을 포함하는 날짜 범위를 선택합니다 `cohorts action timestamp` (따라서 2017년 11월부터 2018년 10월까지 첫 번째 주문을 받은 고객) 이동 날짜 범위 또는 고정 날짜 범위일 수 있습니다.

#### 5. `Time range after cohort occurrence`

을(를) 보시겠습니까? `cohorts` 한 달, 주, 년 단위로 요? 여기서 이러한 선택 사항을 수행합니다. 해당 섹션 아래에서 `time range` 후 `cohort action timestamp` 이(가) 발생했습니다. 예를 들어, 작업 시간 범위 동안 첫 번째 주문을 수행한 고객에 대한 12개월 데이터를 보여줍니다.

![coort-first-action-time-range](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

### 기타 참고 사항

* [!UICONTROL Filters]: 지표에 적용된 내용은 `Standard` 및 `Cohort` 보기
* 자세한 내용은 [`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md).
