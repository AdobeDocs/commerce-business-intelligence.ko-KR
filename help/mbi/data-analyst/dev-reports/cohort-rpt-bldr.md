---
title: 집단 Report Builder
description: 라이프 사이클에 유사한 특성을 공유하는 사용자 그룹의 분석에 대해 알아봅니다.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# 집단 Report Builder

시간이 지남에 따라 사용자의 여러 하위 세트가 어떻게 작동하는지 학습하고 싶었던 적이 있습니까? 예를 들어 프로모션 기간 동안 등록하는 사용자가 그렇지 않은 사용자보다 평균 라이프타임 수입이 더 많은지 궁금해한 적이 있습니까? 만약 `Yes`, 그런 다음 `Cohort Report Builder` 완벽한 도구야 [!DNL MBI] 는 이 분석을 수행하고 비즈니스에 관련이 있도록 특별히 최적화되어 있습니다.

## 집단 분석이란? {#what}

`Cohort` 분석은 라이프 사이클에 유사한 특성을 공유하는 사용자 그룹의 분석으로 광범위하게 정의할 수 있습니다. 여러 사용자 그룹 간에 행동 트렌드를 식별할 수 있습니다.

보다 심층적인 프라이머를 위해 `cohort` 분석, [여기 좀 보세요](https://www.cohortanalysis.com/) - 사이트에 게시했습니다!

사용자 [!DNL MBI] 대시보드, 사용자 만들기가 쉽습니다 `cohorts` 기준 `cohort` 계정의 날짜 및 지표입니다.

## 집단 분석이 중요한 이유는 무엇입니까? {#important}

위에서 언급했듯이 `cohort` 분석을 사용하면 다양한 사용자 그룹 간의 행동 트렌드를 식별할 수 있습니다. 특정 그룹이 어떻게 행동하는지에 대한 확실한 이해를 통해, 당신은 당신의 결정들과 지출을 조절하여 매출을 극대화할 수 있다. 예를 들어 라이프타임 매출 `cohort` 분석 - 이러한 유형의 분석은 여러 가지 이유로 유용하지만, 바로 가까이에 있는 것이 더 나은 고객 확보 의사 결정입니다.

## 직접 만드는 방법 `cohort` 분석?

### 새로운 아키텍처

다음은 를 사용하기 위한 지침입니다 `Cohort Report Builder` on [새로운 아키텍처](../../administrator/account-management/new-architecture.md).

1. 클릭 **[!UICONTROL Report Builder]** 왼쪽 탭에서 또는 **[!UICONTROL Add Report** > **Create Report]** 아무 대시보드에서나 볼 수 있습니다.

1. 에서 `Report Builder` 선택 화면 **[!UICONTROL Create Report]** 다음 `Visual Report Builder` 선택 사항입니다.

**지표 추가**

이제 우리가 `Report Builder`를 채울 지표를 추가합니다(예: `Revenue` 또는 `Orders`).

>[!NOTE]
>
>기본 [!DNL Google Analytics] 지표는 와 호환되지 않습니다 `Cohort Report Builder`.

**지표 보기를 다음으로 전환`Cohort`**

![](../../assets/visual-report-builder-cohort-toggle.png)

그러면 새 창이 열리고 여기에서 `Cohort` 보고서.

### 5가지 사양이 필요합니다. `Cohort` 보고서:

1. 그룹 지정 방법 `cohorts`
1. 다음 `cohort` 기간
1. 숫자 `cohorts` 를 보려면
1. 각 데이터의 최소 양 `cohort` 다음을 포함해야 합니다.
1. 다음 시간 이후 시간 범위 `cohort` 발생 횟수

#### 1. 그룹화 `cohorts`

`Cohorts` 과 같은 타임스탬프로 함께 그룹화됩니다 **등록 날짜** 또는 **최초 주문 날짜**.

>[!NOTE]
>
>지표에 대해 지표가 빌드된 것과 동일한 타임스탬프를 사용할 수 없습니다 `cohort` 날짜. 이를 필요로 하는 분석의 경우 `Standard report builder` 을 가리키도록 업데이트하는 것이 좋습니다.

#### 2. `Cohort` 기간

그룹화할 기간 선택 `cohorts` 기준. 즉, 위에서 선택한 타임스탬프의 일부가 가장 중요합니다. a `week`, `month`, `quarter`, 또는 `year`?  보고서에는 여기에서 선택하는 간격으로 데이터가 표시됩니다

#### 3. 및 4. 숫자 설정 `cohorts` 각 데이터를 보고 양만큼 `cohort` 다음과 같습니다

이러한 매개 변수는 `cohorts` 당신이 관심 있고, `Preview` 창 하단에 있는 상자는 보고서에 어떤 집단이 표시될지 정확히 보여 줍니다.

기본적으로 현재 `cohort` 에 필요한 최소 데이터 양을 변경하지 않는 한 포함되지 않습니다 `cohort` to `0`. 이 경우 `cohort` 현재 기간에 대해서는 부분 데이터만 포함됩니다.

#### 5. 다음 이후 시간 범위 `Cohort` 발생 횟수

이 기능을 사용하면 선택한 항목에 대해 보는 데이터의 시간 범위를 설정할 수 있습니다 `cohorts`. 예를 들어 매월 24개를 보려는 경우 `cohorts` 기준 `customer's first order date`하지만 각 사용자에 대한 처음 3개월 데이터의 `cohort`를 설정하는 경우 `number of cohorts to view` to `24` 그리고 `time range after cohort occurrence` to `3`.

이 값의 간격은 `cohort time period` 및 값이 `12` 기본적으로 달력 아이콘을 클릭하여 편집하지 않으면 값이 변경되지 않습니다.

![](../../assets/cohort-time-range.png)

#### 기타 참고 사항

* [!UICONTROL Filters]: 지표에 적용된 내용은 `Standard` 및 `Cohort` 보기.

* 자세한 내용은 [`Perspectives`](#perspectives).

#### 예

여기 모든 것을 함께 가져오는 예가 있습니다. 이 예제에서는 `cohort`의 첫 번째 구매로 해당 집단이 다음 6개월 내에 다시 구매를 하기 위해 돌아올 예정인지 확인합니다.

![주문 집단](../../assets/crb_example.gif)

### 기존 아키텍처

#### 기존 아키텍처 {#personalinfo}

다음은 의 이전 버전에 대한 지침입니다 `Cohort Report Builder`. 새 버전을 사용하는 데 관심이 있는 경우 [새로운 아키텍처](../../administrator/account-management/new-architecture.md) 로 마이그레이션에 대한 자세한 정보 [!DNL MBI] 새 아키텍처 계정.

#### 직접 만드는 방법 `cohort` 분석? {#create}

![](../../assets/create-cohort-analysis.png)

`Cohort` 분석 작업 여기서는 누적 및 사용자별로 시간이 지남에 따라 매출이 증가하는 것을 볼 수 있습니다.

이 섹션에서는 사용자가 직접 만드는 과정을 안내합니다 `cohort` 분석. 예(및 프로세스를 보여 주는 애니메이션 GIF)의 경우 [예제 섹션](#examples) 이 문서의

1. 클릭 **[!UICONTROL Report Builder]** 왼쪽 탭에서 또는 **[!UICONTROL Add Report** > **Create Report]** 아무 대시보드에서나 볼 수 있습니다.

1. 에서 `Report Builder Selection` 을 클릭하고 **[!UICONTROL Create Report]** 다음 `Cohort Analysis` 선택 사항입니다.

#### 지표 추가

이제 우리가 `Cohort Report Builder`, 지표를 추가하겠습니다(예: `Revenue` 또는 `Number of orders`)에 대한 분석을 수행할 수 있습니다.

>[!NOTE]
>
>기본 [!DNL Google Analytics] 지표는 와 호환되지 않습니다 `Cohort Report Builder`.

#### 집단 날짜 선택 {#date}

다음 단계는 `cohort date`. 사용자를 그룹화하는 날짜입니다. 예를 들어 다음 경우가 있을 수 있습니다 `User's first order date` 또는 `User's registration date`.

>[!NOTE]
>
>지표가 빌드되는 동일한 날짜를 사용할 수 없습니다(예: `created at`) `cohort date`.

#### 간격 및 기간 설정

다음으로, `Interval` 및 `Time Period`.

`Interval`
다음 `Interval` 옵션을 사용하면 `length` 당신의 `cohorts`. 예를 들어, 이 `Month`로 설정되면 보고서가 몇 개월 단위로 측정됩니다.

를 사용하여 x축에 이러한 간격이 표시되는 방식을 변경할 수 있습니다 **기간** 메뉴 아래의 제품에서 사용할 수 있습니다.

`Time Period`
를 사용하십시오 `Time Period` 특정 사용자를 선택하는 메뉴 `cohorts` 을 참조하십시오. 모든 항목을 표시할 수 있습니다 `cohort`를 선택하거나 목록에서 선택하거나 시간 범위를 지정하거나 `cohorts` 을 포함합니다. 예를 들어 `Specific Cohorts` 선택 사항, 분석에 포함할 특정 월을 선택할 수 있습니다.

![사용 `Time Period` 특정 추가 메뉴 `Cohorts`](../../assets/Cohort_Time_Period.gif)

만약 우리가 `cohorts` 등록 날짜별로 선택한 다음 `Specific Cohorts` 목록에 해당 달에 등록한 모든 사용자가 포함됩니다.

#### X축 정의

아래 `duration`차트의 X축 설정을 정의할 수 있습니다. 즉, 각 데이터 포인트가 나타내는 시간 및 분석에 포함할 데이터 포인트 수입니다.

#### 선택 `counting members` 표

사용자를 `cohort date` 다른 테이블에서 연결된 경우 `counting members in the … table` 선택 사항입니다.

![](../../assets/Cohort_Counting_Members_option.png)

이 설정을 이해하는 예를 살펴보겠습니다. 보고서를 작성한 경우 `Revenue` 지표 기준 `Customer's registration date`. 또한 원근감을 사용하고 `Average value per cohort member` 시간 경과에 따른 구매자당 수익을 조회하기 위해. 구매자당 평균 가치를 찾으려면 나눌 구매자의 수를 결정해야 합니다. 등록된 고객 수가 `customers` 표 또는 사용자의 고유 구매자의 수입니다 `orders table` 같은 기간?

이 설정은 해당 질문에 답합니다. 에서 멤버 계산 `customers` 테이블에는 평균적으로 모든 고객(구매했는지 여부에 상관없이)이 포함됩니다. 에서 멤버 계산 `orders` 표에는 구매한 고객만 포함되어 있습니다.

#### 원근 선택 {#perspective}

지표 및 분석 방법을 정의한 후 `perspective` 를 사용하려고 합니다.

보고서 시각화 바로 위에 있는 은 `perspective` 설정.

자세한 내용은 [관점](#perspectives).

![](../../assets/Cohort_Perspective_Menu.png)

## 집단 분석의 예 {#examples}

이제 Adobe Mobile Services에서 `cohort` 분석, 몇 가지 예를 살펴보겠습니다.

### 사용자의 특성을 알고 싶습니다 `cohorts` 시간이 지남에 따라 성장하고 있습니다.

![사용자 `cohorts` 시간이 지남에 따라](../../assets/cohort1.gif)

이 예에서는 `Revenue` 지표, 집단을 `customer's first order date`, 가장 최근 8개를 선택함 `cohorts` (에 정의됨) `Time Period` 메뉴)를 포함할 필요가 없습니다. 시간이 지남에 따라 집단이 어떻게 성장했는지를 보기 위해 `Cumulative Average Value per Cohort Member` `perspective`.

### 평균적으로 사용자가 자신의 라이프타임 동안 몇 번이나 주문을 하는지 알고 싶습니다.

!![Average number of orders users make at different points in their lifetimes](../../assets/cohort2.gif)

이 예에서는 `Number of orders` 지표, 집단을 `customer's first order date`, 및에 가장 최근 집단 8개(에 정의됨) 포함 `Time Period` 메뉴 아래의 제품에서 사용할 수 있습니다. 각 집단에 대한 평균 주문 수를 보기 위해 `perspective` to `Average Value per Cohort Member`.

### 사용자의 향후 구매 활동과 비즈니스의 첫 달 활동을 비교하는 방법을 알고 싶습니다.

![사용자의 향후 구매 활동과 첫 번째 달의 활동 비교](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
이는 해당 라이프 사이클에서 지정된 시점에 주어진 집단 그룹의 증분 기여도를 보여줍니다. (예: &quot;6주&quot; 포인트는 6주 동안 사용자가 수행한 모든 데이터 포인트를 표시합니다.)

`Average Value per Cohort Member`
이렇게 하면 `Standard cohort` (1)에서 각 `cohort` 그룹에 속해 있어야 합니다. 일부 집단 그룹에는 동일한 수의 사용자가 포함되지 않을 수 있으므로 이 기능은 한 개 이상의 사용자를 대상으로 집단 성과를 비교하는 데 유용할 수 있습니다. 예를 들어, 특정 사용자의 사용자당 평균 주 6개 매출 `cohort`.

`Cumulative`
이 `perspective` 전통적인 `cohort` 분석 `cumulative` 기본. 즉, 해당 라이프사이클에서 지정된 시점에 현재까지 해당 집단에 대한 총 기여도를 보여줍니다. 예를 들어, 특정 집단에 있는 6주 사용자의 누적 매출입니다.

`Cumulative Average Value per Cohort Member`
이렇게 하면 `Cumulative` (3)에서 각 사용자 수로 분석 `cohort` 그룹에 속해 있어야 합니다. 페이지당 평균 라이프타임 기여도(종종 평균 라이프타임 매출)를 보여줍니다 `cohort` 각 기간에서 멤버 `cohort's` 삶이요 예를 들어 6월에 가입한 사용자 6개월 후의 평균 라이프타임 수입입니다.

`Percent of First Value (show first value)`
이렇게 하면 집계가 분석됩니다 `cohort` 특정 시간에 기여하기 `cohort's` 첫 번째 기간에 기여의 백분율로 라이프 사이클을 지정할 수 있습니다. 예를 들어, 월 6일 매출액은 6월에 가입한 사용자의 월 1일 매출로 나누어집니다.

`Percent of First Value (hide first value)`
이것은 와 같습니다 `perspective` 위의 경우, 첫 번째 기간 값 100%가 숨겨진다는 점을 제외하고,

## 포장 {#finish}

다음 `Cohort Report Builder` 는 현재 일반적인 방법으로 사용자를 그룹화하기 위해 최적화되어 있습니다 `cohort date`. 비슷한 활동이나 속성별로 사용자를 그룹화하는 데 관심이 있을 수 있습니다. 이러한 경우 기꺼이 도와 드리겠습니다. 체크아웃을 권장합니다 [질적 집단에 대한 이 자습서](../dev-reports/create-qual-cohort-analysis.md) 시작하기
