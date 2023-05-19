---
title: 집단 Report Builder
description: 라이프사이클 동안 유사한 특성을 공유하는 사용자 그룹의 분석에 대해 알아봅니다.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---

# 집단 Report Builder

사용자의 다양한 하위 집합이 시간에 따라 어떻게 행동하는지 연구하고 싶습니까? 예를 들어 프로모션 기간 동안 등록한 사용자가 등록하지 않은 사용자보다 평균 라이프타임 수익이 더 높은지 생각해 본 적이 있습니까? 답변이 다음과 같은 경우 `Yes`, 그런 다음 `Cohort Report Builder` 은(는) 완벽한 도구입니다. [!DNL Adobe Commerce Intelligence] 는 이 분석을 수행하고 귀하의 비즈니스와 관련이 있도록 최적화되었습니다.

## 집단 분석이란? {#what}

`Cohort` 분석은 생활 주기에 걸쳐 유사한 특성을 공유하는 사용자 집단의 분석으로 폭넓게 정의할 수 있다. 이를 통해 다양한 사용자 그룹 간 행동 트렌드를 식별할 수 있습니다.

다음에 대한 심층 입문서: `cohort` 분석, 검토 [이 페이지](https://www.cohortanalysis.com/).

내 [!DNL Commerce Intelligence] 대시보드를 사용하면 사용자를 쉽게 만들 수 있습니다. `cohorts` 를 기반으로 함 `cohort` 날짜 및 계정의 지표를 추적합니다.

## 그렇다면 코호트 분석이 중요한 이유는 무엇입니까? {#important}

위에서 언급했듯이, `cohort` 분석을 통해 다양한 사용자 그룹 간의 행동 트렌드를 식별할 수 있습니다. 특정 그룹의 행동을 확실히 이해하면 의사 결정과 지출을 조정하여 매출을 극대화할 수 있습니다. 예를 들어 라이프타임 수익을 가져오십시오 `cohort` 분석 - 이러한 종류의 분석은 여러 가지 이유로 유익하지만, 즉각적인 분석은 더 나은 고객 확보 결정입니다.

## 나만의 고유한 작성 방법 `cohort` 분석?

### 새로운 아키텍처

다음은 사용 지침입니다. `Cohort Report Builder` 다음에 있음 [새로운 아키텍처](../../administrator/account-management/new-architecture.md).

1. 클릭 **[!UICONTROL Report Builder]** 왼쪽 탭에서 또는 **[!UICONTROL Add Report** > **Create Report]** 모든 대시보드에서

1. 다음에서 `Report Builder` 선택 화면, 클릭 **[!UICONTROL Create Report]** 다음 옆에 `Visual Report Builder` 옵션을 선택합니다.

**지표 추가**

이제 을(를) 방문했습니다. `Report Builder`분석을 수행할 지표를 추가합니다(예: `Revenue` 또는 `Orders`).

>[!NOTE]
>
>기본 [!DNL Google Analytics] 지표가 과 호환되지 않음 `Cohort Report Builder`.

**지표 보기를 다음으로 전환`Cohort`**

![](../../assets/visual-report-builder-cohort-toggle.png)

이렇게 하면 의 세부 사항을 구성하는 새 창이 열립니다. `Cohort` 보고.

### 을(를) 빌드하려면 5개의 사양이 필요합니다. `Cohort` 보고서:

1. 을(를) 그룹화하는 방법 `cohorts`
1. 다음 `cohort` 기간
1. 의 수 `cohorts` 보기
1. 각각 최소 데이터 양 `cohort` 다음을 포함해야 함:
1. 다음 이후 시간 범위 `cohort` 발생 횟수

#### 1. 그룹화 `cohorts`

`Cohorts` 다음과 같이 타임스탬프로 그룹화됩니다. **등록 날짜** 또는 **첫 주문 일자**.

>[!NOTE]
>
>에 대해 지표가 빌드되는 것과 동일한 타임스탬프를 사용할 수 없습니다. `cohort` 날짜. 이를 필요로 하는 분석의 경우 `Standard report builder` 대신,

#### 2. `Cohort` 기간

그룹화할 기간 선택 `cohorts` 기준. 즉, 위에서 선택한 타임스탬프 중 가장 중요한 부분은 입니다. `week`, `month`, `quarter`, 또는 `year`? 보고서는 여기에서 선택한 간격으로 데이터를 표시합니다

#### 3. 및 4. 숫자 설정 `cohorts` 데이터 보기 및 데이터 양 `cohort` 다음을 포함해야 함

이러한 매개 변수는 `cohorts` 귀하가 관심을 갖는 것은 바로 귀하입니다 `Preview` 창 하단의 상자에는 보고서에 표시되는 집단이 정확하게 표시됩니다.

기본적으로 현재 `cohort` 각각에 필요한 최소 데이터 양을 변경하지 않는 한 이(가) 포함되지 않습니다 `cohort` 끝 `0`. 이 경우 `cohort` 현재 기간의 경우 부분 데이터만 포함됩니다.

#### 5. 다음 이후 시간 범위 `Cohort` 발생 횟수

이 기능을 사용하면 선택한 항목에 대해 보는 데이터의 시간 범위를 설정할 수 있습니다 `cohorts`. 예를 들어 24개월을 보려면 `cohorts` 기준 `customer's first order date`, 하지만 각 항목에 대한 처음 3개월의 데이터에만 관심이 있습니다 `cohort`를 설정하는 경우 `number of cohorts to view` 끝 `24` 및 `time range after cohort occurrence` 끝 `3`.

이 값의 간격은 에서 선택한 것에 따라 변경됩니다. `cohort time period` 및 값이 로 설정됩니다. `12` 기본적으로 값은 달력 아이콘을 클릭하여 편집하지 않는 한 변경되지 않습니다.

![](../../assets/cohort-time-range.png)

#### 기타 참고 사항

* [!UICONTROL Filters]: 다음 간을 전환할 때 지표에 적용되는 것이 그대로 유지됩니다. `Standard` 및 `Cohort` 보기.

* 다음을 참조하십시오 [`Perspectives`](#perspectives).

#### 예

다음은 이를 모두 통합하는 예제입니다. 이 예에서는 다음 시간 이후에 주문 동작을 체크 아웃하려고 합니다. `cohort`이 집단이 향후 6개월 이내에 반복 구매를 할 것인지 알아보는 첫 구매입니다.

![주문 집단](../../assets/crb_example.gif)

### 레거시 아키텍처

#### 레거시 아키텍처 {#personalinfo}

다음은 이전 버전의 `Cohort Report Builder`. 새 버전을 사용하려면 다음을 참조하십시오. [새로운 아키텍처](../../administrator/account-management/new-architecture.md) 로 마이그레이션에 대한 자세한 정보 [!DNL Commerce Intelligence] 새 아키텍처 계정.

#### 나만의 고유한 작성 방법 `cohort` 분석? {#create}

![](../../assets/create-cohort-analysis.png)

`Cohort` 분석 실행 중! 여기에서 누적 및 사용자별로 시간이 지남에 따라 증가하는 매출을 확인할 수 있습니다.

이 섹션에서는 나만의 콘텐츠를 만드는 과정을 안내합니다 `cohort` 분석. 예제(및 프로세스를 보여 주는 애니메이션 GIF)는 [예제 섹션](#examples) 이 항목의 을 참조하십시오.

1. 클릭 **[!UICONTROL Report Builder]** 왼쪽 탭에서 또는 **[!UICONTROL Add Report** > **Create Report]** 모든 대시보드에서

1. 다음에서 `Report Builder Selection` 화면, 클릭 **[!UICONTROL Create Report]** 다음 옆에 `Cohort Analysis` 옵션을 선택합니다.

#### 지표 추가

이제 을(를) 방문했습니다. `Cohort Report Builder`, 지표를 추가합니다(예: `Revenue` 또는 `Number of orders`)을 클릭하여 분석을 수행합니다.

>[!NOTE]
>
>기본 [!DNL Google Analytics] 지표가 과 호환되지 않음 `Cohort Report Builder`.

#### 집단 날짜 선택 {#date}

다음 단계는 를 지정하는 것입니다. `cohort date`. 사용자를 그룹화하는 날짜입니다. 예를 들어 다음과 같을 수 있습니다. `User's first order date` 또는 `User's registration date`.

>[!NOTE]
>
>지표가 빌드된 동일한 날짜를 사용할 수 없습니다(예: `created at`)을 로 사용하는 경우 `cohort date`.

#### 간격 및 기간 설정

다음으로, 다음을 설정합니다. `Interval` 및 `Time Period`.

`Interval`
다음 `Interval` 옵션을 사용하면 다음을 설정할 수 있습니다 `length` / `cohorts`. 예를 들어 이 가 로 설정된 경우 `Month`, 보고서는 월 단위로 측정됩니다.

다음을 사용하여 이러한 간격이 x축에 표시되는 방식을 변경할 수 있습니다. **기간** 메뉴 아래의 제품에서 사용할 수 있습니다.

`Time Period`
사용 `Time Period` 특정 사용자를 선택하는 메뉴 `cohorts` 분석. 다음을 모두 표시 `cohort`, 목록에서 선택하거나 시간 범위를 지정하거나 롤링 시간 범위를 정의합니다. `cohorts` 포함할 수 없습니다. 예를 들어 `Specific Cohorts` 옵션을 선택하면 분석에 포함할 특정 월을 선택할 수 있습니다.

![사용 `Time Period` 특정 항목 추가 메뉴 `Cohorts`](../../assets/Cohort_Time_Period.gif)

그룹화하는 경우 `cohorts` 등록 날짜별로 다음 목록에서 4월, 5월, 6월 선택 `Specific Cohorts` 에는 해당 월에 등록한 모든 사용자가 포함됩니다.

#### X축 정의

아래 `duration`, 차트의 X축 설정을 정의할 수 있습니다. 즉, 각 데이터 포인트가 나타내는 기간 수와 분석에 포함할 데이터 포인트 수가 표시됩니다.

#### 선택 `counting members` 표

다음을 기준으로 사용자를 그룹화하도록 선택한 경우: `cohort date` 다른 테이블에서 조인된 경우 `counting members in the … table` 옵션을 선택합니다.

![](../../assets/Cohort_Counting_Members_option.png)

이 설정을 이해하는 예를 참조하십시오. 다음을 그룹화하는 보고서를 작성했다고 가정해 봅시다. `Revenue` 지표 기준 `Customer's registration date`. 또한 이 원근법을 사용하려고 했습니다. `Average value per cohort member` 시간에 따른 구매자당 매출을 확인합니다. 구매자당 평균값을 찾으려면 나눌 구매자 수를 결정해야 합니다. 다음에 등록된 고객 수입니까 `customers` 테이블 또는 의 고유한 구매자 수입니다 `orders table` 같은 기간이요?

이 설정은 해당 질문에 대한 답을 제공합니다. 의 멤버 계산 `customers` 표에는 평균으로 모든 고객 (구매 여부에 상관없이)이 포함됩니다. 의 멤버 계산 `orders` 테이블에는 구매한 고객만 포함됩니다.

#### 원근 선택 {#perspective}

지표를 정의하고 지표를 분석하는 방법을 정의한 후 다음을 선택할 수 있습니다. `perspective` 을(를) 사용합니다.

보고서 시각화 바로 위에 의 드롭다운이 있습니다. `perspective` 설정.

다음을 참조하십시오 [관점](#perspectives).

![](../../assets/Cohort_Perspective_Menu.png)

## 집단 분석의 예 {#examples}

이제 다음을 만드는 방법을 살펴보았습니다. `cohort` 분석, 몇 가지 예를 참조하십시오.

### 내 사용자의 방법을 알고 싶습니다. `cohorts` 시간이 지남에 따라 성장하고 있습니다.

![사용자 `cohorts` 시간이 지남에 따라 성장](../../assets/cohort1.gif)

이 예에서는 `Revenue` 지표, 집단을 그룹별로 `customer's first order date`및 이(가) 가장 최근 8개를 선택함 `cohorts` (에 정의됨) `Time Period` 메뉴)를 사용하십시오. 시간이 지남에 따라 집단이 어떻게 성장했는지 보기 위해 `Cumulative Average Value per Cohort Member` `perspective`.

### 나는 평균적으로 사용자가 라이프타임 동안 다른 시점에서 얼마나 많은 주문을 하는지 알고 싶다.

!![Average number of orders users make at different points in their lifetimes](../../assets/cohort2.gif

이 예에서는 다음을 분석했습니다. `Number of orders` 지표, 집단을 그룹별로 `customer's first order date`, 및 (에 정의된) 가장 최근 8개 집단 포함 `Time Period` 메뉴)를 사용하십시오. 각 집단에 대한 평균 주문 수를 보려면 `perspective` 끝 `Average Value per Cohort Member`.

### 나는 사용자의 향후 구매 활동을 업무 첫 달의 활동과 어떻게 비교하는지 이해하고 싶다.

![사용자의 향후 구매 활동을 활동 첫 달과 비교](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
이는 라이프 사이클의 특정 시점에 특정 집단 그룹의 증분 기여를 보여줍니다. (예: &quot;6주&quot; 포인트에는 사용자가 6주에 만든 모든 데이터 포인트가 표시됩니다.)

`Average Value per Cohort Member`
이렇게 하면 가 나누어집니다. `Standard cohort` 의 (1)에서 각 의 사용자 수별로 분석 `cohort` 그룹입니다. 모든 코호트 그룹에 동일한 수의 사용자가 포함되지 않을 수 있으므로 이 기능은 코호트 성과를 사과 대 사과 기준으로 비교하는 데 유용할 수 있습니다. 예를 들어 특정 지역의 사용자당 평균 주 6 매출액 `cohort`.

`Cumulative`
이 `perspective` 기존 항목 표시 `cohort` 에 대한 분석 `cumulative` 기본. 즉, 라이프 사이클의 특정 시점에서 현재까지 주어진 코호트의 총 기여도를 보여줍니다. 예를 들어 특정 집단의 사용자 6주 후 누적 매출입니다.

`Cumulative Average Value per Cohort Member`
이렇게 하면 가 나누어집니다. `Cumulative` 의 (3)에서 각 의 사용자 수별로 분석 `cohort` 그룹입니다. 이 그래프는 평균 라이프타임 기여도(종종 평균 라이프타임 수익)를 `cohort` 의 각 기간에 있는 멤버 `cohort's` 삶. 예를 들어 6월에 가입한 6개월 이후의 평균 라이프타임 매출입니다.

`Percent of First Value (show first value)`
집계를 분석합니다. `cohort` 의 특정 시간에 대한 기여도 `cohort's` 라이프 사이클은 첫 번째 기간에 기여도를 백분율로 나타낸 것입니다. 예를 들어 6개월 수입은 6월에 가입한 사용자의 1개월 수입으로 나눈 것입니다.

`Percent of First Value (hide first value)`
이는 과(와) 동일합니다 `perspective` 위, 단, 첫 번째 기간 값 100%가 숨겨져 있습니다.

## 요약 {#finish}

다음 `Cohort Report Builder` 는 일반에 따라 사용자를 그룹화하도록 최적화되어 있습니다. `cohort date`. 유사한 활동이나 속성으로 사용자를 그룹화하는 데 관심이 있을 수 있습니다. Adobe은 체크 아웃을 권장합니다. [질적 집단에 대한 이 튜토리얼](../dev-reports/create-qual-cohort-analysis.md) 시작합니다.
