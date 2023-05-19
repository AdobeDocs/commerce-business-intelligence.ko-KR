---
title: Google Analytics - 사용자 획득 소스 데이터 추적 개요
description: 사용자 확보 소스로 데이터를 세그먼트화하는 방법에 대해 알아봅니다.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: af1e3839839b4c419beabb0cc666c996ea2179d4
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---

# 사용자 획득 소스별 세그멘테이션

>[!NOTE]
>
>아래 프로세스는 을 지원하지 않습니다. [!DNL Google Universal Analytics].

사용자 확보 소스별로 데이터를 세그먼트화하는 기능은 마케팅 계획을 효과적으로 관리하는 데 매우 중요합니다. 신규 사용자의 획득 소스를 알면 어떤 채널이 가장 높은 수익을 내는지 알 수 있으며, 이를 통해 팀이 자신감을 가지고 마케팅 달러를 할당할 수 있습니다.

데이터베이스에서 사용자 획득 소스를 아직 추적하지 않는 경우 [!DNL Adobe Commerce Intelligence] 시작하는 데 도움이 될 수 있습니다.

## 사용자 획득 소스 추적

[!DNL Adobe] 는 설정에 따라 참조 소스 데이터를 추적하는 두 가지 방법을 권장합니다.

### (옵션 1) 다음을 통해 주문 참조 소스 데이터 추적 [!DNL Google Analytics E-Commerce] (포함 [!DNL Shopify] Stores)

를 사용하는 경우 [!DNL Google Analytics E-Commerce] 주문 및 판매 데이터를 추적하려면 [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) 각 주문의 조회 소스 데이터를 동기화합니다. 이를 통해 조회 출처별로 매출 및 주문을 세그먼트화할 수 있습니다(예: `utm_source` 또는 `utm_medium`). 또한 다음을 통해 고객 확보 소스에 대한 감을 얻을 수 있습니다. [!DNL Commerce Intelligence] 사용자 정의 차원(예: ) `User's first order source`.

>[!NOTE]
>
>**Shopify 사용자용**: 켜기 [!DNL [Google Analytics E-Commerce] tracking in Shopify](https://help.shopify.com/en/manual/reports-and-analytics/google-analytics#ecommerce-tracking) 에 연결하기 전에 [!DNL Google Analytics E-Commerce] 계정 위치: [!DNL Commerce Intelligence].

### (옵션 2) 저장 [!DNL Google Analytics]&#39; 데이터베이스의 획득 소스 데이터

이 항목에서는 저장 방법을 설명합니다. [!DNL Google Analytics] 고객 확보 채널 정보를 자체 데이터베이스에 저장 - 즉 `source`, `medium`, `term`, `content`, `campaign`, 및 `gclid` 사용자가 웹 사이트를 처음 방문할 때 있었던 매개 변수입니다. 이러한 매개 변수에 대한 설명은 [!DNL [Google Analytics] documentation](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). 그런 다음에서 이 정보로 수행할 수 있는 강력한 마케팅 분석 중 일부를 살펴봅니다. [!DNL Commerce Intelligence].

#### 왜요?

기본값을 보고 있는 경우 [!DNL Google Analytics] 전환 및 획득 지표를 통해 전체적인 상황을 파악할 수 없습니다. 유기 검색 대 유료 검색의 전환 수를 보는 동안 흥미로운, 당신은 그 정보로 무엇을 할 수 있습니까? 유료 검색에 더 많은 돈을 지출해야 합니까? 이는 Google Analytics이 제공하지 않는, 해당 채널에서 오는 고객의 가치에 따라 달라집니다.

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) 트랜잭션 데이터를에 저장하여 이 문제를 완화합니다. [!DNL Google Analytics], 그러나 이 솔루션은 eCommerce가 아닌 사이트에서는 작동하지 않습니다. 또한 코호트 분석과 같은 특정 도구는 [!DNL Google Analytics] 인터페이스.

특정 이메일 캠페인으로 인수한 모든 고객에게 후속 거래를 이메일로 보내려면 어떻게 해야 합니까? 또는 획득 데이터를 CRM 시스템과 통합하시겠습니까? 이는 다음 위치에서 불가능합니다. [!DNL Google Analytics] - 사실, 이는 서비스 약관에 위배됩니다. [!DNL Google Analytics] 개인을 식별하는 모든 데이터를 저장합니다. 그러나 이 데이터는 직접 저장할 수 있습니다.

#### 메서드

[!DNL Google Analytics] 라는 쿠키에 방문자 참조 정보를 저장합니다. `__utmz`. 이 쿠키가 설정된 후(에 의해) [!DNL Google Analytics] 추적 코드)를 입력하면 해당 사용자의 도메인에 대한 모든 후속 요청과 함께 콘텐츠가 전송됩니다. 예를 들어, PHP에서는 `$_COOKIE['__utmz']` 그리고 다음과 같은 문자열이 표시됩니다.

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

문자열로 인코딩된 획득 소스 데이터가 분명히 있습니다. 이를 테스트하여 방문자의 최신 획득 소스 및 관련 캠페인 데이터인지 확인합니다. 이제 데이터를 추출하는 방법을 알아야 합니다.

이 코드는 [Github에서 호스팅된 PHP 라이브러리](https://github.com/RJMetrics/referral-grabber-php). 라이브러리를 사용하려면, `include` 에 대한 참조 `ReferralGrabber.php` 그런 다음

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

반환된 `$data` 배열은 키의 맵입니다. `source`, `medium`, `term`, `content`, `campaign`, `gclid`및 해당 값.

[!DNL Adobe] 는 다음과 같은 테이블을 데이터베이스에 추가할 것을 권장합니다. `user_referral`, 다음과 같은 열이 있는 경우: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. 사용자가 등록할 때마다 추천 정보를 가져와서 이 테이블에 저장합니다.

#### 이 데이터를 사용하는 방법

이제 사용자 확보 소스를 저장했으므로 이를 어떻게 사용할 수 있습니까?

SQL 데이터베이스를 사용하고 있고 `users` 다음 구조를 사용하는 표:

| ID | 이메일 | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | 유기 |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | 직접 | - |
| 4 | jess@ghi.com | 2012-01-26 | 참조 | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | 기타 | 유기 |
| ... | ... | ... | ... | ... |

먼저 데이터베이스에 대해 다음 쿼리를 실행하여 각 조회 채널에서 오는 사용자 수를 계산할 수 있습니다.

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

결과는 다음과 같습니다.

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| 직접 | 156 |
| 참조 | 55 |
| 기타 | 16 |

이것은 흥미롭지만 사용이 제한적입니다. 알고 싶은 사항은 다음과 같습니다.

* 시간의 경과에 따른 이들 숫자의 증가율
* 각 획득 소스에서 생성된 수익 금액
* a [집단 분석](https://en.wikipedia.org/wiki/Cohort_analysis) 각 소스에서 온 사용자 수
* 이러한 채널 중 하나의 사용자가 향후 고객으로 반환될 확률입니다.

이러한 분석을 수행하는 데 필요한 쿼리는 복잡합니다. 이러한 정보로 무장하면 가장 수익성이 높은 획득 채널을 결정하고 그에 따라 마케팅 시간과 비용을 집중할 수 있습니다.

### 관련 항목

* **[가장 가치 있는 확보 소스 및 채널 살펴보기](../analysis/most-value-source-channel.md)**
* **[연결 [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)**
* **[광고 캠페인에 대한 ROI 향상](../analysis/roi-ad-camp.md)**
* **[은 어떻게 합니까? [!DNL Google Analytics] UTM 속성이 작동합니까?](../analysis/utm-attributes.md)**
