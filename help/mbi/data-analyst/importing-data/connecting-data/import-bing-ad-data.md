---
title: Bing 광고 지출 데이터 가져오기
description: 분석을 위해 Bing 광고 지출 데이터를  [!DNL Commerce Intelligence] 에 가져오는 방법을 알아봅니다.
exl-id: c8dec4b4-74ce-41b2-a77d-403fe44e2816
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/66UAmNWDCkiflHxsq9X1MlkwEgzC5Cl1HfRirNd8AHM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 131
ht-degree: 0%

---

# [!DNL Bing] 데이터 가져오기

분석을 위해 [!DNL Bing] 광고 지출 데이터를 [!DNL Adobe Commerce Intelligence]&#x200B;(으)로 가져오려면 [!DNL Bing Ads Editor]의 데이터를 `.csv` 형식으로 내보내고 아래 단계에 따라 [!DNL Commerce Intelligence]에 업로드하면 됩니다.

## [!DNL Bing Ads Editor]

[!DNL Bing Ads] 데이터를 내보내려면 [!DNL Bing Ads Editor]이(가) 설치되어 있어야 합니다. [[!DNL Bing Ads Editor]](https://about.ads.microsoft.com/en-us/solutions/tools/editor)의 무료 다운로드를 찾을 수 있습니다.

## [!DNL Bing Ads] 데이터 내보내기

1. `Browser`의 [!DNL Bing Ads Editor] 창에서 내보낼 캠페인 또는 광고 그룹을 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL Export]**&#x200B;을(를) 클릭합니다.
1. `Export` 대화 상자에서 **[!UICONTROL Export]**&#x200B;을(를) 클릭합니다.
1. `Save As` 대화 상자에서 내보내기 파일을 저장할 폴더를 클릭합니다.
1. `File name` 상자에서 파일 내보내기 이름을 선택합니다.
1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.
1. 파일을 다운로드한 후 [지원팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ko)하여 사용자를 대신하여 첫 번째 업로드를 수행하고 필요한 백엔드 차원을 설정합니다.
