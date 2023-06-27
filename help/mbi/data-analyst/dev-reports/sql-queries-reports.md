---
title: SQL 쿼리를 Commerce Intelligence 보고서로 번역
description: Commerce Intelligence에서 사용하는 계산된 열, 지표로 SQL 쿼리를 변환하는 방법에 대해 알아봅니다.
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
source-git-commit: fa65bd909495d4d73cabbc264e9a47b3e0a0da3b
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Commerce Intelligence에서 SQL 쿼리 번역

SQL 쿼리를 [계산된 열](../data-warehouse-mgr/creating-calculated-columns.md), [지표](../../data-user/reports/ess-manage-data-metrics.md), 및 [보고서](../../tutorials/using-visual-report-builder.md) 다음에서 을 사용합니다. [!DNL Commerce Intelligence]? SQL 사용자가 많은 경우 SQL이 변환되는 방식을 이해합니다. [!DNL Commerce Intelligence] 을(를) 통해 보다 스마트한 작업 수행 [Data Warehouse 관리자](../data-warehouse-mgr/tour-dwm.md) 및 를 최대한 활용하십시오. [!DNL Commerce Intelligence] 플랫폼.

이 항목의 끝에 **변환 행렬** SQL 쿼리 절 및 [!DNL Commerce Intelligence] 요소.

일반 쿼리를 보고 시작하십시오.

| | |
|--- |--- |
| `SELECT` |  |
| `a,` | 보고서 `group by` |
| `SUM(b)` | `Aggregate function` (열) |
| `FROM c` | `Source` 표 |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | 보고서 `time frame` |
| `GROUP BY a` | 보고서 `group by` |

이 예제에서는 대부분의 번역 사례를 다루지만 몇 가지 예외가 있습니다. 시작하는 방법 `aggregate` 함수는 번역됩니다.

## 집계 함수

