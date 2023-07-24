---
title: 엔티티 관계 다이어그램
description: 소수의 공통 Commerce 데이터베이스 테이블 간의 관계를 시각화하는 데 도움이 되는 몇 가지 ER 다이어그램에 대해 알아봅니다.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# 엔티티 관계 다이어그램

(이)란? **[!UICONTROL entity relationship (ER) diagram]**? An [!UICONTROL ER] 다이어그램은 데이터베이스 내의 테이블과 테이블의 상호 관계를 시각화하는 것입니다. 이 주제에는 몇 가지가 포함되어 있습니다 [!UICONTROL ER] 몇 가지 일반적인 Adobe Commerce 데이터베이스 테이블 간의 관계를 시각화하는 데 도움이 되는 다이어그램입니다.

>[!NOTE]
>
>이 항목 전체에서 다음 단어가 표시됩니다 **가입**, **관계**, 및 **경로**. 이 단어는 모두 두 테이블이 연결되는 방식을 설명하는 데 사용됩니다.

## 코어 상거래 [!UICONTROL ER] 다이어그램

![4_DB_Chart](../../assets/4_DB_Chart.png)

이 `ER` 다이어그램은 Commerce 데이터베이스 내의 핵심 테이블 간의 관계를 나타냅니다. 여러 관계를 한 번에 보면 여러 테이블에서 데이터가 어떻게 관련되는지 알 수 있습니다.

아래 섹션에는 다음 항목이 포함됩니다. `ER` 한 번에 두 개의 테이블에 해당하는 다이어그램입니다. 다이어그램과 함께 제공되는 설명을 보려면 해당 섹션의 헤더를 클릭합니다.

## `customer\_entity & sales\_flat\_order`

![1명의 고객 다량 주문](../../assets/2_OneCustomerManyOrders.png)

한 사람이 여러 가지를 주문할 수 있습니다. 이 두 테이블 간의 관계는 다음과 같습니다 `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` 다음과 같지 않음 `sales\_flat\_order.entity\_id`. 첫 번째는 로 생각할 수 있습니다. `customer\_id` 그리고 두 번째는 `order\_id.`

다음 범위 내 [!DNL Commerce Intelligence], 이 두 테이블 간의 경로가 없는 경우 [경로 만들기](../data-warehouse-mgr/create-paths-calc-columns.md) Data Warehouse 탭 내에서 경로를 만들 준비가 되면 다음과 같이 정의됩니다.

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

한 주문에 여러 항목이 포함될 수 있습니다. 이 두 테이블 간의 관계는 다음과 같습니다 `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

다음 범위 내 [!DNL Commerce Intelligence], 이 두 테이블 간의 경로가 없는 경우 [경로 만들기](../data-warehouse-mgr/create-paths-calc-columns.md) Data Warehouse 탭에서 클릭합니다. 경로를 만들 준비가 되면 아래에 표시된 대로 경로를 정의합니다.

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManytimes](../../assets/3_OneProductManyTimes.png)

하나의 제품은 여러 가지 물건을 구매할 수 있습니다. 이 두 테이블 간의 관계는 다음과 같습니다 `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

다음 범위 내 [!DNL Commerce Intelligence], 이 두 테이블 간의 경로가 없는 경우 [경로 만들기](../data-warehouse-mgr/create-paths-calc-columns.md) Data Warehouse 탭 내에서 경로를 만들 준비가 되면 아래에 표시된 대로 경로를 정의합니다.

![](../../assets/SFOI___CPE_path.png)
