---
title: 예상 Mixpanel 데이터
description: Mixpanel에서 로 가져올 수 있는 기본 데이터 표를 살펴봅니다. [!DNL MBI] 계정입니다.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 예상 [!DNL Mixpanel] 데이터

다음 이후 [다음을 연결했습니다. [!DNL Mixpanel] account](../integrations/mixpanel.md), 다음을 사용할 수 있습니다. [Data Warehouse 관리자](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 분석을 위해 관련 데이터 필드를 쉽게 추적할 수 있습니다.

이 문서에서는 가져올 수 있는 기본 데이터 테이블에 대해 살펴봅니다. [!DNL Mixpanel] 에 [!DNL MBI] 계정입니다. Mixpanel을 연결한 후 Data Warehouse에 다음 표가 만들어집니다. 추적에 사용할 수 있는 모든 필드를 보려면 테이블 이름 열의 링크를 클릭합니다.

>[!NOTE]
>
>의 제한 사항으로 인해 [!DNL Mixpanel] API, 내역 데이터 - 연결일로부터 7일이 지난 데이터입니다. [!DNL MBI] - 은 복제되지 않습니다.

| **테이블 이름** | **설명** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | 이 표에는 이벤트, 이벤트 날짜 및 플랫폼 버킷을 포함한 원시 이벤트 데이터가 포함되어 있습니다. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | 이 표에는 단계 ID, 단계 길이(사용자가 단계를 완료해야 하는 일 수) 및 단계의 시작 및 종료 날짜를 포함하여 단계에 대한 데이터가 포함되어 있습니다. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | 여기에는 세션 ID, 페이지 및 사용자 정보와 사용자가 마지막으로 조회된 날짜/시간을 포함하여 People Analytics의 데이터가 포함됩니다. |

{style="table-layout:auto"}

## 관련 설명서

* [연결 중 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
