---
title: 반복 주문 가능성 보고서
description: 반복 주문 가능성 보고서를 학습하고 이해합니다.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# 반복 주문 가능성 보고서

## 은 언제입니까 `Incremental Event Probability` 원근감?

다음 `incremental event probability` 원근법은 필터가 모든 주문(예: 사용자의 `gender`, 사용자의 `age` 또는 사용자 `source`)

이 관점은 `User's order number` 사용자의 구매 내역(예: John의 첫 번째, 두 번째 및 세 번째 주문)을 나타내는 세그먼테이션입니다.

모든 주문에 대해 같지 않은 차원을 사용하는 필터를 추가하는 경우(예: `Order's Region`), `User's order number` 사용자의 주문에 대해 번호 매기기를 수행할 때 특정 지역에 대해 설명하지 않으므로 차원이 더 이상 정확하지 않습니다(예: John의 첫 번째, 두 번째, 세 번째 주문은 해당 지역에 관계없이 여전히 동일합니다.).

## 주문별 차원을 사용자별 차원으로 전환

어떤 경우에는 `order-specific` 차원을 `user-specific` 필터로 추가할 차원 `Repeat Order Probability` 차트. 이러한 경우 사용자의 첫 번째 주문 또는 최신 주문(예: 사용자의 첫 번째 주문 지역 이름)의 주문 속성을 반환합니다.

이러한 새 차원을 만들려면, [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## 주문의 반복 확률과 다른 속성 비교

다른 주문 속성에 대한 반복 구매 수를 비교하려면(예: 주문 `region`), 와 유사한 차트를 만드는 것이 좋습니다 `Users by lifetime number of orders` 주문 수를 1, 2, 3,.. 라이프타임 수로 만들고 주문 수준 필터를 추가한 사용자 수를 보여줍니다. (즉, 사용자가 한 지역 또는 다른 지역에서 반복 구매를 하는지 여부를 표시할 수 있습니다.)

이러한 차트를 구성하는 숫자를 excel로 내보내 반복 주문 확률 비율을 계산할 수 있습니다. 고객 확률을 확인하려고 `(x)` 주문 `(x+1)` 주문, 간단히` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` 구매.

### 예:

|  |  |
|---|---|
| 라이프타임 동안 1회 구입한 고객 수 | `90` |
| 평생 2개를 구입한 고객 수 | `30` |
| 평생 3번 구입한 고객 수 | `10` |
| 두 번째 구매를 위해 생애 동안 한 번 구매한 고객의 반복 주문 가능성 | `(30 + 10) / (30+10+90) = 30.77%` |
