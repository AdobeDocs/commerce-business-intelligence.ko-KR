---
title: 예상 Facebook 광고 데이터
description: Data Warehouse과 동기화하는 것이 권장되는 표에 대한 간략한 개요를 알아봅니다
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/LBpqIMm4nGx-Vu-zxw-iPLgNg1yfDsYi0yDyFHCyxvA
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: c8d7097b4f841a4fe8c5777f207ea0ea53202a0f
workflow-type: tm+mt
source-wordcount: 342
ht-degree: 0%

---

# [!DNL Facebook Ads]개의 데이터가 필요합니다.

[계정 [!DNL Facebook Ads] 연결](../integrations/facebook-ads.md)한 후 [Data Warehouse 관리자](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)를 사용하여 분석할 관련 데이터 필드를 쉽게 추적할 수 있습니다.

이 항목에서는 Adobe에서 Data Warehouse과 동기화하는 데 권장하는 표에 대한 간단한 개요를 제공합니다. 하위 테이블이 상당히 많기 때문에 핵심 테이블만 강조 표시됩니다.

## 핵심 광고 캠페인 테이블

이러한 표에는 핵심 광고 캠페인 구성 요소에 대한 데이터가 포함되어 있습니다.

### `facebook _campaigns_ (account-id)`

[`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

이 테이블은 [!DNL Facebook Ads] 계정의 캠페인의 핵심 테이블입니다. 열에는 `campaign id`, `name`, `status (active/paused)`, `objective`이(가) 포함됩니다.

### `facebook _adsets_ (account-id)`

[`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

이 테이블 레코드는 [!DNL Facebook Ads] 계정에 있는 [!DNL Facebook Ads] 집합의 핵심 테이블입니다. 열에는 광고 집합이 속한 광고 `Campaign id/name`, 예산 책정, 입찰 유형, 일정 및 대상 타깃팅 정보가 포함됩니다.

### `facebook _ads_ (account-id)`

[`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

이 테이블은 [!DNL Facebook Ads] 계정에 모든 광고를 기록합니다. 열에는 광고 세트 및 해당 광고가 속한 광고 캠페인, 광고 입찰, 광고 타겟팅 및 광고가 사용하는 특정 크리에이티브(이미지/텍스트)에 대한 참조가 포함된 광고 정보가 포함됩니다.

### `facebook _adcreative_ (account-id)`

[`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

이 테이블은 [!DNL Facebook Ads]에서 사용되는 크리에이티브를 기록합니다. 크리에이티브에는 크리에이티브 이름, 설명 및 적절한 경우 관련 이미지 URL이 포함됩니다.

## 세그먼트화된 캠페인 테이블

다음 표에는 연령, 성별 및 국가와 같은 차원으로 세그먼트화된 각 날짜의 각 캠페인/세트/광고 조합에 대한 항목이 포함되어 있습니다.

### `facebook _ads insights_ (account-id)`

이 표에는 노출 횟수, 클릭 수, 비용, cpc, cpm, cpp, ctr, 도달 범위, 소셜 도달 범위 및 지출과 같은 통계와 함께 각 날의 각 캠페인/세트/광고 조합에 대한 항목이 포함되어 있습니다.

### `facebook _ads insights_ (account-id)_~\_actions`

`facebook_ads_insights_{account_id}` 테이블의 하위 테이블입니다. 여기에는 다양한 캠페인을 기반으로 발생하는 작업에 대한 전환 데이터가 포함됩니다.

### `facebook _ads insights country_ (account-id)`

이 테이블에는 `facebook_ads_insights_{account_id}` 테이블과 동일한 정보가 포함되어 있으며 국가별로 세그먼트화됩니다.

### `facebook ads insights age and gender (account-id)`

이 테이블에는 `facebook_ads_insights_{account_id}` 테이블과 동일한 정보가 포함되어 있으며 연령별 및 성별별로 구분됩니다.

## 관련 항목

* [&#x200B; [!DNL Facebook Ads] 연결 중](../integrations/facebook-ads.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ko)
