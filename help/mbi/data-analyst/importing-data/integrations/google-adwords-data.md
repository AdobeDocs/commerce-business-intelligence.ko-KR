---
title: 예상 Google Adwords 데이터
description: Data Warehouse 관리자를 사용하여 분석을 위한 관련 데이터 필드를 쉽게 추적하는 방법에 대해 알아봅니다.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# 예상 Google Adwords 데이터

다음 이후 [다음을 연결했습니다. [!DNL Google Adwords] account](../integrations/google-adwords.md), 다음을 사용할 수 있습니다. [Data Warehouse 관리자](../../data-warehouse-mgr/tour-dwm.md) 분석을 위해 관련 데이터 필드를 쉽게 추적할 수 있습니다.

여기에서 Data Warehouse에 복제할 수 있는 테이블이 두 개 있습니다. `campaigns[account-id]` 및 `adwords[account-id]`.

다음 `campaigns` 표 *은(는) 기본적으로 사용해야 합니다.*&#x200B;를 클릭하여 해당 테이블의 모든 관련 필드를 동기화함으로써 시작할 수 있습니다.

다음 `adwords` 테이블에 없는 4개의 열이 포함되어 있습니다. `campaigns` 표:

* `keyword`
* `adContent`
* `adDestinationUrl`
* `adGroup`

이러한 속성을 고려하는 분석을 수행하려는 경우 항상 `adwords` 테이블.

>[!IMPORTANT]
>
>이 표에서는 이러한 네 개의 열이 모두 있는 행을 제외합니다. `null`.

다음은 두 테이블 모두에 대해 예상되는 스키마를 살펴봅니다.

## `Campaigns` 표

다음 `campaigns` 테이블에는 다음 열이 포함되어 있습니다.

| **열** | **설명** |
|-----|-----|
| `\_id` | 테이블의 기본 키 |
| `accountId` | 계정 ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 해당 날짜의 총 클릭 수 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 당일 캠페인에 대한 총 비용 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] 캠페인 ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 캠페인 이름(예: [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | 캠페인이 실행된 날짜 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 해당 날짜의 노출 횟수 |
| `profileId` | 프로필 ID |
| `profileName` | 프로필 이름 |
| `\_updated\_at` | 이 행의 마지막 업데이트 날짜 및 시간 |

{style="table-layout:auto"}

## AdWords 테이블

다음 `adwords` 테이블에는 다음 열이 포함되어 있습니다.

| **열** | **설명** |
|-----|-----|
| `\_id` | 테이블의 기본 키 |
| `accountId` | 계정 ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 해당 날짜의 총 클릭 수 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 당일 캠페인에 대한 총 비용 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] 캠페인 ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 캠페인 이름(예: [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | 캠페인이 실행된 날짜 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 해당 날짜의 노출 횟수 |
| `profileId` | 프로필 ID |
| `profileName` | 프로필 이름 |
| `\_updated\_at` | 이 행의 마지막 업데이트 날짜 및 시간 |
| `keyword` | 캠페인의 키워드 |
| `adContent` | 온라인 캠페인에 대한 텍스트의 첫 줄 |
| `adDestinationUrl` | 에 대한 URL [!DNL Adwords] 광고 참조 트래픽 |
| `adGroup` | 의 이름입니다. [!DNL Adwords] 광고 그룹 |

{style="table-layout:auto"}

이 데이터를 사용하여 만들기를 시작할 수 있습니다 [지표 ](../../../data-user/reports/ess-manage-data-metrics.md) 및 [보고서](../../../tutorials/using-visual-report-builder.md) 지출 데이터 및 [이를 라이프타임 매출과 결합하여 ROI 계산](../../analysis/roi-ad-camp.md).

## 통합 테이블

Adobe은 `consolidated ad spend` 테이블 : 모든 여러 광고 소스의 데이터를 단일 테이블로 결합합니다. 이를 통해 광고 분석에 단일 지표 세트를 사용할 수 있습니다.

통합 테이블이 없는 경우에서 아름다운 대시보드를 만들면 `adwords` 테이블을 사용하려면 보고를 복제하거나 중복 지표를 만들어 해당 데이터를 [!DNL Facebook Ads] 데이터. 통합 테이블을 사용하면 원활하게 통합할 수 있습니다 [!DNL Facebook Ads] 기존 데이터가 있는 데이터 [!DNL Adwords] 보고서. 광고 플랫폼별로 세그먼트화할 수도 있습니다.

위의 필드를 이미 동기화한 경우 당사에 연락하여 광고 지출을 통합하십시오.
