---
title: 질적 집단 분석 만들기
description: 질적 집단은 무엇이며, 이 분석을 작성하는 데 관심이 있는 이유와 이러한 집단을 만들 수 있는 방법을 알아봅니다 [!DNL MBI].
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# 만들기 `Qualitative Cohort Analysis`

어떻게 하는지 아세요? [!DNL Adwords]-획득한 고객 세그먼트는 유기 검색(organic search)을 통해 획득한 고객보다 LTV가 증가합니다. 공연을 해 볼 생각은 없었나요? `cohort` 동일한 보고서에서 서로 다른 고객 세그먼트를 나란히 분석합니까? 있는 경우 `qualitative cohort analysis` 는 이러한 질문에 답변하는 데 도움이 됩니다.

이 문서에서는 질적 집단에 대해, 이 분석을 빌드하는 데 관심을 가질 수 있는 이유 및 이를 작성하는 방법에 대해 설명합니다 [!DNL MBI].

## 이란? `qualitative cohorts`그나저나? {#whatare}

`Cohort` 일반적으로 분석은 수명 주기에 걸쳐 유사한 특성을 공유하는 사용자 집단의 분석으로 광범위하게 정의될 수 있다. 이를 통해 다양한 사용자 그룹 간 행동 트렌드를 식별할 수 있습니다.

다음을 참조하십시오 [집단 분석](https://www.cohortanalysis.com/).

가장 `cohort` 에서 분석 [!DNL MBI] 공통 날짜(예: 주어진 달에 첫 번째 구매한 모든 고객 집합)로 사용자를 함께 그룹화합니다. A `qualitative cohort` 는 약간 다릅니다. 시간 기반이 아닌 특성으로 정의된 사용자 그룹입니다. 예를 들면 다음과 같습니다.

* 광고 캠페인에서 획득한 모든 사용자 세트
* 첫 구매에 쿠폰이 포함된(또는 포함되지 않은) 모든 사용자 세트
* 특정 연령의 모든 사용자 집합

## 그게 보통과 어떻게 다른가요 `cohort` 빌더? {#different}

다음 [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) 은 시간 기반 특성을 사용하여 집단을 그룹화하는 데 최적화되어 있습니다. 이 기능은 사용자의 특정 세그먼트(예: 유료 검색 캠페인을 통해 획득한 모든 사용자)에 중점을 둔 분석에 유용합니다. 다음에서 `Cohort Analysis Builder`, (1)특정 사용자 그룹에 포커스를 두고 (2)를 수행할 수 있습니다 `cohort` (첫 번째 주문 날짜와 같은) 날짜.

그러나 동일한 집단 보고서에서 여러 사용자 세그먼트의 집단 행동을 분석하려는 경우(`paid` 검색 및 `organic` 검색과 직접 트래픽, 아마도?),에서 이 더 고급 분석을 구성할 수 있습니다. `Report Builder`.

## 분석을 설정하기 위해 지원팀에 어떤 정보를 보내야 합니까? {#support}

만들기 `qualitative cohort` 보고서 위치: `Report Builder` Adobe 분석팀이 다음을 생성합니다. [고급 계산 열](../data-warehouse-mgr/creating-calculated-columns.md) 필요한 테이블에.

빌드하려면 [지원 티켓](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) (그리고 이 문서를 참조하십시오!) 다음은 알고 있어야 하는 사항입니다.

* 다음 `metric` 및 사용하는 테이블을 사용하여 집단 분석을 수행하려고 합니다(예: `Revenue`, 빌드 날짜: `orders` table)을 참조하십시오.

* 다음 `user segments` 데이터베이스에서 해당 정보가 있는 위치 및 위치를 정의하려는 경우(예: `User's referral source`, 기본 `users` 테이블을 재배치하여 `orders`).

* 다음 `cohort date` 분석을 사용하려는 경우(예: `User's first order date` timestamp). 이 예제를 통해 각 세그먼트를 보고 질문할 수 있습니다 `How does a user's revenue grow in the months following their first order date?`.

* 다음 `time interval` 분석을 보려는 대상(예: `weeks`, `months`, 또는 `quarters` 다음 이후 `User's first order date`).

Adobe 분석가 팀이 위에 응답하면 보고서를 작성할 새로운 고급 계산 열 두 개가 있습니다. 그러면 아래의 지시 사항을 따라 하시면 됩니다.

## 질적 집단 분석 만들기 {#create}

먼저, 집단에 관심있는 지표를 각각에 대해 한 번씩 추가하려고 합니다 `cohort` 분석 중입니다. 이 예에서는 누적 을 보여 줍니다 `Revenue` 고객의 첫 번째 주문 후 몇 개월 이내에 다음 항목으로 분할됨 `User's referral source`. 즉, 각 세그먼트에 대해 하나를 추가합니다 `Revenue` 특정 세그먼트에 대한 지표 및 필터:

![](../../assets/qualcohort1.gif)

둘째, 보고서의 시간 옵션을 두 가지 변경해야 합니다.

1. 설정 `time interval` 끝 `None`. 이는 일반적인 시간 옵션을 사용하는 대신 시간 간격을 기준으로 차원을 그룹화하기 때문입니다.

1. 설정 `time range` 보고서에서 다룰 시간의 창을 표시합니다.

이 예에서는 `all time` 보기 `Revenue`. 그런 다음 일련의 점으로 끝나야 합니다.

![](../../assets/qualcohort2.gif)

셋째, 를 조정하여 `cohorts`. 를 기반으로 함 `cohort date` 및 `time interval` Adobe 분석가 팀에 을(를) 지정했으며, 계정에서 다음을 수행하는 차원이 있습니다. `cohort` 데이트. 이 예에서 해당 사용자 정의 차원을 호출합니다. `Months between this order and customer's first order date`. 이 차원을 사용하면 다음 작업을 수행할 수 있습니다.

* `Group by` 을 사용하는 차원 `group by` 옵션

* 의 모든 값 선택 `dimension` 관심 있는 항목

* 포함 `Show top/bottom option`에 관심이 있는 상위 X개월을 선택하고 `Months between this order and customer's first order date` 차원

이제 각 줄에 대해 한 줄을 볼 수 있습니다 `cohort` 을(를) 지정했습니다. 지금 예제를 확인해 보십시오. `Revenue` 각 추천 소스의 사용자가 기여, `grouped by` 첫 번째 주문과 이후 주문 사이의 개월 수. 이 예제는 또한 `Cumulative perspective` 을(를) 보려면 `cohorts'` 총 증가 - 보다 세분화된 결과를 보려면 결과 표를 참조하십시오.

이것이 우리에게 무엇을 말해주나요? 여기서 특정 참조 소스 `Paid search` 은 고객의 구매 라이프타임 첫 달에 가치가 있지만 반복 매출로 고객 기반을 유지하지 못합니다. While `Direct Traffic` 낮은 금액에서 시작하여 이후 달의 매출은 실제로 비슷한 속도로 누적됩니다.

아무리 주사위를 던지더라도, `cohort` analysis는 analysis toolbox의 강력한 도구입니다. 이러한 유형의 분석은 일반적인 비즈니스에 대한 흥미로운 통찰력을 제공할 수 있습니다 `time-based cohorts` 그렇지 않을 수 있으므로 더 나은 데이터 기반 결정을 내릴 수 있습니다.
