---
title: 집단 Report Builder
description: 라이프사이클 동안 유사한 특성을 공유하는 사용자 그룹의 분석에 대해 알아봅니다.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# 집단 Report Builder

사용자의 다양한 하위 집합이 시간에 따라 어떻게 행동하는지 연구하고 싶습니까? 예를 들어 프로모션 기간 동안 등록한 사용자가 등록하지 않은 사용자보다 평균 라이프타임 수익이 더 높은지 생각해 본 적이 있습니까? 답변이 `Yes`이면 `Cohort Report Builder`이(가) 완벽한 도구입니다. [!DNL Adobe Commerce Intelligence]은(는) 이 분석을 수행하고 비즈니스와 관련되도록 최적화되었습니다.

## 집단 분석이란? {#what}

`Cohort` 분석은 수명 주기 동안 유사한 특성을 공유하는 사용자 그룹의 분석으로 광범위하게 정의할 수 있습니다. 이를 통해 다양한 사용자 그룹 간 행동 트렌드를 식별할 수 있습니다.

`cohort` 분석에 대한 심도 있는 입문서를 보려면 [이 페이지](https://www.cohortanalysis.com/)를 검토하십시오.

[!DNL Commerce Intelligence] 대시보드에서 계정의 `cohort` 날짜 및 지표를 기반으로 `cohorts` 사용자를 쉽게 만들 수 있습니다.

## 그렇다면 코호트 분석이 중요한 이유는 무엇입니까? {#important}

위에서 언급했듯이 `cohort` 분석을 사용하면 다양한 사용자 그룹 간의 동작 트렌드를 식별할 수 있습니다. 특정 그룹의 행동을 확실히 이해하면 의사 결정과 지출을 조정하여 매출을 극대화할 수 있습니다. 예를 들어 평생 매출 `cohort`을(를) 분석해 보십시오. 이러한 종류의 분석은 여러 가지 이유로 유익하지만, 즉각적인 분석은 더 나은 고객 확보 결정입니다.

## 나만의 `cohort` 분석을 만들려면 어떻게 해야 합니까?

### 새로운 아키텍처

다음은 [새 아키텍처](../../administrator/account-management/new-architecture.md)에서 `Cohort Report Builder`을(를) 사용하기 위한 지침입니다.

1. 왼쪽 탭에서 **[!UICONTROL Report Builder]**&#x200B;을(를) 클릭하거나 대시보드에서 **[!UICONTROL Add Report** > **Create Report]**&#x200B;을(를) 클릭합니다.

1. `Report Builder` 선택 화면에서 `Visual Report Builder` 옵션 옆의 **[!UICONTROL Create Report]**&#x200B;을(를) 클릭합니다.

**지표 추가**

`Report Builder`에 있으므로 분석을 수행할 지표를 추가하십시오(예: `Revenue` 또는 `Orders`).

>[!NOTE]
>
>네이티브 [!DNL Google Analytics] 지표가 `Cohort Report Builder`과(와) 호환되지 않습니다.

**지표 보기를`Cohort`**(으)로 전환

![](../../assets/visual-report-builder-cohort-toggle.png)

`Cohort` 보고서의 세부 정보를 구성할 수 있는 새 창이 열립니다.

### `Cohort` 보고서를 작성하려면 5개의 사양이 필요합니다.

1. `cohorts`을(를) 그룹화하는 방법
1. `cohort` 기간
1. 볼 `cohorts`의 수
1. 각 `cohort`에 포함되어야 하는 최소 데이터 양
1. `cohort`회 발생 이후의 시간 범위

#### 1. `cohorts` 그룹화

`Cohorts`은(는) **등록 날짜** 또는 **첫 번째 주문 날짜**&#x200B;와 같은 타임스탬프로 그룹화됩니다.

>[!NOTE]
>
>`cohort` 날짜에 대해 지표가 빌드된 것과 동일한 타임스탬프를 사용할 수 없습니다. 이를 필요로 하는 분석의 경우 대신 `Standard report builder`을(를) 사용할 수 있습니다.

#### 2. `Cohort` 기간

`cohorts`을(를) 그룹화할 기간을 선택하십시오. 즉, 위에서 선택한 타임스탬프 중 가장 중요한 부분은 `week`, `month`, `quarter` 또는 `year`입니까? 보고서는 여기에서 선택한 간격으로 데이터를 표시합니다

#### 3. 및 4. 보려는 `cohorts`의 수와 각 `cohort`에 필요한 데이터의 양을 설정합니다.

이러한 매개 변수를 사용하면 관심 있는 `cohorts`만 볼 수 있으며, 창 하단의 편리한 `Preview` 상자는 보고서에 표시되는 집단을 정확하게 보여 줍니다.

각 `cohort`에 필요한 최소 데이터 양을 `0`(으)로 변경하지 않으면 기본적으로 현재 `cohort`은(는) 포함되지 않습니다. 이 경우 현재 기간의 `cohort`에는 부분 데이터만 포함됩니다.

#### 5. `Cohort`회 발생 후 시간 범위

이 기능을 사용하면 선택한 `cohorts`에 대해 보는 데이터의 시간 범위를 설정할 수 있습니다. 예를 들어 `customer's first order date`을(를) 기준으로 24개의 월별 `cohorts`을(를) 보려 하지만 각 `cohort`에 대한 처음 3개월간의 데이터에만 관심이 있는 경우 `number of cohorts to view`을(를) `24`(으)로, `time range after cohort occurrence`을(를) `3`(으)로 설정할 수 있습니다.

이 값의 간격은 `cohort time period`에서 선택한 항목에 따라 변경되며 값은 기본적으로 `12`(으)로 설정됩니다. 값을 편집하려면 달력 아이콘을 클릭해야 값이 변경됩니다.

![](../../assets/cohort-time-range.png)

#### 기타 참고 사항

* [!UICONTROL Filters]: `Standard` 보기와 `Cohort` 보기 사이를 전환할 때 지표에 적용된 상태가 그대로 유지됩니다.

* [`Perspectives`](#perspectives)을(를) 참조하십시오.

#### 예

다음은 이를 모두 통합하는 예제입니다. 이 예에서는 `cohort`의 첫 구매 후 주문 동작을 확인하여 해당 집단이 향후 6개월 이내에 반복 구매로 돌아올지 확인하려고 합니다.

![주문 집단](../../assets/crb_example.gif)

### 레거시 아키텍처

#### 레거시 아키텍처 {#personalinfo}

다음은 이전 버전의 `Cohort Report Builder`에 대한 지침입니다. 새 버전을 사용하려면 [!DNL Commerce Intelligence] 새 아키텍처 계정으로 마이그레이션하는 방법에 대한 자세한 내용은 [새 아키텍처](../../administrator/account-management/new-architecture.md)를 참조하십시오.

#### 나만의 `cohort` 분석을 만들려면 어떻게 해야 합니까? {#create}

![](../../assets/create-cohort-analysis.png)

`Cohort` 분석 실행 중! 여기에서 누적 및 사용자별로 시간이 지남에 따라 증가하는 매출을 확인할 수 있습니다.

이 섹션에서는 `cohort` 분석을 만드는 과정을 안내합니다. 예제(및 프로세스를 보여 주는 애니메이션 GIF)는 이 항목의 [예제 섹션](#examples)을 참조하십시오.

1. 왼쪽 탭에서 **[!UICONTROL Report Builder]**&#x200B;을(를) 클릭하거나 대시보드에서 **[!UICONTROL Add Report** > **Create Report]**&#x200B;을(를) 클릭합니다.

1. `Report Builder Selection` 화면에서 `Cohort Analysis` 옵션 옆의 **[!UICONTROL Create Report]**&#x200B;을(를) 클릭합니다.

#### 지표 추가

`Cohort Report Builder`에 있으므로 분석을 수행할 지표(예: `Revenue` 또는 `Number of orders`)를 추가하십시오.

>[!NOTE]
>
>네이티브 [!DNL Google Analytics] 지표가 `Cohort Report Builder`과(와) 호환되지 않습니다.

#### 집단 날짜 선택 {#date}

다음 단계는 `cohort date`을(를) 지정하는 것입니다. 사용자를 그룹화하는 날짜입니다. 예를 들어 `User's first order date` 또는 `User's registration date`일 수 있습니다.

>[!NOTE]
>
>지표가 빌드된 날짜와 동일한 날짜(예: `created at`)를 `cohort date`과(와) 사용할 수 없습니다.

#### 간격 및 기간 설정

그런 다음 `Interval` 및 `Time Period`을(를) 설정합니다.

`Interval`
`Interval` 옵션을 사용하면 `cohorts`의 `length`을(를) 설정할 수 있습니다. 예를 들어 `Month`(으)로 설정된 경우 보고서는 월 단위로 측정됩니다.

**기간** 메뉴를 사용하여 이러한 간격이 x축에 표시되는 방식을 변경할 수 있습니다.

`Time Period`
`Time Period` 메뉴를 사용하여 분석할 특정 사용자 `cohorts`을(를) 선택하십시오. 모든 `cohort`을(를) 표시하거나, 목록에서 선택하거나, 시간 범위를 지정하거나, 포함할 `cohorts`의 롤링 시간 범위를 정의할 수 있습니다. 예를 들어 `Specific Cohorts` 옵션을 사용한 경우 분석에 포함할 특정 월을 선택할 수 있습니다.

![`Time Period` 메뉴를 사용하여 특정 `Cohorts`](../../assets/Cohort_Time_Period.gif) 추가

등록 날짜별로 `cohorts`을(를) 그룹화하고 `Specific Cohorts` 목록에서 4월, 5월, 6월을 선택한 경우 해당 달에 등록한 모든 사용자가 포함됩니다.

#### X축 정의

`duration`에서 차트의 X축 설정을 정의할 수 있습니다. 즉, 각 데이터 포인트가 나타내는 기간 수와 분석에 포함할 데이터 포인트 수가 표시됩니다.

#### `counting members` 테이블 선택

다른 테이블에서 연결된 `cohort date`에 의해 사용자를 그룹화하도록 선택한 경우 `counting members in the … table` 옵션이 표시될 수 있습니다.

![](../../assets/Cohort_Counting_Members_option.png)

이 설정을 이해하는 예를 참조하십시오. `Customer's registration date`까지 `Revenue` 지표를 그룹화한 보고서를 작성했다고 가정합니다. 또한 `Average value per cohort member` 관점을 사용하여 시간에 따른 구매자당 매출을 확인하려고 했습니다. 구매자당 평균값을 찾으려면 나눌 구매자 수를 결정해야 합니다. `customers` 테이블에 등록된 고객 수입니까? 아니면 같은 기간 동안 `orders table`에 있는 개별 구매자의 수입니까?

이 설정은 해당 질문에 대한 답을 제공합니다. `customers` 테이블의 멤버 수 계산에는 평균적으로 모든 고객(구매 여부에 상관없이)이 포함됩니다. `orders` 테이블의 계산 멤버에는 구매한 고객만 포함됩니다.

#### 원근 선택 {#perspective}

지표를 정의하고 지표를 분석하는 방법을 정의한 후 사용할 `perspective`을(를) 선택할 수 있습니다.

보고서 시각화 바로 위에 `perspective` 설정의 드롭다운이 있습니다.

[관점](#perspectives)을 참조하세요.

![](../../assets/Cohort_Perspective_Menu.png)

## 집단 분석의 예 {#examples}

`cohort` 분석을 만드는 방법을 살펴보았으므로, 몇 가지 예를 살펴보십시오.

### 시간이 지남에 따라 내 사용자 `cohorts`이(가) 어떻게 증가하고 있는지 알고 싶습니다.

![시간이 지남에 따라 사용자 `cohorts` 증가](../../assets/cohort1.gif)

이 예에서는 `Revenue` 지표를 분석하고, 집단을 `customer's first order date`(으)로 그룹화하고, 분석에 포함할 8개의 가장 최근 `cohorts`(`Time Period` 메뉴에 정의됨)을(를) 선택했습니다. 시간이 지남에 따라 집단이 어떻게 성장했는지 확인하려면 `Cumulative Average Value per Cohort Member` `perspective`을(를) 사용했습니다.

### 나는 평균적으로 사용자가 라이프타임 동안 다른 시점에서 얼마나 많은 주문을 하는지 알고 싶다.

(../../assets/cohort2.gif

이 예에서는 `Number of orders` 지표를 분석하고, 집단을 `customer's first order date`(으)로 그룹화하고, 분석에 가장 최근 8개의 집단(`Time Period` 메뉴에 정의됨)을 포함했습니다. 각 집단의 평균 주문 수를 보려면 `perspective`을(를) `Average Value per Cohort Member`(으)로 변경했습니다.

### 나는 사용자의 향후 구매 활동을 업무 첫 달의 활동과 어떻게 비교하는지 이해하고 싶다.

![사용자의 향후 구매 활동을 활동 첫 달과 비교](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
이는 라이프 사이클의 특정 시점에 특정 집단 그룹의 증분 기여를 보여줍니다. (예: &quot;6주&quot; 포인트에는 사용자가 6주에 만든 모든 데이터 포인트가 표시됩니다.)

`Average Value per Cohort Member`
(1)의 `Standard cohort` 분석을 각 `cohort` 그룹의 사용자 수로 나눕니다. 모든 코호트 그룹에 동일한 수의 사용자가 포함되지 않을 수 있으므로 이 기능은 코호트 성과를 사과 대 사과 기준으로 비교하는 데 유용할 수 있습니다. 예를 들어 특정 `cohort`의 사용자당 평균 6주 매출입니다.

`Cumulative`
이 `perspective`은(는) `cumulative`을(를) 기준으로 기존 `cohort` 분석을 표시합니다. 즉, 라이프 사이클의 특정 시점에서 현재까지 주어진 코호트의 총 기여도를 보여줍니다. 예를 들어 특정 집단의 사용자 6주 후 누적 매출입니다.

`Cumulative Average Value per Cohort Member`
(3)의 `Cumulative` 분석을 각 `cohort` 그룹의 사용자 수로 나눕니다. `cohort's` 수명 동안 각 기간의 `cohort` 구성원당 평균 수명 기여도(종종 평균 수명 수익)를 표시합니다. 예를 들어 6월에 가입한 6개월 이후의 평균 라이프타임 매출입니다.

`Percent of First Value (show first value)`
`cohort's` 수명 주기의 특정 시간에 집계된 `cohort` 기여도를 첫 번째 기간에 기여도의 비율로 분석합니다. 예를 들어 6개월 수입은 6월에 가입한 사용자의 1개월 수입으로 나눈 것입니다.

`Percent of First Value (hide first value)`
이는 100%의 첫 번째 기간 값이 숨겨져 있다는 점을 제외하고 위의 `perspective`과(와) 동일합니다.

## 요약 {#finish}

`Cohort Report Builder`은(는) 일반 `cohort date`을(를) 기준으로 사용자를 그룹화하는 데 최적화되어 있습니다. 유사한 활동이나 속성으로 사용자를 그룹화하는 데 관심이 있을 수 있습니다. Adobe 시작하려면 질적 집단에 대한 [이 튜토리얼](../dev-reports/create-qual-cohort-analysis.md)을(를) 확인하는 것이 좋습니다.
