---
title: 엔티티 관계 다이어그램
description: 소수의 공통 Commerce 데이터베이스 테이블 간의 관계를 시각화하는 데 도움이 되는 몇 가지 ER 다이어그램에 대해 알아봅니다.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# 엔티티 관계 다이어그램

**[!UICONTROL entity relationship (ER) diagram]**&#x200B;이란? [!UICONTROL ER] 다이어그램은 데이터베이스 내의 테이블과 테이블의 관계 방식을 시각화한 것입니다. 이 항목에는 몇 가지 일반적인 Adobe Commerce 데이터베이스 테이블 간의 관계를 시각화하는 데 도움이 되는 몇 가지 [!UICONTROL ER] 다이어그램이 포함되어 있습니다.

>[!NOTE]
>
>이 항목에서는 **참가**, **관계** 및 **경로**&#x200B;라는 단어가 표시됩니다. 이 단어는 모두 두 테이블이 연결되는 방식을 설명하는 데 사용됩니다.

## 코어 Commerce [!UICONTROL ER] 다이어그램

![4_DB_Chart](../../assets/4_DB_Chart.png)

이 `ER` 다이어그램은 Commerce 데이터베이스 내의 핵심 테이블 간의 관계를 나타냅니다. 여러 관계를 한 번에 보면 여러 테이블에서 데이터가 어떻게 관련되는지 알 수 있습니다.

아래 섹션에는 한 번에 두 개의 테이블에 해당하는 `ER`개의 다이어그램이 있습니다. 다이어그램과 함께 제공되는 설명을 보려면 해당 섹션의 헤더를 클릭합니다.

## `customer\_entity & sales\_flat\_order`

![한 명의 고객에게 많은 주문](../../assets/2_OneCustomerManyOrders.png)

한 사람이 여러 가지를 주문할 수 있습니다. 이 두 테이블 간의 관계는 `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`입니다.

>[!IMPORTANT]
>
>`customer\_entity.entity\_id`이(가) `sales\_flat\_order.entity\_id`과(와) 같지 않습니다. 첫 번째는 `customer\_id`(으)로 생각할 수 있으며 두 번째는 `order\_id.`(으)로 생각할 수 있습니다.

[!DNL Commerce Intelligence] 내에서 이 두 테이블 간의 경로가 없는 경우 Data Warehouse 탭에서 [경로를 만들고](../data-warehouse-mgr/create-paths-calc-columns.md)할 수 있습니다. 경로를 만들 준비가 되면 다음과 같이 정의됩니다.

![sales_flat_order에서 customer_entity로의 경로를 보여 주는 엔터티 관계 다이어그램](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

한 주문에 여러 항목이 포함될 수 있습니다. 이 두 테이블 간의 관계는 `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`입니다.

[!DNL Commerce Intelligence] 내에서 이 두 테이블 간의 경로가 없는 경우 Data Warehouse 탭에서 [경로를 만들고](../data-warehouse-mgr/create-paths-calc-columns.md)할 수 있습니다. 경로를 만들 준비가 되면 아래에 표시된 대로 경로를 정의합니다.

![sales_flat_order_item에서 sales_flat_order로의 경로를 보여 주는 엔터티 관계 다이어그램](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

하나의 제품은 여러 가지 물건을 구매할 수 있습니다. 이 두 테이블 간의 관계는 `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`입니다.

[!DNL Commerce Intelligence] 내에서 이 두 테이블 간의 경로가 없는 경우 Data Warehouse 탭에서 [경로를 만들고](../data-warehouse-mgr/create-paths-calc-columns.md)할 수 있습니다. 경로를 만들 준비가 되면 아래에 표시된 대로 경로를 정의합니다.

![sales_flat_order_item에서 catalog_product_entity로의 경로를 보여 주는 엔터티 관계 다이어그램](../../assets/SFOI___CPE_path.png)
