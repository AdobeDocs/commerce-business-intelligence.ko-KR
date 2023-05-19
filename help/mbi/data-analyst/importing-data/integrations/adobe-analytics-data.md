---
title: 예상 [!DNL Adobe Analytics] 데이터
description: RDS 인스턴스 연결 단계를 알아봅니다.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 예상 [!DNL Adobe Analytics] 데이터

다음 [!DNL Adobe Analytics] 통합 대상 [!DNL Adobe Commerce Intelligence] 를 사용합니다. [Analytics 2.0 Reporting API](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>예상한 데이터를 가져오려면 먼저 [!DNL Adobe Analytics] 원하는 지표 및 차원이 있는 작업 영역 이를 통해 데이터의 호환성과 가용성을 확인할 수 있습니다.

(이)라는 연결된 보고서 세트당 하나의 테이블 `report-suite-<ID>` (여기서 `<ID>` 은(는) 생성한 고유 ID입니다. [!DNL Commerce Intelligence])가 Data Warehouse에 생성됩니다.

이 테이블의 스키마는 통합 설정 프로세스에서 선택한 지표 및 차원으로 구성됩니다. 여러 추가 열이 다음에 의해 생성됩니다. [!DNL Commerce Intelligence], 식별 목적으로.

예를 들어 설정 중에 다음 지표 및 차원을 선택한 경우:
- `Metric`: `Page views`
- `Dimension`: `Page`

테이블에는 다음 열이 포함됩니다.

| 열 이름 | 설명 |
| --- | --- |
| `_id` | 이 열은 기본 키입니다. |
| `_item_hash` | [!DNL Commerce Intelligence] 고유 식별자. 이 열은 다음 사용자에 의해 생성됩니다. [!DNL Commerce Intelligence]. |
| `_updated_at` | 이 열에는 데이터 행이 마지막으로 업데이트된 시간이 포함됩니다. 작성자: [!DNL Commerce Intelligence]. |
| `start_date` | 행에 포함된 데이터의 시작 날짜입니다. `start_date` 는 한 행 내에 항상 같은 날의 00:00입니다. |
| `end_date` | 행에 포함된 데이터의 종료 날짜입니다. `end_date` 는 한 행 내에서 항상 같은 날의 23:59입니다. |
| `page_views` | 선택한 지표: 식별된 기간 동안의 총 페이지 보기 수입니다. |
| `page` | 선택한 차원: 추적된 보기가 있는 개별 페이지 이름. |

에서 사용할 수 있는 데이터가 있는 선택한 지표 및 차원을 제어합니다. [!DNL Commerce Intelligence] 테이블 사용 *동기화* 또는 *동기화 해제* 의 옵션 `Data Warehouse` 페이지를 가리키도록 업데이트하는 중입니다. 현재 동기화되지 않는 열이 회색으로 표시됩니다. 열 동기화를 중지하면 나중에 다시 동기화를 시작할 수 있습니다.

## 현재 제한 사항

이 섹션에서는 다음의 제한 사항에 대해 간략히 설명합니다. [!DNL Adobe Analytics] 통합 대상 [!DNL Commerce Intelligence].

| 제한 사항 | 설명 |
| --- | --- |
| `Historical data period` | 다른 타사 통합과 마찬가지로 [!DNL Adobe Analytics] 통합은 제한된 양의 이전 데이터를 가져온 다음 계속해서 데이터를 업데이트합니다. 이전 기간은 2주로 구성됩니다. |
| `Empty component combinations` | 일부 지표 및 차원 조합에는 데이터가 포함되어 있지 않습니다. 복제를 위해 이러한 조합을 선택한 경우 [!DNL Commerce Intelligence] 복제된 테이블에서 열을 제외합니다. 이러한 조합을 선택하지 않으려면 먼저 [[!DNL Adobe Analytics] 작업 영역](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) 예상한 데이터를 가져오는지 확인하려면 |
| `Re-authorization cadence` | 재인증 [!DNL Adobe Analytics] 2주마다 통합이 필요합니다. 재인증하려면 통합의 [편집] 페이지로 이동하여 **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] 은 한 번에 하나의 차원에 대한 지표 데이터를 제공합니다. 설정 중에 여러 차원을 선택하면 [!DNL Commerce Intelligence] 테이블에는 단일 차원 값과 각 차원에 대한 null이 포함되어 있습니다. |
