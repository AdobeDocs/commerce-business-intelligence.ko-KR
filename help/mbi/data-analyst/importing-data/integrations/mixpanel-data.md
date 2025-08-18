---
title: 예상 Mixpanel 데이터
description: Mixpanel에서  [!DNL Commerce Intelligence]  계정으로 가져올 수 있는 기본 데이터 테이블을 살펴봅니다.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '187'
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
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | 이 표에는 단계 ID, 단계 길이(사용자가 단계를 완료해야 하는 일 수) 및 단계의 시작 및 종료 날짜를 포함하여 단계에 대한 데이터가 포함되어 있습니다. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | 여기에는 세션 ID, 페이지 및 사용자 정보와 사용자가 마지막으로 조회된 날짜/시간을 포함하여 People Analytics의 데이터가 포함됩니다. |

{style="table-layout:auto"}

## 관련 설명서

* [ [!DNL Mixpanel] 연결 중](../integrations/mixpanel.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
