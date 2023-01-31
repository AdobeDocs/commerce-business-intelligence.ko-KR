---
title: Google Adwords 데이터가 필요합니다.
description: Data Warehouse 관리자를 사용하여 분석을 위한 관련 데이터 필드를 쉽게 추적하는 방법을 알아봅니다.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Google Adwords 데이터가 필요합니다.

후 [연결 [!DNL Google Adwords] account](../integrations/google-adwords.md)를 사용하여 다음을 수행할 수 있습니다. [Data Warehouse 관리자](../../data-warehouse-mgr/tour-dwm.md) 분석을 위한 관련 데이터 필드를 쉽게 추적할 수 있습니다.

여기에서 Data Warehouse로 복제하는 데 사용할 수 있는 테이블은 두 개입니다. `campaigns[account-id]` 및 `adwords[account-id]`.

다음 `campaigns` 표 *기본적으로 사용되어야 함*&#x200B;를 채울 수 있으므로 해당 테이블의 모든 관련 필드를 동기화하여 시작할 수 있습니다.

다음 `adwords` 테이블에는 네 개의 열이 포함되어 있으며, `campaigns` 표:

* `keyword`
* `adContent`
* `adDestinationUrl`
* `adGroup`

이러한 속성을 고려하는 분석을 수행하는 데 관심이 있을 때마다 `adwords` 테이블.

>[!IMPORTANT]
>
>이 표는 이러한 열 4개가 모두 포함된 행을 제외합니다 `null`.

다음은 두 테이블의 예상 스키마를 보여 줍니다.

## `Campaigns` 표

다음 `campaigns` 표에는 다음 열이 포함되어 있습니다.

| **열** | **설명** |
|-----|-----|
| `\_id` | 테이블의 기본 키 |
| `accountId` | 계정 ID |
| [`adClicks`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 날짜에 대한 총 클릭 수 |
| [`adCost`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 해당 날의 캠페인에 대한 총 비용 |
| [`adwordsCampaignID`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] 캠페인 ID |
| [`campaign`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 캠페인 이름(예: [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=time&amp;jump=ga_date) | 캠페인이 실행된 날짜 |
| [`impressions`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 일 노출 횟수 |
| `profileId` | 프로필 ID |
| `profileName` | 프로필 이름 |
| `\_updated\_at` | 이 행에 대한 마지막 업데이트 날짜 및 시간입니다 |

{style=&quot;table-layout:auto&quot;}

## AdWords 테이블

다음 `adwords` 표에는 다음 열이 포함되어 있습니다.

| **열** | **설명** |
|-----|-----|
| `\_id` | 테이블의 기본 키 |
| `accountId` | 계정 ID |
| [`adClicks`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 날짜에 대한 총 클릭 수 |
| [`adCost`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 해당 날의 캠페인에 대한 총 비용 |
| [`adwordsCampaignID`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] 캠페인 ID |
| [`campaign`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 캠페인 이름(예: [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=time&amp;jump=ga_date) | 캠페인이 실행된 날짜 |
| [`impressions`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 일 노출 횟수 |
| `profileId` | 프로필 ID |
| `profileName` | 프로필 이름 |
| `\_updated\_at` | 이 행에 대한 마지막 업데이트 날짜 및 시간입니다 |
| `keyword` | 캠페인의 키워드 |
| `adContent` | 온라인 캠페인에 대한 텍스트의 첫 번째 줄 |
| `adDestinationUrl` | URL을 만들 때 [!DNL Adwords] 추천 트래픽 |
| `adGroup` | 의 이름 [!DNL Adwords] 광고 그룹 |

{style=&quot;table-layout:auto&quot;}

이 데이터를 사용하여 만들기를 시작할 수 있습니다 [지표 ](../../../data-user/reports/ess-manage-data-metrics.md) 및 [보고서](../../../tutorials/using-visual-report-builder.md) 데이터 및 [ROI를 계산하기 위해 평생 매출에 맞춰](../../analysis/roi-ad-camp.md).

## 통합 테이블

항상 을(를) 만드는 것이 좋습니다 `consolidated ad spend` 표를 사용하여 여러 광고 소스의 데이터를 하나의 표로 결합할 수 있습니다. 이렇게 하면 광고 분석에 단일 지표 세트를 사용할 수 있습니다.

통합 테이블 없이, `adwords` 표를 만들려면 보고 데이터를 복제하거나 중복 지표를 만들어 데이터와 비교해야 합니다 [!DNL Facebook Ads] 데이터. 통합 테이블을 사용하면 원활하게 통합할 수 있습니다 [!DNL Facebook Ads] 기존 [!DNL Adwords] 보고서. (걱정하지 마십시오. - 광고 플랫폼별로 세그먼트화할 수 있습니다.)

위의 필드를 이미 동기화한 경우 Adobe에 연락하여 광고 비용을 통합하십시오.
