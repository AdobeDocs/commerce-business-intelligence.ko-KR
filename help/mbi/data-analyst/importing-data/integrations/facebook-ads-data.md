---
title: facebook 광고 데이터가 필요합니다
description: Data Warehouse에 동기화하는 것이 좋은 표에 대한 간단한 개요를 살펴보십시오
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# 예상됨 [!DNL Facebook Ads] 데이터

![](../../../assets/Facebook_Logo.png)

그러고 나면 [연결 [!DNL Facebook Ads] account](../integrations/facebook-ads.md)를 사용하여 다음을 수행할 수 있습니다. [Data Warehouse 관리자](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 분석을 위한 관련 데이터 필드를 쉽게 추적할 수 있습니다.

이 문서에서는 Data Warehouse에 동기화하는 것이 권장되는 표에 대한 간단한 개요를 제공합니다. 하위 테이블이 많이 있으므로 전체 목록이 아닙니다. 핵심 테이블만 강조 표시합니다.

## 핵심 광고 캠페인 테이블

이러한 표에는 주요 광고 캠페인 구성 요소에 대한 데이터가 포함되어 있습니다.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adcampaign/)

이 표는 페이지의 [!DNL Facebook Ads] 계정이 필요합니다. 열에는 다음이 포함됩니다 `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

이 테이블 레코드는 [!DNL Facebook Ads] 에 설정 [!DNL Facebook Ads] 계정이 필요합니다. 열에는 광고가 포함됩니다 `Campaign id/name` 광고 세트가 속하는 항목, 예산 책정, 입찰 유형, 예약 및 대상 타깃팅 정보입니다.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adgroup/)

이 표는 모든 광고를 [!DNL Facebook Ads] 계정이 필요합니다. 열에는 광고 세트가 속하는 광고 세트와 광고 캠페인, 광고 입찰, 광고가 사용하는 특정 광고(이미지/텍스트)에 대한 광고 타깃팅 및 참조를 포함하는 광고 정보가 포함됩니다.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adcreative/)

이 테이블에서는 [!DNL Facebook Ads]. 여기에는 적절한 경우 광고 이름, 설명 및 관련 이미지 URL이 포함됩니다.

## 세그먼트화된 캠페인 테이블

다음 표에는 각 날에 대한 각 캠페인/설정/광고 조합, 연령, 성별 및 국가 등의 차원으로 세그먼트화된 항목이 포함되어 있습니다.

### `facebook _ads insights_ (account-id)`

이 표에는 노출 수, 클릭 수, 비용, cpc, cpm, cpp, ctr, 도달 범위, 소셜 도달 및 지출 등의 통계와 함께 각 날의 각 캠페인/세트/광고 조합 항목이 포함되어 있습니다.

### `facebook _ads insights_ (account-id)_~\_actions`

이것은 `facebook_ads_insights_{account_id}` 테이블. 여기에는 다른 캠페인을 기반으로 하는 작업에 대한 전환 데이터가 포함됩니다.

### `facebook _ads insights country_ (account-id)`

이 표에는 `facebook_ads_insights_{account_id}` 표를 만들어 국가별 세그먼트화할 수 있습니다.

### `facebook ads insights age and gender (account-id)`

이 표에는 `facebook_ads_insights_{account_id}` 나이 및 성별 별로 테이블 및 세그먼트화합니다.

## 관련

* [연결 중 [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [통합 재인증](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
