---
title: 예상 Google Analytics 웨어하우스 데이터
description: 웨어하우스된 Google Analytics 데이터와 상호 작용하는 방법에 대해 알아봅니다.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# 예상 [!DNL Google Analytics] 웨어하우징 데이터

>[!NOTE]
>
>필요 [관리자 권한](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>일부 정보는 다음 위치에서 친구들의 승인을 받아 사용되었습니다. [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] 통합 위치 [!DNL MBI] 를 사용합니다. [!DNL Google Analytics] [코어 보고 API](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>예기치 않거나 중요하지 않은 결과를 방지하려면 사용하는 차원이 모두 [하나 이상의 지표와 호환](https://ga-dev-tools.google/dimensions-metrics-explorer/) 다음에서 을 사용합니다. `Report Builder`.

단일 테이블 - 호출됨 `report` - 은(는) Data Warehouse에서 만들어집니다.

이 테이블의 스키마는 설정 프로세스 중에 선택한 지표 및 Dimension과 두 개의 다른 열로 구성됩니다. `start-date` 및 `end-date`.

예를 들어, 설정하는 동안 다음 지표 및 Dimension을 선택했습니다.

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

이 표는 아래 예와 비슷합니다.

| **열 이름** | **설명** |
|-----|-----|
| `\_id` | 이 열은 `primary key`. |
| `\_rjm\_record\_hash` | [!DNL MBI] 고유 식별자. 이 열은 다음 사용자에 의해 생성됩니다. [!DNL MBI]. |
| `\_updated\_at` | 이 열에는 데이터 행이 마지막으로 업데이트된 시간이 포함됩니다. 이 열은 다음 사용자에 의해 생성됩니다. [!DNL MBI]. |
| `start-date` | 행이 지정된 요일에 대한 식별. |
| `end-date` | 행이 지정된 요일에 대한 식별. |
| `month` | 선택한 차원: 세션의 월로, 01에서 12 사이의 두 자리 정수입니다. |
| `users` | 선택한 지표: 요청한 기간의 총 사용자 수입니다. |

{style="table-layout:auto"}

## 미리 알림: 웨어하우스 및 라이브 통합 Google Analytics의 차이점

주요 차별화 요소는 한 개의 통합이 저장된다는 것입니다([!DNL Google Analytics Warehoused]) 및 다른 하나는 ([!DNL Google Analytics Live]). 의 경우에는 [!DNL Google Analytics Warehoused], 이렇게 하면 을 조작할 수 있습니다. [!DNL Google Analytics] 데이터 및 를 결합하여 [!DNL Google Analytics] 통찰력 있는 보고를 만드는 기타 데이터 소스.

다음 항목 보기 [!DNL Google Analytics] 광고 캠페인 : 조작 관점에서 수행할 수 있는 작업의 예입니다. 이름이 다른 4분기 광고 캠페인이 여러 개 있다고 가정해 봅시다. 캠페인은 특정 마케팅 이니셔티브의 결과였습니다. 웨어하우스된 데이터를 사용하여 해당 캠페인 이름을 찾고 의 Q4 이니셔티브 이름을 반환하는 열을 만들 수 있습니다. `Operation Dumbo`.

조합 측면이 허용하는 경우 [!DNL Google Analytics] 분석을 수행하기 위해 다른 데이터에 결합할 데이터. 예를 들어 다음을 수행합니다. `Total Time On Site By Ad Campaign` 데이터 출처: [!DNL Google Analytics] and join가입 it up against `Total Spent Per Campaign` 데이터 출처: [!DNL Facebook Ads] 약정에 얼마나 많은 비용이 소요되고 있는지 전체적으로 파악할 수 있습니다.

포함 [!DNL Google Analytics Live] 반면, 모든 [!DNL Google Analytics] 차트는 파일에 저장되지 않은 작은 사일로와 같습니다 [!DNL MBI] Data Warehouse.

## 관련 항목:

* [연결 중 [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
