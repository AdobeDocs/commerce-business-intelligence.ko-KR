---
title: Google Analytics - 데이터베이스에서 사용자 장치 및 브라우저 데이터 추적
description: 모바일 장치를 통해 실제로 로그인하는 사용자 수와 해당 사용자의 라이프타임 값에 영향을 미치는 방법에 대해 알아봅니다.
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
role: Admin, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# [!UICONTROL Google Analytics] 추적

[!UICONTROL Google Analytics]을(를) 사용하면 [참조 원본 정보를 저장](../analysis/google-track-user-acq.md)하여 가장 중요한 사용자의 출처를 파악할 수 있습니다. 이 항목에서는 사용자가 작업 중인 플랫폼(예: 장치 또는 브라우저)에 대해 설명합니다. 이를 통해 모바일 장치를 통해 실제로 로그인하는 사용자 수와 해당 사용자의 라이프타임 값에 미치는 영향을 파악할 수 있습니다.

## 사용자 장치 및 브라우저 데이터 저장

웹 사이트에 대한 요청이 있을 때마다 사용자의 브라우저는 요청을 하는 플랫폼에 대한 정보가 포함된 사용자 에이전트 문자열을 보냅니다. 다음은 사용자 에이전트 문자열의 몇 가지 예입니다.

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

자세히 살펴보면 문자열에 사용자의 운영 체제, 브라우저 및 사용 중인 디바이스 이름(이름이 있는 경우)에 대한 정보가 포함되어 있습니다. 사용자 에이전트 문자열은 플랫폼 및 동일한 플랫폼의 버전에 따라 크게 다르지만 일반적으로 플랫폼 이름이 내부 어딘가에 존재하는 것은 사실입니다. 예를 들어 위#1 Chrome 브라우저가 있는 Mac이고 위#2 Firefox 브라우저가 있는 Windows 시스템, #3는 iPhone, #4는 iPad, #5는 Android 디바이스입니다.

요청이 있을 때마다 서버에서 이 정보에 액세스할 수 있습니다. PHP에서 사용자 에이전트 문자열은 `$_SERVER['HTTP_USER_AGENT']`에 저장됩니다. Ruby on Rails에서 `request.env['HTTP_USER_AGENT']`에 저장됩니다. 다른 언어 및 환경에서는 유사한 방식으로 액세스할 수 있습니다.

### 이 데이터를 언제 기록해야 합니까?

[!DNL Adobe]은(는) 사용자가 만들어지거나 순서가 지정될 때마다 이 정보를 저장하기 위해 `Platform` 및 `User-Agent` 데이터베이스 테이블에 `Customers` 또는 `Orders`이라는 새 필드를 추가할 것을 권장합니다. SQL 데이터베이스를 사용하는 경우 이 필드는 `VARCHAR(255)`이어야 합니다. 

>[!NOTE]
>
>`User-Agent` 문자열은 이보다 훨씬 길 수 있지만 실제로 이 길이를 초과하는 경우는 거의 없습니다.

### 유용한 세그먼트를 구문 분석하려면 어떻게 해야 합니까?

`User-Agent` 문자열을 운영 체제, 장치 등의 구성 요소로 구문 분석하는 데 도움이 되는 다양한 라이브러리가 있습니다. 자세한 내용은 [ua-parser 프로젝트](https://github.com/tobie/ua-parser)를 참조하세요.

이 새로운 정보를 통해 사용자가 사이트에 액세스하는 방법을 더 잘 이해할 수 있습니다. 그런 다음 경험을 맞춤화하거나 특정 그룹에 대한 마케팅 캠페인을 만들 수 있습니다.

## 관련 항목

* [&#x200B; [!DNL Google Anaytics] E-Commerce을 통해 주문 참조 소스 추적](../importing-data/integrations/google-ecommerce.md)
* [데이터베이스에서 사용자 조회 소스 추적](../analysis/google-track-user-acq.md)
* [가장 가치 있는 확보 소스 및 채널 살펴보기](../analysis/most-value-source-channel.md)
* [&#x200B; [!DNL Google Adwords] 계정 연결](../importing-data/integrations/google-adwords.md)
* [광고 캠페인에 대한 ROI 향상](../analysis/roi-ad-camp.md)
* [&#x200B; [!DNL Google Analytics] UTM 속성은 어떻게 작동합니까?](../analysis/utm-attributes.md)
