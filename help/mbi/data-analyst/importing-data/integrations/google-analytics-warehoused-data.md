---
title: Warehouse에서 가져온 데이터 Google Analytics 예상
description: Google Analytics 웨어하우징 데이터와 상호 작용하는 방법을 알아봅니다.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# 예상됨 [!DNL Google Analytics] 웨어하우스 데이터

>[!NOTE]
>
>필요한 경우 [관리자 권한](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>일부 정보는 다음 위치에서 친구들로부터 허락을 받아 사용되었습니다. [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] 통합 [!DNL MBI] 활용 [!DNL Google Analytics] [핵심 보고 API](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>예기치 않거나 비상식적인 결과를 방지하려면 사용하는 모든 차원이 [지표와 호환됩니다](https://developers.google.com/analytics/devguides/reporting/core/dimsmets) 에서 `Report Builder`.

단일 테이블 - `report` - Data Warehouse에서 만들어집니다.

이 테이블의 스키마는 설정 프로세스 중에 선택한 지표 및 Dimension과 다른 두 열로 구성됩니다. `start-date` 및 `end-date`.

예를 들어, 설정 중에 다음 지표 및 Dimension을 선택한 경우,

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

표는 아래 예와 비슷합니다.

| **열 이름** | **설명** |
|-----|-----|
| `\_id` | 이 열은 `primary key`. |
| `\_rjm\_record\_hash` | [!DNL MBI] 고유 식별자. 이 열은 [!DNL MBI]. |
| `\_updated\_at` | 이 열에는 데이터 행이 마지막으로 업데이트된 시간이 포함됩니다. 이 열은 [!DNL MBI]. |
| `start-date` | 행이 필요한 날의 확인. |
| `end-date` | 행이 필요한 날의 확인. |
| `month` | 선택한 차원: 세션의 월이며 01에서 12까지의 두 자리 정수입니다. |
| `users` | 선택한 지표: 요청한 기간의 총 사용자 수입니다. |

{style=&quot;table-layout:auto&quot;}

## 미리 알림: Warehouse와 Live Integration의 차이점

주요 차별화 요소는 하나의 통합이 저장된다는 것입니다([!DNL Google Analytics Warehoused])이고, 다른 것은 ([!DNL Google Analytics Live]). 의 경우 [!DNL Google Analytics Warehoused]이렇게 하면 사용자의 [!DNL Google Analytics] 데이터 및 는 [!DNL Google Analytics] 통찰력 있는 보고를 만드는 기타 데이터 소스

한번 봅시다 [!DNL Google Analytics] 광고 캠페인을 추가하여 조작 관점에서 수행할 수 있는 작업의 예를 알아봅니다. 이름이 다른 Q4에 대한 여러 광고 캠페인이 있다고 가정합니다. 캠페인은 특정 마케팅 이니셔티브의 결과였습니다. 웨어러블 데이터를 사용하여 문제가 있는 캠페인 이름을 찾아 다음과 같은 Q4 이니셔티브 이름을 반환하는 새 열을 만들 수 있습니다. `Operation Dumbo`.

조합 양상은 [!DNL Google Analytics] 분석을 수행하기 위해 다른 데이터에 결합할 데이터입니다. 예를 들어, `Total Time On Site By Ad Campaign` 데이터 [!DNL Google Analytics] 반대편에 서 `Total Spent Per Campaign` 데이터 [!DNL Facebook Ads] 비용이 얼마나 소요되는지 완전히 파악할 수 있습니다.

사용 [!DNL Google Analytics Live] 반면, 모든 [!DNL Google Analytics] 차트는 작은 사일로(Silo)와 같습니다 [!DNL MBI] data warehouse.

## 관련:

* [연결 중 [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
