---
title: SQL 쿼리 최적화
description: SQL 쿼리를 최적화하는 방법을 알아봅니다.
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# SQL 쿼리 최적화

다음 [!DNL SQL Report Builder] 을(를) 사용하면 언제든지 해당 쿼리를 쿼리하고 반복할 수 있습니다. 이 기능은 작성한 열이나 보고서를 업데이트해야 한다는 사실을 인식하기 전에 업데이트 주기가 끝날 때까지 기다리지 않고 쿼리를 수정해야 할 때 유용합니다.

쿼리를 실행하기 전에, [[!DNL Commerce Intelligence] 예상 비용](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/sql-queries-explain-cost-errors.html). 비용은 쿼리를 실행하는 데 필요한 시간과 리소스 수를 고려합니다. 그 비용이 너무 높거나 반환된 행의 수를 초과하는 경우 [!DNL Commerce Intelligence] 제한, 쿼리가 실패합니다. 쿼리 [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md)를 사용하면 최대한 간소화된 쿼리를 작성할 수 있으므로, Adobe은 다음을 권장합니다.

## SELECT 사용 또는 모든 열 선택

모든 열을 선택해도 적시에 쉽게 실행되는 쿼리는 수행되지 않습니다. 를 사용하는 쿼리 `SELECT *` 를 실행하는 데 시간이 많이 걸릴 수 있습니다. 특히 테이블에 열이 많은 경우 더욱 그렇습니다.

이러한 이유로 Adobe은 를 사용하지 않는 것을 권장합니다 `SELECT *` 가능하면 필요한 열만 포함할 수 있습니다.

| **대신...** | **한번 해봐!** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style="table-layout:auto"}

## 전체 외부 조인 사용

외부 조인은 조인되는 두 테이블 전체를 선택하여 쿼리의 계산 비용을 증가시킵니다. 즉, 실행 제한보다 오래 걸리면 결과가 반환될 수 있으므로 쿼리를 실행하는 데 더 많은 시간이 소요되고 쿼리가 실패할 가능성이 높습니다.

이러한 유형의 조인 대신 내부 또는 왼쪽 조인을 사용하는 것이 좋습니다. 내부 조인은 테이블 간에 열 형식 일치가 있을 때만 결과를 반환합니다(예: `order_id` 은(는) 다음의 두 가지 형태로 존재한다. `customers` 및 `orders` table)을 참조하십시오. 왼쪽 조인은 왼쪽(첫 번째) 테이블의 모든 결과를 오른쪽(두 번째) 테이블의 일치 결과와 함께 반환합니다.

FULL OUTER JOIN 쿼리를 다시 작성하는 방법을 살펴봅니다.

| **대신...** | **한번 해봐!** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style="table-layout:auto"}

이러한 쿼리는 사용하는 JOIN 유형을 제외하고 모든 면에서 동일합니다.

## 여러 조인 사용

쿼리에 여러 조인을 포함할 수 있지만, 이 경우 쿼리 비용이 증가할 수 있습니다. Adobe 비용 임계값에 도달하지 않도록 하려면 가능한 한 여러 조인을 피하는 것이 좋습니다.

## 필터 사용

가능하면 필터를 사용하십시오. `WHERE` 및 `HAVING` 조항은 결과를 필터링하고 원하는 데이터만 제공합니다.

## JOIN 절에서 필터 사용

조인을 수행할 때 필터를 사용하는 경우 조인의 두 테이블 모두에 필터를 적용해야 합니다. 이는 중복이 되더라도 쿼리의 계산 비용을 감소시키고, 실행 시간을 감소시킨다.

| **대신...** | **한번 해봐!** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style="table-layout:auto"}

## 연산자 사용

쿼리를 작성할 때 가능한 &quot;가장 저렴한&quot; 연산자 사용을 고려하십시오. 모든 쿼리에는 계산 비용이 있으며 이는 쿼리를 구성하는 함수, 연산자 및 필터에 의해 결정됩니다. 일부 연산자는 계산 노력이 덜 필요하므로 다른 연산자보다 비용이 덜 든다.

비교 연산자(>, &lt;, = 등)가 가장 저렴하고 그 뒤에 오는 것이 좋습니다 [좋아요. 및 POSIX 연산자와 유사](https://www.postgresql.org/docs/9.5/functions-matching.html) 가장 비싼 교환원이 어디죠?

## 존재함 대 위치 사용

사용 `EXISTS` 및 `IN` 반환하려는 결과 유형에 따라 다릅니다. 단일 값에만 관심이 있는 경우 `EXISTS` 절 대신 `IN`. `IN` 는 쉼표로 구분된 값 목록과 함께 사용되어 쿼리의 계산 비용을 증가시킵니다.

날짜 `IN` 쿼리가 실행되면 시스템이 먼저 하위 쿼리를 처리해야 합니다( `IN` 문)을 참조하고 다음에서 지정한 관계를 기반으로 전체 쿼리를 만듭니다. `IN` 명령문입니다. `EXISTS` 는 쿼리를 여러 번 실행할 필요가 없어 훨씬 효율적입니다. 쿼리에 지정된 관계를 확인하는 동안 true/false 값이 반환됩니다.

간단히 말하면, 시스템은 를 사용할 때 많은 것을 처리하지 않아도 됩니다 `EXISTS`.

| **대신...** | **한번 해봐!** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style="table-layout:auto"}

## 정렬 기준 사용

`ORDER BY` 는 SQL에서 값비싼 함수이며 쿼리 비용을 크게 높일 수 있습니다. 쿼리의 EXPLAIN 비용이 너무 높다는 오류 메시지가 표시되면 아무 항목이나 제거하십시오 `ORDER BY`필요한 경우가 아니면 쿼리에서 을(를) 가져옵니다.

그런 말은 아닙니다 `ORDER BY` 사용할 수 없습니다. 필요한 경우에만 사용해야 합니다.

## 그룹화 기준 및 정렬 기준 사용

이 접근 방식이 수행하려는 작업에 부합하지 않는 경우가 있을 수 있습니다. 일반적인 규칙은 을 사용하는 경우입니다. `GROUP BY` 및 `ORDER BY`를 설정하는 경우 두 절의 열을 같은 순서로 지정해야 합니다. For example:

| **대신...** | **한번 해봐!** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style="table-layout:auto"}

## 요약

SQL을 작성하는 가장 좋은 방법은 시행착오를 통해서입니다. 가장 적합한 기능을 찾으려면 SQL 편집기만 사용하여 몇 개의 보고서를 다시 만드십시오.
