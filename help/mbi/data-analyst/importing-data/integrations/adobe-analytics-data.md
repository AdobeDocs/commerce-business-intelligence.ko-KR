---
title: 예상됨 [!DNL Adobe Analytics] 데이터
description: RDS 인스턴스를 연결하는 단계를 알아봅니다.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# 예상됨 [!DNL Adobe Analytics] 데이터

다음 [!DNL Adobe Analytics] 통합 [!DNL MBI] 사용 [Analytics 2.0 보고 API](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>필요한 데이터를 가져오기 위해 먼저 [!DNL Adobe Analytics] 원하는 지표 및 차원이 있는 작업 공간입니다. 이렇게 하면 데이터의 호환성 및 가용성을 확인할 수 있습니다.

연결된 보고서 세트당 하나의 테이블 - 호출됨 `report-suite-<ID>`, 위치 `<ID>` 에서 생성한 고유 ID입니다. [!DNL MBI] - Data Warehouse에서 만들어집니다.

이 테이블의 스키마는 통합 설정 프로세스에서 선택한 지표와 차원으로 구성됩니다. 몇 개의 추가 열도 [!DNL MBI], 식별을 위한 것입니다.

예를 들어, 설정 중에 다음 지표 및 차원을 선택한 경우,
- `Metric`: `Page views`
- `Dimension`: `Page`

테이블에는 다음 열이 포함됩니다.

| 열 이름 | 설명 |
| --- | --- |
| `_id` | 이 열이 기본 키입니다. |
| `_item_hash` | [!DNL MBI] 고유 식별자. 이 열은 [!DNL MBI]. |
| `_updated_at` | 이 열에는 데이터 행이 마지막으로 업데이트된 시간이 포함됩니다. 이 보고서는 [!DNL MBI]. |
| `start_date` | 행에 포함된 데이터의 시작 날짜입니다. `start_date` 은 항상 한 행 내에 같은 날의 00:00입니다. |
| `end_date` | 행에 포함된 데이터의 종료 날짜입니다. `end_date` 는 항상 한 행 내에 같은 날 23:59가 됩니다. |
| `page_views` | 선택한 지표: 식별된 기간에 대한 총 페이지 보기 수입니다. |
| `page` | 선택한 차원: 추적된 보기가 있는 개별 페이지 이름. |

선택한 지표 및 차원 중 어느 차원에서 데이터를 사용할 수 있는지 제어합니다. [!DNL MBI] 테이블 *동기화* 또는 *unsync* 옵션 `Data Warehouse` 페이지. 현재 동기화되지 않는 열이 회색으로 표시됩니다. 열 동기화를 중지하면 나중에 동기화를 다시 시작할 수 있습니다.

## 현재 제한 사항

이 섹션에서는 [!DNL Adobe Analytics] 통합 [!DNL MBI].

| 제한 사항 | 설명 |
| --- | --- |
| `Historical data period` | 다른 타사 통합과 마찬가지로 [!DNL Adobe Analytics] 통합은 제한된 양의 이전 데이터를 가져온 다음 계속해서 데이터를 업데이트합니다. 이전 기간은 2주로 구성됩니다. |
| `Empty component combinations` | 일부 지표 및 차원 조합에는 데이터가 포함되어 있지 않습니다. 이러한 조합이 복제용으로 선택된 경우, [!DNL MBI] 복제된 테이블에서 열을 제외합니다. 이러한 조합을 선택하지 않으려면 먼저 [[!DNL Adobe Analytics] 작업 공간](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=en) 예상한 데이터를 가져올 수 있는지 확인합니다. |
| `Re-authorization cadence` | 의 재인증 [!DNL Adobe Analytics] 통합은 현재 2주마다 필요합니다. 재인증하려면 통합에 대한 편집 페이지로 이동한 다음 를 클릭합니다 **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] 한 번에 하나의 차원에 대한 지표 데이터를 제공합니다. 설정 중에 여러 차원을 선택하면 [!DNL MBI] 테이블에는 서로 다른 차원에 대한 단일 차원 값과 null이 포함됩니다. |
