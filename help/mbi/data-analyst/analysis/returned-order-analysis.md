---
title: 반환된 주문 분석
description: 스토어 수익에 대한 세부 분석을 제공하는 대시보드를 설정하는 방법에 대해 알아봅니다.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# 반환된 주문

이 항목에서는 스토어 수익에 대한 자세한 분석을 제공하는 대시보드를 설정하는 방법을 보여 줍니다.

![](../../assets/detailed-returns-dboard.png)

시작하기 전에 다음을 수행해야 합니다. [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 고객 및 은(는) 귀사에서 `enterprise\_rma` 반환용 테이블입니다.

이 분석에는 다음이 포함됩니다. [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md).

## 시작

추적할 열

* **`enterprise_rma`** 또는 **`rma`** 표
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* **`enterprise_rma_item_entity`** 또는 **`rma_item_entity`** 표
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

생성할 필터 세트

* **`enterprise_rma`** 표
* 필터 집합 이름: `Returns we count`
* 필터 집합 논리:
   * 자리 표시자 - 여기에 사용자 지정 논리 입력

* **`enterprise_rma_item_entity`** 표
* 필터 집합 이름: `Returns items we count`
* 필터 집합 논리:
   * 자리 표시자 - 여기에 사용자 지정 논리 입력

### 계산된 열

생성할 열

* **`enterprise_rma`** 표
* **`Order's created at`**
* 정의 선택: `Joined Column`
* [!UICONTROL Create Path]:
* 
   [!UICONTROL Many]: `enterprise_rma.order_id`
* 

   [!UICONTROL One]: `sales_flat_order.entity_id`

* 선택 [!UICONTROL table]: `sales_flat_order`
* 선택 [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* 정의 선택: `Joined Column`
* 선택 [!UICONTROL table]: `sales_flat_order`
* 선택 [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** 는 분석가가 의 일부로 만듭니다. `[RETURNS ANALYSIS]` 티켓

* **`enterprise_rma_item_entity`** 표
* **`return_date_requested`**
* 정의 선택: `Joined Column`
* [!UICONTROL Create Path]:
   * 
      [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * 

      [!UICONTROL One]: `enterprise_rma.entity_id`

* 선택 [!UICONTROL table]: `enterprise_rma`
* 선택 [!UICONTROL column]: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** 는 분석가가 의 일부로 만듭니다. `[RETURNS ANALYSIS]` 티켓

* **`sales_flat_order`** 표
* **`Order contains a return? (1=yes/0=No)`**
* 정의 선택: `Exists`
* 선택 [!UICONTROL table]: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** 는 분석가가 의 일부로 만듭니다. `[RETURNS ANALYSIS]` 티켓
* **`Customer's previous order contains return? (1=yes/0=no)`** 는 분석가가 의 일부로 만듭니다. `[RETURNS ANALYSIS]` 티켓

>[!NOTE]
>
>해결 시간(초) 또는 첫 번째 응답 시간(초)에 대한 업무 시간만 분석하려는 경우 티켓을 요청할 때 분석가에게 알립니다.

### 지표

* **반환**
* 다음에서 **`enterprise_rma`** 표
* 이 지표는 다음을 수행합니다. **카운트**
* 다음에서 **`entity_id`** 열
* 정렬 기준: **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **반환된 항목**
* 다음에서 **`enterprise_rma_item_entity`** 표
* 이 지표는 다음을 수행합니다. **합계**
* 다음에서 **`qty_approved`** 열
* 정렬 기준: **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **반환된 항목 합계 값**
* 다음에서 **`enterprise_rma_item_entity`** 표
* 이 지표는 다음을 수행합니다. **합계**
* 다음에서 **`Returned item total value (qty_returned * price)`** 열
* 정렬 기준: **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **주문과 반환 사이의 평균 시간**
* 다음에서 **`enterprise_rma`** 표
* 이 지표는 다음을 수행합니다. **평균**
* 다음에서 **`Time between order's created_at and date_requested`** 열
* 정렬 기준: **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>다음을 확인하십시오. [새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에

### 보고서

* **반품 후 주문 확률 반복**
* 지표 `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is in current month? = No`

* 지표 `B`: `Non-last orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Is customer's last order? (1=yes/0=no) = 0`
   * `Order contains a return? (1=yes/0=No) = 1`

* 공식: 반복 주문 확률
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* 
   [!UICONTROL 차트 유형]: `Bar`

* **평균 반환 시간(모든 시간)**
* 지표 `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Number`

* **반품이 있는 주문 비율**
* 지표 `A`: `Number of orders`
* [!UICONTROL Metric]: `Number of orders`

* 지표 `B`: `Orders w/ return`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`

* 공식: 반품이 있는 주문의 %
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **월별 반환 수익**
* 지표 `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* 

   [!UICONTROL 차트 유형]: `Line`

* **반품을 했지만 다시 구매하지 않은 고객**
* 지표 `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 
   [!UICONTROL 그룹 기준]: `Customer_email`
* 

   [!UICONTROL 차트 유형]: `Table`

* **품목별 반품 비율**
* 지표 `A`: `Returned items` (숨기기)
* [!UICONTROL Metric]: 반환된 항목

* 지표 `B`: `Items sold` (숨기기)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* 
   [!UICONTROL 차트 유형]: `Table`

모든 보고서를 컴파일한 후 원하는 대로 대시보드에서 구성할 수 있습니다. 결과는 위의 샘플 대시보드와 비슷할 수 있습니다.

이 분석을 작성하는 동안 질문이 발생하거나 Professional Services 팀에 문의하고자 하는 경우 [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
