---
title: Google Analytics의 UTM 추적
description: Google Analytics의 UTM 추적(태깅)에 대한 모범 사례에 대해 알아봅니다.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
source-git-commit: 8d4e71363edad0613cc0ab277c2a43aad000965e
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# UTM 추적

`UTM` 추적은 사용자의 출처를 분석할 수 있도록 하는 URL에 대한 태그 지정 규칙입니다. 대부분의 마케팅 이메일 또는 배너 광고에서 클릭하는 URL을 보면 UTM 태깅이 표시됩니다. 다음과 같은 것으로 끝나는 긴 링크입니다. `utm\_source` 및 `utm\_medium`.

[!DNL Google Analytics] 사용 `UTM` 트래픽 출처 파악을 위한 태깅 이 정보 중 일부는 [HTTP 레퍼러](https://en.wikipedia.org/wiki/HTTP_referer) 하지만 나머지 부분은 당신이 공급해야 합니다 `UTM` 매개 변수. 다음을 참조: `google adwords` 또는 `email marketing`즉, `UTM` 원래 링크에서 기록되는 매개 변수는 을 클릭한 다음 사용자의 쿠키에 저장됩니다. 거기서부터 [!DNL Google Analytics] 는 해당 데이터를 다음에 사용 [관심 있는 동작 특성](../data-analyst/analysis/google-track-user-acq.md) 을 클릭합니다. 이러한 매개 변수가 무엇에 사용되는지 이해하면 UTM 태깅을 가장 잘 설정하고 사용하는 방법을 이해하는 데 도움이 됩니다.

## UTM 태그 지정에 대한 우수 사례

다음은으로 URL을 설정할 때 기억해야 할 5가지 가장 중요한 사항을 나열합니다 `UTM` 태그 지정.

### 1. 사이트에 도달하기 위해 제어할 수 있는 모든 URL에 태그를 지정합니다

사람들에게 링크를 클릭하도록 요청할 때마다 다음을 설정해야 합니다. `UTM` 태그 지정. 여기에는 모든 이메일 링크(이메일 서비스 공급업체에서 URL에 자동으로 태그를 지정하는 방법이 있을 수 있음), 광고 링크, 보도 기사, 블로그 게시물이 포함됩니다.

### 2. 도구를 사용하여 URL 만들기

`UTM`태그 지정된 URL은 번거로울 수 있습니다. 긴 입력 대신 도구를 사용하십시오. [좋아요](https://support.google.com/analytics/answer/1033867?hl=en) 도와주려고. 이렇게 하면 모든 감지 가능한 매개 변수를 URL에 추가하여 생각하고 있으며, URL을 바로 복사하여 붙여넣을 수 있습니다. 소셜 링크를 관리하려면 다음과 같은 도구를 사용하십시오 [!DNL Hootsuite] 모든 링크에 사용자 지정 URL 매개 변수를 추가하는 옵션을 포함합니다.

### 3. 매개변수 값에서 대소문자를 구분하는지 확인합니다

태그는 반드시 기억해야 합니다 `utm\_source=adwords` 은(는) 와(과) 다른 태그입니다. `utm\_source=Adwords`. 모든 항목을 소문자로 만드는 것을 고려하십시오.

### 4. 데이터베이스에 UTM 매개변수 값 저장

거래 또는 이벤트가 발생할 때마다 마케팅 활동의 성과를 평가해야 합니다. 이렇게 하려면 다음에서 UTM 매개 변수 값의 값을 읽습니다. [[!DNL Google Analytics] 데이터베이스에 쿠키 삽입](../data-analyst/analysis/google-track-user-acq.md).

### 5. 캠페인 이름을 지정하는 방법 고려

시간이 지남에 따라 마케팅 노력이 어떻게 개선되고 있는지 추적하려면 이름 지정 규칙에 대해 현명해야 합니다. 단순하게 유지하고 가능한 한 최소화하십시오. 복잡한 명칭 체계를 유지하기가 더 어렵다.

데이터베이스에서 이 데이터를 캡처하고 나면 다음을 포함한 보다 정교한 분석을 통해 마케팅 및 광고의 성과를 평가할 수 있습니다. [고객 생애 가치](../data-analyst/analysis/ess-expected-ltv.md), [반복 구매율](../data-analyst/analysis/repurchase-behavior.md), 및 [평균 주문 가격](../data-analyst/analysis/basic-analytics.md).
