---
title: CJ 계열사 (위원회 접합) 마케팅 데이터 가져오기
description: CJ 계열사 (위원회 접합) 데이터를로  [!DNL Commerce Intelligence] 가져오는 방법을 알아봅니다. L 상거래 인텔리전스].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# 가져오기 [!DNL CJ Affiliate] 데이터

데이터를으로 [!DNL Adobe Commerce Intelligence] 가져오려면 [!DNL CJ Affiliate (Commission Junction)] 아래 단계를 팔로우 하 고 결과 파일을 지원 티켓 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 에 [ 첨부 하면 됩니다. Adobe Systems는 계정 데이터 테이블을 설정 하 고 데이터를 개별적으로 업로드할 수 있도록 합니다.

## 데이터 내보내기 [!DNL CJ Affiliate]

1. [!DNL CJ Affiliate]계정에서 탭로 이동 `Reports` 합니다.

1. `Performance`탭에서를 선택 `Report Options` 합니다.

1. 감사할 날짜 범위와 동일 하 게 설정 하 고 `Date Range` 동일 하 게 설정 `Performance By` 합니다. `Program` `Trend` `Daily`

   ![수출-cj-계열사-데이터](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. 를 선택 `Run Report` 합니다.

1. `File Format`드롭다운 목록에서를 선택 `CSV` 합니다.  을 클릭 **[!UICONTROL Download]** 합니다.

   ![cj 계열사 데이터 내보내기](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. 파일을 다운로드 한 후 파일 ](../connecting-data/using-file-uploader.md) [!DNL Commerce Intelligence] 을 데이터 웨어하우스에 업로드 수 [ 있습니다.

   이렇게 하면 데이터 웨어하우스에 테이블 [!DNL Commerce Intelligence] 을 만들어 주기적으로 최신 데이터를 계속 업로드 수 있습니다. 파일을 업로드할 때 파일 업 로더 ](../connecting-data/using-file-uploader.md) 사용에 [ 나열 된 형식 요구 사항을 팔로우 합니다.
