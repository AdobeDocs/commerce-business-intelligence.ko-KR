---
title: SQL 쿼리에서 시각화 만들기
description: SQL Report Builder에 사용되는 용어를 숙지하고 SQL 시각화를 작성하는 데 필요한 견고한 기반을 제공하는 방법에 대해 알아봅니다.
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
role: Admin, Data Architect, Data Engineer, Leader, User
feature: SQL Report Builder, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# SQL 쿼리에서 시각화 만들기

이 자습서의 목표는 [!DNL SQL Report Builder]에서 사용되는 용어를 숙지하고 `SQL visualizations`을(를) 만드는 견고한 기반을 제공하는 것입니다.

[[!DNL SQL Report Builder]](../data-analyst/dev-reports/sql-rpt-bldr.md)은(는) 옵션이 있는 Report Builder입니다. 데이터 테이블을 검색하기 위한 목적으로만 쿼리를 실행하거나 해당 결과를 보고서로 만들 수 있습니다. 이 자습서에서는 SQL 쿼리에서 시각화를 작성하는 방법을 설명합니다.

## Terminology

이 자습서를 시작하기 전에 `SQL Report Builder`에 사용된 다음 용어를 참조하십시오.

- `Series`: 측정하려는 열을 SQL Report Builder에서 시리즈라고 합니다. 일반적인 예로는 `revenue`, `items sold` 및 `marketing spend`이(가) 있습니다. 시각화를 만들려면 하나 이상의 열을 `Series`(으)로 설정해야 합니다.

- `Category`: 데이터를 세그먼트화하는 데 사용할 열을 `Category`이라고 합니다. 이는 `Group By`의 [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) 기능과 같습니다. 예를 들어 고객 생애 매출을 획득 소스로 분할하려면 획득 소스가 포함된 열이 `Category`(으)로 지정됩니다. 두 개 이상의 열을 `Category`(으)로 설정할 수 있습니다.

>[!NOTE]
>
>날짜 및 타임스탬프는 `Categories`(으)로도 사용할 수 있습니다. 쿼리의 다른 데이터 열일 뿐이며 쿼리 자체에서 원하는 대로 형식을 지정하고 순서를 지정해야 합니다.

- `Labels`: X축 레이블로 적용됩니다. 시간 경과에 따른 데이터 트렌드를 분석할 때 연도 및 월 열이 레이블로 지정됩니다. 둘 이상의 열을 레이블로 설정할 수 있습니다.

## 1단계: 쿼리 작성

다음 사항에 유의하십시오.

- [!DNL SQL Report Builder]이(가) [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html)을(를) 사용합니다.

- 시계열이 있는 보고서를 만드는 경우 타임스탬프 열을 `ORDER BY`해야 합니다. 이렇게 하면 타임스탬프가 보고서에서 올바른 순서로 표시됩니다.

- `EXTRACT` 함수는 타임스탬프의 일, 주, 월 또는 연도를 구문 분석하는 데 유용합니다. 보고서에 사용할 `time interval`이(가) `daily`, `weekly`, `monthly` 또는 `yearly`인 경우 유용합니다.

시작하려면 [!DNL SQL Report Builder]을(를) 클릭하여 **[!UICONTROL Report Builder** > **SQL Report Builder]**&#x200B;을(를) 엽니다.

예를 들어 각 제품에 대해 판매된 월별 총 항목 수를 반환하는 이 쿼리를 생각해 보십시오.

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

![제품, 연도 및 월별로 판매된 항목이 있는 SQL 쿼리 결과를 보여 주는 테이블](../assets/SQL_results_table.png)

## 2단계: 시각화 만들기

이러한 결과를 통해 *시각화를 만드는 방법을 알아보세요.* 시작하려면 **[!UICONTROL Chart]** 창에서 `Results` 탭을 클릭하십시오. `Chart settings` 탭이 표시됩니다.

쿼리가 처음 실행될 때 쿼리의 모든 열이 시리즈로 표시되기 때문에 보고서가 무시될 수 있습니다.

![모든 열이 계열로 표시되는 초기 SQL 보고서](../assets/SQL_initial_report_results.png)

이 예에서는 시간이 지남에 따라 트렌드가 바뀌는 선 차트가 되도록 합니다. 만들려면 다음 설정을 사용합니다.

- `Series`: 측정하려는 `Items sold` 열을 `Series`(으)로 선택합니다. `Series` 열을 정의하면 보고서에 한 줄이 표시됩니다.

- `Category`: 이 예에서는 각 제품을 보고서에서 다른 줄로 볼 수 있습니다. 이렇게 하려면 `Product name`을(를) `Category`(으)로 설정합니다.

- `Labels`: `year`을(를) 시간 경과에 따른 트렌드로 보려면 열 `month` 및 `Items Sold`을(를) x축의 레이블로 사용하십시오.

>[!NOTE]
>
>레이블의 열이 `ORDER BY`/`date`개인 경우 쿼리에 `time` 절이 있어야 합니다.

다음은 쿼리 실행에서 보고서 설정에 이르기까지 이 시각화를 만드는 방법을 간략히 보여줍니다.

![SQL 보고서 시각화 설정 구성에 대한 애니메이션 데모](../assets/SQL_report_settings.gif)

## 3단계: `Chart Type` 선택

이 예제에서는 `Line` 차트 유형을 사용합니다. 다른 `chart type`을(를) 사용하려면 차트 옵션 섹션 위의 아이콘을 클릭하여 변경합니다.

![선, 막대, 영역 및 기타 시각화 옵션을 포함한 사용 가능한 차트 유형 아이콘](../assets/Chart_types.png)

## 4단계: 시각화 저장

이 보고서를 다시 사용하려면 보고서 이름을 지정하고 오른쪽 상단의 **[!UICONTROL Save]**&#x200B;을(를) 클릭하십시오.

드롭다운에서 `Chart`을(를) `Type`(으)로 선택한 다음 대시보드를 선택하여 보고서를 저장합니다.

## 요약

한 걸음 더 나아가고 싶으세요? [쿼리 최적화 모범 사례](../best-practices/optimizing-your-sql-queries.md)를 확인하십시오.
