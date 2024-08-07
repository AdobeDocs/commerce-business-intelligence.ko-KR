---
title: 예상 Google Analytics 데이터
description: Google Analytics 지표와 상호 작용하는 방법을 알아봅니다.
exl-id: db9fdaaa-47a9-4095-b1f8-9b6c74c25b7c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# [!DNL Google Analytics]개의 데이터가 필요합니다.

[!DNL Google Analytics] 통합을 연결한 후 `Visual Report Builder`*에서 [!DNL Google Analytics] 지표*&#x200B;과(와) 즉시 상호 작용할 수 있습니다. `Visual Report Builder`을(를) 입력할 때 **[!UICONTROL Add a Metric]**&#x200B;을(를) 클릭하면 [!DNL Google Analytics] 프로필의 일련의 지표가 Data Warehouse의 지표 바로 아래에 드롭다운으로 표시됩니다.

[!DNL Google Analytics] 통합은 *live*&#x200B;입니다. 즉, 보고서에 지표를 추가할 때 `Report Builder`에서 [!DNL Google Analytics] *즉시*&#x200B;의 데이터를 요청합니다. 또한 액세스할 수 있는 지표가 [!DNL Google Analytics]에 있는 그대로 정의되었으며 이러한 값은 [!DNL Commerce Intelligence] 계정에 *웨어하우징*&#x200B;이 아닙니다. 보고서에 시각적으로만 표시됩니다.

+++지원되는 지표 및 Dimension(Google Analytics 3 또는 Universal Analytics)

>[!NOTE]
>
>2023년 7월 1일부터 표준 Universal Analytics([!DNL Google Analytics] 3) 속성은 더 이상 데이터를 처리하지 않습니다. 2023년 7월 1일 이후 일정 기간 동안 Universal Analytics 보고서를 볼 수 있습니다. 그러나 새 데이터는 [!DNL Google Analytics]개의 속성에만 전송됩니다.

