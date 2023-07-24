---
title: Google Analytics 및 UTM 속성
description: Google Analytics 소스 속성 프로세스에 대해 알아봅니다.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Data Architect, Data Engineer, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# [!DNL Google Analytics] 및 UTM 속성

다음과 같은 작업을 수행하는 것이 중요합니다. [사용자 획득 소스 추적](../../data-analyst/analysis/google-track-user-acq.md) 끝 [성과가 가장 좋은 광고 캠페인 식별](../../data-analyst/analysis/most-value-source-channel.md). 이 주제에서는 다음을 살펴봅니다. [!DNL Google Analytics] 소스 속성 프로세스. 즉, 언제 어떤 정보가 기록되는지 알 수 있다.

## 속성이란 무엇입니까?

`Attribution` 특정 활동의 참조 소스를 지정하는 것에 대한 것입니다. 이러한 활동은 일반적으로 매크로 변환 또는 마이크로 변환이며, 매크로는 다음과 같습니다 **구매**, 마이크로 **등록, 이메일 등록, 블로그 댓글,** 기타 등등.

이상적으로는 전환 이벤트가 발생할 때마다 참조 소스가 기록됩니다. 그러나 그 출처는 어떻게 결정됩니까?

현실은 사용자가 마이크로 또는 매크로 변환을 히트/커밋하기 전에 많은 소스에서 오는 경우가 많습니다. 예를 들어, 이들은 유기농 제품을 통해 현장으로 온 다음, 떠나고, 유료 검색을 통해 온 다음, 떠난 다음, 바로 현장으로 올 수 있습니다. 이 소스 추적 정보는 종종 UTM 매개변수를 통해 사이트에 제공되지만 보다 정교한 시스템도 있습니다. 귀하의 목적을 위해, 다음 사항에 집중하십시오. [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## 은 어떻게 합니까? [!DNL Google Analytics] utm 매개변수를 통한 속성 참조 소스

URL에 UTM 매개 변수가 지정되면 구문 분석되어 [!DNL Google Analytics] [쿠키](https://en.wikipedia.org/wiki/HTTP_cookie). 웹 사이트에 이 없는 경우 [!DNL Google Analytics]에서는 UTM을 가질 필요가 없습니다. [!DNL Google Analytics] 는 라이프타임 동안 UTM으로 여러 URL을 조회하는 사용자를 처리하는 방법에 대한 규칙을 가지고 있습니다(자세한 내용은 나중에 설명). 웹 사이트가 UTM 매개 변수를 외부 데이터베이스에 캡처하도록 구성되어 있다고 가정할 때 마이크로 또는 매크로 변환이 발생하면 [!DNL Google Analytics] 전환 시 쿠키가 데이터베이스에 복제됩니다.

## 첫 번째 클릭과 마지막 클릭 비교

### 마지막 클릭 속성

마지막 클릭 기여도 분석은 에서 사용하는 가장 일반적인 기여도 분석 모델입니다. [!DNL Google Analytics]. 이 경우 [!DNL Google Analytics] cookie는 전환 이벤트 이전의 가장 최근 소스에 대한 UTM 매개 변수를 나타내며, 다음과 같습니다. [데이터베이스에 기록됨](../../data-analyst/analysis/google-track-user-acq.md). 다음 [!DNL Google Analytics] 쿠키는 사용자가 새 UTM 매개 변수 세트가 포함된 새 URL을 클릭하는 경우에만 이전 UTM 매개 변수를 덮어씁니다.

예를 들어 를 통해 웹 사이트를 처음 방문하는 사용자를 고려하십시오. [!DNL Google Analytics] *유료 검색*&#x200B;를 반환한 다음 를 통해 반환 *유기 검색*, 그리고 마지막으로 *웹 사이트 직접* 또는 *이메일 링크* **UTM 매개 변수 없음** 전환 이벤트 전. 이 예에서는 [!DNL Google Analytics] cookie는 전환 전의 마지막 소스를 나타내므로 사용자의 소스가 유기적이라고 말합니다. 다음 *경로* 최종 전환 이벤트 이전의 사용자 는 무시됩니다. 대신 사용자가 UTM이 있는 이메일 링크에서 웹 사이트를 방문한 경우 [!DNL Google Analytics] 쿠키는 소스가 &quot;email&quot;이라고 합니다. 따라서 쿠키에 기존 UTM 매개 변수가 있고 사용자가 직접 을 통해 들어오는 경우 [!DNL Google Analytics] cookie는 &quot;직접&quot;이 아닌 UTM 매개 변수를 표시합니다.

>[!NOTE]
>
>특정 사용자 [!DNL Google Analytics] 쿠키 매개 변수는 쿠키가 [만료](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)또는 사용자가 브라우저에서 쿠키를 지우는 경우입니다.*

### 첫 번째 클릭 속성

일부 유료 속성 도구를 사용하면 사용자 경로에서 소스의 &quot;팬케이크 스택&quot;을 캡처할 수 있습니다. 이러한 상황에서 위의 예에서 첫 번째 클릭 기여도 분석은 유료 검색을 알려줍니다. 또는 일부 웹 사이트는 팬케이크 스택을 캡처하고 첫 번째 소스를 데이터베이스에 저장하는 자체 쿠키를 구현합니다.

## 속성을 분석하는 방법

[!DNL Google Analytics] 에는 네 가지 다른 속성 모델을 수행할 수 있도록 해주는 강력한 기능이 웹 인터페이스에 있습니다.

1. 첫 번째 클릭
1. 마지막 클릭
1. 선형(경로의 모든 소스에서 균등하게 수익 분할)
1. 가중(사용자 지정 속성)

이제 각 마이크로 또는 매크로 변환에 대한 속성 모델이 무엇인지 이해했으므로, 질문은 &quot;사용자 전환의 총체로 무엇을 합니까?&quot;가 됩니다.  예를 들어 GA 마지막 클릭 논리를 기반으로 기록된 UTM을 살펴봅니다.

* 유기 등록 아래 사용자 등록
* 유료 검색에서 사용자의 첫 번째 구매 $5.00
* 이메일에 대한 사용자의 두 번째 구매 $50.00
* 유기 $10.00에 따른 사용자의 세 번째 구매

여기 묻습니다. &quot;유료 검색에서 얼마나 많은 수익을 얻었습니까? 이메일에서?  유기농?&quot; 답변이 5, 50, 10(마지막 소스가 무엇이든)이라고 할 수도 있고, 모든 매출을 첫 번째 소스에 귀속시킨다고 할 수도 있습니다(65개 모두 유기농으로 이동). 가중 분석을 적용하거나 선형 모델(즉, 각각 약 22개)을 적용할 수도 있습니다.

## 관련 설명서

* [다음을 통해 주문 참조 소스 추적 [!DNL Google Analytics] 전자 상거래](../importing-data/integrations/google-ecommerce.md)
* [데이터베이스에서 사용자 조회 소스 추적](../analysis/google-track-user-acq.md)
* [데이터베이스에서 사용자 장치, 브라우저 및 OS 데이터 추적](../analysis/google-track-user-acq.md)
* [가장 가치 있는 확보 소스 및 채널 살펴보기](../analysis/most-value-source-channel.md)
* [연결 [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [광고 캠페인에 대한 ROI 향상](../analysis/roi-ad-camp.md)
* [의 UTM 태그 지정에 대한 5가지 우수 사례 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
