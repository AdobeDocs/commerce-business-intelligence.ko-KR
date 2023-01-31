---
title: Mixpanel의 데이터 유효성 검사
description: Mixpanel 내에서 직접 사용할 수 있는 동일한 모든 데이터를 동기화했음을 확인하는 방법을 알아봅니다.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 의 데이터 유효성 검사 `Mixpanel`

When [!DNL MBI] 첫 번째 연결 [!DNL Mixpanel] 데이터, 계정 관리자 또는 분석가는 유효성 검사를 위해 Mixpanel의 데이터 내보내기를 요청할 수 있습니다. 이렇게 하면 내에서 직접 사용할 수 있는 동일한 모든 데이터를 동기화했음을 확인할 수 있습니다 [!DNL Mixpanel].

## 데이터 내보내기 프로세스: `Events`

1. 다음 방문 `Segmentation` 섹션 및 보기 `Your Top Events`.

   ![](../../../assets/your-top-events.png)

1. 선택 `Past 96 Hours` - 시간 범위

   ![](../../../assets/past-96-hours.png)

1. 보고서 오른쪽 아래로 스크롤하여 `.csv` 파일:

   ![](../../../assets/export-csv-mixpanel.png)

1. 보내기 `.csv` 이 검증 프로세스에서 작업 중인 계정 관리자 또는 분석가에게 파일을 보냅니다.
