---
title: 마케팅 ROI
description: ROI를 집계하여 캠페인별로 포함하여 채널 분석을 추적하는 대시보드를 설정하는 방법에 대해 알아봅니다.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
TQID: https://experienceleague.adobe.com/TJ0KsU551M5PkQcY-Ic0PuExtC9SCkO0MhZGdHL4N6g
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 02934da4962380494ab8a2becf5f06efb15d84dc
workflow-type: tm+mt
source-wordcount: 691
ht-degree: 21%

---

# 마케팅 ROI

>[!NOTE]
>
>이 항목에는 원래 아키텍처와 새 아키텍처를 사용하는 클라이언트에 대한 지침이 포함되어 있습니다. 기본 도구 모음에서 &quot;데이터 관리&quot;를 선택한 후 &quot;Data Warehouse 보기&quot; 섹션을 사용할 수 있는 경우 [새 아키텍처](../../administrator/account-management/new-architecture.md)에 있습니다.

온라인 광고에 돈을 지출하는 경우, 이 지출에 대한 수익을 추적하고 향후 투자에 대한 데이터 중심의 결정을 내리기를 원할 수 있습니다. 이 항목에서는 캠페인별로 ROI를 포함하여 채널 분석을 추적하는 대시보드를 설정하는 방법을 보여 줍니다.

![ROI 지표와 캠페인 성과를 표시하는 마케팅 대시보드](../../assets/Marketing_dashboard_example.png)

시작하기 전에 [[!DNL [Facebook Ads]]](../importing-data/integrations/facebook-ads.md), [[!DNL [Adwords]]](../importing-data/integrations/google-adwords.md) 및 [[!DNL [Google Ecommerce]]](../importing-data/integrations/google-ecommerce.md) 계정을 연결하고 추가 온라인 광고 지출 데이터를 가져옵니다. 이 분석에는 [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md)이(가) 포함되어 있습니다.

## 통합 테이블

**원래 아키텍처:** [!DNL Facebook Ads] 또는 [!DNL Google Adwords]과(와) 같은 다양한 소스에서 지출액을 취합하려면 Adobe에서 모든 광고 지출액의 **통합 테이블**&#x200B;을 만드는 것이 좋습니다. 이 단계를 수행하려면 분석가가 필요합니다. 그렇지 않은 경우 [제목이 `[MARKETING ROI ANALYSIS]`인 지원 요청을 &#x200B;](../../guide-overview.md#Submitting-a-Support-Ticket)하면 분석가가 이 테이블을 만듭니다.

**새 아키텍처:** [이 Analysis Library](../../data-analyst/data-warehouse-mgr/create-dw-views.md) 항목에서 예제를 따를 수 있습니다. 이제 통합 테이블을 새 아키텍처에 대한 Data Warehouse 보기 라고 합니다.

## 계산된 열

생성할 열

* **`Consolidated Digital Ad Spend`** 테이블
* **`Campaign name`**&#x200B;은(는) Adobe 분석가가 **[마케팅 ROI 분석]** 티켓의 일부로 만들었습니다.

**원본 및 새 아키텍처:**

* **`sales_flat_order`** 테이블
  * **`Order's GA campaign`**
    * 정의 선택: `Joined Column`
    * [!UICONTROL Create Path]:
    * &#x200B;
      [!UICONTROL Many]&#x200B;: `sales_flat_order.increment_id`
    * &#x200B;
      [!UICONTROL One]&#x200B;: `ecommerce####.transaction_id`

    * [!UICONTROL table] 선택: `ecommerce####`
    * [!UICONTROL column] 선택: `campaign`
    * [!UICONTROL Path]&#x200B;: `sales_flat_order.increment_id = ecommerce#####.transactionID`

  * **`Order's GA medium`**
    * 정의 선택: 조인된 열
    * [!UICONTROL table] 선택: `ecommerce####`
    * [!UICONTROL column] 선택: `medium`
    * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce#####.transactionId

  * **`Order's GA source`**
    * 정의 선택: 조인된 열
    * [!UICONTROL table] 선택: `ecommerce####`
    * [!UICONTROL column] 선택: `source`
    * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce#####.transactionId
