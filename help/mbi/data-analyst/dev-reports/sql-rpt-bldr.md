---
title: SQL Report Builder 사용
description: SQL Report Builder 사용의 원리에 대해 알아봅니다.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# 사용 [!DNL SQL Report Builder]

>[!NOTE]
>
>필요 [관리자 권한](../../administrator/user-management/user-management.md) SQL 차트를 만들고 편집합니다. `Standard` 사용자는 대시보드에서 이러한 차트를 재배열할 수 있습니다. `Read-only` 사용자는 기존 차트와 동일한 경험을 합니다. 또한, `Read-only` 사용자에게 쿼리 텍스트에 대한 액세스 권한이 없습니다.

다음을 참조하십시오. [교육 비디오](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) 자세히 알아보십시오.

[!DNL SQL]또는 Structured Query Language는 데이터베이스와 통신하는 데 사용되는 프로그래밍 언어입니다. 위치 [!DNL Commerce Intelligence], [!DNL SQL] 는 Data Warehouse에서 데이터를 쿼리하거나 검색하는 데 사용됩니다. 대시보드의 보고서를 살펴보십시오. 백그라운드에서 각 보고서를 [!DNL SQL] 쿼리.

다음을 사용할 수 있습니다. [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) Data Warehouse을 직접 쿼리하고 결과를 보고 차트로 변환합니다. 다음을 사용하여 보고서 만들기를 시작할 수 있습니다. [!DNL SQL Report Builder] 다음을 클릭: **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**.

다음을 참조하십시오. [교육 비디오](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) 자세히 알아보십시오.

다음 [!DNL SQL Report Builder] 에서는 Data Warehouse을 직접 쿼리하고 결과를 보고 차트로 빠르게 변환할 수 있습니다. 사용에 대한 가장 좋은 부분 [!DNL SQL] 보고서를 작성하려면 업데이트 주기에서 기다리지 않고 작성한 열을 반복할 필요가 없습니다. 결과가 올바르게 표시되지 않으면 예상과 일치할 때까지 쿼리를 빠르게 편집하고 다시 실행할 수 있습니다.

이 항목에서는 다음을 사용하는 방법을 안내합니다. [!DNL SQL Report Builder]. 방법을 알고 나면 [!DNL SQL] 시각화 튜토리얼의 경우 또는 작성한 쿼리 중 일부를 최적화하여 보십시오.

이 문서에서 다룬 내용:

