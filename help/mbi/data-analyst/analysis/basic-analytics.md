---
title: 기본 분석 이해 및 구축
description: 기본 분석을 이해하고 구축하는 방법을 알아봅니다.
exl-id: 23cea7b3-2e66-40c3-b4bd-d197237782e3
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '3142'
ht-degree: 0%

---

# 기본 Analytics

익숙해지면 [!DNL MBI] 플랫폼 및 도구에 대한 기본적인 이해를 바탕으로 보고서 작성을 시작할 수 있습니다. 여러분이 가질 수 있는 가장 일반적인 질문 중 하나는 &quot;내가 무엇을 봐야 하는가?&quot; 입니다.

아래 정보에서는 유용할 수 있는 몇 가지 일반적인 지표 및 보고서에 대해 간략하게 설명합니다. 이러한 보고서 중 일부가 계정 내에 이미 있으므로 중복 항목을 생성하지 않도록 계정 내에 있는 지표와 보고서를 검토하십시오.

## 이해할 테이블 및 열

지표를 작성할 때에는 네 가지 정보를 알고 있어야 합니다.

1. 데이터가 있는 테이블
1. 수행할 특정 작업
1. 해당 작업을 수행할 열 및
1. 해당 데이터 추적에 사용할 타임스탬프입니다.

이러한 예에서 사용하는 테이블의 이름은 각 데이터베이스가 고유하므로 데이터베이스의 열 및 테이블 이름과 약간 다릅니다. 데이터베이스에서 해당 테이블 또는 열을 식별하는 데 도움이 필요한 경우 아래 정의를 참조하십시오.

## 고객 테이블

이 표에는 고유한 고객 ID, 이메일 주소, 계정 생성 날짜 등 각 고객에 대한 주요 정보가 포함되어 있습니다. 아래 예에서는 **[!UICONTROL customer_entity]** 샘플 고객 테이블의 이름으로 사용됩니다.

이러한 계산 중 일부가 현재 데이터베이스에 없는 경우 계정의 모든 관리자가 이러한 계산을 작성할 수 있습니다. 또한 이러한 차원이 적용 가능한 모든 지표에 대해 그룹화할 수 있는지 확인해야 합니다.

**Dimension**

