---
title: Mixpanel 데이터가 필요합니다.
description: Mixpanel에서 로 가져올 수 있는 기본 데이터 표를 탐색합니다. [!DNL MBI] 계정이 필요합니다.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 예상됨 [!DNL Mixpanel] 데이터

후 [연결 [!DNL Mixpanel] account](../integrations/mixpanel.md)를 사용하여 다음을 수행할 수 있습니다. [Data Warehouse 관리자](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 분석을 위한 관련 데이터 필드를 쉽게 추적할 수 있습니다.

이 문서에서는 가져올 수 있는 기본 데이터 테이블을 살펴봅니다 [!DNL Mixpanel] 내 [!DNL MBI] 계정이 필요합니다. Mixpanel을 연결한 후 데이터 웨어하우스에 다음 테이블이 만들어집니다. 추적에 사용할 수 있는 모든 필드를 보려면 테이블 이름 열의 링크를 클릭합니다.

>[!NOTE]
>
>의 제한 사항으로 인해 [!DNL Mixpanel] API, 내역 데이터 - 연결 날짜로부터 7일 이전 [!DNL MBI] - 복제되지 않습니다.

| **테이블 이름** | **설명** |
|-----|-----|
| [`mixpanel\_export`](https://mixpanel.com/docs/api-documentation/exporting-raw-data-you-inserted-into-mixpanel#datafeed) | 이 표에는 이벤트, 이벤트 날짜 및 플랫폼 버킷을 포함한 원시 이벤트 데이터가 포함되어 있습니다. |
| [`mixpanel\_funnels`](https://mixpanel.com/docs/api-documentation/data-export-api#funnels-default) | 이 표에는 단계 ID, 단계 길이( 사용자가 단계를 완료해야 하는 일 수), 단계 시작일과 종료 날짜 등 단계 관련 데이터가 포함되어 있습니다. |
| [`mixpanel\_engage`](https://mixpanel.com/docs/api-documentation/data-export-api#engage-default) | 여기에는 세션 ID, 페이지 및 사용자 정보, 사용자가 마지막으로 본 날짜/시간 등 People Analytics의 데이터가 포함됩니다. |

{style=&quot;table-layout:auto&quot;}

## 관련 설명서

* [연결 중 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
