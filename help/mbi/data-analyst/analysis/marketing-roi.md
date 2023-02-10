---
title: 마케팅 ROI
description: 총계 및 캠페인별로 ROI를 포함하여 채널 분석을 추적할 대시보드를 설정하는 방법을 알아봅니다.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# 마케팅 ROI

>[!NOTE]
>
>이 문서에는 원래 아키텍처와 새로운 아키텍처를 활용하는 고객을 위한 지침이 포함되어 있습니다. 다음 단계에 있습니다. [새로운 아키텍처](../../administrator/account-management/new-architecture.md) 기본 도구 모음에서 &quot;데이터 관리&quot;를 선택한 후 &quot;Data Warehouse 보기&quot; 섹션을 사용할 수 있는 경우.

온라인 광고에 투자할 경우 이러한 지출 수익률을 추적하고 추가 투자에 대한 데이터 중심의 결정을 내려야 합니다. 이 문서에서는 집계 및 캠페인별 ROI를 포함하여 채널 분석을 추적할 대시보드를 설정하는 방법을 보여줍니다.

![](../../assets/Marketing_dashboard_example.png)

시작하기 전에 [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md), [!DNL [Adwords]](../importing-data/integrations/google-adwords.md), 및 [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) 계정 및 추가 온라인 광고 지출 데이터를 가져올 수 있습니다. 이 분석에는 다음이 포함됩니다 [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md).

## 통합 테이블

**원래 아키텍처:** 다양한 소스에서 비용을 통합하려면 [!DNL Facebook Ads] 또는 [!DNL Google Adwords]). **통합 테이블** 광고비 지출 중 이 단계를 완료하려면 분석가가 필요합니다. 아직 안하셨다면, [지원 요청 파일](../../guide-overview.md) 그 문제를 `[MARKETING ROI ANALYSIS]`, 및 분석가가 이 테이블을 만듭니다.

**새로운 아키텍처:** 에 제시된 예를 따를 수 있습니다. [이 분석 라이브러리](../../data-analyst/data-warehouse-mgr/create-dw-views.md) 주제. 이제 통합 테이블을 새 아키텍처에 대한 Data Warehouse 보기라고 합니다.

## 계산된 열

만들 열

* **`Consolidated Digital Ad Spend`** 표
* **`Campaign name`** 분석가가 의 일부로 **[마케팅 ROI 분석]** 티켓

>[!NOTE]
>
>새로운 아키텍처 차이점에 대해서는 위의 내용을 참조하십시오.

**기존 아키텍처 및 신규 아키텍처:**

