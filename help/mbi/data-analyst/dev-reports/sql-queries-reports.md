---
title: SQL 쿼리를 Commerce Intelligence 보고서로 번역
description: SQL 쿼리를 Commerce Intelligence에서 사용하는 계산된 열, 지표로 변환하는 방법에 대해 알아봅니다.
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 0%

---

# Commerce Intelligence에서 SQL 쿼리 번역

SQL 쿼리가 [에서 사용하는 ](../data-warehouse-mgr/creating-calculated-columns.md)계산된 열[, ](../../data-user/reports/ess-manage-data-metrics.md)지표[ 및 ](../../tutorials/using-visual-report-builder.md)보고서[!DNL Commerce Intelligence]&#x200B;(으)로 변환되는 방식에 대해 궁금하셨습니까? SQL 사용자가 많은 경우 [!DNL Commerce Intelligence]에서 SQL을 변환하는 방법을 이해하면 [Data Warehouse 관리자](../data-warehouse-mgr/tour-dwm.md)에서 보다 효율적으로 작업하고 [!DNL Commerce Intelligence] 플랫폼을 최대한 활용할 수 있습니다.

이 항목의 끝에 SQL 쿼리 절 및 **요소에 대한**&#x200B;변환 매트릭스[!DNL Commerce Intelligence]가 있습니다.

일반 쿼리를 보고 시작하십시오.

| | |
|--- |--- |
| `SELECT` |  |
| `a,` | 보고서 `group by` |
| `SUM(b)` | `Aggregate function`(열) |
| `FROM c` | `Source` 테이블 |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | 보고서 `time frame` |
| `GROUP BY a` | 보고서 `group by` |

이 예제에서는 대부분의 번역 사례를 다루지만 몇 가지 예외가 있습니다. `aggregate` 함수를 변환하는 방법부터 시작하여 자세히 살펴보십시오.

## 집계 함수

쿼리의 집계 함수(예: `count`, `sum`, `average`, `max`, `min`)는 **에서**&#x200B;지표 집계&#x200B;**또는**&#x200B;열 집계[!DNL Commerce Intelligence] 형식을 사용합니다. 구별 요인은 응집을 수행하기 위해 가입이 필요한지 여부이다.

위의 각 예제를 참조하십시오.

## 지표 집계 {#aggregate}

`within a single table`을(를) 집계할 때 지표가 필요합니다. 예를 들어, 위의 쿼리의 `SUM(b)` 집계 함수는 열 `B`을(를) 합산하는 지표로 표시될 가능성이 높습니다. 

