---
title: Linkshare 데이터 가져오기
description: Linkshare 데이터를 로 가져오는 방법을 알아봅니다. [!DNL MBI].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 가져오기 `Linkshare` 데이터

다음 항목을 `Linkshare` 데이터를에 [!DNL MBI]이렇게 하려면 두 가지 작업을 수행해야 합니다.

1. [Linkshare 데이터 내보내기 위치 ](#export)
1. [스프레드시트를 (으)로 업로드합니다 [!DNL MBI]](../connecting-data/using-file-uploader.md)

## Linkshare에서 데이터 내보내기 {#export}

1. 사용자 `Linkshare` 계정, **[!UICONTROL Reports** > **Run Reports].**

1. 에서 `Report` 드롭다운, 선택 **[!UICONTROL Sales & Activity Report]**.

1. 다른 모든 드롭다운 옵션을 기본 선택 항목으로 둡니다.

1. 에서 `Date Range` 드롭다운 옵션 선택(`Sun - Sat`, `Mon - Sun`)가 와 일치합니다 `Start of Week` 설정 [!DNL MBI].

1. 지우기 `Compare Year-Over-Year Data` 확인란을 선택합니다.

1. 아래 `Data Type`, 선택 `Transaction Date`.

   ![import\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. 클릭 **[!UICONTROL View Report]**.

1. 클릭 **[!UICONTROL Download]**.

   이 시점에서 `.csv` 파일이 만들어지고 다운로드됩니다.

파일을 다운로드한 후에 업로드할 수 있습니다. [!DNL MBI] 사용 [`File Upload` 기능](../connecting-data/using-file-uploader.md).
