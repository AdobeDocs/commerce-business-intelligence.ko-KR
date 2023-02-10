---
title: SQL Report Builder 사용
description: SQL Report Builder 사용에 대한 세부 사항을 알아봅니다.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1501'
ht-degree: 0%

---

# 사용 `SQL Report Builder`

>[!NOTE]
>
>필요한 경우 [관리자 권한](../../administrator/user-management/user-management.md) SQL 차트를 만들고 편집하려면 다음을 수행하십시오. `Standard` 사용자는 이러한 차트를 대시보드에서 다시 정렬할 수 있으며 `Read-only` 사용자는 기존 차트와 동일한 경험을 하게 됩니다. 게다가, `Read-only` 사용자는 쿼리의 텍스트에 액세스할 수 없습니다.

다음 문서를 참조하십시오 [교육 비디오](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=en) 추가 정보

`SQL`또는 구조화된 쿼리 언어인 는 데이터베이스와 통신하는 데 사용되는 프로그래밍 언어입니다. in [!DNL MBI], SQL은 Data Warehouse에서 데이터를 쿼리하거나 검색하는 데 사용됩니다. 대시보드의 보고서를 살펴봅니다. 이 보고서는 백그라운드에서 실행되며 각 보고서는 SQL 쿼리를 기반으로 합니다.

를 사용할 수 있습니다 [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) 데이터 웨어하우스를 직접 쿼리하려면 결과를 보고 차트로 변환합니다. 을 사용하여 보고서 만들기를 시작할 수 있습니다 `SQL Report Builder` 으로 이동 **[!UICONTROL Report Builder** > **SQL Report Builder]**.

다음 문서를 참조하십시오 [교육 비디오](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=en) 추가 정보

다음 `SQL Report Builder` 데이터 웨어하우스를 직접 쿼리하고 결과를 보고 차트로 빠르게 변환할 수 있습니다. SQL을 사용하여 보고서를 작성하는 데 가장 좋은 점은 업데이트 주기를 기다리지 않고 생성한 열을 반복할 필요가 없다는 것입니다. 결과가 제대로 표시되지 않으면 원하는 대로 쿼리를 신속하게 편집하고 다시 실행할 수 있습니다.

이 문서에서는 `SQL Report Builder`. 방법을 알고 나면 SQL에서 시각화 자습서를 확인하거나 작성한 쿼리 중 일부를 최적화합니다.

다음은 이 문서에서 다루는 내용에 대한 개요입니다.

