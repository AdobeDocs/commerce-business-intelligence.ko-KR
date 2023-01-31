---
title: Google Analytics - 데이터베이스에서 사용자 장치 및 브라우저 데이터를 추적합니다
description: 모바일 장치를 통해 실제로 로그인하는 사용자 수와 이 사용자가 그러한 사용자의 라이프타임 값에 어떻게 영향을 주는지를 알아봅니다.
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# [!UICONTROL Google Analytics] 추적

사용 [!UICONTROL Google Analytics] 다음을 수행할 수 있습니다. [참조 소스 정보 저장](../analysis/google-track-user-acq.md) 가장 가치 있는 사용자가 어디에서 오는지 이해하기 위해 노력합니다. 이 항목에서는 사용자가 작업 중인 플랫폼(예: 장치 또는 브라우저)에 대해 알아봅니다. 이를 통해 모바일 장치를 통해 실제로 로그인하는 사용자의 수와 이 사용자가 그러한 사용자의 라이프타임 값에 어떻게 영향을 주는지를 이해할 수 있습니다.

## 사용자 장치 및 브라우저 데이터 저장

웹 사이트에 요청이 수행될 때마다 사용자의 브라우저는 요청을 수행하는 플랫폼에 대한 정보가 있는 사용자-에이전트 문자열을 전송합니다. 다음은 사용자-에이전트 문자열의 몇 가지 예입니다.

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.
` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

자세히 살펴보면 문자열에 사용자의 운영 체제, 브라우저 및 사용 중인 장치 이름(이름이 있는 경우)에 대한 정보가 포함되어 있음을 알 수 있습니다. 사용자-에이전트 문자열은 플랫폼마다, 심지어 동일한 플랫폼의 버전마다 광범위하게 다르지만 일반적으로 플랫폼 이름이 내 어딘가에 있다는 것은 사실입니다. 예를 들어, 위#1 Chrome 브라우저가 있는 Mac이고, 위의 #2는 Firefox 브라우저를 사용하는 Windows 시스템이며, #3는 iPhone이고, #4는 iPad이고, #5는 Android 장치입니다.

이 정보는 요청이 수행될 때마다 서버에서 액세스할 수 있습니다. PHP에서 User-Agent 문자열은 `$_SERVER['HTTP_USER_AGENT']`. 레일의 루비에서 `request.env['HTTP_USER_AGENT']`. 다른 언어 및 환경에서는 비슷한 방법으로 액세스할 수 있습니다.

### 이 데이터는 언제 기록해야 합니까?

라는 새 필드를 추가하는 것이 좋습니다 `Platform` 또는 `User-Agent` 아래와 같이 `Customers` 및 `Orders` 사용자가 만들어지거나 주문이 수행될 때마다 이 정보를 저장할 데이터베이스 테이블입니다. SQL 데이터베이스를 사용하는 경우 이 필드는 `VARCHAR(255)`. 

>[!NOTE]
>
>다음 `User-Agent` 문자열은 이보다 훨씬 길어질 수 있지만 실제로 이 길이를 거의 초과할 수 없습니다.

### 유용한 세그먼트를 어떻게 구문 분석합니까?

분석을 지원하기 위해 많은 라이브러리가 있습니다 `User-Agent` 문자열을 운영 체제, 장치 등과 같은 구성 요소에 넣을 수 있습니다. 자세한 내용은 [ua-parser 프로젝트](https://github.com/tobie/ua-parser) 추가 정보

이 새로운 정보를 사용하면 사용자가 사이트에 액세스하는 방법을 더 잘 이해할 수 있습니다. 그런 다음 경험을 조정하거나 특정 그룹에 대한 마케팅 캠페인을 만들 수 있습니다.

## 관련

* [를 통해 주문 참조 소스 추적 [!DNL Google Anaytics] 전자 상거래](../importing-data/integrations/google-ecommerce.md)
* [데이터베이스에서 사용자 참조 소스 추적](../analysis/google-track-user-acq.md)
* [가장 가치 있는 획득 소스 및 채널 살펴보기](../analysis/most-value-source-channel.md)
* [연결 [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [광고 캠페인에 대한 ROI 향상](../analysis/roi-ad-camp.md)
* [어떻게 [!DNL Google Analytics] UTM 속성 작업?](../analysis/utm-attributes.md)