* **`sales_flat_order`** 표
   * **`Order's GA campaign`**
      * 정의를 선택합니다. `Joined Column`
      * [!UICONTROL Create Path]:
      * 
         [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 

         [!UICONTROL One]: `ecommerce####.transaction_id`

      * 선택 [!UICONTROL table]: `ecommerce####`
      * 선택 [!UICONTROL column]: `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`
   * **`Order's GA medium`**
      * 정의를 선택합니다. 연결된 열
      * 선택 [!UICONTROL table]: `ecommerce####`
      * 선택 [!UICONTROL column]: `medium`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce###.transactionId
   * **`Order's GA source`**
      * 정의를 선택합니다. 연결된 열
      * 선택 [!UICONTROL table]: `ecommerce####`
      * 선택 [!UICONTROL column]: `source`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce####.transactionId^




* **`customer_entity`** 표
* **`Customer's first order GA campaign`**
   * 정의를 선택합니다. `Max`
   * 선택 [!UICONTROL table]: `sales_flat_order`
   * 선택 [!UICONTROL column]: `Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * 정의를 선택합니다. `Max`
   * 선택 [!UICONTROL table]: `sales_flat_order`
   * 선택 [!UICONTROL column]: `Order's GA source`
   * [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * 정의를 선택합니다. `Max`
   * 선택 [!UICONTROL table]: `sales_flat_order`
   * 선택 [!UICONTROL column]: `Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** 표
* **`Customer's first order GA campaign`**
   * 정의를 선택합니다. `Joined Column`
   * 선택 [!UICONTROL table]: `customer_entity`
   * 선택 [!UICONTROL column]: `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * 정의를 선택합니다. 연결된 열
   * 선택 [!UICONTROL table]: `customer_entity`
   * 선택 [!UICONTROL column]: `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * 정의를 선택합니다. `Joined Column`
   * 선택 [!UICONTROL table]: `customer_entity`
   * 선택 [!UICONTROL column]: `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## 지표

* **광고 비용**
* 에서 **`Consolidated Digital Ad Spend`** 표
* 이 지표는 다음을 수행합니다 **합계**
* 설정 **`adCost`** 열
* 정렬 기준 **`date`** timestamp

* **광고 노출 횟수**
* 에서 **`Consolidated Digital Ad Spend`** 표
* 이 지표는 다음을 수행합니다 **합계**
* 설정 **`Impressions`** 열
* 정렬 기준 **`Month`** timestamp

* **광고 클릭 수**
* 에서 **`Consolidated Digital Ad Spend`** 표
* 이 지표는 다음을 수행합니다 **합계**
* 설정 **`adClicks`** 열
* 정렬 기준 **`Month`** timestamp

>[!NOTE]
>
>다음을 확인하십시오 [새 열을 지표에 차원으로 추가](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에

## 보고서

* **광고 비용(항상)**
   * [!UICONTROL Metric]: 광고 비용

* 지표 `A`: 광고 비용
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **광고 고객 확보(항상)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 필터 논리: ([`A`] 또는 [`B`] 또는 [`C`]) 및 [`D`]

* 지표 `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **광고 ROI**
   * [!UICONTROL Metric]: 광고 비용

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 필터 논리: ([`A`] 또는 [`B`] 또는 [`C`]) 및 [`D`]
   * [!UICONTROL Metric]: 평균 라이프타임 매출
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 필터 논리: ([`A`] 또는 [`B`] 또는 [`C`]) 및 [`D`]
   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`



* 지표 `A`: `Ad Spend (hide)`
* 지표 `B`: `Ad customer acquisitions (hide)`
* 지표 `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Ga별 주문**
   * 

      [[!UICONTROL 지표]: `Orders`

* 지표 `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* 

   [!UICONTROL Chart Type]: `Area`

* **캠페인별 광고 ROI**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 필터 논리: ([`A`] 또는 [`B`] 또는 [`C`]) 및 [`D`]
   * [!UICONTROL Metric]: 평균 라이프타임 매출
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 필터 논리: ([`A`] 또는 [`B`] 또는 [`C`]) 및 [`D`]
   * [!UICONTROL Metric]: 평균 주문 라이프타임 수
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 필터 논리: ([`A`] 또는 [`B`] 또는 [`C`]) 및 [`D`]
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `(C - (A / B))`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Ad Clicks`

   * [!UICONTROL Metric]: `Ad Impressions`

   * [!UICONTROL Formula]: `(H / I)`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]: `(A / H)`
   * 

      [!UICONTROL Format]: `Currency`




* 지표 `A`: `Ad Spend` (숨기기)
* 지표 `B`: `Ad customer acquisitions`
* 지표 `C`: `Average LTV`
* 지표 `D`: `Average lifetime # of orders`
* 
   [[!UICONTROL 공식]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* 지표 `H`: `adClicks`
* 지표 `I`: `Impressions`
* 
   [[!UICONTROL 공식]: `CTR`
* 
   [[!UICONTROL 공식]: `CPC`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 
   [[!UICONTROL 그룹]: `campaign` (비광고 비용 테이블 지표에 &#39;고객의 첫 번째 주문&#39;캠페인 사용)
* 

   [!UICONTROL Chart Type]: `Table`

이 분석을 작성하는 동안 질문이 있거나 전문 서비스 팀에 참여하려는 경우 [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

### 관련

* [의 UTM 태그 지정에 대한 우수 사례 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [어떻게 [!DNL Google Analytics] UTM 속성 작업?](../analysis/utm-attributes.md)
