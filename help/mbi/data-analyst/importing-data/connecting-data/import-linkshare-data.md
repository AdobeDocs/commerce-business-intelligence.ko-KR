---
title: Linkshare 데이터 가져오기
description: Linkshare 데이터를 [!DNL Commerce Intelligence] (으)로 가져오는 방법을 알아봅니다.
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/TsQYXEwH-8m1rpKg6It8wa-B2eQH0oqDkLcgx-tRBWU'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%
---
# [!DNL Linkshare] 데이터 가져오기

[!DNL Linkshare] 데이터를 [!DNL Adobe Commerce Intelligence]&#x200B;(으)로 가져오려면 다음 두 가지 작업을 수행해야 합니다.

1. [Linkshare 데이터를 `.csv` 형식으로 내보내기](#export)
1. [스프레드시트를  [!DNL Commerce Intelligence]에 업로드](../connecting-data/using-file-uploader.md)

## Linkshare에서 데이터 내보내기 {#export}

1. [!DNL Linkshare] 계정에서 **[!UICONTROL Reports** > **Run Reports].**(으)로 이동

1. `Report` 드롭다운에서 **[!UICONTROL Sales & Activity Report]**&#x200B;을(를) 선택합니다.

1. 다른 모든 드롭다운 옵션을 기본 선택으로 둡니다.

1. `Date Range` 드롭다운에서 [!DNL Commerce Intelligence]의 `Start of Week` 설정과 일치하는 옵션(`Sun - Sat`, `Mon - Sun`)을 선택합니다.

1. `Compare Year-Over-Year Data` 확인란의 선택을 취소합니다.

1. `Data Type`에서 `Transaction Date`을(를) 선택합니다.

   ![가져오기\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. **[!UICONTROL View Report]**&#x200B;을(를) 클릭합니다.

1. **[!UICONTROL Download]**&#x200B;을(를) 클릭합니다.

   이 시점에서 `.csv` 파일을 다운로드했습니다.

파일을 다운로드한 후 [`File Upload` 기능](../connecting-data/using-file-uploader.md)을 사용하여 [!DNL Commerce Intelligence]에 업로드할 수 있습니다.
