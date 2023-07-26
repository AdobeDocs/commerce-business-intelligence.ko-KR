---
title: SQL Report Builder 작업
description: 결과를 로컬 데이터베이스의 데이터와 비교할 수 있도록 SQL Report Builder을 사용하여 데이터 및 지표를 감사하는 방법을 알아봅니다.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Data Architect, Data Engineer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# [!DNL SQL Report Builder]

다음 [!DNL SQL Report Builder] 는 주로 새 보고서를 작성하고 분석을 반복하는 데 사용되지만, 데이터 및 지표를 효과적으로 감사하는 데에도 사용할 수 있습니다. 다음 정보는 다음을 사용하여 데이터 및 지표를 감사하는 방법을 설명합니다. [!DNL SQL Report Builder] 로컬 데이터베이스의 데이터와 결과를 비교할 수 있습니다.

## 지표 쿼리

시작하려면 [!DNL SQL Report Builder] 로 이동하여 **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. 다음에서 사이드바를 사용할 수 있습니다. [!DNL SQL] 지표 위로 마우스를 이동하고 을 클릭하여 지표를 쿼리에 직접 삽입하는 편집기 **[!UICONTROL Insert]**. 이렇게 하면 해당 지표의 쿼리 정의가 편집기에 추가됩니다. 정의에는 다음 구성 요소가 포함됩니다.

- 다음 **지표 작업** 수행 중, 표시 `SUM()` 아래 예제에서.
- 다음 **테이블 기준** 지표가 만들어지는에 의해 표시됩니다. `FROM` 절.
- 임의 **필터(및 필터 세트)** 로 표시된 지표에 추가되었습니다. `WHERE` 아래 예제의 조항입니다.
- 의 구성 요소 **timestamp** (년, 월) 데이터를 주문할 때 (으)로 표시 `ORDER BY` 아래 예제의 조항입니다.

쿼리를 더 명확하게 보려면 쿼리 필드에 쿼리가 표시되는 방식을 다시 지정할 수 있습니다. 준비가 되면 다음을 선택합니다. `Run Query`. 결과는 쿼리 아래의 보고서 패널에 표로 채워집니다.

![](../../assets/run-query-results.gif)

## 쿼리 제한

특정 불일치나 데이터 세트를 찾아내려면 쿼리를 특정 샘플로 제한하여 로컬 데이터베이스를 확인해야 합니다. 원하는 제한 사항과 일치하도록 쿼리를 편집하여 이 작업을 수행할 수 있습니다. 다음 예제에서는 2013년 1월 1일 이후의 매출만 포함하도록 쿼리를 제한합니다. 쿼리를 업데이트한 후 **[!UICONTROL Run Query]** 다시 클릭하여 결과를 업데이트합니다.

![](../../assets/restricting-query.gif)

## 저장 및 내보내기

보고서가 사용자의 요구를 충족하면 보고서에 고유한 이름을 지정하고 **[!UICONTROL Save]**&#x200B;을 클릭하고 저장할 보고서 유형과 대시보드를 선택합니다. Adobe 지표를 감사할 때는 보고서를 (으)로 저장하는 것이 좋습니다. `Table` 테스트 대시보드에 저장합니다.

보고서가 저장되면 을 선택하여 해당 대시보드로 이동합니다. `Go to Dashboard`. 여기에서 보고서를 찾고 을 선택하여 데이터를 내보낼 수 있습니다 **[!UICONTROL Options gear > Full `.csv`내보내기]** 또는 **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## 사용자 정의 쿼리

사용자 지정 쿼리를 작성하고 결과를 내보내 로컬 데이터베이스와 비교할 수도 있습니다. 팔로우 중 [쿼리 최적화 지침](../../best-practices/optimizing-your-sql-queries.md)SQL 편집기에서 쿼리를 작성합니다. 사이드바 상단에 있는 버튼을 사용하여 다음에서 사용할 수 있는 테이블 및 지표 목록 간을 전환할 수 있습니다. [!DNL SQL Report Builder] 쿼리에 추가합니다. 사용자 지정 쿼리가 요구 사항에 맞으면 보고서를 저장하고 대시보드에서 해당 데이터를 내보낼 수 있습니다.

>[!NOTE]
>
>데이터를 감사한 후 불일치가 발견되면 [지원 문의: 데이터 불일치](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) 지원 주제에서 다음 작업에 대해 자세히 알아보십시오.
