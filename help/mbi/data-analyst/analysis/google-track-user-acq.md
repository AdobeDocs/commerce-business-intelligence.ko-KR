---
title: Google Analytics - 사용자 획득 소스 데이터 추적 개요
description: 사용자 획득 소스별로 데이터를 세그먼트화하는 방법을 알아봅니다.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 1%

---

# 사용자 획득 소스별 세그먼테이션

>[!NOTE]
>
>아래 프로세스는 지원되지 않습니다 [!DNL GoogleUniversal Analytics].

사용자 확보 소스별로 데이터를 세그먼트화하는 기능은 마케팅 계획을 효과적으로 관리하는 데 중요합니다. 새 사용자의 획득 소스를 파악하면 최고 수익을 산출하는 채널을 보여주며 팀이 신뢰할 수 있도록 마케팅 달러를 할당할 수 있습니다.

데이터베이스에서 사용자 획득 소스를 아직 추적하지 않는 경우, [!DNL MBI] 시작하는 데 도움이 될 수 있습니다.

## 사용자 획득 소스 추적

설정에 따라 참조 소스 데이터를 추적하려면 다음 두 가지 방법을 사용하는 것이 좋습니다.

### (옵션 1) 를 통해 주문 참조 소스 데이터를 추적합니다. [!DNL Google Analytics E-Commerce] (포함) [!DNL Shopify] Stores)

