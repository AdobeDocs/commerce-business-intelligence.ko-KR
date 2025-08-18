---
title: 예상 Google Adwords 데이터
description: Data Warehouse Manager를 사용하여 분석을 위한 관련 데이터 필드를 쉽게 추적하는 방법에 대해 알아봅니다.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# [!DNL Google Adwords]개의 데이터가 필요합니다.

[계정 [!DNL Google Adwords] 연결](../integrations/google-adwords.md)한 후 [Data Warehouse 관리자](../../data-warehouse-mgr/tour-dwm.md)를 사용하여 분석할 관련 데이터 필드를 쉽게 추적할 수 있습니다.

여기에서 Data Warehouse에 복제할 수 있는 테이블이 두 개 있습니다.

* `campaigns[account-id]`
* `adwords[account-id]`

`campaigns` 테이블 *은(는) 기본적으로 사용되어야 합니다*. 따라서 해당 테이블에서 모든 관련 필드를 동기화하여 시작할 수 있습니다.

`adwords` 테이블에 `campaigns` 테이블에 없는 4개의 열이 있습니다.

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

이러한 특성을 고려한 분석을 수행하려는 경우 `adwords` 테이블을 사용해야 합니다.

>[!IMPORTANT]
>
>이 테이블은 이러한 네 개의 열이 모두 `null`인 행을 제외합니다.

아래에서는 두 테이블에 대해 예상되는 스키마를 살펴봅니다.

## [!DNL Campaigns] 테이블

`campaigns` 테이블에는 다음 열이 포함되어 있습니다.

| **열** | **설명** |
|-----|-----|
| `\_id` | 테이블의 기본 키 |
| `accountId` | 계정 ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | 해당 날짜의 총 클릭 수 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | 당일 캠페인에 대한 총 비용 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] 캠페인 ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | 캠페인 이름(예: [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | 캠페인이 실행된 날짜 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | 해당 날짜의 노출 횟수 |
| `profileId` | 프로필 ID |
| `profileName` | 프로필 이름 |
| `\_updated\_at` | 이 행의 마지막 업데이트 날짜 및 시간 |

{style="table-layout:auto"}

## [!DNL AdWords] 테이블

`adwords` 테이블에는 다음 열이 포함되어 있습니다.

| **열** | **설명** |
|-----|-----|
| `\_id` | 테이블의 기본 키 |
| `accountId` | 계정 ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | 해당 날짜의 총 클릭 수 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | 당일 캠페인에 대한 총 비용 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] 캠페인 ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | 캠페인 이름(예: [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | 캠페인이 실행된 날짜 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | 해당 날짜의 노출 횟수 |
| `profileId` | 프로필 ID |
| `profileName` | 프로필 이름 |
| `\_updated\_at` | 이 행의 마지막 업데이트 날짜 및 시간 |
| `keyword` | 캠페인의 키워드 |
| `adContent` | 온라인 캠페인에 대한 텍스트의 첫 줄 |
| `adDestinationUrl` | [!DNL Adwords] 광고가 트래픽을 참조한 URL |
| `adGroup` | [!DNL Adwords] 광고 그룹의 이름 |

{style="table-layout:auto"}

이 데이터를 사용하면 지출 데이터를 기반으로 [지표](../../../data-user/reports/ess-manage-data-metrics.md) 및 [보고서](../../../tutorials/using-visual-report-builder.md)를 만들고 [이를 라이프타임 매출과 결합](../../analysis/roi-ad-camp.md)하여 ROI를 계산할 수 있습니다.

## 통합 테이블

[!DNL Adobe]에서는 `consolidated ad spend` 테이블을 만들어 여러 광고 원본의 데이터를 하나의 테이블로 결합하는 것이 좋습니다. 이를 통해 광고 분석에 단일 지표 세트를 사용할 수 있습니다.

통합 테이블이 없고 `adwords` 테이블에 멋진 대시보드를 작성하는 경우 보고를 복제하거나 중복 지표를 만들어 해당 데이터를 [!DNL Facebook Ads] 데이터와 비교해야 합니다. 통합 테이블을 사용하면 [!DNL Facebook Ads] 데이터를 기존 [!DNL Adwords] 보고서에 원활하게 통합할 수 있습니다. 광고 플랫폼별로 세그먼트화할 수도 있습니다.

위의 필드를 이미 동기화한 경우 [문의하기](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)하여 광고 지출을 통합하십시오.
