---
title: 게스트 주문
description: 게스트 주문이 데이터에 미치는 영향 및  [!DNL Commerce Intelligence] Data Warehouse에서 게스트 주문을 올바르게 고려해야 하는 옵션에 대해 알아봅니다.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# 게스트 주문

주문을 검토하는 동안 많은 `customer\_id` 값이 null이거나 `customers` 테이블에 다시 연결할 값이 없는 경우 스토어에서 게스트 주문을 허용함을 나타냅니다. 즉, `customers` 테이블에 모든 고객이 포함되지 않을 수 있습니다.

이 항목에서는 게스트 주문이 데이터에 미치는 영향 및 [!DNL Commerce Intelligence] Data Warehouse에서 게스트 주문을 올바르게 고려해야 하는 옵션에 대해 설명합니다.

## 게스트 주문이 데이터에 미치는 영향

일반적인 상거래 데이터베이스에는 `orders` 테이블에 조인하는 `customers` 테이블이 있습니다. `orders` 테이블의 모든 행에는 `customer\_id` 테이블의 한 행에 고유한 `customers` 열이 있습니다.

* **모든 고객이 등록되고** 게스트 주문이 허용되지 않으면 `orders` 테이블의 모든 레코드에 `customer\_id` 열의 값이 있는 것입니다. 따라서 모든 순서가 `customers` 테이블로 다시 연결됩니다.

  ![](../../assets/guest-orders-4.png)

* **게스트 주문이 허용되는 경우**&#x200B;은(는) 일부 주문에 `customer\_id` 열의 값이 없음을 의미합니다. 등록된 고객에게만 `customer\_id` 테이블의 `orders` 열에 대한 값이 제공됩니다. 등록되지 않은 고객은 이 열에 대해 `NULL`(또는 빈) 값을 받습니다. 따라서 모든 주문 레코드에 `customers` 테이블에 일치하는 레코드가 있는 것은 아닙니다.

  >[!NOTE]
  >
  >주문을 한 고유한 개인을 식별하려면 주문에 연결된 `customer\_id` 옆에 다른 고유한 사용자 특성이 있어야 합니다. 일반적으로 고객의 이메일 주소가 사용됩니다.

## Data Warehouse 설정에서 게스트 주문을 처리하는 방법

일반적으로 계정을 구현하는 영업 엔지니어는 Data Warehouse의 기반을 구축할 때 게스트 주문을 고려합니다.

게스트 주문을 고려하는 가장 최적의 방법은 `orders` 표에 모든 고객 수준 지표를 사용하는 것입니다. 이 설정에서는 게스트를 포함하여 모든 고객이 보유한 고유한 고객 ID를 사용합니다(일반적으로 고객 이메일이 사용됨). `customers` 테이블의 등록 데이터를 무시합니다. 이 옵션을 사용하면 최소 한 번 이상 구매한 고객만 고객 수준 보고서에 포함됩니다. 아직 한 번 구매하지 않은 등록된 사용자는 포함되지 않습니다. 이 옵션을 사용하면 `New customer` 지표는 `orders` 테이블에서 고객의 첫 번째 주문 날짜를 기반으로 합니다.

이 유형의 설정에서 설정된 `Customers we count` 필터에 `Customer's order number = 1`에 대한 필터가 있습니다.

![](../../assets/guest-orders-filter-set.png)

게스트 주문이 없는 상황에서는 각 고객이 고객 테이블에 고유한 행으로 존재합니다(이미지 1 참조). `New customers`과(와) 같은 지표는 `created\_at` 날짜를 기준으로 이 테이블의 ID를 계산하여 등록 날짜를 기준으로 새 고객을 이해할 수 있습니다.

모든 고객 지표가 게스트 주문을 설명하기 위해 `orders` 테이블을 기반으로 하는 게스트 주문 설정에서 `not counting customers twice`인지 확인해야 합니다. orders 테이블의 ID를 계산하면 모든 주문을 계산합니다. 대신 `orders` 테이블의 ID를 계산하고 필터 `Customer's order number = 1`을(를) 사용하는 경우 각 고유 고객 `only one time`을(를) 계산합니다. `Customer's lifetime revenue` 또는 `Customer's lifetime number of orders`과(와) 같은 모든 고객 수준 지표에 적용됩니다.

위에서 `customer\_ids` 테이블에 null `orders`이(가) 있음을 확인할 수 있습니다. `customer\_email`을(를) 사용하여 고유 고객을 식별하면 `erin@test.com`에서 3개의 주문을 했음을 알 수 있습니다. 따라서 다음 조건에 따라 `New customers` 테이블에 `orders` 지표를 만들 수 있습니다.

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
