---
title: Report Builder의 공식
description: Report Builder에서 수식을 사용하는 방법을 알아봅니다.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# 의 공식 `Report Builder`

다음에서 [`Report Builder`](../../tutorials/using-visual-report-builder.md)를 사용하여 강력한 시각화를 만들 수 있습니다. [정의된 지표](../../data-user/reports/ess-manage-data-metrics.md) 계정에서. 이러한 지표를 수식에 결합하면 데이터에서 추가적인 통찰력을 얻을 수 있습니다. 이 문서에서는 다음에서 수식을 사용하는 방법을 자세히 설명합니다. `Report Builder` 뛰어들자!

## (이)란? `formula`? {#what}

다음에서 `Report Builder`, a `formula` 는 일부 수학 논리를 기반으로 한 하나 이상의 지표의 조합입니다. 일반적인 예는 다음과 같습니다.

![](../../assets/formula-example.png)

이 예제에서는 `Number of orders metric (A)` 및 a `Distinct buyers metric (B)`, 그리고 목표는 질문에 답변하는 것입니다. 내 구매자가 매달 주문하는 평균 주문 수는 얼마입니까? 공식의 매개 변수는 다음과 같습니다.

* `Definition`: 여기에서 입력 지표에 계산을 적용합니다. 이 예에서 주문의 수를 개별 구매자의 수로 나누면 평균 주문 수를 알 수 있습니다. 따라서 정의는 (A/B)입니다.

* `Format`: 숫자, 기간 또는 통화 금액을 반환하는 수식입니까? 공식의 정의 옆에는 반환의 형식을 지정하는 데 사용할 수 있는 드롭다운이 있습니다. 이 경우 숫자입니다.

* `Miscellaneous`: 공식의 타임스탬프, 그룹화, 관점 및 필터가 모두 입력 지표에 상속됩니다. 여기에는 할 일이 없습니다!

## 사용 방법 `formulas` 내 보고서에서? {#how}

이제 기본 사항을 다루었으니 몇 가지 예를 살펴보십시오.

### 예: 첫 번째 주문으로 인한 매출의 몇 퍼센트를 확인하려고 합니다.

![최초 주문으로 인한 매출의 퍼센트를 찾기 위해 공식 사용](../../assets/first_time_orders.gif)

이 예에서는 `Revenue` 및 `Revenue (first time orders)` 지표. 다음을 나누기 `Revenue (first time orders)(B)` 지표별 `Revenue metric (A)` 반환 형식을 로 설정 `Percent`, 첫 번째 주문의 결과로 발생할 수 있는 매출의 백분율을 확인할 수 있습니다.

### 예: 다음을 수행하고 을 제공하지 않을 때 주문당 평균 수익이 무엇인지 알고 싶습니다. `promo code`.

![공식 을 사용하여 프로모션 코드가 있거나 없는 주문당 평균 매출 찾기](../../assets/promo_code.gif)

이 예에서는 `Revenue` 및 `Number of orders` 지표. 이 질문에 대한 대답은 두 단계 - 나누기 를 포함합니다. `Revenue (A)` 작성자 `Number of orders (B)` 반환 형식을 로 설정 `Currency`. 그런 다음 공식 결과(`Avg. Revenue per order`) - 결과를 표시하고 그룹화합니다. `Promo code`.

### 예: 새 고객의 UTM 소스 분포를 알고 싶습니다.

![공식을 사용하여 새 고객의 UTM 소스 분포 찾기](../../assets/distro.gif)

이 질문에 대한 답을 찾는 데는 다음 몇 가지 단계가 포함됩니다.

1. 먼저 을(를) 추가했습니다. `New Customers` 지표, 그룹화 기준: `utm_source - all`. 지표 `A`, 또는 `New Customers (grouped)`.

1. 그런 다음 을 복제했습니다. `New Customers (grouped)` 지표를 만든 다음 독립 차원을 사용하도록 설정합니다. 지표 `B` - `New customers (ungrouped)` - 총 신규 고객 수를 표시합니다.

1. 두 지표를 모두 숨긴 후 공식 정의를 다음으로 설정합니다. `A/B`. 이렇게 하면 가 나누어집니다. `New customers (grouped)` 작성자 `New Customers (ungrouped)`.

1. 그런 다음 결과 형식을 다음으로 설정합니다. `Percent`.

이 예에서는 `Stacked Columns` 관점 을 사용하여 월별 결과를 표시할 수 있습니다. 이를 통해 신규 고객의 분포를 월별로 비교할 수 있다.

## 요약 {#wrapup}

위의 예에서 공식이 `timestamp`, `groupings`, `perspectives`, 및 `filters` 입력 지표에서 상속됩니까? 수식을 사용하여 `perspectives` 및 [독립 시간 옵션](../../tutorials/time-options-visual-rpt-bldr.md){: target=&quot;_blank&quot;}. 지표와 마찬가지로

에서 수식 사용에 대한 추가 질문이 있는 경우 `Report Builder`, [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
