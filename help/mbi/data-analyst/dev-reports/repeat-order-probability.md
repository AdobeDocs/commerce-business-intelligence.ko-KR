---
title: 반복 주문 확률 보고서
description: 반복 주문 확률 보고서를 학습하고 이해합니다.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 반복 주문 확률 보고서

## 은(는) 언제 입니까? `Incremental Event Probability` 관점을 사용할 수 있습니까?

다음 `incremental event probability` 관점은 필터가 모든 주문에 대해 동일한 차원을 사용하는 경우(예: `gender`, 사용자의 `age` 또는 사용자의 `source`).

이는 이 관점이 이라는 차원에 의존하기 때문입니다 `User's order number` 세그먼테이션의 경우, 사용자의 구매(예: John의 첫 번째, 두 번째 및 세 번째 주문)에 번호를 매깁니다.

모든 주문에 대해 같지 않은 차원을 사용하는 필터를 추가한 경우(예: `Order's Region`), `User's order number` 차원이 더 이상 정확하지 않습니다. 이는 사용자의 주문에 번호를 매길 때 특정 지역을 고려하지 않기 때문입니다(예: John의 첫 번째, 두 번째, 세 번째 주문은 지역에 상관없이 동일함).

## 주문별 차원을 사용자별 차원으로 변환

경우에 따라 다음을 실행할 수 있습니다. `order-specific` 차원 대상: `user-specific` 에서 필터로 추가할 차원 `Repeat Order Probability` 차트. 이러한 경우 사용자의 1차 주문 또는 최근 주문의 주문 속성(예: 사용자의 1차 지역 이름)을 반환합니다.

이러한 새 차원을 만들려면 [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## 다른 속성을 가진 주문 반복 확률 비교

다른 주문 속성(예: 주문)에 대한 반복 구매 수를 비교하려면 `region`), Adobe은 다음과 유사한 차트를 만들 것을 권장합니다. `Users by lifetime number of orders`. 이는 1, 2, 3,... 라이프타임 주문 수를 생성한 사용자 수를 보여주고 주문 레벨 필터를 추가합니다. (즉, 사용자가 한 지역에서 반복 구매할지 또는 다른 지역에서 반복 구매할지 여부를 보여 줄 수 있습니다.)

그런 다음 이러한 차트를 구성하는 숫자를 Excel로 내보내 반복 순서 확률비를 계산할 수 있습니다. 다음을 수행한 고객의 확률을 확인합니다. `(x)` 주문 제작 `(x+1)` 주문, 간단히` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` 구매.

### 예:

| 범주 | 값 |
|---|---|
| 라이프타임 동안 1회 구입한 고객 수 | `90` |
| 일생 동안 2회 구입한 고객 수 | `30` |
| 일생 동안 3회 구입한 고객 수 | `10` |
| 일생 동안 한 번 구매한 고객이 두 번째 구매를 할 반복 주문 확률 | `(30 + 10) / (30+10+90) = 30.77%` |
