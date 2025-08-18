---
title: ' [!DNL Adobe Analytics] 데이터가 필요합니다.'
description: RDS 인스턴스 연결 단계를 알아봅니다.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# [!DNL Adobe Analytics]개의 데이터가 필요합니다.

[!DNL Adobe Analytics]에 대한 [!DNL Adobe Commerce Intelligence] 통합에서 [Analytics 2.0 보고 API](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md)를 사용합니다.

>[!INFO]
>
>예상한 데이터를 얻으려면 먼저 원하는 지표 및 차원을 사용하여 [!DNL Adobe Analytics] Workspace에서 보고서를 빌드할 수 있습니다. 이를 통해 데이터의 호환성과 가용성을 확인할 수 있습니다.

연결된 보고서 세트당 하나의 테이블 `report-suite-<ID>`(여기서 `<ID>`은(는) [!DNL Commerce Intelligence]에서 생성한 고유 ID임)이 Data Warehouse에 만들어집니다.

이 테이블의 스키마는 통합 설정 프로세스에서 선택한 지표 및 차원으로 구성됩니다. [!DNL Commerce Intelligence]에서도 식별 목적으로 몇 개의 추가 열을 생성합니다.

예를 들어 설정 중에 다음 지표 및 차원을 선택한 경우:
- `Metric`: `Page views`
- `Dimension`: `Page`

테이블에는 다음 열이 포함됩니다.

| 열 이름 | 설명 |
| --- | --- |
| `_id` | 이 열은 기본 키입니다. |
| `_item_hash` | [!DNL Commerce Intelligence] 고유 식별자입니다. 이 열은 [!DNL Commerce Intelligence]에 의해 만들어집니다. |
| `_updated_at` | 이 열에는 데이터 행이 마지막으로 업데이트된 시간이 포함됩니다. [!DNL Commerce Intelligence]에 의해 만들어집니다. |
| `start_date` | 행에 포함된 데이터의 시작 날짜입니다. `start_date`은(는) 한 행 내에서 항상 같은 날의 00:00입니다. |
| `end_date` | 행에 포함된 데이터의 종료 날짜입니다. `end_date`은(는) 한 행 내에서 항상 같은 날의 23:59입니다. |
| `page_views` | 선택한 지표: 식별된 기간 동안의 총 페이지 보기 수입니다. |
| `page` | 선택한 차원: 추적된 보기가 있는 개별 페이지 이름. |

[!DNL Commerce Intelligence] 페이지의 *동기화* 또는 *비동기화* 옵션을 사용하여 선택한 지표 및 차원 중 `Data Warehouse` 테이블에서 사용할 수 있는 데이터가 있는 차원을 제어합니다. 현재 동기화되지 않는 열이 회색으로 표시됩니다. 열 동기화를 중지하면 나중에 다시 동기화를 시작할 수 있습니다.

## 현재 제한 사항

이 섹션에서는 [!DNL Adobe Analytics]에 대한 [!DNL Commerce Intelligence] 통합의 제한 사항에 대해 간략히 설명합니다.

| 제한 사항 | 설명 |
| --- | --- |
| `Historical data period` | 다른 타사 통합과 마찬가지로 [!DNL Adobe Analytics] 통합은 제한된 양의 이전 데이터를 가져온 다음 데이터를 계속 업데이트합니다. 이전 기간은 2주로 구성됩니다. |
| `Empty component combinations` | 일부 지표 및 차원 조합에는 데이터가 포함되어 있지 않습니다. 복제를 위해 이러한 조합을 선택한 경우 [!DNL Commerce Intelligence]은(는) 복제된 테이블에서 열을 제외합니다. 이러한 조합을 선택하지 않으려면 먼저 [[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=ko)에서 보고서를 만들어 예상한 데이터를 가져오는지 확인할 수 있습니다. |
| `Re-authorization cadence` | [!DNL Adobe Analytics] 통합의 재인증이 2주마다 필요합니다. 다시 승인하려면 통합을 위한 편집 페이지로 이동하여 **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**&#x200B;을(를) 클릭합니다. |
| `One dimension per row` | [!DNL Adobe Analytics]에서 한 번에 하나의 차원에 대한 지표 데이터를 제공합니다. 설정하는 동안 여러 차원을 선택하는 경우 [!DNL Commerce Intelligence] 테이블의 각 행에는 각 차원에 대한 단일 차원 값과 Null이 포함됩니다. |
