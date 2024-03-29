---
title: CJ 계열사(커미션 정션) 마케팅 데이터 가져오기
description: CJ 계열사(커미션 정션) 데이터를 로 가져오는 방법 알아보기 [!DNL Commerce Intelligence].L Commerce Intelligence].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# 가져오기 [!DNL CJ Affiliate] 데이터

가져오기 [!DNL CJ Affiliate (Commission Junction)] 데이터 입력 [!DNL Adobe Commerce Intelligence]를 클릭하고 아래 단계를 따라 결과 파일을 [지원 티켓](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). Adobe은 계정에 데이터 테이블을 설정하고 독립적으로 데이터를 계속 업로드할 수 있습니다.

## 내보내기 [!DNL CJ Affiliate] 데이터

1. 내 [!DNL CJ Affiliate] 계정, 다음으로 이동 `Reports` 탭.

1. 다음에서 `Performance` 탭, 선택 `Report Options`.

1. 설정 `Performance By` 다음과 같음 `Program`, `Trend` 다음과 같음 `Daily`, 및 `Date Range` 감사 중인 날짜 범위와 같습니다.

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. 선택 `Run Report`.

1. 다음에서 `File Format` 드롭다운, 선택 `CSV`.  클릭 **[!UICONTROL Download]**.

   ![cj 계열사 데이터 내보내기](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. 파일을 다운로드한 후 다음과 같은 작업을 수행할 수 있습니다 [파일 업로드](../connecting-data/using-file-uploader.md) (으)로 [!DNL Commerce Intelligence] Data Warehouse.

   이렇게 하면 [!DNL Commerce Intelligence] 정기적으로 새 데이터를에 계속 업로드할 수 있는 Data Warehouse. 파일을 업로드할 때에에 나열된 형식 요구 사항을 따르십시오. [File Uploader 사용](../connecting-data/using-file-uploader.md).
