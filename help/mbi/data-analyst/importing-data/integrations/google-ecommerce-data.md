---
title: '[!DNL Google ECommerce]데이터가 필요합니다.'
description: Google Commerce와 공유하는 데이터 유형을 알아봅니다.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/tGcSyz6DHcusK-RomMkRZoyY7acXb0dmXlHcc5pW7cg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 158
ht-degree: 0%

---

# [!DNL Google ECommerce]개의 데이터가 필요합니다.

[!DNL Google ECommerce] 계정이 [!DNL Commerce Intelligence]에 연결되면 시스템에서 데이터를 `ecommerce`(으)로 가져오기 시작합니다. 이 테이블은 각 트랜잭션에 대한 데이터 행을 기록합니다. 여기에는 다음과 같은 주문 수준 데이터 열이 포함됩니다.

| 열 이름 | 설명 |
|-----|-----|
| `\_id` | 이 열은 기본 키입니다. |
| `accountId` | 이 열에는 [!DNL Google Analytics] 전자 상거래 계정과 연결된 계정 ID가 포함되어 있습니다. |
| `profileName` | 이 열에는 [!DNL Google Analytics] 프로필 이름이 포함되어 있습니다. |
| `profileId` | 이 열에는 [!DNL Google Analytics] 프로필 ID가 포함되어 있습니다. |
| `socialNetwork` | 이 열에는 소셜 네트워크의 이름이 포함되어 있습니다(예: [!DNL Facebook] 또는 [!DNL YouTube]). |
| `campaign` | 이 열에는 캠페인 이름(예: [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en))이 포함되어 있습니다. |
| `medium` | 이 열에는 미디어 이름이 포함되어 있습니다(예: [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `source` | 이 열에는 소스 이름이 포함되어 있습니다. (예: [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | 이 열에는 키워드 설명(예: [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en))이 포함되어 있습니다. |
| `transactionId` | 이 열에는 주문 ID가 포함되어 있습니다. 참조 데이터를 주문 데이터로 다시 결합하는 데 사용됩니다. |
| `updated\_at` | 이 열에는 데이터 행이 마지막으로 업데이트된 시간이 포함됩니다. |

{style="table-layout:auto"}
