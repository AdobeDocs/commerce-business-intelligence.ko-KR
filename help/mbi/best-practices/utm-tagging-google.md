---
title: Google Analytics의 UTM 추적
description: Google Analytics의 UTM 추적(태그 지정)에 대한 우수 사례에 대해 배웁니다.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# UTM 추적

`UTM` 추적은 사용자가 어디에서 오는지 분석할 수 있도록 해주는 URL에 대한 태그 지정 규칙입니다. 대부분의 마케팅 이메일 또는 배너 광고에서 클릭한 URL을 보면 UTM 태깅이 표시됩니다. 이런 것들로 끝나는 긴 링크입니다 `utm\_source` 및 `utm\_medium`.

[!DNL Google Analytics] 사용 `UTM` 태깅하여 트래픽이 발생하는 위치를 파악합니다. 이 정보 중 일부는 [HTTP 레퍼러](https://en.wikipedia.org/wiki/HTTP_referer) 하지만 그 나머지 부분은 스스로 공급해야 합니다 `UTM` 매개 변수. 다음에 `google adwords` 또는 `email marketing` 그것은 `UTM` 원래 링크에서 기록되는 매개 변수를 클릭한 다음 사용자의 쿠키에 저장합니다. 거기서 [!DNL Google Analytics] 해당 데이터를에 사용 [흥미로운 행동](../data-analyst/analysis/google-track-user-acq.md) 구현합니다. 이러한 매개 변수가 무엇인지 이해하면 UTM 태깅을 설정하고 사용하는 방법을 이해하는 데 도움이 됩니다.

## UTM 태깅 우수 사례

다음은 URL을 설정할 때 기억해야 할 5가지 가장 중요한 목록입니다 `UTM` 태깅합니다.

### 1. 사이트 방문에서 제어할 수 있는 모든 URL에 태그를 지정하는 것을 목표로 합니다

사람들에게 링크를 클릭하도록 요청할 때마다 `UTM` 태깅합니다. 여기에는 모든 이메일 링크(이메일 서비스 제공업체는 URL에 자동으로 태그를 지정할 수 있는 방법이 있을 수 있음), 광고 링크, 기사, 블로그 게시물이 포함됩니다.

### 2. 도구를 사용하여 URL을 만듭니다

`UTM`-태그가 지정된 URL은 꽤 번거로울 수 있습니다. 길게 입력하는 대신 도구를 사용하십시오 [좋아요](https://support.google.com/analytics/answer/1033867?hl=en) 널 돕기위해 이렇게 하면 URL에 모든 적절한 매개 변수를 추가하여 URL에서 바로 복사하여 붙여넣을 URL을 얻을 수 있습니다. 소셜 링크를 관리하려면 다음과 같은 도구를 사용하십시오 [!DNL Hootsuite] 모든 링크에 사용자 지정 URL 매개 변수를 추가하는 옵션을 포함합니다.

### 3. 매개 변수 값에서 대/소문자를 구분하는지 확인합니다

태그가 `utm\_source=adwords` 는 와(과) 다른 태그입니다 `utm\_source=Adwords`. 모든 것을 소문자로 만드는 것이 좋습니다.

### 4. UTM 매개 변수 값을 데이터베이스에 저장합니다

트랜잭션 또는 이벤트가 발생할 때마다 마케팅 활동의 성과를 평가하게 됩니다. UTM 매개변수 값의 값을 [[!DNL Google Analytics] 쿠키를 데이터베이스에 추가](../data-analyst/analysis/google-track-user-acq.md).

### 5. 캠페인의 이름을 지정하는 방법에 대해 생각해 보십시오

마케팅 활동이 시간이 지남에 따라 향상되는 방식을 추적하려면 이름 지정 규칙에 대해 똑똑해야 합니다. 간단하며 가능한 한 최소화하십시오. 복잡한 명명 시스템은 유지 관리하기가 어렵습니다.

데이터베이스에서 이 데이터를 캡처하면 다음을 포함한 보다 정교한 분석을 통해 마케팅 및 광고의 성과를 평가할 수 있습니다 [고객 생애 가치](../data-analyst/analysis/ess-expected-ltv.md), [구매 비율 반복](../data-analyst/analysis/repurchase-behavior.md), 및 [평균 주문 가격](../data-analyst/analysis/basic-analytics.md).
