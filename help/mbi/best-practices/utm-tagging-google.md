---
title: Google Analytics의 UTM 추적
description: Google Analytics의 UTM 추적(태깅)에 대한 모범 사례에 대해 알아봅니다.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# UTM 추적

`UTM` 추적은 사용자의 출처를 분석할 수 있도록 하는 URL에 대한 태그 지정 규칙입니다. 대부분의 마케팅 이메일 또는 배너 광고에서 클릭하는 URL을 보면 UTM 태깅이 표시됩니다. `utm\_source` 및 `utm\_medium`(으)로 끝나는 긴 링크입니다.

[!DNL Google Analytics]은(는) `UTM` 태깅을 사용하여 트래픽이 발생하는 위치를 파악합니다. 이 정보 중 일부는 [HTTP 레퍼러](https://en.wikipedia.org/wiki/HTTP_referer)에서 가져오지만 나머지 정보는 `UTM` 매개 변수를 제공해야 합니다. `google adwords` 또는 `email marketing`이(가) 표시되면 해당 `UTM` 매개 변수가 원래 링크 클릭에서 기록된 다음 사용자의 쿠키에 저장됨을 의미합니다. 여기에서 [!DNL Google Analytics]은(는) 해당 데이터를 사이트의 [관심 있는 동작 특성](../data-analyst/analysis/google-track-user-acq.md)에 사용합니다. 이러한 매개 변수가 무엇에 사용되는지 이해하면 UTM 태깅을 가장 잘 설정하고 사용하는 방법을 이해하는 데 도움이 됩니다.

## UTM 태그 지정에 대한 우수 사례

다음은 `UTM` 태깅으로 URL을 설정할 때 기억해야 할 5가지 가장 중요한 사항 목록입니다.

### &#x200B;1. 사이트에 도달하기 위해 제어할 수 있는 모든 URL에 태그를 지정합니다

사람들에게 링크를 클릭하도록 요청할 때마다 `UTM` 태그 지정을 설정해야 합니다. 여기에는 모든 이메일 링크(이메일 서비스 공급업체에서 URL에 자동으로 태그를 지정하는 방법이 있을 수 있음), 광고 링크, 보도 기사, 블로그 게시물이 포함됩니다.

### &#x200B;2. 도구를 사용하여 URL 만들기

`UTM`개의 태그가 지정된 URL은 번거로울 수 있습니다. 더 오래 입력하지 말고 [이와 같은 ](https://support.google.com/analytics/answer/1033867?hl=en) 도구를 사용하여 도움을 받으십시오. 이렇게 하면 모든 감지 가능한 매개 변수를 URL에 추가하여 생각하고 있으며, URL을 바로 복사하여 붙여넣을 수 있습니다. 소셜 링크를 관리하기 위해 [!DNL Hootsuite]과(와) 같은 도구에 모든 링크에 사용자 지정 URL 매개 변수를 추가하는 옵션이 포함되어 있습니다.

### &#x200B;3. 매개변수 값에서 대소문자를 구분하는지 확인합니다

`utm\_source=adwords` 태그는 `utm\_source=Adwords`과(와) 다른 태그입니다. 모든 항목을 소문자로 만드는 것을 고려하십시오.

### &#x200B;4. 데이터베이스에 UTM 매개변수 값 저장

거래 또는 이벤트가 발생할 때마다 마케팅 활동의 성과를 평가해야 합니다. 이렇게 하려면 [[!DNL Google Analytics] 쿠키에서 데이터베이스로](../data-analyst/analysis/google-track-user-acq.md)의 UTM 매개 변수 값을 읽습니다.

### &#x200B;5. 캠페인 이름을 지정하는 방법 고려

시간이 지남에 따라 마케팅 노력이 어떻게 개선되고 있는지 추적하려면 이름 지정 규칙에 대해 현명해야 합니다. 단순하게 유지하고 가능한 한 최소화하십시오. 복잡한 명칭 체계를 유지하기가 더 어렵다.

데이터베이스에서 이 데이터를 캡처하고 나면 [고객 생애 가치](../data-analyst/analysis/ess-expected-ltv.md), [반복 구매율](../data-analyst/analysis/repurchase-behavior.md), [평균 주문 가격](../data-analyst/analysis/basic-analytics.md)을 포함하여 보다 정교한 분석을 통해 마케팅 및 광고의 성과를 평가할 수 있습니다.
