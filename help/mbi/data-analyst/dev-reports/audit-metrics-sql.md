---
title: SQL Report Builder 작업
description: 결과를 로컬 데이터베이스의 데이터와 비교할 수 있도록 SQL Report Builder을 사용하여 데이터 및 지표를 감사하는 방법을 알아봅니다.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# `SQL Report Builder`

다음 `SQL Report Builder` 는 주로 새 보고서를 작성하고 분석을 반복하는 데 사용되지만, 데이터 및 지표를 효과적으로 감사하는 데 사용할 수도 있습니다. 다음 정보는 를 사용하여 데이터 및 지표를 감사하는 방법을 설명합니다. `SQL Report Builder` 결과를 로컬 데이터베이스의 데이터와 비교할 수 있습니다.

## 지표 쿼리

시작하려면 `SQL Report Builder` 으로 이동 **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. SQL 편집기의 사이드바를 사용하여 지표를 마우스로 가리키고 를 클릭하여 쿼리에 직접 지표를 삽입할 수 있습니다 **[!UICONTROL Insert]**. 이렇게 하면 해당 지표의 쿼리 정의가 편집기에 추가됩니다. 정의에는 다음 구성 요소가 포함됩니다.

- 다음 **지표 작업** 수행 중, 아래 예에서 SUM()으로 표시됩니다.
- 다음 **테이블** FROM 절에 의해 지시되는 지표가 빌드된 지표입니다.
- 임의 **필터(및 필터 세트)** 이 값은 아래 예에서 WHERE 절로 표시되어 지표에 추가되었습니다.
- 의 구성 요소 **timestamp** (년, 월) 데이터를 정렬할 대상. 아래 예에서 ORDER BY 절로 표시됩니다.

쿼리의 내용을 더 명확하게 보려면 쿼리 필드에 표시되는 방식을 다시 지정할 수 있습니다. 준비가 되면 을(를) 선택합니다. `Run Query`. 결과는 쿼리 아래 보고서 패널에 표로 채워집니다.

![](../../assets/run-query-results.gif)

## 쿼리 제한

특정 불일자나 데이터 집합을 찾아낼 경우 로컬 데이터베이스를 확인하기 위해 쿼리를 특정 샘플로 제한해야 합니다. 원하는 제한 사항과 일치하도록 쿼리를 편집하여 이 작업을 수행할 수 있습니다. 다음 예제에서는 2013년 1월 1일 이후 수익만 포함하도록 쿼리를 제한합니다. 쿼리를 업데이트한 후 **[!UICONTROL Run Query]** 결과를 업데이트하기 위해 다시 선택합니다.

![](../../assets/restricting-query.gif)

## 저장 및 내보내기

보고서가 사용자의 요구를 충족하면 보고서에 고유 이름을 지정하고 을(를) 클릭하여 대시보드에 저장합니다 **[!UICONTROL Save]**, 저장할 보고서 유형과 대시보드를 선택합니다. 지표를 감사할 때 보고서를 `Table` 테스트 대시보드에 저장합니다.

보고서가 저장되면 을(를) 선택하여 해당 대시보드로 이동합니다 `Go to Dashboard`. 여기에서 보고서를 찾고 데이터를 선택하여 내보낼 수 있습니다 **[!UICONTROL Options gear > Full `.csv`내보내기]** 또는 **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## 사용자 지정 쿼리

사용자 정의 쿼리를 작성하고 결과를 내보내 로컬 데이터베이스와 비교할 수도 있습니다. 다음을 수행합니다 [쿼리 최적화 지침](../../best-practices/optimizing-your-sql-queries.md)SQL 편집기에서 쿼리를 작성합니다. 사이드바 상단에 있는 버튼을 사용하여 `SQL Report Builder` 쿼리에 추가합니다. 사용자 지정 쿼리가 필요한 경우 보고서를 저장하고 대시보드에서 해당 데이터를 내보낼 수 있습니다.

### 아직도 얼어?

데이터를 감사한 후 불일치가 발견되면 [지원 문의: 데이터 불일치](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html?lang=en) 다음으로 수행할 작업에 대한 자세한 내용은 지원 문서를 참조하십시오.
