---
title: Google Analytics 및 UTM 속성
description: Google Analytics 소스 속성 프로세스에 대해 알아봅니다.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Google Analytics 및 UTM 속성

이것은 [사용자 획득 소스 추적](../../data-analyst/analysis/google-track-user-acq.md) to [성과가 가장 좋은 광고 캠페인 식별](../../data-analyst/analysis/most-value-source-channel.md). 이 자습서에서는 Google Analytics 소스 속성 프로세스를 살펴봅니다. 즉, 어떤 정보가 언제 기록되는지 알 수 있다.

## 속성이란 무엇입니까?

`Attribution` 은 특정 활동의 참조 소스를 지정하는 것에 대한 것입니다. 이러한 활동은 일반적으로 매크로와 같은 매크로 전환 또는 마이크로 전환입니다 **구매**&#x200B;과 같은 **등록, 이메일 등록, 블로그 댓글,** 기타.

가장 좋은 방법은 전환 이벤트가 발생할 때마다 참조 소스가 기록됩니다. 그러나 그 출처를 어떻게 결정하는가?

실제로는 사용자가 마이크로 또는 매크로 전환을 실행/커밋하기 전에 많은 소스에서 온 경우가 많습니다(예: 유제품을 통해 사이트를 방문한 다음 유료 검색을 통해 방문한 다음 사이트를 직접 방문하고 나올 수 있음). 이 소스 추적 정보는 종종 UTM 매개 변수를 통해 사이트에 제공되지만, 더 복잡한 시스템도 있습니다. 우리는 목적을 위해 [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## 어떻게 [!DNL Google Analytics] UTM 매개 변수를 통해 속성 참조 소스를 제공하시겠습니까?

UTM 매개 변수가 URL에 지정되면 구문 분석되어 [!DNL Google Analytics] [쿠키](https://en.wikipedia.org/wiki/HTTP_cookie). 웹 사이트에 [!DNL Google Analytics]UTM을 사용할 필요가 없습니다. [!DNL Google Analytics] 은 라이프타임 동안(그 이상 버전) UTM을 사용하여 여러 URL을 히트하는 사용자를 처리하는 방법에 대한 규칙을 가지고 있습니다. 웹 사이트가 UTM 매개 변수를 외부 데이터베이스로 캡처하도록 구성되어 있다고 가정할 경우, 마이크로 또는 매크로 변환이 발생할 때마다 페이지에 있는 모든 것을 캡처할 수 있습니다 [!DNL Google Analytics] 전환 시 쿠키가 데이터베이스에 복제됩니다.

## 첫 번째 클릭과 마지막 클릭 비교

### 마지막 클릭 속성

마지막 클릭 속성은 [!DNL Google Analytics]. 이 경우 [!DNL Google Analytics] 쿠키는 전환 이벤트 전의 마지막 또는 가장 최근 소스에 대한 UTM 매개 변수를 나타내며 이것이 바로 [데이터베이스에 기록](../../data-analyst/analysis/google-track-user-acq.md). 다음 사항에 유의하십시오. [!DNL Google Analytics] 쿠키는 사용자가 새 UTM 매개 변수 세트가 포함된 새 URL을 클릭하는 경우에만 이전 UTM 매개 변수를 덮어씁니다.

예를 들어 를 통해 웹 사이트를 처음 방문하는 사용자를 고려합니다. [!DNL Google Analytics][!DNL Google Analytics][!DNL Google Analytics] *유료 검색*, 그런 다음 를 통해 반환 *유기 검색*, 그리고 마지막으로 다시 *웹 사이트 직접* 또는 *이메일 링크* **UTM 매개 변수 사용** 전환 이벤트 전. 이 예에서 [!DNL Google Analytics] 쿠키에는 전환 전의 마지막 소스를 나타내므로 사용자의 소스가 유기적이라고 표시됩니다. 다음 *경로* 최종 전환 이벤트 이전의 사용자 수는 무시됩니다. 대신 사용자가 UTM을 사용하는 이메일 링크에서 웹 사이트를 방문한 경우 [!DNL Google Analytics] 쿠키에는 소스가 &quot;이메일&quot;이라고 표시됩니다. 따라서 쿠키에 기존 UTM 매개 변수가 있고 사용자가 직접 를 통해 들어오는 경우, [!DNL Google Analytics] 쿠키는 항상 &quot;direct&quot;가 아닌 UTM 매개 변수를 표시합니다.

>[!NOTE]
>
>특정 사용자의 [!DNL Google Analytics] 쿠키 매개 변수는 쿠키 시 지워집니다 [만료](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)또는 사용자가 브라우저에서 쿠키를 지울 때)

### 첫 번째 클릭 속성

일부 유료 속성 도구를 사용하면 사용자 경로에 있는 소스의 &quot;팬케이크 스택&quot;을 캡처할 수 있습니다. 이 경우 위의 예에서 첫 번째 클릭 속성은 유료 검색을 알려줍니다. 또는, 소수의 웹 사이트에서는 팬케이크 스택을 캡처하고 첫 번째 소스를 데이터베이스에 저장하는 자체 쿠키를 구현합니다.

## 속성을 분석하는 방법

[!DNL Google Analytics] 에는 네 가지 다른 속성 모델을 수행할 수 있도록 해주는 몇 가지 강력한 웹 기능이 있습니다. 첫 번째 클릭, 마지막 클릭, 선형(경로의 모든 소스에서 동일하게 수익 나누기) 및 가중(사용자 지정된 속성)입니다.

이제 각 마이크로 또는 매크로 변환에 대한 속성 모델이 무엇인지 이해했으므로 질문은 사용자 전환의 합계로 무엇을 수행합니까?  예를 들어 GA 마지막 클릭 논리를 기반으로 기록된 UTM을 봅니다.

* 유기반에 사용자 등록
* 유료 검색 $5.00에서 사용자의 첫 번째 구매
* $50.00로 이메일을 통해 사용자의 두 번째 구매
* 유무기 $10.00로 사용자의 세 번째 구매

다음은 질문할 사항입니다. 유료 검색에서 얻은 수입은 얼마입니까?  이메일요?  유기물?  5, 50, 10(즉, 마지막 출처가 무엇이든지)이라고 말할 수도 있고, 혹은 모든 수입을 첫 번째 출처에 귀속한다고 말할 수도 있다(즉, 65개 모두 유기물로 간다). 일부 가중 분석을 적용하거나 선형 모델(즉, 각 22개)을 적용할 수도 있습니다.

## 관련 설명서

* [를 통해 주문 참조 소스 추적 [!DNL Google Analytics] 전자 상거래](../importing-data/integrations/google-ecommerce.md)
* [데이터베이스에서 사용자 참조 소스 추적](../analysis/google-track-user-acq.md)
* [데이터베이스에서 사용자 장치, 브라우저 및 OS 데이터 추적](../analysis/google-track-user-acq.md)
* [가장 가치 있는 획득 소스 및 채널 살펴보기](../analysis/most-value-source-channel.md)
* [연결 [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [광고 캠페인에 대한 ROI 향상](../analysis/roi-ad-camp.md)
* [의 UTM 태깅에 대한 5가지 우수 사례 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
