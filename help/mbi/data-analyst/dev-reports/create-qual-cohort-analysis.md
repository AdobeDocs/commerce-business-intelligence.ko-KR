---
title: 질적 집단 분석 만들기
description: 질적 집단 식별, 이 분석을 작성하는 데 관심이 있는 이유 및 분석에 작성하는 방법을 알아봅니다 [!DNL MBI].
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 0%

---

# 만들기 `Qualitative Cohort Analysis`

당신 어떻게 [!DNL Adwords]&quot;획득한 고객 세그먼트가 유기 검색으로 획득한 고객보다 LTV가 증가합니까? 공연을 할 생각을 해 본 적이 있나요 `cohort` 동일한 보고서에서 서로 다른 고객 세그먼트에 대한 분석 그렇다면 `qualitative cohort analysis` 당신이 그 질문에 대답하는 것을 도와줄 것입니다.

이 문서에서, 질적 집단, 이 분석을 구축하는 데 관심이 있는 이유 및 이 분석을 작성하는 방법에 대해 살펴봅니다 [!DNL MBI].

## 정의 `qualitative cohorts`어쨌든? {#whatare}

`Cohort` 일반적으로 분석은 라이프 사이클에 유사한 특성을 공유하는 사용자 그룹의 분석으로 광범위하게 정의할 수 있습니다. 여러 사용자 그룹 간에 행동 트렌드를 식별할 수 있습니다.

자세한 내용은 [집단 분석](https://www.cohortanalysis.com/) - 사이트에 게시했습니다!

가장 많이 `cohort` 분석 [!DNL MBI] 공통 날짜(예: 지정된 월에 첫 번째 구매를 한 모든 고객 세트)로 사용자를 그룹화합니다. A `qualitative cohort` 약간 다릅니다. 시간 기반이 아닌 특성에 의해 정의된 사용자 그룹입니다. 예를 들면 다음과 같습니다.

* 광고 캠페인에서 취득한 모든 사용자 집합
* 첫 번째 구매에 쿠폰이 포함되거나 구매하지 않은 모든 사용자 집합
* 특정 나이의 모든 사용자 집합

## 그게 정상과 어떻게 다른가요 `cohort` 빌더? {#different}

다음 [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) 는 시간 기반 특성을 사용하여 그룹을 그룹화하도록 최적화되었습니다. 이는 특정 사용자 세그먼트(예: 유료 검색 캠페인을 통해 획득한 모든 사용자)에 중점을 두는 분석에 유용합니다. 에서 `Cohort Analysis Builder`, (1) 특정 사용자 그룹에 중점을 둘 수 있습니다. (2) `cohort` 날짜로(첫 번째 주문 일자 등).

그러나 동일한 집단 보고서(`paid` 검색 대 `organic` 검색과 직접 트래픽(아마도?)) 이러한 고급 분석은 `Report Builder`.

## 분석을 설정하기 위해 지원을 위해 어떤 정보를 보내야 합니까? {#support}

만들기 `qualitative cohort` 의 보고서 `Report Builder` 몇 가지 작업을 수행하는 분석가 팀이 [고급 계산 열](../data-warehouse-mgr/creating-calculated-columns.md) 필요한 테이블에

이러한 코드를 만들려면 [지원 티켓](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) (이 문서를 참조!) 다음은 알아야 할 사항입니다.

* 다음 `metric` 집단 분석을 사용하여 수행할 및 집단 분석이 사용하는 테이블(예: `Revenue`, `orders` 테이블).

* 다음 `user segments` 및 해당 정보가 데이터베이스에 있는 위치를 정의하려는 경우(예: 다른 값 `User's referral source`, 고유함 `users` 테이블 위로 내려가서 `orders`).

* 다음 `cohort date` 분석을 사용할 수 있습니다(예: a `User's first order date` timestamp). 이 예에서는 각 세그먼트를 보고 질문할 수 있습니다 `How does a user's revenue grow in the months following their first order date?`.

* 다음 `time interval` 분석 대상(예: `weeks`, `months`, 또는 `quarters` 후 `User's first order date`).

분석가 팀이 위에 응답하면 보고서를 작성할 새로운 고급 계산된 열 두 개가 있습니다. 그러면 아래 지침에 따라 이 작업을 수행할 수 있습니다.

## 질적 집단 분석 만들기 {#create}

먼저, 각 항목에 대해 한 번씩 작성에 관심이 있는 지표를 추가하려고 합니다 `cohort` 분석 중입니다. 이 예에서는 누적 사항을 확인하려고 합니다 `Revenue` 고객이 첫 번째 주문을 한 후 다음 세그먼트를 통해 세그먼트화되었습니다. `User's referral source`. 즉, 각 세그먼트에 대해 하나를 추가합니다 `Revenue` 특정 세그먼트에 대한 지표 및 필터:

![](../../assets/qualcohort1.gif)

두 번째, 보고서의 시간 옵션을 두 번 변경해야 합니다.

1. 설정 `time interval` to `None`. 이것은 결국 일반적인 시간 옵션을 사용하지 않고 시간 간격에 따라 차원으로 그룹화하기 때문입니다.

1. 설정 `time range` 보고서를 적용할 시간 창에 표시합니다.

이 예제에서는 `all time` 보기 `Revenue`. 그 후에는 일련의 점이 표시됩니다.

![](../../assets/qualcohort2.gif)

세 번째, 을 실제로 설정하도록 조정합니다 `cohorts`. 기준 `cohort date` 및 `time interval` 분석가 팀에 지정한 경우, `cohort` 데이트 이 예에서 해당 사용자 지정 차원은 라고 합니다 `Months between this order and customer's first order date`. 이 차원을 사용하면 다음 작업을 수행해야 합니다.

* `Group by` 을 사용하는 차원 `group by` 옵션

* 의 모든 값을 선택합니다 `dimension` 관심 있는 곳

* 사용 `Show top/bottom option`원하는 위쪽 X 월을 선택하고 `Months between this order and customer's first order date` 차원

이제 각 행에 대해 한 줄을 볼 수 있습니다 `cohort` 지정한 URL입니다. 이제 예를 살펴보겠습니다. `Revenue` 각 참조 소스 사용자가 기여 `grouped by` 첫 번째 주문과 후속 주문 사이의 개월 수입니다. 또한 `Cumulative perspective` 다음을 참조하십시오 `cohorts'` 전체 성장 - 더 세분화된 결과 표를 살펴보십시오.

이것이 우리에게 무엇을 의미합니까? 여기에서 특정 참조 소스 `Paid search` 는 고객의 구매 라이프타임 첫 달 동안 매우 유용하지만 반복 매출로 고객 기반을 유지하지 못합니다. While `Direct Traffic` 적은 양에서 시작하며, 다음 달의 수익은 실제로 비슷한 속도로 축적됩니다.

아무리 주사위를 던지더라도 `cohort` analysis 는 analysis toolbox에서 강력한 도구입니다. 이러한 유형의 분석은 기존의 `time-based cohorts` 그렇지 않을 수 있으므로 보다 나은 데이터 기반 의사 결정을 내릴 수 있습니다.
