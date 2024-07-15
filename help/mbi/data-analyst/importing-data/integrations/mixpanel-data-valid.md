---
title: Mixpanel의 데이터 유효성 검사
description: Mixpanel 내에서 직접 사용할 수 있는 모든 동일한 데이터를 동기화했는지 확인하는 방법에 대해 알아봅니다.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# [!DNL Mixpanel]의 데이터 유효성 검사

[!DNL Adobe Commerce Intelligence]이(가) [!DNL Mixpanel] 데이터에 처음 연결되면 계정 관리자나 분석가는 유효성 검사를 위해 [!DNL Mixpanel]의 데이터 내보내기를 제공하도록 요청할 수 있습니다. 이를 통해 [!DNL Mixpanel] 내에서 직접 사용할 수 있는 모든 동일한 데이터를 동기화했는지 확인할 수 있습니다.

## 데이터 내보내기 프로세스: `Events`

1. `Segmentation` 섹션을 방문하여 `Your Top Events`을(를) 봅니다.

   ![](../../../assets/your-top-events.png)

1. 시간 범위에 대해 `Past 96 Hours` 선택

   ![](../../../assets/past-96-hours.png)

1. 보고서의 오른쪽 아래로 스크롤하여 `.csv` 파일을 내보냅니다.

   ![](../../../assets/export-csv-mixpanel.png)

1. 이 유효성 검사 프로세스에서 작업 중인 계정 관리자 또는 분석가에게 `.csv` 파일을 보냅니다.
