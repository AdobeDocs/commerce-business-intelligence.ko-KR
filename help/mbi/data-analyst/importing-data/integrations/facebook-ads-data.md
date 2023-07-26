---
title: 예상 Facebook 광고 데이터
description: Data Warehouse과 동기화하는 것이 권장되는 표에 대한 간략한 개요를 알아봅니다
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 예상 [!DNL Facebook Ads] 데이터

다음 작업을 수행한 후 [을(를) 연결했습니다. [!DNL Facebook Ads] account](../integrations/facebook-ads.md), 다음을 사용할 수 있습니다. [Data Warehouse 관리자](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 분석을 위해 관련 데이터 필드를 쉽게 추적할 수 있습니다.

이 항목에서는 Adobe이 Data Warehouse과 동기화할 것을 권장하는 표에 대한 간략한 개요를 제공합니다. 하위 테이블이 상당히 많기 때문에 핵심 테이블만 강조 표시됩니다.

## 핵심 광고 캠페인 테이블

이러한 표에는 핵심 광고 캠페인 구성 요소에 대한 데이터가 포함되어 있습니다.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

이 테이블은 의 핵심 캠페인 테이블입니다. [!DNL Facebook Ads] 계정입니다. 열은 다음과 같습니다. `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

이 테이블 레코드는 의 핵심 테이블입니다. [!DNL Facebook Ads] 에 설정 [!DNL Facebook Ads] 계정입니다. 열에는 광고가 포함됩니다 `Campaign id/name` 광고 세트는 예산, 입찰 유형, 일정 및 대상자 타겟팅 정보에 속합니다.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

이 표는에 있는 모든 광고를 기록합니다 [!DNL Facebook Ads] 계정입니다. 열에는 광고 세트 및 해당 광고가 속한 광고 캠페인, 광고 입찰, 광고 타겟팅 및 광고가 사용하는 특정 크리에이티브(이미지/텍스트)에 대한 참조가 포함된 광고 정보가 포함됩니다.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

이 표는에서 사용되는 크리에이티브를 기록합니다. [!DNL Facebook Ads]. 크리에이티브에는 크리에이티브 이름, 설명 및 적절한 경우 관련 이미지 URL이 포함됩니다.

## 세그먼트화된 캠페인 테이블

다음 표에는 연령, 성별 및 국가와 같은 차원으로 세그먼트화된 각 날짜의 각 캠페인/세트/광고 조합에 대한 항목이 포함되어 있습니다.

### `facebook _ads insights_ (account-id)`

이 표에는 노출 횟수, 클릭 수, 비용, cpc, cpm, cpp, ctr, 도달 범위, 소셜 도달 범위 및 지출과 같은 통계와 함께 각 날의 각 캠페인/세트/광고 조합에 대한 항목이 포함되어 있습니다.

### `facebook _ads insights_ (account-id)_~\_actions`

다음은 의 하위 테이블입니다. `facebook_ads_insights_{account_id}` 테이블. 여기에는 다양한 캠페인을 기반으로 발생하는 작업에 대한 전환 데이터가 포함됩니다.

### `facebook _ads insights country_ (account-id)`

이 표에는 와 동일한 정보가 포함되어 있습니다. `facebook_ads_insights_{account_id}` 국가별로 표를 작성하고 세그먼트화합니다.

### `facebook ads insights age and gender (account-id)`

이 표에는 와 동일한 정보가 포함되어 있습니다. `facebook_ads_insights_{account_id}` 나이와 성별에 따라 분류하여 표시합니다.

## 관련 항목

* [연결 중 [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
