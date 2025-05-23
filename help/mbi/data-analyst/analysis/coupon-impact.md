---
title: 쿠폰 영향 분석
description: 고객 확보 및 유지에 대한 쿠폰 영향을 분석하는 방법에 대해 알아봅니다.
exl-id: b0619365-fa75-49b5-a393-87f3364a390f
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 1%

---

# 쿠폰 영향

고객이 쿠폰을 사용하는 방법을 분석하면 비즈니스에 대한 중요한 통찰력을 제공할 수 있습니다. 특히, 쿠폰을 통해 고객을 획득하고 유지하는 방법을 분석합니다. 이 주제에서는 다음 유형의 질문에 답변하는 데 도움이 되는 분석을 살펴봅니다.

* 쿠폰으로 얼마나 많은 고객을 확보하나요?
* 쿠폰을 획득한 고객이 쿠폰을 통해 획득하지 않은 고객보다 반복 구매를 할 가능성이 높은가?
* 쿠폰을 통해 획득한 고객과 쿠폰을 통해 획득하지 않은 고객 간 평균 라이프타임 수익은 어떻게 다릅니까?
* 쿠폰으로 취득한 고객은 쿠폰으로 반복 구매하나요?

[쿠폰을 획득한 고객과 쿠폰을 획득하지 않은 고객 비교](#compare), [쿠폰 획득에서 1차 주문 세부 사항 분석](#firstorder) 및 [쿠폰을 첫 번째 주문에서 사용하는 고객의 특성을 살펴보는 것에 초점을 맞추어 이 질문에 답변하십시오.](#attributes)

시작합니다!

## 쿠폰 획득 고객과 비쿠폰 획득 고객 비교 {#compare}

쿠폰 획득 및 유지를 탐색하는 분석을 작성할 때 다음 지표 사용을 고려하십시오.

### 신규 고객 수

이 지표는 전체 기간 동안 쿠폰을 획득한 고객 및 쿠폰을 획득하지 않은 고객의 수를 보여줍니다. 쿠폰을 통해 고객 확보 비율을 결정하는 데 도움이 될 수 있습니다.

### 평균 라이프타임 수익

이 지표는 쿠폰 및 비쿠폰 획득 고객의 평균 라이프타임 수익을 보여줍니다. 이를 통해 고객의 라이프타임 값이 고객 확보 유형에 따라 달라지는지 확인할 수 있습니다.

### 반복 주문 수

이 지표는 두 유형의 고객 확보 활동에서 수행한 반복 주문 수를 보여 줍니다. 쿠폰을 획득한 고객 또는 쿠폰을 획득하지 않은 고객이 추가 주문을 했는지 확인하는 데 도움이 될 수 있습니다.

### 쿠폰이 포함된 반복 주문 수 및 비율

쿠폰이 적용된 반복 주문 수 및 쿠폰이 적용된 반복 주문 비율을 보여 줍니다. 이렇게 하면 쿠폰 획득 고객이 비쿠폰 획득 고객보다 쿠폰으로 반복 주문을 하는 경향이 있는지, 쿠폰 획득 고객이 후속 주문에 쿠폰을 불균형적으로 사용하는지 확인하는 데 도움이 될 수 있습니다.

쿠폰 획득과 비쿠폰 획득 지표에 대한 몇 가지 샘플 데이터를 살펴보십시오.

| **고객 확보** | **신규 고객 수** | **평균 라이프타임 수익** | **반복 주문 수** | **쿠폰이 포함된 반복 주문 수** | 쿠폰이 포함된 반복 주문의 **%** |
|-----|-----|-----|-----|-----|-----|
| 쿠폰 | 1,206 | US$356.91 | 2,570 | 1,248 | 48.56% |
| 비쿠폰 | 11,561 | US$498.30 | 20,145 | 3,251 | 16.14% |

{style="table-layout:auto"}

여기에서 무엇을 제거할 수 있는지 살펴보십시오.

### 신규 고객 수

위의 예에서, 쿠폰 취득보다 비쿠폰 취득의 수가 훨씬 많다. 그러나 여전히 1,206명의 고객이 쿠폰을 통해 구매했으며, 그렇지 않을 경우 고객이 되지 않았을 수 있습니다.

### 평균 라이프타임 수익

이 예에서, 비쿠폰 획득은 쿠폰 획득보다 더 높은 평균 라이프타임 수익을 갖는다. 이는 비-쿠폰 취득이 더 많은 반복 구매를 행하고 및/또는 더 높은 가치의 구매를 행하고 있음을 암시한다.

### 반복 주문 수

비쿠폰 취득에 대한 반복 주문 건수가 쿠폰 취득보다 훨씬 많다. 비쿠폰 획득 고객이 더 많기 때문에 기대되는 부분이다.

### 쿠폰이 포함된 반복 주문 수

이와 유사하게, 쿠폰으로 이루어진 반복 주문 수는 비-쿠폰 취득에 대해 더 높다.

## 쿠폰이 포함된 반복 주문 비율

쿠폰이 적용되지 않은 비쿠폰 획득 고객은 쿠폰 획득 고객에 비해 쿠폰이 적용된 반복 주문 비율이 훨씬 낮다. 따라서 쿠폰 획득 고객의 경우 반복 주문의 거의 절반이 쿠폰을 적용하고 있다. 이 예에서 쿠폰 획득 고객은 쿠폰으로 반복 구매를 하는 경향이 있습니다.

## 쿠폰 획득의 첫 번째 주문 세부 사항 분석 {#firstorder}

이 섹션에서는 쿠폰별로 분류된 쿠폰 획득의 **첫 번째 주문에만 중점을 둡니다.** 분석에 다음 지표를 사용합니다.

### 주문/고객 수

이 지표는 각 쿠폰에 대한 첫 번째 주문 수 또는 첫 번째 주문에서 해당 쿠폰을 사용한 고객 수를 보여 줍니다. 이렇게 하면 특정 쿠폰이 다른 쿠폰보다 더 많은 최초 구매를 유도하는지 확인하는 데 도움이 될 수 있습니다.

### 총 수익

이 지표는 고객의 첫 번째 주문에 사용된 특정 쿠폰에서 얻은 매출을 보여줍니다. 이 수익은 할인이 적용되기 전에 판매된 품목을 계산한 것입니다.

### 쿠폰 할인

이 지표는 쿠폰에서 적용되는 총 할인 금액을 보여 줍니다.

### 순 수익

이 지표는 고객의 첫 번째 주문에 사용된 특정 쿠폰에서 얻은 매출을 보여줍니다. 이 수익은 모든 할인이 적용된 후 판매된 품목을 계산한 것이다. 쿠폰 없이는 순수익이 발생하지 않았을 수 있다는 점을 유의해야 한다.

### 평균 주문 가격

이 지표는 특정 쿠폰에 대한 평균 주문 값을 보여 줍니다.

### 평균 라이프타임 주문 수

이 지표는 특정 쿠폰을 사용하는 고객이 생성한 충성도 및 평균 주문 수를 평가하는 데 도움이 됩니다.

### 평균 라이프타임 수익

이 지표는 특정 쿠폰을 사용하는 고객이 생성한 충성도 및 평균 매출을 평가하는 데 도움이 됩니다. 쿠폰을 사용하는 고객이 다른 고객보다 가치가 높은지 평가할 때는 각 쿠폰이 사용된 주문 수를 파악하여 샘플 크기가 유의한지 확인해야 합니다.

이제 고객의 최초 주문에 사용되는 세 가지 다른 쿠폰과 관련된 예를 살펴보겠습니다.

| **쿠폰** | **처음 주문(FTO)** | **FTO의 총 수익** | **FTO에 적용되는 할인** | **FTO의 순 수익** | **FTO의 평균 순서 값** |
|-----|-----|-----|-----|-----|-----|
| $100 이상 **25% 할인** | 56 | US$8,531.04 | US$2,132.76 | US$6,398.28 | US$152.34 |
| **$10 떨어짐** | 87 | US$3,707.07 | US$426.10 | US$3,280.97 | US$42.61 |
| **20% 할인** | 145 | US$10,975.05 | US$2,195.01 | US$8,780.04 | US$75.69 |

{style="table-layout:auto"}

이것으로부터 무엇을 얻을 수 있습니까? 먼저 &#39;20% 할인&#39; 쿠폰이 첫 주문 건수가 가장 많았다. 그러나 각 쿠폰과 연관된 주문 수는 다음을 포함한 여러 요인에 따라 달라질 수 있습니다.

* 각 쿠폰에 대한 광고 금액.
* 쿠폰이 제공된 기간.
* 쿠폰이 제공된 시간(일/주/월/년).
* 비즈니스에 따라 쿠폰이 제공되는 시즌.

  **예:** 여름 기간 동안 &quot;20% 할인&quot; 쿠폰이 제공되었지만 업체에서 겨울 의류를 판매합니다.
* 쿠폰에 대한 제한.

  **예:** &quot;10% 할인&quot; 쿠폰은 같은 순서로 겨울 코트를 구입하는 고객에게만 제공됩니다.

&quot;100달러 이상 대비 25% 할인&quot; 쿠폰에 대한 **총 수익**&#x200B;이 &quot;$10 할인&quot; 쿠폰에 대한 총 수익보다 훨씬 높습니다. 그러나 &quot;$10 할인&quot; 쿠폰은 **주문 수**&#x200B;가 훨씬 큽니다. **평균 주문 값**&#x200B;을 분석하면 이러한 차이점에 대한 통찰력을 얻을 수 있습니다. &#39;25% 할인 100달러 이상&#39; 쿠폰은 주문 건수가 적었음에도 평균 주문 가치는 &#39;10달러 할인&#39; 쿠폰보다 3배 이상 높다. 따라서, 더 큰 총 수익은 &quot;100달러 이상을 25% 할인&quot; 쿠폰에 귀속됩니다.

&quot;100달러 이상 대비 25% 할인&quot; 및 &quot;20% 할인&quot; 쿠폰에 대한 **할인** 및 **순 수익**&#x200B;이 근접한 값입니다. &#39;100달러 이상 대비 25% 할인&#39; 평균 주문 가격이 &#39;20% 할인&#39; 평균 주문 가격의 2배에 육박하는데도, 후자 쿠폰은 주문 건수의 3배에 조금 못 미친다.

## 첫 번째 순서로 쿠폰을 사용하는 고객의 속성 {#attributes}

이제 주문 항목을 직접 살펴보았으므로, 첫 번째 주문에서 쿠폰을 사용하는 고객을 살펴보십시오.

| **고객의 첫 번째 주문 쿠폰** | **고객 수** | **평균 수명 주문 수** | **평균 라이프타임 수익** |
|-----|-----|-----|-----|
| $100 이상 **25% 할인** | 56 | 2.8 | US$554.54 |
| **$10 떨어짐** | 87 | 1.9 | US$115.50 |
| **20% 할인** | 145 | 1.3 | US$103.75 |

{style="table-layout:auto"}

처음 주문하는 건수와 쿠폰별 고객수가 동일합니다. 고객마다 1차 주문을 하나만 할 수 있기 때문에 이는 일리가 있다.

&#39;20% 할인&#39; 쿠폰을 통해 가장 많은 고객을 획득했다. 그러나 이러한 고객의 주문 수가 **평균 수명**&#x200B;과(와) **평균 수명 수익**&#x200B;이(가) 가장 낮습니다. 일반적으로 대부분의 쿠폰 획득 고객은 반복 주문을 하지 않습니다. 또한 &quot;100달러 이상 할인율 25%&quot; 쿠폰을 통해 획득한 고객은 **평균 수명 주문 수**&#x200B;를 높이며, **평균 수명 매출**&#x200B;을 높입니다. 일반적으로 이 쿠폰을 통해 획득한 이용자는 다시 와서 더 많이 반복 구매한다.

## 요약 {#wrapup}

고객이 쿠폰을 사용하는 방법을 더 잘 이해하기 위해 생성할 수 있는 다양한 분석이 있습니다. 고객이 쿠폰을 어떻게 사용하는지 또는 쿠폰을 사용하는 데 걸리는 시간을 분석하는 것에 대해 생각해 본 적이 있습니까? 최적의 할인 금액을 찾는 것은 어떻습니까? 어떤 금액이 반복 구매자를 격려하고, 더 높은 평균 주문 가격을 제공하며, 더 높은 생애 수익을 얻습니까? 이러한 유형의 질문에 대한 도움말을 보려면 [지원팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ko)하세요.
