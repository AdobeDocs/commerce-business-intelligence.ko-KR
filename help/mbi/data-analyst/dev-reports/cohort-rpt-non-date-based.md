---
title: 비날짜 기반 집단에 대한 집단 Report Builder
description: 유사한 활동이나 속성으로 사용자를 그룹화하는 방법에 대해 알아봅니다.
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# [!DNL Cohort Report Builder] 비 날짜 기반 집단의 경우

다음 [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) 는 상인이 사용자의 다양한 하위 집합이 시간에 따라 어떻게 행동하는지 학습할 수 있도록 돕습니다. 과거에는 `Cohort Report Builder` 은(는) 일반별로 사용자를 그룹화하도록 최적화되었습니다. `cohort date` (예: 주어진 달에 첫 번째 구매한 모든 고객 세트). 다음 `Non-Date Based Cohort` 이제 기능을 사용하여 유사한 활동이나 속성으로 사용자를 그룹화할 수 있습니다. 이 기능에 대한 몇 가지 사용 사례를 살펴보십시오.

## 사용 사례

이것은 포괄적인 목록이 아니지만, 다음은 이 기능으로 수행할 수 있는 몇 가지 잠재적인 분석입니다.

* 에서 획득한 고객의 수익 검토 [!DNL Google] 및 [!DNL Facebook]
* 미국과 캐나다에서 첫 구매가 이루어진 고객 분석
* 다양한 광고 캠페인에서 획득한 고객의 행동을 살펴봅니다

## 분석을 만드는 방법

1. 클릭 **[!UICONTROL Report Builder]** 왼쪽 탭에서 또는 **[!UICONTROL Add Report** > **Create Report]** 모든 대시보드에서

1. 다음에서 `Report Builder Selection` 화면, 클릭 **[!UICONTROL Create Report]** 다음 옆에 `Visual Report Builder` 옵션을 선택합니다.

### 지표 추가

이제 을(를) 방문했습니다. `Report Builder`분석을 수행할 지표를 추가합니다(예: `Revenue` 또는 `Orders`).

>[!NOTE]
>
>기본 [!DNL Google Analytics] 지표가 과 호환되지 않음 `Cohort Report Builder`. 이 예제의 목표는 다른 을 통해 인수한 첫 번째 주문 고객의 시간 경과에 따른 매출을 확인하는 것입니다 [!DNL Google Analytics] 소스.

### 전환 `Metric View` 끝 `Cohort`

![1-집단 지표 보기 전환](../../assets/1-toggle-metric-view-to-cohort.png)

그러면 집단 보고서의 세부 사항을 구성할 수 있는 새 창이 열립니다.

집단 보고서를 작성하려면 다음 5가지 사양이 필요합니다.

1. 집단을 그룹화하는 방법
1. 집단 선택
1. 작업 타임스탬프
1. 집단 첫 번째 작업 시간 범위
1. 집단 발생 이후의 시간 범위

![집단](../../assets/2-cohort-groups.png)<!--{: width="200" height="224"}-->

!![cohort-first-action-time-range]<!--(../../assets/3-cohort-first-action-time-range.png){: width="400" height="554"}-->

#### 1. 그룹화 `cohorts`

`Cohorts` 다음 예에서는 동작 특성별로 그룹화됩니다 `Customer's first order GA source`. 여기에서 사용할 수 있는 옵션은 이미 로 지정된 열입니다. `groupable` 지표에 사용됩니다.

#### 2. 집단 선택

해당 특성에 대한 모든 결과를 표시할 수 있습니다. 이로 인해 많은 문제가 발생할 수 있습니다. `cohorts`, 특정 `cohorts` (다음에 사용 가능한 다양한 값에 해당) `Customer's first order GA source`)을 참조하십시오.

![집단](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. `Action timestamp`

지표를 만든 열이 아닌 날짜 기반 열을 선택할 수 있습니다. 아래에서는 지정된 시간에 적용되는 시간 범위를 선택합니다 `action timestamp`.

#### 4. `Cohort first action time range`

여기에서 다음을 포함하는 날짜 범위를 선택합니다. `cohorts action timestamp` (따라서 2017년 11월부터 2018년 10월까지 첫 번째 주문을 한 고객). 이동 날짜 범위 또는 고정 날짜 범위일 수 있습니다.

#### 5. `Time range after cohort occurrence`

다음 항목을 보시겠습니까? `cohorts` 월별, 주별 또는 연별로 시간이 지남에 따라 어떤 작업을 수행합니까? 여기에서 이러한 항목을 선택할 수 있습니다. 해당 섹션 아래에서 `time range` 다음 이후 `cohort action timestamp` 발생했습니다. 예를 들어 작업 시간 범위 동안 첫 번째 주문을 한 고객에 대한 12개월의 데이터를 보여줍니다.

![cohort-first-action-time range](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

>[!NOTE]
>
>[!UICONTROL Filters] 다음 간을 전환할 때 지표에 적용된 상태는 그대로 유지됩니다. `Standard` 및 `Cohort` 보기.

### 관련 항목

다음을 참조하십시오 [`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md).