* **[!UICONTROL Entity_id]**: 각 고객에 대한 고유 식별자입니다. 고유한 고객 번호 또는 고객 이메일 주소일 수 있으며, 주문 테이블의 참조 키로 기능해야 합니다.
* **[!UICONTROL Created_at]**: 고객 계정이 생성되어 데이터베이스에 추가된 날짜입니다.
* **[!UICONTROL Customer's lifetime revenue]**: 고객이 생성한 총 라이프타임 수입입니다.
* **[!UICONTROL Customer's first 30-day revenue]**: 첫 30일 동안 고객이 생성한 총 매출액.
* **[!UICONTROL Customer's lifetime number of orders]**: 고객이 라이프타임 동안 수행한 주문 수입니다.
* **[!UICONTROL Customer's lifetime number of coupons]**: 고객이 라이프타임 동안 사용한 총 쿠폰 수입니다.
* **[!UICONTROL Customer's first order date]**: 고객의 첫 번째 주문 날짜입니다. 고객이 생성 시 주문을 하지 않은 경우 created_at 날짜와 다를 수 있습니다.

**손님주문을 받나요?**

*이 경우 이 테이블에 모든 고객이 포함되지 않을 수 있습니다. 연락처 [지원 팀](https://support.magento.com/hc/en-us/articles/360016503692) 고객 분석에 모든 고객이 포함되었는지 확인합니다.*

*손님주문을 수락하는지 확실하지 않습니까? 을(를) 참조하십시오. [이 항목](../data-warehouse-mgr/guest-orders.md) 자세히 알아보기*

## 주문 테이블

이 테이블에서 각 행은 하나의 순서를 나타냅니다. 이 테이블의 열에는 주문 ID, 생성 날짜, 상태, 주문을 수행한 고객 ID 등과 같은 각 주문에 대한 기본 정보가 포함됩니다. 아래 예에서는 **[!UICONTROL sales_flat_order]** 는 샘플 주문 테이블의 이름으로 사용됩니다.

**Dimension**

* **[!UICONTROL Customer_id]**: 주문을 한 고객의 고유 식별자입니다. 종종 고객과 주문 테이블 간에 정보를 이동하는 데 사용됩니다. 예제에서는 customer_id 를 **[!UICONTROL sales_flat_order]** 맞춤 테이블 **[!UICONTROL entitiy_id]** on **[!UICONTROL customer_entity]** 테이블.
* **[!UICONTROL Created_at]**: 주문이 생성되거나 실행된 날짜입니다.
* **[!UICONTROL Customer_email]**: 주문을 한 고객의 이메일 주소입니다. 고객의 고유 식별자일 수도 있습니다.
* **[!UICONTROL Customer's lifetime number of orders]**: 열 사본이 `Customers` 테이블.
* **[!UICONTROL Customer's order number]**: 주문과 연관된 고객의 순차적 주문 번호입니다. 예를 들어 보고 있는 행이 고객의 첫 번째 주문인 경우 이 열은 &quot;1&quot;입니다. 그러나 고객의 15번째 주문인 경우 이 열에 &quot;15&quot;가 표시됩니다. 이 차원이 `Customers` 테이블 [지원 팀](https://support.magento.com/hc/en-us/articles/360016503692) 빌드하는 데 도움이 됩니다.
* **[!UICONTROL Customer's order number (previous-current)]**: 에서 두 값의 연결 **[!UICONTROL Customer's order number]** 열. 아래 샘플 보고서에서 두 주문 사이의 경과 시간을 표시하는 데 사용됩니다. 예를 들어, 고객의 첫 번째 주문 일자와 두 번째 주문 일자 사이의 시간은 이 계산에서 &quot;1-2&quot;로 표시됩니다.
* **[!UICONTROL Coupon_code]**: 각 주문에 사용된 쿠폰을 표시합니다.
* **[!UICONTROL Seconds since previous order]**: 고객의 주문 사이의 시간(초)입니다.

## 주문 품목 테이블

이 테이블에서 각 행은 판매된 하나의 항목을 나타냅니다. 이 테이블에는 주문 참조 번호, 제품 번호, 수량 등과 같이 각 주문으로 판매된 품목에 대한 정보가 포함되어 있습니다. 아래 예에서는 `sales_flat_order_item` 는 샘플 주문 품목 테이블의 이름으로 사용됩니다.

**Dimension**

* **[!UICONTROL Item_id]**: 테이블의 각 행에 대한 고유 식별자입니다.
* **[!UICONTROL Order_id]**: 에 대한 참조 키 `Orders` 동일한 순서로 구매한 항목을 알려주는 테이블입니다. 주문에 여러 항목이 포함되어 있는 경우 이 값이 반복됩니다.
* **[!UICONTROL Product_id]**: 구입한 특정 제품(예: 색상, 크기 등)에 대한 정보를 원하는 경우 이 열을 사용하여 제품 테이블에서 해당 정보를 가져옵니다.
* **[!UICONTROL Order's created_at]**: 주문이 배치된 타임스탬프이며, 일반적으로 `order line items` 표 `Orders` 테이블.
* **[!UICONTROL Order's coupon_code]**: 와 비슷합니다 `Order's created_at` 차원. 이 열은 주문 테이블에서 복사됩니다.

## 가입 테이블

이 표는 구독 ID, 구독자의 이메일 주소, 구독 시작 날짜 등과 같은 구독 정보를 관리하는 데 사용됩니다.

**Dimension**

* **[!UICONTROL Customer_id]**: 주문을 한 고객의 고유 식별자입니다. Customers 테이블과 Orders 테이블 간의 경로를 만드는 일반적인 방법입니다. 예제에서는 customer_id 를 **sales_flat_order** 맞춤 테이블 `entitiy_id` on `customer_entity` 테이블.
* **[!UICONTROL Start date]**: 고객의 구독이 시작된 날짜입니다.

## 마케팅 지출 테이블

마케팅 비용을 분석할 때 다음을 포함할 수 있습니다 [!DNL Facebook], [!DNL Google AdWords]또는 분석 시 다른 소스를 확인할 수 있습니다. 마케팅 비용 소스가 여러 개인 경우 Adobe에 문의하십시오 [서비스 팀](https://business.adobe.com/products/magento/fully-managed-service.html) 를 참조하십시오.

**Dimension**

* **[!UICONTROL Spend]**: 총 광고 지출입니다. in [!DNL Facebook]로 지정하는 경우, `facebook_ads_insights_####` 테이블. 대상 [!DNL Google AdWords]이렇게 되면 `adCost` 열 `campaigns####` 테이블.
* 다음 `####` 다음 각 표에 추가되되, 사용자의 특정 계정 ID와 관련이 있습니다 [!DNL Facebook] 또는 [!DNL Google AdWords] 계정이 필요합니다.
* **[!UICONTROL Clicks]**: 총 클릭 수입니다. in [!DNL Facebook]를 채울 수 있습니다. `facebook_ads_insights_####` 테이블. in [!DNL Google AdWords]를 채울 수 있습니다. `campaigns####` 테이블.
* **[!UICONTROL Impressions]**: 총 노출 횟수. in [!DNL Facebook]의 노출 횟수로서, `facebook_ads_insights_####` 테이블. in [!DNL Google AdWords]에 대한 노출 횟수는 다음과 같습니다. `campaigns####` 테이블.
* **[!UICONTROL Campaign]**: 총 클릭 수입니다. in [!DNL Facebook]를 채울 때 `facebook_ads_insights_####` 테이블. in [!DNL Google AdWords]를 채울 수도 있습니다. `campaigns####` 테이블.
* **[!UICONTROL Date]**: 특정 캠페인에 대해 사용한 시간, 클릭 또는 노출이 발생한 타임스탬프입니다. in [!DNL Facebook]이렇게 되면 `date_start` 열 `facebook_ads_insights_####` 테이블. in [!DNL Google AdWords]의 날짜 열은 `campaigns####` 테이블.
* **[!UICONTROL Customer's first order's source]**: 고객의 첫 번째 주문에서 주문된 주문입니다. 먼저 이름이 인 열이 있는지 확인합니다 `customer's first order's source` 내 계정에 있을 때 이 열이 표시되지 않으면 이러한 지침을 사용하여 원하는 열을 만들 수 있습니다.
* **[!UICONTROL Customer's first order's medium]**: 주문서는 고객의 첫 주문에서 나온 미디엄입니다. 먼저 이름이 인 열이 있는지 확인합니다 `customer's first order's source` 내 계정에 있을 때 이 열이 표시되지 않으면 이러한 지침을 사용하여 원하는 열을 만들 수 있습니다.
* **[!UICONTROL Customer's first order's campaign]**: 고객의 첫 번째 주문에서 주문 캠페인. 먼저 이름이 인 열이 있는지 확인합니다 `customer's first order's source` 내 계정에 있을 때 이 열이 표시되지 않으면 이러한 지침을 사용하여 원하는 열을 만들 수 있습니다.

## 일반적인 보고서 및 지표

다음은 유용한 보고서 및 지표에 대한 몇 가지 일반적인 예입니다.

* [Customer Analytics](#customeranalytics)
* [Order Analytics](#orderanalytics)
* [마케팅 비용 분석](#mktgspendanalytics)

## 고객 분석 {#customeranalytics}

### 새 사용자

* **설명**: 주어진 기간 동안 새로 획득한 사용자의 총 수입니다. `New Users` 과(와) 다릅니다. `Unique Customers`, `New Users` 에는 서비스를 사용하여 계정을 만든 타임스탬프가 있습니다. 이는 사용자가 반드시 주문을 해야 함을 의미하지는 않습니다 `Unique Customers` 적어도 하나 이상의 주문을 했습니다.
* **지표 정의**: 이 지표는 다음을 수행합니다 **카운트** 의 `entity_id` 변환 전: `customer_entity` 테이블 정렬 기준 `created_at`.
* **보고서 예**: 지난 달에 만든 새 사용자 수
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Time Range]**: `Last Month`
   * **[!UICONTROL Time Interval]**: `By Day`

![새 사용자](../../assets/New_Users_Last_Month.png)<!--{: width="929"}-->

### 고유 고객 수

* **설명**: 지정된 기간 동안의 총 고유 고객 수 카운트입니다. 이것은 `New Users`하나 이상의 주문을 수행한 고객만 추적하므로 개별 고객 보고서는 지정된 시간 간격으로 고객을 한 번만 추적합니다. 시간 간격을 로 설정하면 `By Day` 그리고 그 날 두 번 이상 고객이 구매하면 한 번만 카운트됩니다. 일반적으로 총 구매 횟수를 보려면 `Number of Orders`.
* **지표 정의**: 이 지표는 다음을 수행합니다 **고유 개수** 의 `customer_id` 변환 전: `sales_flat_order` 테이블 정렬 기준 `created_at`.
* **보고서 예**: 지난 90일 동안 주별 개별 고객
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Time Range]**: `Moving range > Last 90 Days`
   * **[!UICONTROL Time Interval]**: `By Day`

![고유 고객 수.](../../assets/Unique_customers_last_7_days.png)<!--{: width="929"}-->

### 새 구독자

* **설명**: 지정된 기간 동안 취득한 새 구독자의 총 수 카운트입니다.
* **지표 정의**: 이 지표는 다음을 수행합니다 **고유 개수** 의 `customer_id` 변환 전: `subscriptions` 테이블 정렬 기준 `start_date`.
* **보고서 예**: 올해 월별 신규 가입자
   * **[!UICONTROL Metric]**: `New Subscribers`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 0 Days Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

![구독자](../../assets/New_Subscribers_This_Year_by_Month.png)<!--{: width="929"}-->

### 반복 고객

* **설명**: 일정 기간 동안 두 개 이상의 주문을 한 총 고객 수입니다. 반복 고객 보고서에서 `Distinct Customers` 지표 및 `Customer's Order Number` 차원 `orders` 테이블.
* **사용된 지표**: `Distinct Customers`
* **보고서 예**: 작년에 수행한 2차 및 3차 구매 수
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Time Range]**: `Moving Range > Last Year`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Group By]**: `Customer's Order Number`를 선택하고 을 선택합니다. `2` 및 `3`

   ![](../../assets/2nd_and_3rd_purchases_last_year.png)

* **보고서 예제 2**: 작년에 반복 고객 수
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Filters]**: `Customer's Order Number Greater Than 1`
   * **[!UICONTROL Time Range]**: `Moving range > Last Year`
   * **[!UICONTROL Time Interval]**: `By Month`

   ![지난해 반복 고객](../../assets/Repeat_customers_last_year.png)<!--{: width="929"}-->

### 라이프타임 주문 수별 상위 고객

* **설명**: 총 주문 수를 기반으로 하는 상위 고객 목록입니다. 이렇게 하면 가장 자주 이용하는 고객 목록이 표시됩니다.
* **사용된 지표**: `Orders`
* **보고서 예**: 라이프타임 주문 수별 상위 25개 고객
   * **[!UICONTROL Metric]**: `Orders`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `customer_email`
   * **[!UICONTROL Show Top/Bottom]**: 주문별로 정렬된 상위 25개

   ![주문별 상위 25개 고객](../../assets/Top_25_customers_by_lifetime_orders.png)<!--{: width="929"}-->

### 라이프타임 수입별 상위 고객

* **설명**: 라이프타임 매출을 기반으로 한 주요 고객 목록입니다.
* **사용된 지표**: `Average Lifetime Revenue`
* **보고서 예**: 라이프타임 수입별 상위 25개 고객
   * **[!UICONTROL Metric]**: `Average Lifetime Revenue`
   * **[!UICONTROL Time Range]**: `All time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `customer_email`
   * **[!UICONTROL Show Top Bottom]**: 라이프타임 매출별로 분류된 상위 25개

   ![매출액별 상위 25개 고객](../../assets/top_25_customers_by_lifetime_revneue.png)<!--{: width="929"}-->

### 집단별 평균 라이프타임 매출

* **설명**: 추적 [개별 집단에 대한 평균 라이프타임 매출](../dev-reports/lifetime-rev-cohort-analysis.md) 시간 경과에 따라 사용자를 식별하여 성과가 가장 좋은 집단을 식별합니다. 집단은 첫 번째 주문 날짜 또는 생성 날짜와 같은 공통 날짜별로 그룹화됩니다.
* **사용된 지표**: `Revenue`
* **보고서 예**: 집단별 평균 고객 생애 매출
   * **[!UICONTROL Metric]**: `Revenue`
   * **[!UICONTROL Cohort Date]**: `Customer's first order date`
   * **[!UICONTROL Time Interval]**: `Month`
   * **[!UICONTROL Time Period]**: 최소 4개월 데이터의 최근 8개 집단 중 집단 이동
   * **[!UICONTROL Duration]**: `12 Month(s)`
   * **[!UICONTROL Table]**: `Customer_entity`
   * **[!UICONTROL Perspective]**: 집단 멤버당 누적 평균 값

   ![집단별 고객 생애 매출](../../assets/Avg_customer_lifetime_revenue_by_cohort.png)<!--{: width="929"}-->

### 쿠폰 사용별 고객

* **설명**: 쿠폰/할인 코드를 사용한 고객 수 계산. 이렇게 하면 할인 구매자와 전체 가격 구매자를 정확하게 파악할 수 있습니다.
* **사용된 지표**: `New Users`
* **보고서 예**: 월별 쿠폰 및 비쿠폰 고객
   * **[!UICONTROL Metric A]**: `Non coupon customers`
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Filters]**: 고객의 라이프타임 주문 수가 0보다 크고 고객의 라이프타임 쿠폰 수는 0입니다.
   * **[!UICONTROL Metric B]**: `Coupon customers`
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Filters]**: 고객 라이프타임 0보다 큰 주문 수 및 0보다 큰 고객의 라이프타임 쿠폰 수
   * **[!UICONTROL Time range]**: `All Time`
   * **[!UICONTROL Time interval]**: `By Month`

   ![쿠폰 사용별 고객](../../assets/Customers_by_coupon_usage.png)<!--{: width="929"}-->

* **보고서 예제 2**: 월별 쿠폰 및 비쿠폰 고객 비율
   * **[!UICONTROL Metric A]**: `Non coupon customers` (지표 숨기기)
      * **[!UICONTROL Metric]**: `New Users`
      * **[!UICONTROL Filters]**: `Customer's Lifetime Number of Orders Greater Than 0` 및 `Customer's Lifetime Number of Coupons Equal to 0`
   * **[!UICONTROL Metric B]**: `Coupon customers`
      * **[!UICONTROL Metric]**: `New Users`
      * **[!UICONTROL Filters]**: `Customers Lifetime Number of Orders Greater Than 0` 및 `Customer's Lifetime Number of Coupons Greater Than 0`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Formula]**: `B/(A+B)`

>[!NOTE]
>
> **모든 지표 숨기기**

![쿠폰 사용](../../assets/Customers_by_coupon_usage_formula.png)<!--{: width="929"}-->

### 평균 처음 30일 매출

* **설명**: 고객으로서 처음 30일 이내에 고객이 생성한 매출액의 평균.
* **지표 설명**: 이 지표는 다음을 수행합니다 **평균** 의 `Customer's First 30 Day Revenue` 변환 전: `customer_entity` 테이블 정렬 기준 `created_at`.
* **보고서 설명**: 고객의 최초 30일 매출에 대한 모든 시간 평균
* **[!UICONTROL Metric]**: `Average First 30 Day Revenue`
* **[!UICONTROL Time Range]**: `All Time`
* **[!UICONTROL Time Interval]**: `None`

![평균 최초 30일 매출](../../assets/Avg_first_30_day_revenue.png)<!--{: width="929"}-->

### 평균 고객 생애 매출

* **설명**: 라이프타임 동안 고객이 생성한 평균 매출액.
* **지표 설명**: 이 지표는 다음을 수행합니다 **평균** 의 `Customer's Lifetime Revenue` 열 `customer_entity` 테이블 기준 `created_at`.
* **보고서 설명**: 고객의 라이프타임 매출에 대한 모든 시간 평균
   * **[!UICONTROL Metric]**: `Average Customer Lifetime Revenue`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `None`

![고객 생애 매출](../../assets/Avd_customer_lifetime_revenue_.png)<!--{: width="929"}-->

## Order analytics {#orderanalytics}

### 매출

* **설명**: 수입 지표는 선택한 기간 동안 발생한 총 매출액을 표시합니다.
* 이 지표는 다음을 수행합니다 **sum** 의 `grand_total` 변환 전: `sales_flat_order` 테이블 정렬 기준 `created_at`.
* **보고서 예**: 월별 수입, YTD
   * **[!UICONTROL Metric]**: `Revenue`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **시간 간격**: `By Month`

>[!TIP]
>
>수입 지표의 계산이 내부적으로 설명하는 정의와 일치하는지 확인합니다. 예를 들어 출하된 주문에서 수익만 계산하려는 경우, 다른 지역에서 통화를 변환해야 할 수 있으며, 세금을 제외할 수 있습니다. 또한 [필터 세트](../../data-user/reports/ess-manage-data-filters.md) 를 사용하여 동일한 표에 작성된 모든 지표 간에 일관성을 유지할 수 있습니다.

![매출](../../assets/revenue.png)<!--{: width="929"}-->

### 주문

* **설명**: 지정된 기간 동안의 총 주문 수의 카운트입니다. 주문 보고서는 신규 제품 제공, 프로모션 또는 트랜잭션 볼륨을 증가(또는 감소)할 수 있는 그 밖의 모든 것으로 인해 주문 볼륨의 변경 사항을 추적합니다. 종종 질문에 답변하기 위해 많은 변수별로 이 지표를 세그먼트화하려는 경우가 있습니다.
* **지표 정의**: 이 지표는 다음을 수행합니다 **카운트** 의 `entity_id` 변환 전: `sales_flat_order` 테이블 정렬 기준 `created_at`.
* **보고서 예**: 월별 주문, YTD
   * **[!UICONTROL Metric]**: `number of orders`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

>[!TIP]
>
>매출 지표와 마찬가지로 [필터 세트](../../data-user/reports/ess-manage-data-filters.md) 미완료, 테스트 또는 반환된 주문을 제외하기 위해 사용됩니다.

![주문](../../assets/orders_pic.png)<!--{: width="929"}-->

### 주문 제품

* **설명**: 제품 주문 지표는 특정 기간 동안 판매된 품목의 수량을 알려줍니다.
* **지표 정의**: 이 지표는 다음을 수행합니다 **sum** 의 `qty_ordered` 변환 전: `sales_flat_order_item` 테이블 정렬 기준 `created_at`.
* **보고서 예**: 월별 판매량, 연간
   * **[!UICONTROL Metric]**: `Products ordered`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

   ![주문된 제품](../../assets/products_ordered_pic1.png)<!--{: width="929"}-->

* 이 지표를 주문 수 지표와 결합하여 주문당 항목 수를 계산합니다. 다음으로, 보고서에 쿠폰 코드를 추가하여 판촉 행사가 장바구니 크기에 미치는 영향을 결정하거나 신규 주문과 반복 주문별로 세그먼트화하여 고객 행동을 더 잘 이해할 수 있습니다.
* **보고서 예**: 주문당 제품: 첫 번째 주문과 반복 주문
   * **[!UICONTROL Metric A]**: 주문 제품: 첫 번째 주문
      * **[!UICONTROL Metric]**: `Products ordered`
      * **[!UICONTROL Filter]**: `Customer's order number = 1`
   * **[!UICONTROL Metric B]**: 주문: 첫 번째 주문
      * **[!UICONTROL Metric]**: `Orders`
      * **[!UICONTROL Filter]**: `Customer's order number = 1`
   * **[!UICONTROL Metric C]**: 주문 제품: 반복 주문
      * **[!UICONTROL Metric]**: `Products ordered`
      * **[!UICONTROL Filter]**: `Customer's order number > 1`
   * **[!UICONTROL Metric D]**: 주문: 반복 주문
      * **[!UICONTROL Metric]**: `Orders`
      * **[!UICONTROL Filter]**: `Customer's order number > 1`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Week`
   * **[!UICONTROL Formula 1]**: `A/B`
   * **[!UICONTROL Formula 2]**: `C/D`

>[!NOTE]
>
>선택을 취소하고 `Multiple Y-Axes box` 및 `Hide` 모든 지표

![주문 제품 2](../../assets/products_ordered_pic2.png)<!--{: width="929"}-->

### 평균 주문 가격

* **설명**: 일정 기간 동안 수행한 주문의 평균 값을 추적합니다. 이 지표를 사용하여 마케팅 활동, 제품 서비스 및/또는 비즈니스의 기타 변경으로 인해 AOV(평균 주문 가격)가 어떻게 변했는지 신속하게 확인할 수 있습니다.
* **지표 정의**: 이 지표는 다음을 수행합니다 **평균** 의 `grand_total` 변환 전: `sales_flat_order` 테이블 정렬 기준 `created_at`.
* **보고서 예**: AOV와 이전 연도, YTD
   * **[!UICONTROL Metric]**: `Average order value`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Perspective]**: `Amount Change vs Previous Year`

   ![AOV](../../assets/aov_pic.png)<!--{: width="929"}-->

### 쿠폰으로 가장 많이 구입한 제품

* **설명**: 이 보고서는 프로모션 또는 쿠폰을 제공할 때 판매되는 제품에 대한 통찰력을 제공합니다.
* **사용된 지표**: 주문 제품
* **보고서 예**: 쿠폰으로 가장 많이 구입한 제품
   * **[!UICONTROL Metric]**: `Products ordered`
   * **[!UICONTROL Filter]**: `Order's coupon_code Is Not \[NULL\]`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By**]: `name` 또는 `SKU`, 또는 기타 제품 식별자 ).
   * **[!UICONTROL Show top/bottom]**: 주문된 제품별로 정렬된 상위 25개

   ![쿠폰이 있는 제품](../../assets/prod_coupons_pic.png)<!--{: width="929"}-->

### 주문 간 시간

* **설명**: 고객의 구매 주기에 대한 가정 및 기대치를 **주문 간 시간** 평균을 보는 분석(또는 중간값!) 구매 사이의 시간입니다. 아래 차트에서는, 3개 이상의 주문을 하는 우수 고객 - 이 6개월 이내에 두 번째 구매를 수행하는 것을 볼 수 있습니다. 네 번째 주문을 하지 않은 고객은 두 번째 구매를 하기 전에 14개월 대기합니다.
* **지표 정의**: 이 지표는 다음을 수행합니다 **평균** 의 `Time since previous order` 변환 전: `sales_flat_order` 정렬 기준 `created_at`.
* **보고서 예**:
   * **지표 1**: ≤ 3 주문
      * **[!UICONTROL Metric]**: `Average time between orders`
      * **[!UICONTROL Filter]**: `Customer's lifetime number of orders ≤ 3`
   * **지표 2**: > 3개 주문
      * **[!UICONTROL Metric]**: `Average time between orders`
      * **[!UICONTROL Filter]**: `Customer's lifetime number of orders > 3`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**:` Customer's order number (previous-current)`

>[!NOTE]
>
>선택을 취소하고 `Multiple Y-Axes` 상자.

![주문 간 시간](../../assets/time_bw_orders_pic.png)<!--{: width="929"}-->

## 마케팅 비용 분석 {#mktgspendanalytics}

### 광고 비용

* **설명**: 캠페인, 광고 세트 또는 기타 세그먼테이션별로 다양한 시간 및 간격 동안 마케팅 비용을 분석할 수 있습니다.
* **지표 정의**: 이 지표는 페이지의 `Marketing Spend` 테이블 `date` 열.
* **보고서 예**: 캠페인별 광고 비용
   * **[!UICONTROL Metric]**: `Ad spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `campaign`

![광고 비용](../../assets/ad_spend.png)<!--{: width="929"}-->

### 광고 노출 횟수 및 광고 클릭 수

* **설명**: 광고 비용을 분석하는 것 외에도 광고 노출 수 및 광고 클릭 수를 분석할 수 있습니다.
* **지표 정의**: 이 지표는 페이지의 `Marketing Spend` 날짜 열별로 정렬된 테이블.
* **보고서 예**: 일별 노출 횟수 및 광고 클릭 수 추가
   * **[!UICONTROL Metric A]**: `Ad impressions`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 3 Months Ago`
   * **[!UICONTROL Time Interval]**: `By Day`

   ![광고 노출 횟수](../../assets/ad_impressions.png)<!--{: width="929"}-->

### 클릭스루 비율(CTR)

* **설명**: 위에서 만든 광고 노출 횟수 및 광고 클릭 수 지표를 사용하면 시간에 따라 다른 캠페인별로 클릭스루 비율을 분석할 수 있습니다.
* **보고서 예**: 캠페인별 CTR
   * **[!UICONTROL Metric A]**: `Ad impressions`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**:`All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `B/A`
   * 을(를) 선택합니다 `%` 선택 사항입니다.
   * **[!UICONTROL Group By]**: `campaign`

>[!NOTE]
>
>다음을 수행할 수 있습니다 **제목** 수식 `CTR`, 및 **숨기기** 모든 지표.

![CTR](../../assets/CTR.png)<!--{: width="929"}-->

### 클릭당 비용(CPC)

* **설명**: 위에서 만든 광고 비용 및 광고 클릭 지표를 사용하면 시간에 따라 다른 캠페인으로 클릭당 비용을 분석할 수 있습니다.
* **보고서 예**: 캠페인별 CPC
   * **[!UICONTROL Metric A]**: `Ad spend`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `A/B`
   * 을(를) 선택합니다 `currency` 옵션
   * **[!UICONTROL Group By]**: `campaign`

>[!NOTE]
>
>다음을 수행할 수 있습니다 **제목** 수식 `CPC`, 및 **숨기기** 모든 지표.

![CPC](../../assets/CPC.png)<!--{: width="929"}-->

### 획득 소스별 고객

* **설명**: 를 사용하여 주문의 소스, 미디어 및 캠페인을 추적하는 경우 [!DNL Google eCommerce]를 입력하면 고객 확보 소스별로 고객을 분석할 수 있습니다. 이 URL을 통해 고객을 확보하고 있는 마케팅 소스를 확인하고 &quot;대부분의 고객이 첫 번째 주문을 하고 있습니까&quot;와 같은 질문에 답변할 수 있습니다 [!DNL Google], [!DNL Facebook]또는 다른 소스를 사용할 수 있습니까?&quot;
* **보고서 예**: 획득 소스별 고객
   * **[!UICONTROL Metric Used]**: `New Customers`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Group By]**: `Customer's first order's source`

>[!NOTE]
>
>체크 아웃 [이 문서](../analysis/most-value-source-channel.md) 획득 소스를 사용한 보고서에 대한 자세한 예

![획득 소스](../../assets/acquisition_source.png)<!--{: width="929"}-->

### 획득 매체 및 획득 캠페인별 고객

* **설명**: 획득 소스별 고객 분석과 유사하게 첫 번째 주문의 미디어 및 캠페인으로 고객을 분석할 수도 있습니다. 이를 통해 &quot;신규 고객을 유치하고 있는 캠페인&quot;과 같은 질문에 답변할 수 있습니다.
* **보고서 예**: 유료 매체를 사용한 획득 캠페인별 고객
   * **[!UICONTROL Metric Used]**: `New customers`
   * **[!UICONTROL Filter]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `Customer's first order's campaign`

>[!NOTE]
>
>에 있는 필터 `New Customers` 지표를 사용하면 cpc 또는 유료 검색과 같이 비즈니스에 대해 &quot;유료&quot; 미디어로 간주되는 다른 모든 미디어를 추가할 수 있습니다.

![획득 매체](../../assets/acquisition_medium.png)<!--{: width="929"}-->

### 고객 확보 비용(CAC) 또는 취득당 비용(CPA)

* **설명**: 캠페인 비용을 분석하는 한 가지 방법은 모든 비용을 캠페인을 통해 획득한 고객에게만 적용하는 것입니다.
* **보고서 예**: 캠페인별 CAC
   * **[!UICONTROL Metric A]**: `New customers`
   * **[!UICONTROL Filter]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Ad Spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `B/A`
   * 을(를) 선택합니다 `currency` 옵션
   * **[!UICONTROL Group By]**:
      * 지표 `A`, 선택 `Customer's first order's campaign`
      * 지표 `B`, 선택 `campaign`

   ![새 사용자.](../../assets/New_Users_Last_Month.png)

>[!NOTE]
>
>다음을 수행할 수 있습니다 **제목** 수식 `CTR`, 및 **숨기기** 모든 지표. 또한, [이 문서](../analysis/roi-ad-camp.md) 추가 정보.

![CAC 1](../../assets/New_Users_Last_Month.png)

![CAC 2](../../assets/cac-2.png)

### 획득 소스, 미디어 및 캠페인별 라이프타임 값

* **설명**: 각 캠페인에서 획득한 고객 수를 분석하여 이러한 고객의 평균 라이프타임 수익을 분석할 수 있습니다. 이 정보는 다음을 식별하는 데 도움이 됩니다.
   * 특정 캠페인이 많은 고객을 유치하지만 고객의 라이프타임 값은 낮은 경우
   * 특정 캠페인이 적은 수의 고객을 유치하지만 고객의 라이프타임 가치는 높습니다.
* **보고서 예**: 먼저 을(를) 추가합니다 `New customers` 지표. 그런 다음 `Average lifetime revenue` 지표. 원하는 시간대를 선택하고 `interval` 로서의 `None`. 마지막으로 `group by` 옵션`Customer's first order's campaign`.
   * **[!UICONTROL Metric A]**: `New Customers`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Average lifetime revenue`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `Customer's first order's campaign`

>[!NOTE]
>
>두 필터의 경우 cpc 또는 유료 검색과 같이 비즈니스에 대해 &quot;유료&quot; 미디어로 간주되는 다른 모든 매체를 추가할 수 있으며, Facebook과 같이 분석할 다른 소스를 추가할 수 있습니다. 또한, [이 문서](../analysis/roi-ad-camp.md) 를 참조하십시오.

![획득 소스, 미디어 및 캠페인별 라이프타임 값](../../assets/LTV_2.png)<!--{: width="929"}-->

### 투자 수익률(ROI)

* **설명**: 캠페인별 ROI를 계산하는 한 가지 방법은 캠페인을 통해 수행한 모든 주문을 분석하는 것입니다. 그러나 다른 방법은 캠페인을 통해 획득한 고객의 라이프타임 값을 분석하는 것입니다. ROI를 분석하려면 지출 데이터 및 트랜잭션 데이터에서 캠페인 이름이 일관되어야 합니다. 다음 보고서를 만들고 일치하지 않는 캠페인 이름으로 인해 ROI 값이 없는 경우 [UTM 태깅](../../best-practices/utm-tagging-google.md) 구현했습니다.
* **보고서 예**: 캠페인별 ROI
   * **[!UICONTROL Metric A]**: `New Customers`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Average lifetime revenue`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric C]**: `Ad spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `(B-(C/A))/(C/A)`
   * 을(를) 선택합니다 `% `옵션
   * **[!UICONTROL Group By]**:
      * 지표 `A` 및 `B`, 선택 `Customer's first order's campaign`
      * 지표 `C`, 선택 `campaign`

>[!NOTE]
>
>공식의 제목을 &quot;ROI&quot;로 지정하고 모든 지표를 숨길 수 있습니다. 또한 지표에서 필터를 조정하여 대체 소스 및 매체를 분석할 수 있습니다. 또한, [이 문서](../analysis/roi-ad-camp.md) 를 참조하십시오.

![ROI 1](../../assets/ROI_1.png)<!--{: width="929"}-->

![ROI 2](../../assets/ROI_2.png)<!--{: width="929"}-->