집계 함수(예: `count`, `sum`, `average`, `max`, `min`쿼리에서 의 형식을 가져옵니다. **지표 집계** 또는 **열 집계** 위치: [!DNL Commerce Intelligence]. 구별 요인은 응집을 수행하기 위해 가입이 필요한지 여부이다.

위의 각 예제를 참조하십시오.

## 지표 집계 {#aggregate}

집계할 때 지표가 필요합니다 `within a single table`. 예를 들어 `SUM(b)` 위의 쿼리의 집계 함수는 열 합계를 나타내는 지표로 표시될 가능성이 높습니다 `B`. 

이(가) `Total Revenue` 지표는에서 정의할 수 있습니다. [!DNL Commerce Intelligence]. 번역할 아래 쿼리를 참조하십시오.

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (열) |
| `FROM orders` | `Metric source` 표 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 지표 `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | 지표 `timestamp` (및 보고 `time range`) |

을 클릭하여 지표 빌더로 이동합니다. **[!UICONTROL Manage Data** > **&#x200B;지표&#x200B;**> **새 지표 만들기]**, 먼저 적절한 을(를) 선택해야 합니다. `source` 테이블, 이 경우 `orders` 테이블. 그런 다음 지표가 아래와 같이 설정됩니다.

![지표 집계](../../assets/Metric_aggregation.png)

## 열 집계

다른 테이블에서 조인된 열을 집계할 때는 계산된 열이 필요합니다. 따라서 예를 들어 `customer` 테이블 호출됨 `Customer LTV`: 의 해당 고객과 연관된 모든 주문의 총 값을 합계합니다. `orders` 테이블.

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

에서 설정 중 [!DNL Commerce Intelligence] 를 사용하려면 Data Warehouse 관리자 를 사용하여 `orders` 및 `customers` 테이블을 만든 다음 라는 열을 만듭니다. `Customer LTV` 고객 테이블에서.

다음 사이에 새 경로를 설정하는 방법 살펴보기 `customers` 및 `orders`. 최종 목표는 의 새 집계된 열을 만드는 것입니다. `customers` 테이블을 참조하려면 먼저 `customers` Data Warehouse에서 테이블을 만든 다음 **[!UICONTROL Create a Column** > **&#x200B;정의 선택&#x200B;**> **합계]**.

그런 다음 소스 테이블을 선택해야 합니다. 에 대한 경로가 존재하는 경우 `orders` 테이블에서 드롭다운에서 선택하기만 하면 됩니다. 그러나 새 경로를 만드는 경우 **[!UICONTROL Create new path]** 그리고 아래 화면이 표시됩니다.

![새 경로 만들기](../../assets/Create_new_path.png)

여기서 결합하려는 두 테이블 간의 관계를 신중하게 고려해야 합니다. 이 경우 다음과 같은 문제가 발생할 수 있습니다 `Many` 연결된 주문 수 `One` customer, 따라서 `orders` 표는 다음에 나열됩니다. `Many` 반면에 `customers` 다음에서 선택된 테이블 `One` 옆이요.

>[!NOTE]
>
>위치 [!DNL Commerce Intelligence], a `path` 와 같음 `Join` SQL에서.

경로가 저장되면 다음을 만들 수 있습니다 `Customer LTV` 열! 아래를 참조하십시오.

![](../../assets/Customer_LTV.gif)

이제 새 을(를) 빌드했으므로 `Customer LTV` 의 열 `customers` 테이블, 다음을 만들 준비가 되었습니다. [지표 집계](#aggregate) 이 열 사용(예: 고객당 평균 LTV 찾기). 다음을 수행할 수도 있습니다. `group by` 또는 `filter` 를 기반으로 작성된 기존 지표를 사용하여 보고서에서 계산된 열 사용 `customers` 테이블.

>[!NOTE]
>
>후자의 경우 새 계산된 열을 작성할 때마다 다음을 수행해야 합니다 [기존 지표에 차원 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 를 로 사용하기 전에 `filter` 또는 `group by`.

다음을 참조하십시오 [계산된 열 만들기](../data-warehouse-mgr/creating-calculated-columns.md) Data Warehouse 관리자 사용.

## `Group By` 절

`Group By` 쿼리의 함수는에 자주 표시됩니다. [!DNL Commerce Intelligence] 시각적 보고서를 세그먼트화하거나 필터링하는 데 사용되는 열입니다. 예를 들어 을 다시 방문하겠습니다. `Total Revenue` 이전에 탐색한 쿼리이지만 이번에는 다음을 기준으로 매출을 세그먼트화합니다. `coupon\_code` 어떤 쿠폰이 가장 많은 매출을 창출하고 있는지 더 잘 이해하려면.

아래 쿼리로 시작하십시오.

| | |
|--- |--- |
| `SELECT coupon_code,` | 보고서 `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(열) |
| `FROM orders` | `Metric source` 표 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 지표 `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | 지표 `timestamp` (및 보고 `time range`) |
| `GROUP BY coupon_code` | 보고서 `group by` |

>[!NOTE]
>
>이전에 시작한 쿼리와 유일하게 다른 점은 group by로 &#39;coupon\_code&#39;를 추가한 것입니다._

동일하게 사용 `Total Revenue` 이전에 만든 지표이므로 이제 쿠폰 코드로 세그먼트화된 매출 보고서를 만들 준비가 되었습니다! 9월부터 11월까지 데이터를 보고 이 시각적 보고서를 설정하는 방법을 보여 주는 아래 gif를 참조하십시오.

![쿠폰 코드별 수익](../../assets/Revenue_by_coupon_code.gif)

## 공식

경우에 따라 쿼리는 개별 열 간의 관계를 계산하기 위해 여러 개의 집계를 포함할 수 있습니다. 예를 들어 다음 두 가지 방법 중 하나를 통해 쿼리의 평균 순서 값을 계산할 수 있습니다.

* `AVG('order\_total')` 또는
* `SUM('order\_total')/COUNT('order\_id')`

전자의 방법은 의 평균을 수행하는 새 지표를 만드는 것입니다. `order\_total` 열. 그러나 후자의 메서드는 를 계산하도록 이미 지표가 설정되어 있다고 가정할 때 Report Builder에서 직접 만들 수도 있습니다 `Total Revenue` 및 `Number of orders`.

한 걸음 물러서서 의 전체 쿼리를 살펴보십시오. `Average order value`:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | 지표 `operation` (열) |
| `COUNT(order_id) as "Number of orders"` | 지표 `operation` (열) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | 지표 `operation` (열) / 지표 작업 (열) |
| `FROM orders` | 지표 `source` 표 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 지표 `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | 지표 타임스탬프(및 보고 시간 범위) |

이제 를 계산하기 위해 이미 지표가 설정되어 있다고 가정합니다. `Total Revenue` 및 `Number of orders`. 이러한 지표가 있으므로 `Report Builder` 및 를 사용하여 온디맨드 계산을 만듭니다. `Formula` 기능:

![AOV 포물라](../../assets/AOV_forumula.gif)

## 요약

SQL 사용자가 많은 경우 쿼리가 번역되는 방식을 고려하십시오. [!DNL Commerce Intelligence] 를 사용하여 계산된 열, 지표 및 보고서를 작성할 수 있습니다.

빠른 참조를 위해 아래 표를 확인하십시오. SQL 절의 동등한 항목이 표시됩니다. [!DNL Commerce Intelligence] 요소 및 쿼리에서 사용하는 방법에 따라 두 개 이상의 요소에 매핑하는 방법을 설명합니다.

## Commerce Intelligence 요소

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` (시간 요소 포함) | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
