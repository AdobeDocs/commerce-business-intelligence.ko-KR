---
title: SQL Report Builder 사용
description: SQL Report Builder 사용의 원리에 대해 알아봅니다.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 0%

---

# [!DNL SQL Report Builder] 사용 중

>[!NOTE]
>
>SQL 차트를 만들고 편집하려면 [관리자 권한](../../administrator/user-management/user-management.md)이 필요합니다. `Standard`명의 사용자가 대시보드에서 이러한 차트를 다시 정렬할 수 있으며 `Read-only`명의 사용자가 기존 차트와 동일한 경험을 합니다. 또한 `Read-only`명의 사용자가 쿼리 텍스트에 액세스할 수 없습니다.

자세한 내용은 [교육 비디오](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=ko)를 참조하세요.

[!DNL SQL] 또는 Structured Query Language는 데이터베이스와 통신하는 데 사용되는 프로그래밍 언어입니다. [!DNL Commerce Intelligence]에서 [!DNL SQL]은(는) Data Warehouse에서 데이터를 쿼리하거나 검색하는 데 사용됩니다. 대시보드의 보고서를 살펴보십시오. 각 보고서는 [!DNL SQL] 쿼리로 제공됩니다.

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)을(를) 사용하여 Data Warehouse을 직접 쿼리하고 결과를 보고 차트로 변환할 수 있습니다. [!DNL SQL Report Builder]을(를) 클릭하여 **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**&#x200B;에서 보고서 만들기를 시작할 수 있습니다.

자세한 내용은 [교육 비디오](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=ko)를 참조하세요.

[!DNL SQL Report Builder]을(를) 사용하면 Data Warehouse을 직접 쿼리하고 결과를 보고 차트로 빠르게 변환할 수 있습니다. [!DNL SQL]을(를) 사용하여 보고서를 작성하는 가장 좋은 방법은 업데이트 주기를 기다리지 않고 만든 열을 반복할 필요가 없다는 것입니다. 결과가 올바르게 표시되지 않으면 예상과 일치할 때까지 쿼리를 빠르게 편집하고 다시 실행할 수 있습니다.

이 항목에서는 [!DNL SQL Report Builder]을(를) 사용하는 방법을 소개합니다. 방법을 알고 나면 [!DNL SQL]에서 시각화 튜토리얼을 확인하거나 작성한 쿼리 중 일부를 최적화해 보십시오.

이 문서에서 다룬 내용:

