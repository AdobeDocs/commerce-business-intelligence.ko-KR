---
title: Report Builder의 공식
description: Report Builder에서 공식을 사용하는 방법을 알아봅니다.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# 수식 `Report Builder`

에서 [`Report Builder`](../../tutorials/using-visual-report-builder.md)를 사용하면 [정의된 지표](../../data-user/reports/ess-manage-data-metrics.md) 내 계정에 있을 때 이러한 지표를 수식에 결합하면 데이터에서 추가 통찰력을 얻을 수 있습니다. 이 문서에서 공식을 사용할 수 있는 방법에 대해 자세히 살펴봅니다 `Report Builder` 뛰어들어!

## 정의 `formula`? {#what}

에서 `Report Builder`, `formula` 는 일부 수학 논리를 기반으로 하나 이상의 지표의 조합입니다. 일반적인 예는 다음과 같습니다.

![](../../assets/formula-example.png)

이 예제에서는 `Number of orders metric (A)` 그리고 `Distinct buyers metric (B)`그리고 우리의 목표는 다음과 같은 질문에 답하는 것입니다. 매달에 바이어들이 주문하는 평균 주문 수는 얼마입니까? 수식의 매개 변수는 다음과 같습니다.

* `Definition`: 여기서는 입력 지표에 수학을 적용합니다. 이 예에서는 주문 수를 고유한 구매자 수로 나누면 평균 주문 수가 표시됩니다. 따라서 정의는 (A/B)입니다.

* `Format`: 배합표가 숫자, 기간 또는 통화 금액을 반환합니까? 수식의 정의 옆에 드롭다운이 있습니다. 드롭다운을 사용하여 반환 형식을 지정할 수 있습니다. 이 경우 숫자입니다.

* `Miscellaneous`: 수식의 타임스탬프, 그룹화, 관점 및 필터는 모두 입력 지표로 상속됩니다. 여기서 할 일이 없어!

## 사용 방법 `formulas` 내 보고서에? {#how}

이제 기본 사항을 다루었으니 몇 가지 예를 살펴보겠습니다.

### 예: 최초 주문으로 인해 발생하는 수익의 몇 퍼센트를 알고 싶습니다.

![배합표를 사용하여 최초 주문으로 인한 매출 퍼센트를 찾습니다](../../assets/first_time_orders.gif)

이 예제에서는 `Revenue` 및 `Revenue (first time orders)` 지표 를 참조하십시오. 다음을 `Revenue (first time orders)(B)` 지표 `Revenue metric (A)` 반환 형식을으로 설정하고 `Percent`, 최초 주문으로 인한 매출 퍼센트를 확인할 수 있습니다.

### 예: 주문당 평균 매출액이 어떻게 되는지 알고 싶으며, `promo code`.

![공식 을 사용하여 프로모션 코드가 있는 주문당 평균 매출을 찾습니다](../../assets/promo_code.gif)

이 예제에서는 `Revenue` 및 `Number of orders` 지표 를 참조하십시오. 이 질문에 대한 답은 두 단계로 나누어져 있습니다 `Revenue (A)` 기준 `Number of orders (B)` 반환 형식을으로 설정하고 `Currency`. 다음으로, 공식 결과(`Avg. Revenue per order`)을 클릭하여 결과를 표시하고 그룹화합니다 `Promo code`.

### 예: 새로운 고객의 UTM 출처의 분포를 알고 싶습니다.

![새 고객의 UTM 소스 분포를 찾기 위한 공식 사용](../../assets/distro.gif)

이 질문에 대한 답변을 찾으려면 다음과 같은 몇 가지 단계가 포함됩니다.

1. 먼저 을 추가했습니다. `New Customers` 지표를 사용하여 그룹화한 다음 `utm_source - all`. 지표 `A`, 또는 `New Customers (grouped)`.

1. 다음으로, 우리는 `New Customers (grouped)` 지표를 설정하고 독립 차원을 사용하도록 설정합니다. 지표 `B` - `New customers (ungrouped)` - 신규 고객의 총 수를 보여줍니다.

1. 두 지표를 모두 숨긴 후 공식 정의를 로 설정합니다 `A/B`. 이렇게 하면 `New customers (grouped)` 기준 `New Customers (ungrouped)`.

1. 다음으로 결과 형식을 `Percent`.

이 예제에서는 `Stacked Columns` 원근 을 사용하여 월별로 결과를 표시합니다. 이를 통해 월별로 신규 고객 분포를 비교할 수 있습니다.

## 포장 {#wrapup}

위의 예에서 그 수식의 `timestamp`, `groupings`, `perspectives`, 및 `filters` 입력 지표에서 상속됩니까? 수식을 사용하여 활용할 수 있습니다 `perspectives` 및 [독립 시간 옵션](../../tutorials/time-options-visual-rpt-bldr.md){: target=&quot;_blank&quot;}. 지표가 할 수 있는 것과 같습니다.

공식 사용에 대한 추가 질문이 있는 경우 `Report Builder`, [연락처 지원](../../guide-overview.md).
