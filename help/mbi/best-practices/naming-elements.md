---
title: Commerce Intelligence에서 보고서 및 요소 이름 지정
description: ' [!DNL Commerce Intelligence]에서 보고서 및 요소의 이름을 지정하는 모범 사례에 대해 알아봅니다.'
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
role: Admin, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# 보고서 및 요소 이름 지정

[!DNL Adobe Commerce Intelligence]에서 빌드를 시작하기 전에 Adobe이 성공에 대한 몇 가지 비밀을 공유하려고 합니다. 지표, 필터 등을 만드는 방법을 아는 것은 중요하지만, 필요한 것을 찾을 수 없거나 모호한 경우 모든 작업이 무용지물이 될 수 있습니다.

## 명명법이 중요한 이유 {#why}

계산된 열, 지표 및 보고서의 이름을 지정하는 방식은 다른 사용자가 [!DNL Commerce Intelligence] 계정을 쉽게 탐색할 수 있음을 나타냅니다. 이러한 기능의 이름을 지정할 때는 세 가지 C에 유의하십시오.

* **명확성** - 보고서에 표시되는 내용, 지표가 수행하는 작업 등을 한눈에 파악할 수 있습니다.
* **일관성** - 사용자(및 Adobe 지원 팀)가 계정의 요소 및 보고서를 쉽게 찾고 이해할 수 있도록 합니다.
* **신뢰도** - 다른 데이터 기반 [!DNL Commerce Intelligence] 사용자에게 영감을 주고 권한을 부여하려면 해당 사용자가 데이터를 이해하고 사용하는 방법에 대한 자신감을 심어주어야 합니다!

시도되고 진정한 명명법 팁을 계속 읽어보십시오!

## 일반 모범 사례 {#general}

### 의미 있게 되기 {#meaningful}

가능하면 항상 구체적으로 나타내십시오! 예를 들어 해당 국가라면 배송 국가인지 결제 국가인지 알 수 있습니까? 사용자의 도시입니까, 아니면 거래의 도시입니까?

**잘못된 예:**
매출

이것은 애매하고 우리에게 많은 것을 말해주지 않는다.

**좋은 예:**
매출(기본 총계 + 수수료)
사용자의 배송 국가

이러한 예는 구체적이며, 이는 혼동 가능성을 감소시킨다.

### 대문자 사용 {#capitalize}

[!DNL Adobe]은(는) 적절한 명사 스타일의 대소문자가 아닌 경우 첫 글자 대문자를 나머지 문자와 소문자로 바꿀 것을 권장합니다. 예를 들어 **사용자 주문 번호가 아닌**&#x200B;사용자 주문 번호&#x200B;**입니다.**

이것은 정말로 선호도의 문제이지만, 기억해야 할 것은 당신이 무엇을 선택하든 일관되는 것이다.

### 엔티티 일관성 {#entity}

이미 회사에 명명법이 있을 수 있습니다. 배치한 지표 및 차원을 다른 데이터베이스 및 도구에서 사용되는 것과 일관되게 유지합니다. For example:

* 사용자 대 고객 대 멤버 대 계정
* 회사 대 계정 대 조직
* 등록과 작성 비교

### 맞춤법 및 문법 {#spelling}

철자를 다시 한 번 확인하고 성가신 점유율을 잊지 마세요!

## 차트 {#charts}

[차트](../tutorials/using-visual-report-builder.md)의 이름을 지정할 때 다음 수식을 따르는 것이 좋습니다. **(데이터 관점) + (지표) + (기간) + (시간 간격)**

**잘못된 예:**
매출

이것은 우리에게 그 보고서에 대해 아무 것도 말해주지 않는데, 그것은 나쁘다.

**좋은 예:**
월별 30일 경과 누적 수익

이는 보고서에 있는 내용을 **정확하게**&#x200B;하여 알려줍니다. 환상적입니다.

## 대시보드 {#dashboards}

대시보드의 이름은 대시보드 내에 포함된 보고서를 체계적으로 나타내는 방식으로 지정해야 합니다. 예를 들어 대시보드에 매출 및 주문과 관련된 정보만 포함되어 있는 경우 이름을 **스토어 이름 - 매출 및 주문**&#x200B;과 같이 지정할 수 있습니다.

반대로, 대시보드가 서로 다른 보고서를 실험하는 곳이라면 이름을 **내 이름의 샌드박스**&#x200B;로 지정하여 해당 보고서에 포함된 보고서가 초안임을 알 수 있도록 하십시오.

## Dimension(계산된 열) {#dimensions}

새 [차원](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)의 이름을 지정할 때 다음 공식을 따르는 것이 가장 유용합니다. **(엔티티) + (N번째) + (시간대) + (계산) + (댓글)**. For example:

사용자의 첫 30일 매출
* 사용자 주문 번호
* 사용자 주문 번호(감사 대기 중)

## 필터 세트 {#filterset}

[필터 집합](../data-user/reports/ess-manage-data-filters.md)은(는) 일반적으로 포함 또는 제외하는 정보를 설명하는 방식으로 이름이 지정됩니다. 예를 들어, 필터 집합 **주문 항목**&#x200B;의 이름을 지정하면 모든 사용자가 들어갈 수 있고, 필터 집합의 논리를 볼 수 있으며, 비즈니스 전반에 걸쳐 계산되는 항목을 결정하는 주문 정보를 이해할 수 있습니다. 필터 세트는 계산된 열과 지표 모두에 적용할 수 있으며 쉽게 이해할 수 있어야 합니다.

## 지표 {#metrics}

[지표](../data-user/reports/ess-manage-data-metrics.md)은(는) 기본적으로 정기적으로 답변을 얻고자 하는 질문입니다. 지난 한 달 동안 주문 건수는 몇 건이었습니까? 고객의 평균 라이프타임 값은 얼마입니까? 사용자에게 제공하는 답변을 반영하도록 지표의 이름을 지정하는 것이 좋습니다. 또한 특정 스토어 또는 부서에 대해 동일한 지표를 필터링한 경우 이러한 지표에는 동일한 지표라는 레이블이 지정되어야 합니다. For example:

평균 고객 LTV(처음 30일)
저장소 이름 - 수익

마지막으로, 개별 사용자가 지표를 계산하는 방식에 따라 동일한 지표를 다른 타임스탬프로 구성할 수도 있습니다. 그럴 경우 이름에 타임스탬프를 포함해야 합니다.

매출(배송됨\_at)
수익(created\_at)

## 요약 {#wrapup}

스타일 및 명명 규칙을 초기에 설정하면 [!DNL Commerce Intelligence] 계정에서 성공을 설정할 수 있습니다. 명확성, 일관성 및 신뢰성 세 가지 C를 기억하십시오.
