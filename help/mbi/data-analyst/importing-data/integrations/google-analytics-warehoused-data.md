---
title: 예상 Google Analytics 웨어하우스 데이터
description: Google Analytics 웨어하우스 데이터와 상호 작용하는 방법에 대해 알아봅니다.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# [!DNL Google Analytics Warehoused]개의 데이터가 필요합니다.

>[!NOTE]
>
>[관리자 권한](../../../administrator/user-management/user-management.md)이 필요합니다.

>[!NOTE]
>
>일부 정보는 [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics)에 있는 친구의 사용 권한과 함께 사용되었습니다.

[!DNL Google Analytics Warehoused]의 [!DNL Commerce Intelligence] 통합에서 [!DNL Google Analytics] [핵심 보고 API](https://developers.google.com/analytics/devguides/reporting/core/v3/)를 사용합니다.

>[!NOTE]
>
>예기치 않거나 중요하지 않은 결과를 방지하려면 사용하는 모든 차원이 [에서 사용하는 ](https://ga-dev-tools.google/dimensions-metrics-explorer/)하나 이상의 지표와 호환`Report Builder`되는지 확인하십시오.

단일 테이블(`report`)이 Data Warehouse에 만들어집니다.

이 테이블의 스키마는 설정 프로세스 중에 선택한 지표 및 차원과 `start-date` 및 `end-date` 두 개의 다른 열로 구성됩니다.

예를 들어, 설정하는 동안 다음 지표 및 차원을 선택했습니다.

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

이 표는 아래 예와 비슷합니다.

| **열 이름** | **설명** |
|-----|-----|
| `\_id` | 이 열은 `primary key`입니다. |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] 고유 식별자입니다. 이 열은 [!DNL Commerce Intelligence]에 의해 만들어집니다. |
| `\_updated\_at` | 이 열에는 데이터 행이 마지막으로 업데이트된 시간이 포함됩니다. 이 열은 [!DNL Commerce Intelligence]에 의해 만들어집니다. |
| `start-date` | 행이 지정된 요일에 대한 식별. |
| `end-date` | 행이 지정된 요일에 대한 식별. |
| `month` | 선택한 차원: 세션의 월로, 01에서 12 사이의 두 자리 정수입니다. |
| `users` | 선택한 지표: 요청한 기간의 총 사용자 수입니다. |

{style="table-layout:auto"}

## [!DNL Google Analytics Warehoused]과(와) [!DNL Live Integration]의 차이점

주요 차별화 요소는 하나의 통합이 저장되며([!DNL Google Analytics Warehoused]), 다른 통합은 저장되지 않는다는 점입니다([!DNL Google Analytics Live]). [!DNL Google Analytics Warehoused]의 경우 [!DNL Google Analytics] 데이터를 조작할 수 있으며, 이를 통해 [!DNL Google Analytics]과(와) 다른 데이터 소스를 결합하여 통찰력 있는 보고를 만들 수 있습니다.

[!DNL Google Analytics] 광고 캠페인에서 조작 관점에서 수행할 수 있는 작업의 예를 살펴보십시오. 이름이 다른 4분기 광고 캠페인이 여러 개 있다고 가정해 봅시다. 캠페인은 특정 마케팅 이니셔티브의 결과였습니다. 웨어하우스된 데이터를 사용하여 해당 캠페인 이름을 찾고 Q4 이니셔티브 이름 `Operation Dumbo`을(를) 반환하는 열을 만들 수 있습니다.

결합 측면을 사용하면 분석을 수행하기 위해 [!DNL Google Analytics] 데이터를 다른 데이터에 결합할 수 있습니다. 예를 들어, `Total Time On Site By Ad Campaign`의 [!DNL Google Analytics] 데이터를 가져와서 `Total Spent Per Campaign`의 [!DNL Facebook Ads] 데이터와 함께 참여하면 참여로 인해 비용이 얼마나 많이 소요되는지 전체적으로 파악할 수 있습니다.

반면에 [!DNL Google Analytics Live] 통합을 사용하면 모든 [!DNL Google Analytics] 차트는 [!DNL Commerce Intelligence] Data Warehouse에 저장되지 않은 작은 사일로와 같습니다.

## 관련 항목:

* [ [!DNL Google Analytics Warehoused] 연결 중](../integrations/google-analytics-warehoused.md)
