---
title: 재고 레벨 분석
description: 재고 수준을 분석하는 방법에 대해 알아봅니다.
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 재고 레벨 분석

이 항목에서는 현재 인벤토리에 대한 통찰력을 제공하고 기존 아키텍처 또는 새 아키텍처 모두의 클라이언트에 대한 지침을 포함하는 대시보드를 설정하는 방법을 보여 줍니다. **[!UICONTROL Manage Data]** 메뉴 아래에 **[!UICONTROL Data Warehouse Views]** 옵션이 없는 경우 레거시 아키텍처를 사용하는 것입니다. 기존 아키텍처를 사용하는 경우 아래 _계산된 열_ 지침에 따라 지정된 섹션에 도달하면 제목이 **[!UICONTROL INVENTORY ANALYSIS]**&#x200B;인 [새 지원 요청](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)을 제출하십시오.

## 추적할 열:

### 지침을 추적할 열

* **[!UICONTROL cataloginventory_stock_item]** 테이블:
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* **[!UICONTROL catalog_product_entity]** 테이블:
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## 계산된 열:

+++ 새로운 아키텍처

* **[!UICONTROL catalog_product_entity]** 테이블:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] 선택: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] 선택: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `AGE`
      * [!UICONTROL DATETIME column] 선택: `Product's most recent order date`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] 선택: `qty_ordered`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] 입력:
         * A: `Product's lifetime number of items sold`
         * B: `Product's first order date`
      * 
        [!UICONTROL Datatype]: `Decimal`
      * 정의:
         * a가 null이거나 B가 null인 경우 다른 null은 round(A::decimal/(extract(epoch from (current_timestamp - B))::decimal/604800.0),2) 끝입니다.

* **[!UICONTROL cataloginventory_stock_item]** 테이블:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] 선택: `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] 선택: `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] 선택: `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] 선택: `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] 입력:
         * A: `qty`
         * B: `Avg products sold per week (all time)`
      * 
        [!UICONTROL Datatype]: `Decimal`
      * 정의:
         * A가 null이거나 B가 null이거나 B = 0.0일 때 null이거나 다른 round(A::decimal/B,2) 끝인 경우

+++
+++ 레거시 아키텍처

* **[!UICONTROL catalog_product_entity]** 테이블:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] 선택: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] 선택: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `AGE`
      * DATETIME 열 선택: **`Product's most recent order date`**

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * [!UICONTROL column] 선택: **`qty_ordered`**
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * **[INVENTORY ANALYSIS]** 지원 요청을 제출할 때 분석가가 생성함

* **[!UICONTROL cataloginventory_stock_item]** 테이블:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] 선택: `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] 선택: `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] 선택: `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] 선택: `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * **[!UICONTROL INVENTORY ANALYSIS]** 지원 요청을 제출할 때 애널리스트가 만든 항목

+++

## 지표

### 지표 지침

* **[!UICONTROL cataloginventory_stock_item]** 테이블:
   * **`Inventory on hand`**: 이 지표는 다음을 수행합니다.
      * 다음에 대한 **합계**
      * **`qty`** 열이 다음에 의해 정렬됨
      * [없음] 열

## 보고서

### 보고서 지침

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * 시간 간격: `None`
   * [!UICONTROL Group by]:
      * `Sku`
      * `Weeks on hand`
   * 
     [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `< 2`

   * [!UICONTROL Time period]: `All time`
   * 시간 간격: `None`
   * 
     [!UICONTROL 그룹 기준]: `Sku`
   * 
     [!UICONTROL Chart type]: `Table`

* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `> 26`

   * [!UICONTROL Time period]: `All time`
   * 시간 간격: `None`
   * 
     [!UICONTROL 그룹 기준]: `Sku`
   * 
     [!UICONTROL Chart type]: `Table`

이 분석을 작성하는 동안 질문이 있거나 Professional Services 팀에 문의하려는 경우 [지원 팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)하십시오.