1. [쿼리 쓰기](#writing)

1. [쿼리 실행 및 결과 보기](#runquery)

1. [시각화 만들기](#createviz)

1. [보고서 저장](#save)

## SQL Report Builder 통합

세계의 현 상태에서 [[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) 에서는 사용할 수 없는 유일한 통합입니다 [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md). Adobe는 이후 릴리스에서 이 기능을 포함하는 것을 계속 노력하고 있습니다.

새 SQL 보고서 만들기를 시작하려면 **[!UICONTROL Report Builder]** 또는 **[!UICONTROL Add Report]** 대시보드 맨 위에 있습니다. 에서 `Report Picker` 을 클릭하고 **[!UICONTROL SQL Report Builder]** SQL 편집기를 엽니다.

## 시작하기

보고서를 편집하려면 톱니바퀴(![](../../assets/gear-icon.png)) 아이콘을 클릭하고 **[!UICONTROL Edit]**.

## 쿼리 쓰기 {#writing}

>[!NOTE]
>
>`SQL Report Builder` 쿼리는 대/소문자를 구분합니다. 쿼리를 작성할 때 올바른 대/소문자를 사용하고 있는지 확인하거나 예기치 않은 결과나 오류가 발생할 수 있습니다.

다음을 수행합니다 [쿼리 최적화 지침](../../best-practices/optimizing-your-sql-queries.md)SQL 편집기에서 쿼리를 작성합니다.

>[!IMPORTANT]
>
>**SQL 보고서의 지표** - SQL 보고서에 지표를 삽입하면 `current definition` 이 사용됩니다.

지표가 나중에 업데이트되는 경우 SQL 보고서가 *안 함* 변경 사항을 반영합니다. 변경 사항을 적용하려면 보고서를 수동으로 편집해야 합니다.

사이드바 상단에 있는 버튼을 사용하여 `SQL Report Builder`. 목록에서 찾고 있는 내용이 표시되지 않으면 사이드바 위쪽에 있는 검색 막대를 사용하여 검색해 보십시오.

SQL 편집기의 사이드바를 사용하여 지표, 테이블 및 열을 마우스로 가리키고 를 클릭하여 쿼리에 직접 삽입할 수도 있습니다 **[!UICONTROL Insert]**:

![SQL 편집기에 테이블 삽입](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>임의 [SELECT 함수](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST)또는 PostgreSQL에서 지원하는 데이터를 변형하지 않는 모든 함수는 SQL Report Builder에서 지원됩니다. 여기에는 AVG, COUNT, COUNT DISTINCT, MIN/MAX 및 SUM이 포함되지만, 이에 제한되지 않습니다.

또한 모든 JOIN 유형이 지원되지만 INNER JOIN은 JOIN 유형에서 가장 저렴한 가격이므로 사용만 사용하는 것이 좋습니다.

## 쿼리 실행 및 결과 보기 {#runquery}

쿼리 작성을 마쳤으면 **[!UICONTROL Run Query]**. 결과는 SQL 편집기 아래의 표에 표시됩니다.

![쿼리 실행 및 결과 보기](../../assets/SQL_Run_Query.gif)

결과가 잘못된 것 같은 경우 쿼리를 편집하고 만족될 때까지 다시 실행할 수 있습니다.

가끔 [편집기 아래에 EXPLAIN이 포함된 메시지](../../best-practices/optimizing-your-sql-queries.md). 이 중 하나가 표시된다면 쿼리가 실행되지 않고 약간 세밀하게 조정해야 함을 의미합니다.

쿼리 편집을 완료한 후 시각화를 만들거나 작업을 대시보드에 저장할 수 있습니다.

## 시각화 만들기 {#createviz}

쿼리 결과를 사용하여 시각화를 만들려면 **[!UICONTROL Chart]** 탭에서 다음을 수행합니다. `Results` 창 이 탭에서 다음을 선택합니다.

* 다음 `Series`또는 측정할 열(예: ) **판매된 품목**.
* 다음 `Category`또는 데이터를 세그먼트화하는 데 사용할 열(예: ) **획득 소스**.
* 다음 `Labels`또는 X축 값.

다음은 시각화 프로세스가 어떻게 표시되는지 간략히 설명한 것입니다.

![](../../assets/SQL_RB_viz_overview.gif)

시각화를 만드는 방법에 대한 자세한 설명은 [SQL 쿼리에서 시각화 만들기 자습서](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;}.

## 보고서 저장 {#save}

작업을 저장하려면 먼저 보고서에 이름을 지정해야 합니다. 다음 사항을 따라야 합니다 [우수 사례 이름 지정 지침](../../best-practices/naming-elements.md){: target=&quot;_blank&quot;} 를 선택하고 보고서가 무엇인지 명확하게 전달하는 항목을 선택하십시오.

클릭 **[!UICONTROL Save]** sql 편집기 오른쪽 상단 모서리에서 보고서를 선택합니다 `Type` (`Chart` 또는 `Table`). 마무리하려면 보고서를 저장할 대시보드를 선택하고 을(를) 클릭합니다 **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### 데이터 분석

#### `SQL Report Builder`

[`The SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) 는 데이터 웨어하우스를 직접 쿼리하고 결과를 보고 신속하게 보고서로 변환할 수 있는 기능을 제공합니다. SQL을 사용하면 [사용할 수 없는 SQL 함수를 활용하려면](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) 에서 `Visual` 또는 `Cohort` Report Builder으로 인해 데이터를 보다 세밀하게 제어할 수 있습니다.

SQL을 사용하여 만든 계산된 열은 업데이트 주기에 종속되지 않으므로 원하는 대로 반복할 수 있으며 결과를 즉시 볼 수 있습니다.

>[!NOTE]
>
>이는 데이터의 새로 고침이 아니라 열의 구조에만 적용됩니다. 새 데이터는 여전히 성공적으로 완료된 업데이트 주기에 따라 달라집니다.

| **이건..** | **이건...** |
|---|---|
| 중간/고급 분석가 | 초보자 - SQL을 알아야 합니다. |
| SQL 지식 | 단순 분석 - 쿼리 작성은 Visual Report Builder을 사용하는 것보다 더 많은 작업을 수행할 수 있습니다. |
| 일회용 계산된 열 작성 | 다른 사람과 공유 - 대상을 고려합니다. SQL을 이해합니까? 그렇지 않으면 보고서가 작성되는 방식에 대해 혼동될 수 있습니다. |
| 데이터 `one-to-many` 관계 |  |
| 새 열 또는 분석 테스트 |  |

#### 데이터베이스와 SQL 편집기 결과 비교

대부분의 경우 결과의 차이는 업데이트 주기에 영향을 줄 수 있습니다. If [!DNL MBI] 는 데이터베이스에서 Data Warehouse으로 데이터를 복제하는 과정에 있으며, 동일한 쿼리를 사용해도 다른 결과를 볼 수 있습니다.

연결 문제로 인해 불일치가 발생할 수도 있습니다. 로 이동합니다 `Connections` 페이지를 클릭하여 **[!DNL Manage Data** > **Connections]**)에서 확인할 수 있습니다. 해당 데이터베이스 통합에 오류가 있습니까? 그런 경우 다음을 수행해야 합니다. [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en) 다시 실행할 수 있도록

모든 통합이 성공적으로 연결되고 업데이트 주기 중에 있지 않은 경우 다른 문제가 될 수 있습니다.

#### SQL 보고서를 삭제하면 내 Data Warehouse에서 기본 열도 삭제됩니까?

아니요. Data Warehouse을 작성한 방식에 관계없이 열의 일부를 잃지 않습니다.

를 사용하여 만든 열 `Data Warehouse Manager` 사용하는 보고서나 쿼리를 삭제해도 영향을 받지 않습니다.

를 사용하여 만든 열 `SQL Report Builder` Data Warehouse에 저장되지 않습니다.


#### `Report Builder` 비교 `SQL Report Builder`

다음 `SQL Report Builder` 차트를 만들고 구조화할 때 보다 유연하게 만듭니다. 예를 들어, `X` 및 `Y` 축. 차트 만들기에 대한 자세한 내용은 `SQL Report Builder`, 다음 문서를 확인하십시오. [SQL 쿼리에서 시각화 만들기](../../tutorials/create-visuals-from-sql.md) 자습서입니다.

#### `Cohort Report Builder` {#cohortrb}

와 달리 `Visual Report Builder`, [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) 시간 경과에 따라 유사한 사용자 그룹의 행동 트렌드를 분석 및 식별하는 단일 목적을 위한 것입니다. 집단 Report Builder을 사용하는 것은 SQL 지식이 필요하지 않으므로 바로 시작하는 중이라면 망설이지 않고 바로 시작할 수 있습니다.

| **이건..** | **이건...** |
|---|---|
| 중간/고급 분석가 | 초보자 - 집단을 정의하는 연습이 필요합니다. |
| 시간 경과에 따른 행동 트렌드 식별 | 질적 분석 - 다음을 수행할 수 있습니다. [완료](../dev-reports/create-qual-cohort-analysis.md)하지만 도움이 필요합니다. |

## 업데이트 주기 후 질의 재구축

쿼리를 다시 빌드할 필요는 없습니다. 보고서를 사용하여 만든 보고서 [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) 기존 제품에서 생성된 와 마찬가지로 저장됩니다. `Report Builder`. SQL 차트의 업데이트 프로세스는 동일합니다. 데이터가 업데이트되면 차트의 값이 다시 계산되고 다시 표시됩니다.

>[!NOTE]
>
>SQL 보고서/쿼리를 삭제할 때 Data Warehouse에서 기본 열이 삭제되지 않습니다. 작성된 방식에 관계없이 열이 손실되지 않습니다.

* Data Warehouse 관리자를 사용하여 만든 열은 해당 열을 사용하는 보고서나 쿼리를 삭제하면 영향을 받지 않습니다.

* SQL Report Builder을 사용하여 만든 열은 Data Warehouse에 저장되지 않습니다.

## 포장 {#wrapup}

좀 더 어려운 작업을 시도하려면 시각화에 최적화된 쿼리를 작성해 보십시오. 저희 회사 [SQL 쿼리에서 시각화 만들기 자습서](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;} 를 시작할 수 있습니다.
