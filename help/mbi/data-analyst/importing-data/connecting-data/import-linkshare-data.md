---
title: Linkshare 데이터 가져오기
description: Linkshare 데이터를 로 가져오는 방법 알아보기 [!DNL MBI].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# 가져오기 `Linkshare` 데이터

가져오려면 `Linkshare` 데이터 입력 [!DNL MBI], 다음 두 가지 작업을 수행해야 합니다.

1. [Linkshare 데이터 내보내기 ](#export)
1. [스프레드시트를에 업로드합니다 [!DNL MBI]](../connecting-data/using-file-uploader.md)

## Linkshare에서 데이터 내보내기 {#export}

1. 내 `Linkshare` 계정, 다음으로 이동 **[!UICONTROL Reports** > **Run Reports].**

1. 다음에서 `Report` 드롭다운, 선택 **[!UICONTROL Sales & Activity Report]**.

1. 다른 모든 드롭다운 옵션을 기본 선택으로 둡니다.

1. 다음에서 `Date Range` 드롭다운에서 원하는 옵션(`Sun - Sat`, `Mon - Sun`)는 와 일치합니다 `Start of Week` 의 설정 [!DNL MBI].

1. 지우기 `Compare Year-Over-Year Data` 확인란.

1. 아래 `Data Type`, 선택 `Transaction Date`.

   ![가져오기\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. 클릭 **[!UICONTROL View Report]**.

1. 클릭 **[!UICONTROL Download]**.

   이 시점에서 `.csv` 파일을 다운로드했습니다.

파일을 다운로드한 후에는에 업로드할 수 있습니다. [!DNL MBI] 사용 [`File Upload` 기능](../connecting-data/using-file-uploader.md).
