---
title: SQL 쿼리에서 시각화 만들기
description: SQL Report Builder에서 사용되는 용어를 숙지하고 SQL 시각화를 만드는 탄탄한 기반을 제공하는 방법을 알아봅니다.
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# SQL 쿼리에서 시각화 만들기

이 자습서의 목표는 에서 사용되는 용어를 숙지하는 것입니다 `SQL Report Builder` 그리고, `SQL visualizations`.

다음 [`SQL Report Builder`](../data-analyst/dev-reports/sql-rpt-bldr.md) 는 선택 사항이 있는 report builder 입니다. 데이터 테이블 검색을 위해 쿼리를 실행하거나 해당 결과를 보고서로 변환할 수 있습니다. 이 자습서에서는 SQL 쿼리에서 시각화를 만드는 방법을 설명합니다.

## 용어

이 자습서를 시작하기 전에 `SQL Report Builder`.

- `Series`: 측정하려는 열을 SQL Report Builder에서 시리즈라고 합니다. 일반적인 예는 다음과 같습니다 `revenue`, `items sold`, 및 `marketing spend`. 하나 이상의 열을 `Series` 시각화를 만들려면

- `Category`: 데이터를 세그먼트화하는 데 사용할 열을 `Category` 이것은 `Group By` 의 기능 [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md). 예를 들어 고객의 라이프타임 매출을 획득 소스별로 세그먼트화하려는 경우 획득 소스가 포함된 열을 로 지정합니다. `Category`. 두 개 이상의 열을 `Category`.

>[!NOTE]
>
>날짜 및 타임스탬프를 `Categories`. 이는 쿼리의 다른 데이터 열이며 쿼리 자체에서 원하는 대로 형식을 지정하고 순서를 지정해야 합니다.

- `Labels`: x축 레이블로 적용됩니다. 시간 경과에 따른 데이터 트렌드를 분석할 때 연도 및 월 열은 일반적으로 레이블로 지정됩니다. 두 개 이상의 열을 레이블로 설정할 수 있습니다.

## 1단계: 쿼리 쓰기

다음 사항에 주의하십시오.

- 다음 `SQL Report Builder` 사용 [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html).

- 시계열로 보고서를 만드는 경우 다음을 수행하십시오 `ORDER BY` 타임스탬프 열입니다. 이렇게 하면 타임스탬프가 보고서에서 올바른 순서로 표시되는지 확인합니다.

- 다음 `EXTRACT` 함수는 타임스탬프의 일, 주, 월 또는 연도를 구문 분석하는 데 사용할 수 있습니다. 이 기능은 `time interval` 보고서에서 을 사용하려면 `daily`, `weekly`, `monthly`, 또는 `yearly`.

시작하려면 `SQL Report Builder` 를 클릭합니다. **[!UICONTROL Report Builder** > **SQL Report Builder]**.

예를 들어, 각 제품에 대해 판매된 월별 총 항목 수를 반환하는 이 쿼리를 고려해 보십시오.

```sql
    SELECT SUM("qty") AS "Items Sold", "products's name" AS "product name",
    EXTRACT(year from "Order date") AS "year",
    EXTRACT(month from "Order date") AS "month"
    FROM "items"
    WHERE "products's name" LIKE '%Jeans'
    GROUP BY  "products's name", "year","month"
    ORDER BY "year" ASC,"month" ASC
    LIMIT 3500
```

이 쿼리는 다음 결과 테이블을 반환합니다.

![](../assets/SQL_results_table.png)

## 2단계: 시각화 만들기

이 결과를 보면 *시각화를 만드는 방법* 시작하려면 **[!UICONTROL Chart]** 탭에서 다음을 수행합니다. `Results` 창 그러면 `Chart settings` 탭.

쿼리가 처음 실행되면 쿼리의 모든 열이 시리즈로 표시되므로 보고서가 실행 취소할 수 없습니다.

![](../assets/SQL_initial_report_results.png)

이 예제에서는 시간에 따른 트렌드를 나타내는 선 차트가 되도록 합니다. 만들려면 다음 설정을 사용합니다.

- `Series`: 을(를) 선택합니다 `Items sold` 열 `Series` 측정하고 싶으니까 을(를) 정의한 후 `Series` 열에서 보고서에 한 줄이 표시됩니다.

- `Category`: 이 예에서는 보고서에서 각 제품을 다른 라인으로 확인하려고 합니다. 이를 위해 `Product name` 로서의 `Category`.

- `Labels`: 열 사용 `year` 및 `month` 를 볼 수 있도록 x축에 있는 레이블로 `Items Sold` 시간 경과에 대한 트렌드입니다.

>[!NOTE]
>
>쿼리에 `ORDER BY` 라벨이 있는 경우 라벨에 조항 `date`/`time` 열.

다음은 쿼리 실행에서 보고서 설정에 이르기까지 이 시각화를 만든 방법을 간략히 설명한 것입니다.

![](../assets/SQL_report_settings.gif)

## 3단계: 선택 `Chart Type`

이 예제에서는 `Line` 차트 유형입니다. 다른 `chart type`을 눌러 차트 옵션 섹션 위에 있는 아이콘을 눌러 변경합니다.

![](../assets/Chart_types.png)

## 4단계: 시각화 저장

이 보고서를 다시 사용하려면 보고서에 이름을 지정하고 **[!UICONTROL Save]** 오른쪽 상단 모서리에서

드롭다운에서 을(를) 선택합니다. `Chart` 로서의 `Type` 그런 다음 보고서를 저장할 대시보드입니다.

## 축하합니다! 다 끝났어

한 걸음 더 나아가실래요? 다음을 확인하십시오 [쿼리 최적화 모범 사례](../best-practices/optimizing-your-sql-queries.md).