1. [쿼리 작성](#writing)

1. [쿼리 실행 및 결과 보기](#runquery)

1. [시각화 만들기](#createviz)

1. [보고서 저장](#save)

## [!DNL SQL Report Builder] 통합

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) 은(는) 다음 제품과 함께 사용할 수 없는 유일한 통합입니다. [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md). 이 기능은 개발 중입니다.

만들기 시작하기 [!DNL SQL] 보고서, 클릭 **[!UICONTROL Report Builder]** 또는 **[!UICONTROL Add Report]** 을 클릭합니다. 다음에서 [!DNL Report Picker] 화면, 클릭 **[!UICONTROL SQL Report Builder]** 을(를) 열려면 [!DNL SQL] 편집자.

## 시작

보고서를 편집하려면 톱니바퀴(![](../../assets/gear-icon.png))의 오른쪽 위 모서리에 있는 아이콘 [!DNL SQL]-기반 차트 및 클릭 **[!UICONTROL Edit]**.

## 쿼리 작성 {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder] 쿼리는 대/소문자를 구분합니다. 쿼리를 작성할 때 올바른 대/소문자를 사용하고 있는지 또는 예기치 않은 결과나 오류가 발생할 수 있는지 확인하십시오.

팔로우 중 [쿼리 최적화 지침](../../best-practices/optimizing-your-sql-queries.md), 다음에 쿼리를 작성합니다. [!DNL SQL] 편집자.

>[!IMPORTANT]
>
>**의 지표 [!DNL SQL] 보고서** - SQL 보고서에 지표를 삽입할 때 `current definition` / 지표가 사용됩니다.

나중에 지표가 업데이트되면 SQL 보고서 *다음이 아님* 변경 사항을 반영합니다. 변경 사항을 적용하려면 보고서를 수동으로 편집해야 합니다.

사이드바 상단에 있는 버튼을 사용하여, [!DNL SQL Report Builder]. 목록에서 찾고 있는 항목이 표시되지 않으면 사이드바 상단에 있는 검색창을 사용하여 검색해 보십시오.

에서 사이드바를 사용할 수도 있습니다 [!DNL SQL] 마우스로 지표, 테이블 및 열을 가리키고 클릭하여 쿼리에 직접 삽입하는 편집기 **[!UICONTROL Insert]**:

![에 표 삽입 [!DNL SQL] 편집자.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>임의 [함수 선택](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST)또는 PostgreSQL에서 지원하는 데이터를 변경하지 않는 모든 함수는 SQL Report Builder에서 지원됩니다. 여기에는 AVG, COUNT, COUNT DISTINCT, MIN/MAX 및 SUM이 포함되지만 이에 국한되지 않습니다.

또한 `JOIN` 유형이 지원되지만 Adobe은 INNER JOIN이 `JOIN` 유형.

## 쿼리 실행 및 결과 보기 {#runquery}

쿼리 작성이 끝나면 **[!UICONTROL Run Query]**. 결과는 SQL 편집기 아래 표에 표시됩니다.

![쿼리를 실행하고 결과를 봅니다.](../../assets/SQL_Run_Query.gif)

결과에 문제가 있으면 쿼리를 편집하고 만족할 때까지 다시 실행할 수 있습니다.

가끔 볼 수 있습니다 [편집기 아래에 설명 메시지가 있습니다.](../../best-practices/optimizing-your-sql-queries.md). 이 중 하나가 표시되면 쿼리가 실행되지 않은 것이므로 약간의 세부 조정이 필요합니다.

쿼리 편집이 완료되면 시각화 만들기 또는 대시보드에 작업 저장으로 이동할 수 있습니다.

## 시각화 만들기 {#createviz}

쿼리 결과를 사용하여 시각화를 만들려면 **[!UICONTROL Chart]** 의 탭 `Results` 창. 이 탭에서 다음을 선택합니다.

* 다음 `Series`또는 측정할 열(예: ) **판매된 항목**.
* 다음 `Category`또는 데이터를 세그먼트화하는 데 사용할 열, 예: **획득 소스**.
* 다음 `Labels`또는 X축 값입니다.

다음은 시각화 프로세스의 모습입니다.

![](../../assets/SQL_RB_viz_overview.gif)

시각화를 만드는 방법에 대한 자세한 설명은 다음을 참조하십시오. [SQL 쿼리에서 시각화 만들기 자습서](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;}.

## 보고서 저장 {#save}

작업을 저장하려면 먼저 보고서에 이름을 지정해야 합니다. 다음 사항을 기억하십시오. [이름 지정에 대한 우수 사례 지침](../../best-practices/naming-elements.md){: target=&quot;_blank&quot;} 보고서 내용을 명확하게 전달하는 항목을 선택하십시오.

클릭 **[!UICONTROL Save]** 의 오른쪽 위 모서리 [!DNL SQL] 보고서를 편집하고 선택합니다. `Type` (`Chart` 또는 `Table`). 요약하려면 보고서를 저장할 대시보드를 선택하고 을(를) 클릭합니다 **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### 데이터 분석

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) 에서는 Data Warehouse을 직접 쿼리하고 결과를 보고 빠르게 보고서로 변환할 수 있습니다. 사용 [!DNL SQL] 을(를) 통해 다음을 수행할 수도 있습니다. [사용 [!DNL SQL] 사용할 수 없는 함수](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) 다음에서 `Visual` 또는 `Cohort` Report Builder을 통해 데이터를 보다 세밀하게 제어할 수 있습니다.

다음을 사용하여 생성된 계산된 열 [!DNL SQL] 는 업데이트 주기에 의존하지 않습니다. 즉, 원하는 대로 반복하고 결과를 즉시 확인할 수 있습니다.

>[!NOTE]
>
>이는 열의 구조에만 적용되며 데이터의 신선도는 적용되지 않습니다. 새 데이터는 여전히 성공적으로 완료된 업데이트 주기에 따라 달라집니다.

| **이건...** | **이것은 ...에게 그다지 좋지 않다.** |
|---|---|
| 중간/고급 분석가 | 초보자 - 다음을 알아야 합니다. [!DNL SQL]. |
| 다음 [!DNL SQL] 총명하 | 간단한 분석 - 쿼리를 작성하는 것은 을 사용하는 것보다 더 많은 작업이 가능합니다. [!UICONTROL Visual Report Builder]. |
| 일회성 계산된 열 작성 | 다른 사용자와 공유 - 대상자를 고려합니다. 이해 여부 [!DNL SQL]? 그렇지 않으면 보고서가 작성되는 방식에 의해 혼동될 수 있습니다. |
| 데이터 포함 `one-to-many` 관계 |  |
| 새 열 또는 분석 테스트 |  |

#### 데이터베이스와 SQL 편집기 결과 비교

대부분의 경우 업데이트 주기 때문에 결과의 차이가 발생할 수 있습니다. If [!DNL Commerce Intelligence] 은(는) 데이터베이스에서 Data Warehouse으로 데이터를 복제하는 중입니다. 동일한 쿼리를 사용하더라도 다른 결과가 표시될 수 있습니다.

연결 문제로 인해 불일치가 발생할 수도 있습니다. 다음 위치로 이동 `Connections` 클릭하여 페이지 만들기 **[!DNL Manage Data** > **Connections]** 확인하려면 해당 데이터베이스 통합에 오류가 있습니까? 이 경우 다음을 수행해야 합니다 [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html) 작업을 다시 실행할 수 있습니다.

모든 통합이 성공적으로 연결되었으며 업데이트 주기 중에 있지 않으면 다른 문제가 발생할 수 있습니다.

#### 삭제 중 [!DNL SQL] 내 Data Warehouse에서 기본 열도 삭제하시겠습니까?

아니요. 작성 방법과 관계없이 Data Warehouse에서 열을 손실하지 않습니다.

을 사용하여 생성된 열 `Data Warehouse Manager` 를 사용하는 보고서나 쿼리를 삭제해도 영향을 받지 않습니다.

을 사용하여 생성된 열 [!DNL SQL Report Builder] 이(가) Data Warehouse에 저장되지 않았습니다.


#### `Report Builder` 및 `SQL Report Builder`

다음 [!DNL SQL Report Builder] 차트를 만들고 구조화할 때 보다 유연하게 대처할 수 있습니다. 예를 들어 `X` 및 `Y` 도끼에. 에서 차트를 만드는 방법에 대한 자세한 내용은 [!DNL SQL Report Builder], 다음을 확인하십시오. [시각화 만들기 [!DNL SQL] 쿼리](../../tutorials/create-visuals-from-sql.md) 튜토리얼.

#### `Cohort Report Builder` {#cohortrb}

와(과) 달리 [!DNL Visual Report Builder], [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md) 은 시간의 흐름에 따라 유사한 사용자 그룹의 행동 트렌드를 분석하고 식별하는 단일 목적을 의미합니다. 사용 [!DNL Cohort Report Builder] 은(는) 다음을 필요로 하지 않습니다. [!DNL SQL] 사비, 그러니 이제 막 시작하기만 하면 망설임 없이 바로 뛰어들 수 있어.

| **이건...** | **이것은 ...에게 그다지 좋지 않다.** |
|---|---|
| 중간/고급 분석가 | 초보자 - 연습을 정의하는 집단이 필요합니다. |
| 시간 경과에 따른 행동 트렌드 식별 | 질적 분석 - 다음과 같을 수 있습니다. [완료](../dev-reports/create-qual-cohort-analysis.md), 그러나 Adobe 지원이 필요합니다. |

## 업데이트 주기 후 쿼리 다시 작성

쿼리를 다시 빌드할 필요는 없습니다. 를 사용하여 생성된 보고서 [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) 기존 템플릿에서 생성된 템플릿처럼 저장됩니다 `Report Builder`. 에 대한 업데이트 프로세스 [!DNL SQL] 차트는 동일합니다. 데이터가 업데이트되면 차트의 값이 다시 계산되고 다시 표시됩니다.

>[!NOTE]
>
>삭제 시 [!DNL SQL] 보고서/쿼리에서는 Data Warehouse의 기본 열이 삭제되지 않습니다. 열 작성 방법과 관계없이 열을 손실하지 않습니다.

* Data Warehouse 관리자를 사용하는 보고서나 쿼리를 삭제하면 보고서 관리자를 사용하여 만든 열은 영향을 받지 않습니다.

* SQL Report Builder을 사용하여 생성된 열은 Data Warehouse에 저장되지 않습니다.

## 요약 {#wrapup}

좀 더 어려운 작업을 시도하려면 시각화에 최적화된 쿼리를 작성해 보십시오. 다음을 확인하십시오. [시각화 만들기 [!DNL SQL] 쿼리 자습서](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;}
