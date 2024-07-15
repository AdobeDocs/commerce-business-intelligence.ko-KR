---
title: 비날짜 기반 집단에 대한 집단 Report Builder
description: 유사한 활동이나 속성으로 사용자를 그룹화하는 방법에 대해 알아봅니다.
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 76c5329c3f55570fa4e46601e902dc5a09e319e7
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# 비날짜 기반 집단의 [!DNL Cohort Report Builder]

[`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md)은(는) 상인이 시간의 흐름에 따라 다양한 사용자 하위 집합이 어떻게 동작하는지 학습하는 데 유용합니다. 이전에는 `Cohort Report Builder`이(가) 일반 `cohort date`(예: 주어진 달에 첫 번째 구매한 모든 고객 집합)별로 사용자를 그룹화하는 데 최적화되었습니다. 이제 `Non-Date Based Cohort` 기능을 사용하여 유사한 활동이나 특성으로 사용자를 그룹화할 수 있습니다. 이 기능에 대한 몇 가지 사용 사례를 살펴보십시오.

## 사용 사례

이것은 포괄적인 목록이 아니지만, 다음은 이 기능으로 수행할 수 있는 몇 가지 잠재적인 분석입니다.

* [!DNL Google]과(와) [!DNL Facebook]에서 얻은 고객의 수익을 검사하는 중
* 미국과 캐나다에서 첫 구매가 이루어진 고객 분석
* 다양한 광고 캠페인에서 획득한 고객의 행동을 살펴봅니다

## 분석을 만드는 방법

1. 왼쪽 탭에서 **[!UICONTROL Report Builder]**&#x200B;을(를) 클릭하거나 대시보드에서 **[!UICONTROL Add Report** > **Create Report]**&#x200B;을(를) 클릭합니다.

1. `Report Builder Selection` 화면에서 `Visual Report Builder` 옵션 옆의 **[!UICONTROL Create Report]**&#x200B;을(를) 클릭합니다.

### 지표 추가

`Report Builder`에 있으므로 분석을 수행할 지표를 추가합니다(예: `Revenue` 또는 `Orders`).

>[!NOTE]
>
>네이티브 [!DNL Google Analytics] 지표가 `Cohort Report Builder`과(와) 호환되지 않습니다. 이 예제의 목표는 서로 다른 [!DNL Google Analytics] 소스를 통해 획득한 첫 번째 주문 고객의 시간 경과에 따른 매출을 확인하는 것입니다.

### `Metric View`에서 `Cohort`(으)로 전환

![1개 지표 보기를 집단으로 전환](../../assets/1-toggle-metric-view-to-cohort.png)

그러면 집단 보고서의 세부 사항을 구성할 수 있는 새 창이 열립니다.

집단 보고서를 작성하려면 다음 5가지 사양이 필요합니다.

1. 집단을 그룹화하는 방법
1. 집단 선택
1. 작업 타임스탬프
1. 집단 첫 번째 작업 시간 범위
1. 집단 발생 이후의 시간 범위

![집단](../../assets/2-cohort-groups.png)<!--{: width="200" height="224"}-->



#### 1. `cohorts` 그룹화

`Cohorts`은(는) 동작 특성별로 그룹화됩니다(이 예제 `Customer's first order GA source`). 여기에서 사용할 수 있는 옵션은 지표에 대해 이미 `groupable`(으)로 지정된 열입니다.

#### 2. 집단 선택

해당 특성에 대한 모든 결과를 표시할 수 있습니다. 이로 인해 `cohorts`이(가) 많이 발생할 수 있으므로 필요한 특정 `cohorts`(`Customer's first order GA source`에 사용할 수 있는 다양한 값에 해당됨)을(를) 선택할 수 있습니다.

![집단](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. `Action timestamp`

지표를 만든 열이 아닌 날짜 기반 열을 선택할 수 있습니다. 아래에서는 지정된 `action timestamp`에 적용되는 시간 범위를 선택해 봅니다.

#### 4. `Cohort first action time range`

여기에서 `cohorts action timestamp`이(가) 포함된 날짜 범위를 선택합니다(따라서 2017년 11월부터 2018년 10월까지 첫 번째 주문을 한 고객). 이동 날짜 범위 또는 고정 날짜 범위일 수 있습니다.

#### 5. `Time range after cohort occurrence`

월별, 주별 또는 연도별로 시간 경과에 따라 `cohorts`을(를) 보시겠습니까? 여기에서 이러한 항목을 선택할 수 있습니다. 해당 섹션 아래에서 `cohort action timestamp`이(가) 발생한 후 `time range`을(를) 선택합니다. 예를 들어 작업 시간 범위 동안 첫 번째 주문을 한 고객에 대한 12개월의 데이터를 보여줍니다.

![집단 우선 작업 시간 범위](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

>[!NOTE]
>
>`Standard` 보기와 `Cohort` 보기 사이를 전환할 때 지표에 적용된 [!UICONTROL Filters]이(가) 그대로 유지됩니다.

### 관련 항목

[`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md)을(를) 참조하십시오.