`Total Revenue`에서 [!DNL Commerce Intelligence] 지표를 정의하는 방법에 대한 특정 예를 살펴보십시오. 번역할 아래 쿼리를 참조하십시오.

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(열) |
| `FROM orders` | `Metric source` 테이블 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 지표 `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | 지표 `timestamp`(및 보고 `time range`) |

**[!UICONTROL Manage Data** > **&#x200B;지표&#x200B;**> **새 지표 만들기]**&#x200B;를 클릭하여 지표 빌더로 이동합니다. 먼저 적절한 `source` 테이블을 선택해야 합니다. 이 테이블은 `orders` 테이블입니다. 그런 다음 지표가 아래와 같이 설정됩니다.

![지표 집계](../../assets/Metric_aggregation.png)

## 열 집계

다른 테이블에서 조인된 열을 집계할 때는 계산된 열이 필요합니다. 예를들어, `customer` 테이블에 `Customer LTV`(이)라는 열이 만들어져 `orders` 테이블에서 해당 고객과 관련된 모든 주문의 총 값을 합산할 수 있습니다.

이 합계에 대한 쿼리는 다음과 같이 표시될 수 있습니다.

|  |  |
|--- |--- |
| `Select` | |
| `c.customer_id` | 집계 소유자 |
| `SUM(o.order_total) as "Customer LTV"` | 집계 작업(열) |
| `FROM customers c` | 집계 소유자 테이블 |
| `JOIN orders o` | 집계 소스 테이블 |
| `ON c.customer_id = o.customer_id` | 경로 |
| `WHERE o.status = 'success'` | 집계 필터 |

이 설정을 [!DNL Commerce Intelligence]에서 설정하려면 Data Warehouse 관리자를 사용해야 합니다. 여기서 `orders`과(와) `customers` 테이블 사이에 경로를 만든 다음 고객의 테이블에 `Customer LTV`이라는 열을 만듭니다.

`customers`과(와) `orders` 사이에 새 경로를 설정하는 방법을 살펴봅니다. 최종 목표는 `customers` 테이블에 새 집계된 열을 만드는 것이므로 먼저 Data Warehouse의 `customers` 테이블로 이동한 다음 **[!UICONTROL Create a Column** > **&#x200B;정의 선택&#x200B;**> **합계]**&#x200B;를 클릭합니다.

그런 다음 소스 테이블을 선택해야 합니다. `orders` 테이블에 경로가 있는 경우 드롭다운에서 해당 경로를 선택하면 됩니다. 그러나 새 경로를 만드는 경우 **[!UICONTROL Create new path]**&#x200B;을(를) 클릭하면 아래 화면이 표시됩니다.

![새 경로 만들기](../../assets/Create_new_path.png)

여기서 결합하려는 두 테이블 간의 관계를 신중하게 고려해야 합니다. 이 경우 `Many` 고객과 연결된 주문이 `One`개 있을 수 있으므로 `orders` 테이블은 `Many` 쪽에 나열되는 반면 `customers` 테이블은 `One` 쪽에서 선택됩니다.

>[!NOTE]
>
>[!DNL Commerce Intelligence]에서 `path`은(는) SQL의 `Join`과(와) 같습니다.

경로를 저장하면 `Customer LTV` 열을 만들 수 있습니다! 아래를 참조하십시오.

![SQL을 사용한 고객 생애 가치 분석 애니메이션 데모](../../assets/Customer_LTV.gif)

`Customer LTV` 테이블에 새 `customers` 열을 만들었으므로 이 열을 사용하여 [지표 집계](#aggregate)를 만들 준비가 되었습니다(예: 고객당 평균 LTV를 찾기 위해). `group by` 테이블에 빌드된 기존 지표를 사용하여 보고서에서 계산된 열을 기준으로 `filter` 또는 `customers`할 수도 있습니다.

>[!NOTE]
>
>후자의 경우 새 계산된 열을 작성할 때마다 [기존 지표에 차원을 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md)해야 `filter` 또는 `group by`(으)로 사용할 수 있습니다.

Data Warehouse 관리자를 사용하여 [계산된 열 만들기](../data-warehouse-mgr/creating-calculated-columns.md)를 참조하십시오.

## `Group By` 절

쿼리의 `Group By` 함수는 종종 [!DNL Commerce Intelligence]에서 시각적 보고서를 세그먼트화하거나 필터링하는 데 사용되는 열로 표시됩니다. 예를 들어 이전에 탐색한 `Total Revenue` 쿼리를 다시 방문해보겠습니다. 하지만 이번에는 `coupon\_code`을(를) 기준으로 매출을 세분화하여 가장 많은 매출을 창출하는 쿠폰을 더 잘 이해합니다.

아래 쿼리로 시작하십시오.

| | |
|--- |--- |
| `SELECT coupon_code,` | 보고서 `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(열) |
| `FROM orders` | `Metric source` 테이블 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 지표 `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | 지표 `timestamp`(및 보고 `time range`) |
| `GROUP BY coupon_code` | 보고서 `group by` |

>[!NOTE]
>
>이전에 시작한 쿼리와 유일하게 다른 점은 group by로 &#39;coupon\_code&#39;를 추가한 것입니다._

이전에 만든 것과 동일한 `Total Revenue` 지표를 사용하여 이제 쿠폰 코드로 세그먼트화된 매출 보고서를 만들 준비가 되었습니다! 9월부터 11월까지 데이터를 보고 이 시각적 보고서를 설정하는 방법을 보여 주는 아래 gif를 참조하십시오.

![쿠폰 코드별 매출](../../assets/Revenue_by_coupon_code.gif)

## 공식

경우에 따라 쿼리는 개별 열 간의 관계를 계산하기 위해 여러 개의 집계를 포함할 수 있습니다. 예를 들어 다음 두 가지 방법 중 하나를 통해 쿼리의 평균 순서 값을 계산할 수 있습니다.

* `AVG('order\_total')` 또는
* `SUM('order\_total')/COUNT('order\_id')`

이전 방법에는 `order\_total` 열에서 평균을 수행하는 새 지표를 만드는 작업이 포함됩니다. 그러나 `Total Revenue` 및 `Number of orders`을(를) 계산하기 위해 이미 지표가 설정되어 있다고 가정할 경우 후자의 메서드를 Report Builder에서 직접 만들 수 있습니다.

한 단계 뒤로 돌아가 `Average order value`에 대한 전체 쿼리를 살펴보십시오.

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | 지표 `operation`(열) |
| `COUNT(order_id) as "Number of orders"` | 지표 `operation`(열) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | 지표 `operation`(열)/지표 작업(열) |
| `FROM orders` | 지표 `source` 테이블 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 지표 `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | 지표 타임스탬프(및 보고 시간 범위) |

이제 `Total Revenue` 및 `Number of orders`을(를) 계산하기 위해 이미 설정된 지표가 있다고 가정합니다. 이러한 지표가 있으므로 `Report Builder`을(를) 열고 `Formula` 기능을 사용하여 온디맨드 계산을 만들 수 있습니다.

![AOV 형식](../../assets/AOV_forumula.gif)

## 요약

SQL 사용자가 많은 경우 [!DNL Commerce Intelligence]에서 쿼리가 변환되는 방식을 고려하면 계산된 열, 지표 및 보고서를 작성할 수 있습니다.

빠른 참조를 위해 아래 표를 확인하십시오. SQL 절의 동등한 [!DNL Commerce Intelligence] 요소와 쿼리에서 사용하는 방법에 따라 둘 이상의 요소에 매핑하는 방법을 보여 줍니다.

## Commerce Intelligence 요소

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE`(시간 요소 포함) | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
