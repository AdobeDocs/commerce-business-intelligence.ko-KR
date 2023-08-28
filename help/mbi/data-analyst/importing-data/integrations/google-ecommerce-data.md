---
title: 예상[!DNL Google ECommerce]데이터
description: Google Commerce와 공유하는 데이터 유형을 알아봅니다.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 3f16484f189f6b4a8b072d2e3514d2f170993d60
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# 예상 [!DNL Google ECommerce] 데이터

다음 이후 [!DNL Google ECommerce] 계정이 정상적으로 연결되었습니다. [!DNL Commerce Intelligence], 시스템은 제목이 있는 테이블로 데이터 가져오기를 시작합니다 `ecommerce`. 이 테이블은 각 트랜잭션에 대한 데이터 행을 기록합니다. 여기에는 다음과 같은 주문 수준 데이터 열이 포함됩니다.

| 열 이름 | 설명 |
|-----|-----|
| `\_id` | 이 열은 기본 키입니다. |
| `accountId` | 이 열에는 사용자와 연결된 계정 ID가 포함되어 있습니다. [!DNL Google Analytics] 전자 상거래 계정. |
| `profileName` | 이 열에는 [!DNL Google Analytics] 프로필 이름. |
| `profileId` | 이 열에는 [!DNL Google Analytics] 프로필 ID. |
| `socialNetwork` | 이 열에는 소셜 네트워크의 이름이 포함됩니다(예: [!DNL Facebook], 또는 [!DNL YouTube]) |
| `campaign` | 이 열에는 캠페인 이름(예: [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | 이 열에는 미디어 이름이 포함됩니다(예: [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | 이 열에는 소스 이름이 포함되어 있습니다. (예: [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | 이 열에는 키워드 설명(예: [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | 이 열에는 주문 ID가 포함되어 있습니다. 참조 데이터를 주문 데이터로 다시 결합하는 데 사용됩니다. |
| `updated\_at` | 이 열에는 데이터 행이 마지막으로 업데이트된 시간이 포함됩니다. |

{style="table-layout:auto"}