^

* **`customer_entity`** 테이블
* **`Customer's first order GA campaign`**
  * 정의 선택: `Max`
  * [!UICONTROL table] 선택: `sales_flat_order`
  * [!UICONTROL column] 선택: `Order's GA campaign`
  * [!UICONTROL Path]&#x200B;: `sales_flat_order.customer_id = customer_entity.entity_id`
  * [!UICONTROL Filter]:
    * `Orders we count`
    * `Customer's order number = 1`

* **`Customer's first order GA source`**
  * 정의 선택: `Max`
  * [!UICONTROL table] 선택: `sales_flat_order`
  * [!UICONTROL column] 선택: `Order's GA source`
  * [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
  * [!UICONTROL Filter]:
    * `Orders we count`
    * `Customer's order number = 1`

* **`Customer's first order GA medium`**
  * 정의 선택: `Max`
  * [!UICONTROL table] 선택: `sales_flat_order`
  * [!UICONTROL column] 선택: `Order's GA medium`
  * [!UICONTROL Path]&#x200B;: `sales_flat_order.customer_id = customer_entity.entity_id`
  * [!UICONTROL Filter]:
    * `Orders we count`
    * `Customer's order number = 1`

* **`sales_flat_order`** 테이블
* **`Customer's first order GA campaign`**
  * 정의 선택: `Joined Column`
  * [!UICONTROL table] 선택: `customer_entity`
  * [!UICONTROL column] 선택: `Customer's first order GA campaign`
  * [!UICONTROL Path]&#x200B;: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
  * 정의 선택: 조인된 열
  * [!UICONTROL table] 선택: `customer_entity`
  * [!UICONTROL column] 선택: `Customer's first order GA source`
  * [!UICONTROL Path]&#x200B;: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
  * 정의 선택: `Joined Column`
  * [!UICONTROL table] 선택: `customer_entity`
  * [!UICONTROL column] 선택: `Customer's first order GA medium`
  * [!UICONTROL Path]&#x200B;: `sales_flat_order.customer_id = customer_entity.entity_id`

## 지표

* **광고 지출**
* **`Consolidated Digital Ad Spend`** 테이블에서
* 이 지표는 **합계**&#x200B;를 수행합니다.
* **`adCost`** 열에서
* **`date`** 타임스탬프로 정렬됨

* **광고 노출 횟수**
* **`Consolidated Digital Ad Spend`** 테이블에서
* 이 지표는 **합계**&#x200B;를 수행합니다.
* **`Impressions`** 열에서
* **`Month`** 타임스탬프로 정렬됨

* **광고 클릭수**
* **`Consolidated Digital Ad Spend`** 테이블에서
* 이 지표는 **합계**&#x200B;를 수행합니다.
* **`adClicks`** 열에서
* **`Month`** 타임스탬프로 정렬됨

>[!NOTE]
>
>새 보고서를 작성하기 전에 [모든 새 열을 지표에 차원으로 추가](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md)하십시오.

## 보고서

* **광고 체류 시간(전체 시간)**
  * [!UICONTROL Metric]: 광고 지출

* 지표 `A`: 광고 지출
* [!UICONTROL Time period]&#x200B;: `All time`
* &#x200B;
  [!UICONTROL 간격]&#x200B;: `None`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Scalar`

* **고객 확보 추가(항상)**
  * [!UICONTROL Metric]&#x200B;: `New customers`
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * 필터 논리: ([`A`] 또는 [`B`] 또는 [`C`]) 및 [`D`]

* 지표 `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]&#x200B;: `All time`
* &#x200B;
  [!UICONTROL 간격]&#x200B;: `None`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Scalar`

* **광고 ROI**
  * [!UICONTROL Metric]: 광고 지출

  * [!UICONTROL Metric]&#x200B;: `New customers`
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * 필터 논리: ([`A`] 또는 [`B`] 또는 [`C`]) 및 [`D`]

  * [!UICONTROL Metric]: 평균 라이프타임 수익
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * 필터 논리: ([`A`] 또는 [`B`] 또는 [`C`]) 및 [`D`]

  * [!UICONTROL Formula]&#x200B;: `((C - (A / B)) / (A / B))`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `Percentage`

* 지표 `A`: `Ad Spend (hide)`
* 지표 `B`: `Ad customer acquisitions (hide)`
* 지표 `C`: `Average LTV (hide)`
* [!UICONTROL Formula]&#x200B;: `Ads ROI`
* [!UICONTROL Time period]&#x200B;: `All time`
* &#x200B;
  [!UICONTROL 간격]&#x200B;: `None`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Scalar`

* **ga 매체별 주문**
  * &#x200B;
    [!UICONTROL 지표]&#x200B;: `Orders`

* 지표 `A`: `Orders`
* [!UICONTROL Time period]&#x200B;: `All time`
* [!UICONTROL Interval]&#x200B;: `By Month`
* [!UICONTROL Group by]&#x200B;: `Order's medium`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Area`

* 캠페인별 **광고 ROI**
  * [!UICONTROL Metric]&#x200B;: `Ad Spend`

  * [!UICONTROL Metric]&#x200B;:`New customers`
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * 필터 논리: ([`A`] 또는 [`B`] 또는 [`C`]) 및 [`D`]

  * [!UICONTROL Metric]: 평균 라이프타임 수익
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * 필터 논리: ([`A`] 또는 [`B`] 또는 [`C`]) 및 [`D`]

  * [!UICONTROL Metric]: 평균 수명 주문 수
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * 필터 논리: ([`A`] 또는 [`B`] 또는 [`C`]) 및 [`D`]

  * [!UICONTROL Formula]&#x200B;: `(A / B)`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `Currency`

  * [!UICONTROL Formula]&#x200B;: `(C - (A / B))`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `Currency`

  * [!UICONTROL Formula]&#x200B;: `((C - (A / B)) / (A / B))`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `Percentage`

  * [!UICONTROL Metric]&#x200B;: `Ad Clicks`

  * [!UICONTROL Metric]&#x200B;: `Ad Impressions`

  * [!UICONTROL Formula]&#x200B;: `(H / I)`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `Percentage`

  * [!UICONTROL Formula]&#x200B;: `(A / H)`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `Currency`

* 지표 `A`: `Ad Spend`(숨기기)
* 지표 `B`: `Ad customer acquisitions`
* 지표 `C`: `Average LTV`
* 지표 `D`: `Average lifetime # of orders`
* &#x200B;
  [!UICONTROL 공식]&#x200B;: `CAC`
* [!UICONTROL Formula]&#x200B;: `Avg return`
* [!UICONTROL Formula]&#x200B;: `Ads ROI`
* 지표 `H`: `adClicks`
* 지표 `I`: `Impressions`
* &#x200B;
  [!UICONTROL 공식]&#x200B;: `CTR`
* &#x200B;
  [!UICONTROL 공식]&#x200B;: `CPC`
* [!UICONTROL Time period]&#x200B;: `All time`
* &#x200B;
  [!UICONTROL 간격]&#x200B;: `None`
* &#x200B;
  [!UICONTROL 그룹 기준]: `campaign` (비광고 지출 테이블 지표에 &#39;고객 첫 번째 주문&#39; 캠페인 사용)
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Table`

이 분석을 작성하는 동안 질문이 있거나 Professional Services 팀에 문의하려는 경우 [지원 팀에 문의](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies)하십시오.

### 관련 항목

* [&#x200B; [!DNL Google Analytics]의 UTM 태그 지정에 대한 모범 사례](../../best-practices/utm-tagging-google.md)
* [&#x200B; [!DNL Google Analytics] UTM 속성은 어떻게 작동합니까?](../analysis/utm-attributes.md)
