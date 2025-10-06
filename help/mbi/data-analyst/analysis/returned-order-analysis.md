---
title: 반환된 주문 분석
description: 스토어 수익에 대한 세부 분석을 제공하는 대시보드를 설정하는 방법에 대해 알아봅니다.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 반환된 주문

이 항목에서는 스토어 수익에 대한 자세한 분석을 제공하는 대시보드를 설정하는 방법을 보여 줍니다.

![반환 비율과 이유를 보여주는 자세한 반환 대시보드](../../assets/detailed-returns-dboard.png)

시작하기 전에 [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 고객이어야 하며 귀사에서 반품에 `enterprise\_rma` 테이블을 사용하고 있는지 확인해야 합니다.

이 분석에는 [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md)이(가) 포함되어 있습니다.

## 시작

추적할 열

* **`enterprise_rma`** 또는 **`rma`** 테이블
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* **`enterprise_rma_item_entity`** 또는 **`rma_item_entity`** 테이블
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

생성할 필터 세트

* **`enterprise_rma`** 테이블
* 필터 집합 이름: `Returns we count`
* 필터 집합 논리:
   * 자리 표시자 - 여기에 사용자 지정 논리 입력

* **`enterprise_rma_item_entity`** 테이블
* 필터 집합 이름: `Returns items we count`
* 필터 집합 논리:
   * 자리 표시자 - 여기에 사용자 지정 논리 입력

### 계산된 열

생성할 열

* **`enterprise_rma`** 테이블
* **`Order's created at`**
* 정의 선택: `Joined Column`
* [!UICONTROL Create Path]:
* 
  [!UICONTROL Many]: `enterprise_rma.order_id`
* 
  [!UICONTROL One]: `sales_flat_order.entity_id`

* [!UICONTROL table] 선택: `sales_flat_order`
* [!UICONTROL column] 선택: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* 정의 선택: `Joined Column`
* [!UICONTROL table] 선택: `sales_flat_order`
* [!UICONTROL column] 선택: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* 분석가가 **`Time between order's created_at and date_requested`** 티켓의 일부로 `[RETURNS ANALYSIS]`을(를) 만들었습니다.

* **`enterprise_rma_item_entity`** 테이블
* **`return_date_requested`**
* 정의 선택: `Joined Column`
* [!UICONTROL Create Path]:
   * 
     [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * 
     [!UICONTROL One]: `enterprise_rma.entity_id`

* [!UICONTROL table] 선택: `enterprise_rma`
* [!UICONTROL column] 선택: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* 분석가가 **`Return item total value (qty_returned * price)`** 티켓의 일부로 `[RETURNS ANALYSIS]`을(를) 만들었습니다.

* **`sales_flat_order`** 테이블
* **`Order contains a return? (1=yes/0=No)`**
* 정의 선택: `Exists`
* [!UICONTROL table] 선택: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* 분석가가 **`Customer's previous order number`** 티켓의 일부로 `[RETURNS ANALYSIS]`을(를) 만들었습니다.
* 분석가가 **`Customer's previous order contains return? (1=yes/0=no)`** 티켓의 일부로 `[RETURNS ANALYSIS]`을(를) 만들었습니다.

>[!NOTE]
>
>해결 시간(초) 또는 첫 번째 응답 시간(초)에 대한 업무 시간만 분석하려는 경우 티켓을 요청할 때 분석가에게 알립니다.

### 지표

* **반환**
* **`enterprise_rma`** 테이블에서
* 이 지표는 **Count**&#x200B;을 수행합니다.
* **`entity_id`** 열에서
* **`date_requested`**&#x200B;이(가) 정렬함
* [!UICONTROL Filter]: `Returns we count`

* **반환된 항목**
* **`enterprise_rma_item_entity`** 테이블에서
* 이 지표는 **합계**&#x200B;를 수행합니다.
* **`qty_approved`** 열에서
* **`return date_requested`**&#x200B;이(가) 정렬함
* [!UICONTROL Filter]: `Returns we count`

* **반환된 항목 합계 값**
* **`enterprise_rma_item_entity`** 테이블에서
* 이 지표는 **합계**&#x200B;를 수행합니다.
* **`Returned item total value (qty_returned * price)`** 열에서
* **`return date_requested`**&#x200B;이(가) 정렬함
* [!UICONTROL Filter]: `Returns we count`

* **주문과 반환 사이의 평균 시간**
* **`enterprise_rma`** 테이블에서
* 이 지표는 **평균**&#x200B;을 수행합니다.
* **`Time between order's created_at and date_requested`** 열에서
* **`date_requested`**&#x200B;이(가) 정렬함
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>새 보고서를 작성하기 전에 [모든 새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md)하십시오.

### 보고서

* **반환 후 순서 반복 확률**
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

* **평균 반환 시간(항상)**
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

* **월별 수익**
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

* 항목별 **반환 비율**
* 지표 `A`: `Returned items`(숨기기)
* [!UICONTROL Metric]: 반환된 항목

* 지표 `B`: `Items sold`(숨기기)
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

이 분석을 작성하는 동안 질문이 있거나 Professional Services 팀에 참여하려는 경우 [지원팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)하십시오.
