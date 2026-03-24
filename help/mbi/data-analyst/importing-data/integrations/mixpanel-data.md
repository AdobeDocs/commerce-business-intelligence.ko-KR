---
title: 예상 Mixpanel 데이터
description: Mixpanel에서  [!DNL Commerce Intelligence]  계정으로 가져올 수 있는 기본 데이터 테이블을 살펴봅니다.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iM6GzisImrjed7uCZf6lf6HIze9MwWdhq2gEP-IrIXA
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 187
ht-degree: 0%

---

# [!DNL Mixpanel]개의 데이터가 필요합니다.

[계정 [!DNL Mixpanel] 연결](../integrations/mixpanel.md)한 후 [Data Warehouse 관리자](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)를 사용하여 분석할 관련 데이터 필드를 쉽게 추적할 수 있습니다.

이 항목에서는 [!DNL Mixpanel]에서 [!DNL Commerce Intelligence] 계정으로 가져올 수 있는 기본 데이터 테이블을 살펴봅니다. [!DNL Mixpanel]을(를) 연결한 후 Data Warehouse에 다음 테이블이 만들어집니다. 추적에 사용할 수 있는 모든 필드를 보려면 테이블 이름 열의 링크를 클릭합니다.

>[!NOTE]
>
>[!DNL Mixpanel] API의 제한으로 인해 내역 데이터(연결 날짜로부터 [!DNL Commerce Intelligence]까지 7일 이상 경과한 데이터)는 복제되지 않습니다.

| **테이블 이름** | **설명** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | 이 표에는 이벤트, 이벤트 날짜 및 플랫폼 버킷을 포함한 원시 이벤트 데이터가 포함되어 있습니다. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | 이 표에는 funnel ID, funnel 길이(사용자가 funnel을 완료하는 데 필요한 일 수), funnel의 시작 및 종료 날짜 등 유입 경로에 대한 데이터가 포함되어 있습니다. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | 여기에는 세션 ID, 페이지 및 사용자 정보와 사용자가 마지막으로 조회된 날짜/시간을 포함하여 People Analytics의 데이터가 포함됩니다. |

{style="table-layout:auto"}

## 관련 설명서

* [ [!DNL Mixpanel] 연결 중](../integrations/mixpanel.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
