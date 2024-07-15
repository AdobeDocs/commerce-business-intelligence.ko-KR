---
title: 반복 주문 확률 보고서
description: 반복 주문 확률 보고서를 학습하고 이해합니다.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# 반복 주문 확률 보고서

## `Incremental Event Probability` 관점은 언제 사용할 수 있습니까?

`incremental event probability` 관점은 필터가 모든 주문에 대해 동일한 차원(예: 사용자의 `gender`, 사용자의 `age` 또는 사용자의 `source`)을 사용하는 경우에만 사용할 수 있습니다.

이는 이 관점이 사용자의 구매(예: John의 첫 번째, 두 번째 및 세 번째 주문)에 번호를 매기는 세그먼테이션을 위해 `User's order number`이라는 차원에 의존하기 때문입니다.

모든 주문에 대해 같지 않은 차원을 사용하는 필터를 추가한 경우(예: `Order's Region`), `User's order number` 차원이 더 이상 정확하지 않습니다. 이는 사용자의 주문에 번호를 매길 때 특정 지역을 고려하지 않기 때문입니다(예: John의 첫 번째, 두 번째, 세 번째 주문은 지역에 상관없이 동일함).

## 주문별 차원을 사용자별 차원으로 변환

경우에 따라 `order-specific` 차원을 `user-specific` 차원으로 전환하여 `Repeat Order Probability` 차트에서 필터로 추가할 수 있습니다. 이러한 경우 사용자의 1차 주문 또는 최근 주문의 주문 속성(예: 사용자의 1차 지역 이름)을 반환합니다.

이러한 새 차원을 만들려면 [지원팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)하십시오.

## 다른 속성을 가진 주문 반복 확률 비교

Adobe 다른 주문 특성(예: 주문의 `region`)에 대한 반복 구매 수를 비교하려면 `Users by lifetime number of orders`과(와) 유사한 차트를 만드는 것이 좋습니다. 이는 1, 2, 3,... 라이프타임 주문 수를 생성한 사용자 수를 보여주고 주문 레벨 필터를 추가합니다. (즉, 사용자가 한 지역에서 반복 구매할지 또는 다른 지역에서 반복 구매할지 여부를 보여 줄 수 있습니다.)

그런 다음 이러한 차트를 구성하는 숫자를 Excel로 내보내 반복 순서 확률비를 계산할 수 있습니다. 고객이 `(x)`개 주문하여 `(x+1)`개 주문을 했을 확률을 보려면 간단히 ` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)`개를 구매하십시오.

### 예:

| 범주 | 값 |
|---|---|
| 라이프타임 동안 1회 구입한 고객 수 | `90` |
| 일생 동안 2회 구입한 고객 수 | `30` |
| 일생 동안 3회 구입한 고객 수 | `10` |
| 일생 동안 한 번 구매한 고객이 두 번째 구매를 할 반복 주문 확률 | `(30 + 10) / (30+10+90) = 30.77%` |
