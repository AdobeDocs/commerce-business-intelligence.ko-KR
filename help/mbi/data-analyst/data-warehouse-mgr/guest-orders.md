---
title: 게스트 주문
description: 게스트 주문이 데이터에 미치는 영향 및 사용자의 주문에서 게스트 주문을 적절하게 고려해야 하는 옵션에 대해 알아봅니다 [!DNL MBI] data warehouse.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 게스트 주문

주문을 검토하는 동안 `customer\_id` 값이 null이거나 다시 연결할 값이 없습니다. `customers` 표, 이는 일반적으로 스토어가 게스트 주문을 허용함을 나타냅니다. 이것은 `customers` 표는 모든 고객을 포함하지 않을 수 있습니다.

이 주제에서는 게스트 주문이 데이터에 미치는 영향 및 귀하의 게스트 주문에서 적절히 처리해야 하는 옵션에 대해 설명합니다 [!DNL MBI] data warehouse.

## 게스트 주문이 데이터에 미치는 영향

일반적인 상거래 데이터베이스에는 `orders` 에 연결된 테이블 `customers` 테이블. 모든 행 `orders` 테이블에 `customer\_id` 한 행에 고유한 열 `customers` 테이블.

* **모든 고객이 등록된 경우** 그리고 게스트 주문은 허용되지 않습니다. 이는 `orders` 변수에는 `customer\_id` 열. 따라서 모든 주문은 `customers` 테이블. 아래 이미지에서 이를 볼 수 있습니다.

   ![](../../assets/guest-orders-4.png)

* **게스트 주문이 허용된 경우**&#x200B;즉, 일부 주문에는 `customer\_id` 열. 등록된 고객에게만 `customer\_id` 열 `orders` 테이블. 등록되지 않은 고객은 `NULL` (또는 비어 있음) 이 열에 대한 값. 따라서 모든 주문 레코드에 `customers` 테이블.

   >[!NOTE]
   >
   >주문을 한 고유한 개인을 식별하려면 옆에 다른 고유한 사용자 특성이 있어야 합니다 `customer\_id` 주문서에 첨부합니다. 일반적으로 고객의 이메일 주소가 사용됩니다.

## Data Warehouse 설정에서 게스트 주문을 처리하는 방법

일반적으로 계정을 구현하는 영업 엔지니어는 Data Warehouse의 기반을 구축할 때 게스트 주문을 고려합니다.

게스트 주문을 설명하는 가장 적합한 방법은 `orders` 테이블. 이 설정에서는 게스트(일반적으로 고객 이메일이 사용됨)를 포함하여 모든 고객이 가지고 있는 고유한 고객 ID를 사용합니다. 이 경우 `customers` 테이블. 이 옵션을 사용하면 하나 이상의 구매를 한 고객만 고객 수준 보고서에 포함됩니다. 아직 한 번 구매하지 않은 등록된 사용자는 포함되지 않습니다. 이 옵션을 사용하면 `New customer` 지표는 고객의 첫 번째 주문 날짜를 기준으로 합니다 `orders` 테이블.

다음 사항에 주의하십시오. `Customers we count` 이 유형의 설정에 설정된 필터에는 `Customer's order number = 1`. 왜 이런 건지 생각해 보자.

![](../../assets/guest-orders-filter-set.png)

게스트 주문이 없는 상황에서 각 고객은 고객 테이블에서 고유한 행으로 존재합니다(이미지 1 참조). 과 같은 지표 `New customers` 는 단순히 `created\_at` 등록 날짜를 기준으로 새 고객을 이해하는 날짜입니다.

모든 고객 지표가 `orders` 게스트 주문을 설명하기 위한 테이블입니다. `not counting customers twice`. 주문 테이블의 id를 카운트하면 모든 주문이 계산됩니다. 대신 `orders` 표, 필터 사용, `Customer's order number = 1`를 계산하면 각 고유 고객을 카운트하게 됩니다 `only one time`. 다음과 같은 모든 고객 수준 지표에 적용할 수 있습니다 `Customer's lifetime revenue` 또는 `Customer's lifetime number of orders`.

위의 이미지 2에서 null이 있음을 확인할 수 있습니다 `customer\_ids` 에서 `orders` 테이블. 를 사용하는 경우 `customer\_email` 고유 고객을 식별하려면 `erin@test.com` 3개의 주문을 받았습니다. 따라서, `New customers` 지표 `orders` 다음 조건을 기반으로 하는 표:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
