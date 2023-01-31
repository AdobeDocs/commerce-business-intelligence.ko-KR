---
title: CJ 제휴(커미션 접합) 마케팅 데이터 가져오기
description: CJ 제휴(Commission Junction) 데이터를 로 가져오는 방법을 알아봅니다. [!DNL MBI].L MBI].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# 가져오기 `CJ Affiliate` 데이터

가져오려면 `CJ Affiliate` (커미션 접합) 데이터 [!DNL MBI]아래의 단계를 따르기만 하면 결과 파일을 지원 티켓에 첨부할 수 있습니다. 계정이 데이터 테이블을 설정하고 독립적으로 데이터 업로드를 계속 수행할 수 있도록 합니다.

## 내보내기 `CJ Affiliate` 데이터

1. 사용자 `CJ Affiliate` 계정, `Reports` 탭.

1. 에서 `Performance` 탭, 선택 `Report Options`.

1. 설정 `Performance By` 같음 `Program`, `Trend` 같음 `Daily`, 및 `Date Range` 감사되는 날짜 범위와 같습니다.

   ![export-cj-제휴-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. 선택 `Run Report`.

1. 에서 `File Format` 드롭다운, 선택 `CSV`.  클릭 **[!UICONTROL Download]**.

   ![cj 제휴 데이터 내보내기](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. 파일을 다운로드한 후에는 다음을 수행할 수 있습니다 [파일 업로드](../connecting-data/using-file-uploader.md) 아래와 같이 [!DNL MBI] data warehouse.

   이렇게 하면 [!DNL MBI] 새 데이터를에 정기적으로 계속 업로드할 수 있는 data warehouse입니다. 파일을 업로드할 때에는 다음에 나열된 형식 요구 사항을 따라야 합니다. [파일 업로더 사용](../connecting-data/using-file-uploader.md).