활용 [!DNL Google Analytics E-Commerce] 주문 및 판매 데이터를 추적하려면 [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) 각 주문의 참조 소스 데이터를 동기화하기 위해 이렇게 하면 참조 소스별로 매출과 주문을 세그먼트화할 수 있습니다(예: `utm_source` 또는 `utm_medium`) 또한 를 통해 고객 확보 소스를 파악할 수 있습니다. [!DNL MBI] 사용자 지정 차원(예: `User's first order source`.

>[!NOTE]
>
>Shopify 사용자의 경우**: 켜기 [!DNL [Google Analytics E-Commerce] tracking in Shopify](http://docs.shopify.com/manual/settings/general/google-analytics#ecommerce-tracking) 연결하기 전에 [!DNL Google Analytics E-Commerce] 계정 대상 [!DNL MBI].

### (옵션 2) 저장 [!DNL Google Analytics]&#39; 데이터베이스의 획득 소스 데이터

이 문서에서는 저장 방법을 설명합니다 [!DNL Google Analytics] 획득 채널 정보를 자체 데이터베이스에 추가 - `source`, `medium`, `term`, `content`, `campaign`, 및 `gclid` 사용자가 웹 사이트를 처음 방문할 때 있었던 매개 변수입니다. 이러한 매개 변수에 대한 자세한 내용은 [!DNL [Google Analytics] documentation](http://support.google.com/analytics/bin/answer.py?hl=en&amp;answer=1191184). 다음으로, 다음 정보를 사용하여 수행할 수 있는 강력한 마케팅 분석 중 일부를 살펴보겠습니다 [!DNL MBI].

#### 왜?

기본값을 보고 있다면 [!DNL Google Analytics] 전환 및 획득 지표에서 전체적인 상황을 파악할 수 없습니다. 유기 검색과 유료 검색의 전환 수를 확인하는 동안 해당 정보를 사용하여 어떤 작업을 수행할 수 있습니까? 유료 검색에 더 많은 돈을 써야 합니까? 이는 Google Analytics이 제공하는 것이 아닌 해당 채널에서 오는 고객의 값에 따라 달라집니다.

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) 트랜잭션 데이터를 [!DNL Google Analytics]그러나 이 솔루션은 eCommerce 이외의 사이트에서는 작동하지 않으며, 집단 분석과 같은 특정 도구에서는 수행하기가 쉽지 않습니다 [!DNL Google Analytics] 인터페이스.

특정 이메일 캠페인에서 획득한 모든 고객에게 후속 거래를 이메일로 보내려면 어떻게 해야 합니까? 또는 획득 데이터를 CRM 시스템과 통합하시겠습니까? 이것은 불가능하다 [!DNL Google Analytics] &quot; 사실, 이것은 서비스 약관에 위배됩니다 [!DNL Google Analytics] 개인을 식별하는 모든 데이터를 저장합니다.  그러나 그렇다고 해서 이 데이터를 직접 저장할 수 없습니다.

#### 메서드

[!DNL Google Analytics] 라는 쿠키에 방문자 참조 정보를 저장합니다. `__utmz`. 이 쿠키가 설정되면( [!DNL Google Analytics] 추적 코드), 해당 사용자의 도메인에 대한 후속 요청과 함께 해당 콘텐츠가 전송됩니다. 예를 들어 PHP에서는 `$_COOKIE['__utmz']` 다음과 같은 문자열을 볼 수 있습니다.

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

분명히 일부 획득 소스 데이터가 문자열로 인코딩되어 있으며, 이 데이터가 방문자의 최신 획득 소스 및 관련 캠페인 데이터임을 확인하기 위해 테스트했습니다. 이제 우리는 데이터를 추출하는 방법을 알아야 합니다. 다행히 Justin Cutroni는 이전에 이 인코딩의 작동 방식을 설명했고, 몇 가지 javascript 코드를 공유하여 주요 정보 비트를 추출했습니다.

이 코드를 받아서 [github에 호스팅된 PHP 라이브러리](https://github.com/RJMetrics/referral-grabber-php).   라이브러리를 사용하려면 `include` 에 대한 참조 `ReferralGrabber.php` 그런 다음

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

반환된 `$data` 배열은 키의 맵이 됩니다 `source`, `medium`, `term`, `content`, `campaign`, `gclid` 및 해당 값.

데이터베이스에 새 테이블을 추가하는 것이 좋습니다(예: `user_referral`과 같은 열이 있는 경우: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. 사용자가 등록할 때마다 참조 정보를 가져와서 이 표에 저장합니다.

#### 이 데이터를 사용하는 방법

사용자 획득 소스를 저장하고 있으므로 어떻게 사용할 수 있습니까?

SQL 데이터베이스를 사용하고 있으며 `users` 다음 구조의 표:

| ID | 이메일 | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | 유기 |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | 직접 | - |
| 4 | jess@ghi.com | 2012-01-26 | 참조 | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | 기타 | 유기 |
| ... | ... | ... | ... | ... |

우선, Adobe에서는 데이터베이스에 대해 다음 쿼리를 실행하여 각 참조 채널에서 들어오는 사용자 수를 계산할 수 있습니다.

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

결과는 다음과 같습니다.

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| 직접 | 156 |
| 참조 | 55 |
| 기타 | 16 |

이것은 흥미롭지만 사용이 제한적입니다. 우리가 정말 알고 싶은 것은 시간이 지남에 따라 이 수치들의 증가율, 각 획득 출처에 의해 생성된 수익의 양, [집단 분석](http://cohortanalysis.com/) 각 소스에서 온 사용자 수 및 이러한 채널 중 하나의 사용자가 향후에 고객으로 재방문할 가능성이 있습니다. 이러한 분석을 수행하는 데 필요한 쿼리는 복잡합니다. 이러한 이유로 Dell이 [!DNL MBI]. 이러한 정보를 바탕으로 Adobe는 가장 수익성이 높은 획득 채널을 결정하고 그에 따라 마케팅 시간과 비용을 집중시킬 수 있습니다.

### 관련

* **[가장 가치 있는 획득 소스 및 채널 살펴보기](../analysis/most-value-source-channel.md)**
* **[연결 [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)**
* **[광고 캠페인에 대한 ROI 향상](../analysis/roi-ad-camp.md)**
* **[어떻게 [!DNL Google Analytics] UTM 속성 작업?](../analysis/utm-attributes.md)**