[!DNL Commerce Intelligence]의 [!DNL Google Analytics] 통합에서 [!DNL Google Analytics] [Core Reporting API](https://developers.google.com/analytics/devguides/reporting/core/v3/)를 사용하고 다음 지표 및 차원을 지원합니다.

>[!NOTE]
>
>예기치 않거나 중요하지 않은 결과를 방지하려면 사용하는 모든 차원이 `Report Builder`에서 사용하는 하나 이상의 지표와 호환되는지 확인하십시오. [여기](https://ga-dev-tools.google/dimensions-metrics-explorer/)에서 확인할 수 있습니다.

## 지원되는 지표

| [!DNL Commerce Intelligence] 표시 이름 | [!DNL Google Analytics] 이름/공식 |
| --- | --- |
| `Page Views` | `ga:pageviews` |
| `Total Time Spent On Page` | `ga:timeOnPage` |
| `Bounces (One Page Visits)` | `ga:bounces` |
| `Entrances` | `ga:entrances` |
| `Exits` | `ga:exits` |
| `Unique Pageviews` | `ga:uniquePageviews` |
| `Ad Clicks` | `ga:adClicks` |
| `Ad Cost` | `ga:adCost` |
| `Cost per Click (CPC)` | `ga:CPC` |
| `Cost per Thousand Impressions (CPM)` | `ga:CPM` |
| `Click-Through Rate (CTR)` | `ga:CTR` |
| `Impressions` | `ga:impressions` |
| `Product Revenue` | `ga:itemRevenue` |
| `Products Purchased` | `ga:itemQuantity` |
| `Revenue` | `ga:transactionRevenue` |
| `Transactions` | `ga:transactions` |
| `Shipping Revenue` | `ga:transactionShipping` |
| `Tax Revenue` | `ga:transactionTax` |
| `Unique Purchases` | `ga:uniquePurchases` |
| `Pageviews After Internal Search` | `ga:searchDepth` |
| `Visit Duration After Internal Search` | `ga:searchDuration` |
| `Exits After Internal Search` | `ga:searchExits` |
| `Internal Search Refinements` | `ga:searchRefinements` |
| `Unique Users Using Internal Search` | `ga:searchUniques` |
| `Bounce Rate` | `ga:visitBounceRate` |
| `Average Time on Page` | `ga:avgTimeOnPage` |
| `Average Session Length` | `ga:avgSessionDuration` |
| `All Goals Conversion Rate` | `ga:goalConversionRateAll` |
| `Total Events` | `ga:totalEvents` |
| `Unique Events` | `ga:uniqueEvents` |
| `Event Value` | `ga:eventValue` |
| `Average Domain Lookup Time` | `ga:avgDomainLookupTime` |
| `Average Page Download Time` | `ga:avgPageDownloadTime` |
| `Average Page Load Time` | `ga:avgPageLoadTime` |
| `Transactions Per Visit` | `ga:transactionsPerVisit` |
| `Sessions` | `ga:sessions` |
| `Users` | `ga:users` |
| `New Users | ga:newUsers` |
| `Sessions Where Internal Search Used` | `ga:searchSessions` |
| `Goal X Starts` | `ga:goal...Starts` |
| `Goal X Completions` | `ga:goal...Completions` |
| `Goal X Conversion Rate` | `ga:goal...ConversionRate` |
| `Goal X Total Value` | `ga:goal...Value` |
| `All Goal Starts` | `ga:goalStartsAll` |
| `All Goal Completions` | `ga:goalCompletionsAll` |
| `All Goals Conversion Rate` | `ga:goalConversionRateAll` |
| `Total Goal Value` | `ga:goal1ValueAll` |

{style="table-layout:auto"}

## 지원되는 Dimension

| [!DNL Commerce Intelligence] 표시 이름 | [!DNL Google Analytics] 이름/공식 | 그룹화할 수 있습니까? |
| --- | --- | --- |
| `Ad Content` | `ga:adContent` | `Yes` |
| `Ad Group` | `ga:adGroup` | `Yes` |
| `Matched Search Query` | `ga:adMatchedQuery` | `Yes` |
| `Placement Domain` | `ga:adPlacementDomain` | `Yes` |
| `Placement URL` | `ga:adPlacementUrl` | `Yes` |
| `Affiliation` | `ga:affiliation` | `Yes` |
| `Browser` | `ga:browser` | `Yes` |
| `Browser Version` | `ga:browserVersion` | `Yes` |
| `Campaign` | `ga:campaign` | `Yes` |
| `Continent` | `ga:continent` | `Yes` |
| `Custom Variable 2` | `ga:customVarValue2` | `Yes` |
| `Custom Variable 3` | `ga:customVarValue3` | `Yes` |
| `Custom Variable 5` | `ga:customVarValue5` | `Yes` |
| `Date` | `ga:date` | `No` |
| `Day` | `ga:day` | `No` |
| `Days Since Last Session` | `ga:daysSinceLastSession` | `Yes` |
| `Days Since Referring Campagin` | `ga:daysToTransaction` | `Yes` |
| `Device Category` | `ga:deviceCategory` | `Yes` |
| `Custom Dimension 10` | `ga:dimension10` | `Yes` |
| `Custom Dimension 12` | `ga:dimension12` | `Yes` |
| `Custom Dimension 13` | `ga:dimension13` | `Yes` |
| `Custom Dimension 18` | `ga:dimension18` | `Yes` |
| `Custom Dimension 2` | `ga:dimension2` | `Yes` |
| `Custom Dimension 20` | `ga:dimension20` | `Yes` |
| `Custom Dimension 3` | `ga:dimension3` | `Yes` |
| `Custom Dimension 4` | `ga:dimension4` | `Yes` |
| `Custom Dimension 5` | `ga:dimension5` | `Yes` |
| `Custom Dimension 8` | `ga:dimension8` | `Yes` |
| `Custom Dimension 9` | `ga:dimension9` | `Yes` |
| `Event Action` | `ga:eventAction` | `Yes` |
| `Event Category` | `ga:eventCategory` | `Yes` |
| `Event Label` | `ga:eventLabel` | `Yes` |
| `Exit Page Path` | `ga:exitPagePath` | `Yes` |
| `Flash Version Supported` | `ga:flashVersion` | `Yes` |
| `Hour` | `ga:hour` | `No` |
| `In-Market Segment` | `ga:interestInMarketCategory` | `Yes` |
| `Language` | `ga:language` | `Yes` |
| `Longitude` | `ga:longitude` | `No` |
| `Medium` | `ga:medium` | `Yes` |
| `Metro` | `ga:metro` | `Yes` |
| `Mobile Device Branding` | `ga:mobileDeviceBranding` | `Yes` |
| `Mobile Device Info` | `ga:mobileDeviceInfo` | `Yes` |
| `Month` | `ga:month` | `No` |
| `Operating System` | `ga:operatingSystem` | `Yes` |
| `Operating System Version` | `ga:operatingSystemVersion` | `Yes` |
| `Pages Viewed per Session` | `ga:pageDepth` | `Yes` |
| `Page Path` | `ga:pagePath` | `Yes` |
| `Product Category` | `ga:productCategory` | `Yes` |
| `Product Name` | `ga:productName` | `Yes` |
| `Referral URL` | `ga:referralPath` | `No` |
| `Region (State)` | `ga:region` | `Yes` |
| `Screen Colors` | `ga:screenColors` | `Yes` |
| `Screen Resolution` | `ga:screenResolution` | `Yes` |
| `Internal Search Category` | `ga:searchCategory` | `Yes` |
| `Internal Search Refined Keyword(s)` | `ga:searchKeywordRefinement` | `Yes` |
| `Internal Search Used?` | `ga:searchUsed` | `Yes` |
| `Second Page Path` | `ga:secondPagePath` | `Yes` |
| `Source` | `ga:source` | `Yes` |
| `Sub-Continent` | `ga:subContinent` | `Yes` |
| `Transaction ID` | `ga:transactionId` | `Yes` |
| `Custom (User Defined) Value` | `ga:userDefinedValue` | `Yes` |
| `Year` | `ga:year` | `No` |

{style="table-layout:auto"}

+++

+++지원되는 지표 및 Dimension (Google Analytics 4)

[!DNL Commerce Intelligence]의 [!DNL Google Analytics] 통합에서 [!DNL Google Analytics] [데이터 API v1(GA4)](https://developers.google.com/analytics/devguides/reporting/data/v1)을(를) 사용합니다.

>[!NOTE]
>
> Commerce Intelligence은 `cohort`, `cohortNthDay`, `cohortNthMonth` 및 `cohortNthWeek` 차원을 지원하지 않습니다.
>
>예기치 않거나 중요하지 않은 결과를 방지하려면 사용하는 모든 차원이 `Visual Report Builder`에서 사용하는 하나 이상의 지표와 호환되는지 확인하십시오. [GA4 Dimension 및 지표 탐색기](https://ga-dev-tools.google/ga4/dimensions-metrics-explorer/)를 확인할 수 있습니다.

+++