1. [쿼리 작성](#writing)

1. [쿼리 실행 및 결과 보기](#runquery)

1. [시각화 만들기](#createviz)

1. [보고서 저장](#save)

## [!DNL SQL Report Builder] 통합

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md)은(는) [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)에서 사용할 수 없는 유일한 통합입니다. 이 기능은 개발 중입니다.

[!DNL SQL] 보고서 만들기를 시작하려면 대시보드 맨 위에서 **[!UICONTROL Report Builder]** 또는 **[!UICONTROL Add Report]**&#x200B;을(를) 클릭합니다. [!DNL Report Picker] 화면에서 **[!UICONTROL SQL Report Builder]**&#x200B;을(를) 클릭하여 [!DNL SQL] 편집기를 엽니다.

## 시작

보고서를 편집하려면 ![&#x200B; 기반 차트의 오른쪽 위 모서리에 있는 톱니바퀴(](../../assets/gear-icon.png)톱니바퀴 아이콘[!DNL SQL]) 아이콘을 클릭하고 **[!UICONTROL Edit]**&#x200B;을(를) 클릭하십시오.

## 쿼리 작성 {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder] 쿼리는 대/소문자를 구분합니다. 쿼리를 작성할 때 올바른 대/소문자를 사용하고 있는지 또는 예기치 않은 결과나 오류가 발생할 수 있는지 확인하십시오.

[쿼리 최적화에 대한 지침](../../best-practices/optimizing-your-sql-queries.md)에 따라 [!DNL SQL] 편집기에서 쿼리를 작성하십시오.

>[!IMPORTANT]
>
>**개 보고서의 [!DNL SQL]지표** - SQL 보고서에 지표를 삽입하면 지표의 `current definition`이(가) 사용됩니다.

나중에 지표가 업데이트되면 SQL 보고서 *이(가) 변경 내용을 반영하지 않습니다*. 변경 사항을 적용하려면 보고서를 수동으로 편집해야 합니다.

사이드바 상단의 단추를 사용하여 [!DNL SQL Report Builder]에서 사용할 수 있는 테이블 목록과 지표 목록을 전환할 수 있습니다. 목록에서 찾고 있는 항목이 표시되지 않으면 사이드바 상단에 있는 검색창을 사용하여 검색해 보십시오.

[!DNL SQL] 편집기의 사이드바를 사용하여 지표, 테이블 및 열을 마우스로 가리키고 **[!UICONTROL Insert]**&#x200B;을(를) 클릭하여 쿼리에 직접 삽입할 수도 있습니다.

![테이블을 [!DNL SQL] 편집기에 삽입합니다.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>PostgreSQL에서 지원하는 모든 [SELECT 함수](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST) 또는 데이터를 변경하지 않는 모든 함수는 SQL Report Builder에서 지원됩니다. 여기에는 AVG, COUNT, COUNT DISTINCT, MIN/MAX 및 SUM이 포함되지만 이에 국한되지 않습니다.

또한 모든 `JOIN` 형식이 지원되지만, Adobe에서는 `JOIN` 형식 중 비용이 가장 저렴하므로 INNER JOIN만 사용하는 것이 좋습니다.

## 쿼리 실행 및 결과 보기 {#runquery}

쿼리 쓰기가 완료되면 **[!UICONTROL Run Query]**&#x200B;을(를) 클릭합니다. 결과는 SQL 편집기 아래 표에 표시됩니다.

![쿼리를 실행하고 결과를 봅니다.](../../assets/SQL_Run_Query.gif)

결과에 문제가 있으면 쿼리를 편집하고 만족할 때까지 다시 실행할 수 있습니다.

편집기 아래에 [EXPLAIN이 포함된 메시지](../../best-practices/optimizing-your-sql-queries.md)가 표시될 수 있습니다. 이 중 하나가 표시되면 쿼리가 실행되지 않은 것이므로 약간의 세부 조정이 필요합니다.

쿼리 편집이 완료되면 시각화 만들기 또는 대시보드에 작업 저장으로 이동할 수 있습니다.

## 시각화 만들기 {#createviz}

쿼리 결과를 사용하여 시각화를 만들려면 **[!UICONTROL Chart]** 창의 `Results` 탭을 클릭합니다. 이 탭에서 다음을 선택합니다.

* `Series` 또는 측정할 열(예: **판매된 항목**).
* `Category` 또는 데이터를 세그먼트화하는 데 사용할 열(예: **획득 소스**).
* `Labels` 또는 X축 값입니다.

다음은 시각화 프로세스의 모습입니다.

![SQL Report Builder 시각화 개요 애니메이션 데모](../../assets/SQL_RB_viz_overview.gif)

시각화를 만드는 방법에 대한 자세한 설명은 [SQL 쿼리에서 시각화 만들기 자습서](../../tutorials/create-visuals-from-sql.md){: target="_blank"}를 참조하십시오.

## 보고서 저장 {#save}

작업을 저장하려면 먼저 보고서에 이름을 지정해야 합니다. [명명 모범 사례 지침](../../best-practices/naming-elements.md){: target="_blank"}을(를) 따르고 보고서가 무엇인지 명확하게 전달하는 항목을 선택하십시오.

**[!UICONTROL Save]** 편집기의 오른쪽 상단 모서리에서 [!DNL SQL]을(를) 클릭하고 보고서 `Type`(`Chart` 또는 `Table`)을(를) 선택합니다. 정리하려면 보고서를 저장할 대시보드를 선택하고 **[!UICONTROL Save to Dashboard]**&#x200B;을(를) 클릭합니다.

![대시보드에 SQL 보고서를 저장하는 애니메이션 데모](../../assets/SQL_Save_Report.gif)

### 데이터 분석

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)을(를) 사용하면 Data Warehouse을 직접 쿼리하고 결과를 보고 빠르게 보고서로 변환할 수 있습니다. [!DNL SQL]을(를) 사용하면 [&#x200B; 또는  [!DNL SQL]  보고서 빌더에서 &#x200B;](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html)사용할 수 없는`Visual`함수를 사용`Cohort`할 수 있으므로 데이터를 보다 세밀하게 제어할 수 있습니다.

[!DNL SQL]을(를) 사용하여 만든 계산된 열은 업데이트 주기에 종속되지 않습니다. 즉, 원하는 대로 반복하고 결과를 즉시 확인할 수 있습니다.

>[!NOTE]
>
>이는 열의 구조에만 적용되며 데이터의 신선도는 적용되지 않습니다. 새 데이터는 여전히 성공적으로 완료된 업데이트 주기에 따라 달라집니다.

| **다음 작업에 적합합니다...** | **다음 용도로는 적합하지 않습니다...** |
|---|---|
| 중간/고급 분석가 | 초보자 - [!DNL SQL]을(를) 알아야 합니다. |
| [!DNL SQL] 지식인 | 간단한 분석 - [!UICONTROL Visual Report Builder]을(를) 사용하는 것보다 쿼리를 작성하는 것이 더 효과적입니다. |
| 일회성 계산된 열 작성 | 다른 사람과 공유하기 - 대상자를 고려합니다. [!DNL SQL]을(를) 이해합니까? 그렇지 않으면 보고서가 작성되는 방식에 의해 혼동될 수 있습니다. |
| 관계가 `one-to-many`인 데이터 |  |
| 새 열 또는 분석 테스트 |  |

#### 데이터베이스와 SQL 편집기 결과 비교

대부분의 경우 업데이트 주기 때문에 결과의 차이가 발생할 수 있습니다. [!DNL Commerce Intelligence]이(가) 데이터베이스에서 Data Warehouse으로 데이터를 복제하는 중이면 동일한 쿼리를 사용하더라도 다른 결과가 표시될 수 있습니다.

연결 문제로 인해 불일치가 발생할 수도 있습니다. `Connections`을(를) 클릭하여 **[!DNL Manage Data** > **Connections]** 페이지로 이동하여 확인합니다. 해당 데이터베이스 통합에 오류가 있습니까? 이 경우 다시 실행하려면 [통합을 다시 인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ko)해야 할 수 있습니다.

모든 통합이 성공적으로 연결되었으며 업데이트 주기 중에 있지 않으면 다른 문제가 발생할 수 있습니다.

#### [!DNL SQL] 보고서를 삭제하면 내 Data Warehouse에서 기본 열도 삭제됩니까?

아니요. 작성 방법과 관계없이 Data Warehouse에서 열을 손실하지 않습니다.

`Data Warehouse Manager`을(를) 사용하여 만든 열은 해당 열을 사용하는 보고서나 쿼리를 삭제하면 영향을 받지 않습니다.

[!DNL SQL Report Builder]을(를) 사용하여 만든 열이 Data Warehouse에 저장되지 않습니다.


#### `Report Builder` 및 `SQL Report Builder`

[!DNL SQL Report Builder]을(를) 사용하면 차트를 만들고 구조화할 때 보다 유연하게 작업할 수 있습니다. 예를 들어, `X` 및 `Y` 축에 표시할 값을 선택할 수 있습니다. [!DNL SQL Report Builder]에서 차트를 만드는 방법에 대한 자세한 내용을 보려면 [쿼리 [!DNL SQL] 쿼리에서 시각화 만들기](../../tutorials/create-visuals-from-sql.md) 자습서를 확인하십시오.

#### `Cohort Report Builder` {#cohortrb}

[!DNL Visual Report Builder]과(와) 달리 [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md)은(는) 시간 경과에 따른 유사한 사용자 그룹의 동작 트렌드를 분석하고 식별하는 단일 목적입니다. [!DNL Cohort Report Builder]을(를) 사용하면 [!DNL SQL] 지식이 필요하지 않으므로 막 시작하는 경우에는 주저하지 않고 바로 시작할 수 있습니다.

| **다음 작업에 적합합니다...** | **다음 용도로는 적합하지 않습니다...** |
|---|---|
| 중간/고급 분석가 | 초보자 - 연습을 정의하는 집단이 필요합니다. |
| 시간 경과에 따른 행동 트렌드 식별 | 질적 분석 - [완료](../dev-reports/create-qual-cohort-analysis.md)할 수 있지만 Adobe 지원이 필요합니다. |

## 업데이트 주기 후 쿼리 다시 작성

쿼리를 다시 빌드할 필요는 없습니다. [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)을(를) 사용하여 만든 보고서는 기존 `Report Builder`에서 만든 보고서와 같이 저장됩니다. [!DNL SQL] 차트에 대한 업데이트 프로세스는 동일합니다. 데이터가 업데이트되면 차트의 값이 다시 계산되고 다시 표시됩니다.

>[!NOTE]
>
>[!DNL SQL] 보고서/쿼리를 삭제할 때 Data Warehouse에서 기본 열이 삭제되지 않습니다. 열 작성 방법과 관계없이 열을 손실하지 않습니다.

* Data Warehouse Manager를 사용하여 생성된 열은 이를 사용하는 보고서나 쿼리를 삭제하는 경우 영향을 받지 않습니다.

* SQL Report Builder을 사용하여 만든 열은 Data Warehouse에 저장되지 않습니다.

## 요약 {#wrapup}

좀 더 어려운 작업을 시도하려면 시각화에 최적화된 쿼리를 작성해 보십시오. 시작하려면 [시각화 만들기 [!DNL SQL] 쿼리 튜토리얼](../../tutorials/create-visuals-from-sql.md){: target="_blank"}을 확인하십시오.
