---
title: 첫 구매까지의 평균 시간 보고서
description: 평균 최초 구매 시간 보고서를 사용하는 방법을 알아봅니다.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 330832e2668024b00edb2b7c49b92bb042bd004a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# 첫 구매까지의 평균 시간 보고서

많은 Adobe 고객에게는 사용자 그룹의 등록 날짜와 첫 번째 구매 날짜 사이의 평균 시간을 보여 주는 `Average time to first purchase`(이)라는 지표와 차트가 있습니다. 데이터는 시간이 현재에 더 가까워짐에 따라 거의 변함없이 아래로 기울어진다.

![첫 번째 주문까지의 평균 시간](../../assets/average-time-to-first-order.png)

이는 이러한 신규 고객이 아직 가입일로부터 1개월 이상 경과한 구매를 생성할 수 있는 기회를 갖지 못했기 때문입니다. 구매한 적이 없는 사용자는 전혀 포함되지 않기 때문에(구매할 때까지), 이는 새로운 고객 그룹의 평균을 편향시킵니다.

이 지표를 보는 몇 가지 다른 잠재적 방법이 있는데, 이러한 방법은 더 적은 편향을 초래한다. 한 가지 예를 살펴보십시오.

## 예: 첫 번째 주문에 대한 `cohort` 분석 수행

`Users` 대시보드에 이름이 `Time to first order cohort`인 차트가 있을 수 있습니다. 이 보고서는 `Distinct buyers` 지표를 사용하고, 등록 후 `cohort`주 또는 개월별로 사용자를 그룹화하고, 등록 후 다음 주 또는 개월 내에 첫 번째 구매한 사용자의 비율(`0`에서 `1` 사이)을 표시합니다.

이 차트는 2014년 12월에 등록한 사용자의 경우 `0.56`(또는 `56%`)이(가) 2개월까지(예: 2015년 1월) 첫 번째 주문을 했음을 보여 줄 수 있습니다.

이러한 코호트 분석은 시간에 따른 사용자 활성화율을 나타내는 좋은 지표이다. 이 차트가 평평해지거나 안정되기 시작하고 구매자에게 여전히 100% 전환하지 않는 경우 이메일 캠페인을 통해 나머지 사용자를 활성화해야 할 시기일 수 있습니다.
