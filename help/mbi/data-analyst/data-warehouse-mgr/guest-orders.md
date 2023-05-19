---
title: 게스트 주문
description: 게스트 주문이 데이터에 미치는 영향 및 의 게스트 주문에 대해 올바르게 고려해야 하는 옵션에 대해 알아봅니다. [!DNL Commerce Intelligence] Data Warehouse.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# 게스트 주문

주문을 검토하는 동안, 그렇게 많은 것을 발견하면 `customer\_id` 값이 null이거나 다음에 다시 연결할 값이 없습니다. `customers` 테이블, 이는 귀하의 스토어에서 손님 주문을 허용함을 나타냅니다. 즉, `customers` 테이블에 모든 고객이 포함되지 않을 수 있습니다.

이 항목에서는 게스트 주문이 데이터에 미치는 영향과 의 게스트 주문에 대해 올바르게 고려해야 하는 옵션에 대해 설명합니다. [!DNL Commerce Intelligence] Data Warehouse.

## 게스트 주문이 데이터에 미치는 영향

일반적인 상거래 데이터베이스에는 `orders` 에 조인하는 테이블 `customers` 테이블. 의 모든 행 `orders` 테이블에 `customer\_id` 의 한 행에 고유한 열 `customers` 테이블.

* **모든 고객이 등록된 경우** 그리고 손님 주문은 허용되지 않습니다. 이것은 의 모든 레코드가 `orders` 테이블에 있는 값은 `customer\_id` 열. 결과적으로 모든 주문은 `customers` 테이블.

   ![](../../assets/guest-orders-4.png)

* **게스트 주문이 허용되는 경우**&#x200B;즉, 일부 주문은 `customer\_id` 열. 등록된 고객에게만 `customer\_id` 의 열 `orders` 테이블. 등록되지 않은 고객은 `NULL` (또는 비어 있음) 이 열의 값입니다. 따라서 모든 주문 레코드에 와 일치하는 레코드가 `customers` 테이블.

   >[!NOTE]
   >
   >주문을 한 고유한 개인을 식별하려면 옆에 다른 고유한 사용자 속성이 있어야 합니다 `customer\_id` 주문에 첨부되었습니다. 일반적으로 고객의 이메일 주소가 사용됩니다.

## Data Warehouse 설정에서 게스트 주문을 처리하는 방법

일반적으로 계정을 구현하는 영업 엔지니어는 Data Warehouse의 기반을 구축할 때 게스트 주문을 고려합니다.

게스트 주문을 고려하는 가장 최적의 방법은 모든 고객 수준 지표를 기반으로 하는 것입니다. `orders` 테이블. 이 설정에서는 게스트를 포함하여 모든 고객이 보유한 고유한 고객 ID를 사용합니다(일반적으로 고객 이메일이 사용됨). 에서 등록 데이터를 무시합니다. `customers` 테이블. 이 옵션을 사용하면 최소 한 번 이상 구매한 고객만 고객 수준 보고서에 포함됩니다. 아직 한 번 구매하지 않은 등록된 사용자는 포함되지 않습니다. 이 옵션을 사용하면 `New customer` 지표는 다음에 있는 고객의 첫 번째 주문 날짜를 기반으로 합니다. `orders` 테이블.

다음과 같은 점을 알 수 있습니다. `Customers we count` 이 유형의 설정에서 설정된 필터에 대한 필터가 있습니다. `Customer's order number = 1`.

![](../../assets/guest-orders-filter-set.png)

게스트 주문이 없는 상황에서는 각 고객이 고객 테이블에 고유한 행으로 존재합니다(이미지 1 참조). 지표(예: ) `New customers` 은 다음을 기반으로 이 테이블의 id를 간단히 카운트할 수 있습니다. `created\_at` 등록 날짜를 기반으로 신규 고객을 파악하는 날짜.

모든 고객 지표가 를 기반으로 하는 게스트 주문 설정에서 `orders` 게스트 주문을 설명하기 위해 다음 사항을 확인해야 합니다. `not counting customers twice`. orders 테이블의 ID를 계산하면 모든 주문을 계산합니다. 대신 `orders` 표를 작성하고 필터를 사용합니다. `Customer's order number = 1`, 그런 다음 각 고유 고객을 계산합니다 `only one time`. 다음과 같은 모든 고객 수준 지표에 적용할 수 있습니다 `Customer's lifetime revenue` 또는 `Customer's lifetime number of orders`.

위에서 null이 있음을 확인할 수 있습니다. `customer\_ids` 다음에서 `orders` 테이블. 를 사용하는 경우 `customer\_email` 고유 고객을 식별하기 위해 다음을 확인할 수 있습니다. `erin@test.com` 이(가) 3개의 주문을 했습니다. 따라서 `New customers` 에 대한 지표 `orders` 다음 조건에 따른 표:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
