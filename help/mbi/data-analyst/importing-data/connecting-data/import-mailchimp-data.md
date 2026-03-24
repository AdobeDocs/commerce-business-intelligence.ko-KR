---
title: MailChimp 데이터 가져오기
description: MailChimp 데이터를  [!DNL Commerce Intelligence](으)로 가져오는 방법을 알아봅니다.
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/HJJYKfqc1sbslQimSNituG6Pm6wi6QpU-vn6GtKvV-Y
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 0%

---

# [!DNL Mailchimp] 데이터 가져오기

캠페인 활동을 종합적으로 파악하려면 [!DNL Mailchimp] 이메일 캠페인 데이터를 [!DNL Commerce Intelligence]&#x200B;(으)로 가져올 수 있습니다. 가져오기를 완료하려면 보유한 각 [!DNL Mailchimp] 캠페인에 대해 다음을 수행해야 합니다.

## 열기 데이터 내보내기 {#opens}

1. [!DNL Mailchimp]에 로그인한 후 `Campaigns` 탭으로 이동합니다.

   ![mailchimp 1](../../../assets/import-mailchimp-1.png) 가져오기

1. 캠페인 이름 옆의 **[!UICONTROL View Report]**&#x200B;을(를) 클릭합니다.

   ![mailchimp 가져오기 2](../../../assets/import-mailchimp-2.png)

1. **[!UICONTROL Opened]** 번호를 클릭합니다.

   ![mailchimp 가져오기 3](../../../assets/import-mailchimp-3.png)

1. **[!UICONTROL Export]**&#x200B;을(를) 클릭하고 `.csv` 파일을 저장합니다.

   이 파일에 `primary key`, `date (mm/dd/yyyy)` 및 `campaign name` 열을 추가해야 합니다. `primary keys`이(가) 각 행에 고유한지 확인하십시오.

   ![mailchimp 가져오기 4](../../../assets/import-mailchimp-4.png)

## 클릭 수 데이터 내보내기 {#clicks}

1. 캠페인의 `View Report` 화면으로 다시 이동합니다.

1. `Clicked`의 번호를 클릭합니다.

   ![mailchimp 가져오기 5](../../../assets/import-mailchimp-5.png)

1. `Total Clicks` 또는 `Unique Clicks` 열 아래의 숫자를 클릭합니다.

   ![mailchimp 가져오기 6](../../../assets/import-mailchimp-6.png)

1. **[!UICONTROL Export]**&#x200B;을(를) 클릭하고 `.csv` 파일을 저장합니다.

   이 파일에 `Primary Key`, `date (mm/dd/yyyy)`, `campaign name` 및 `URL` 열을 추가해야 합니다. 전체 URL을 추가할 필요는 없으며, 단지 클릭한 내용을 알려주는 것입니다.

   ![mailchimp 가져오기 7](../../../assets/import-mailchimp-7.png)

1. 전자 메일에서 클릭한 각 URL에 대해 3단계와 4단계를 반복하여 모든 데이터를 완료되면 동일한 `.csv` 파일에 결합합니다.

## 보낸 데이터 내보내기 {#sent}

1. `Campaigns`의 [!DNL Mailchimp] 탭으로 이동합니다.

1. 캠페인 이름 옆에 있는 **[!UICONTROL View Report]**&#x200B;을(를) 클릭합니다.

1. `Recipients` 옆에 있는 숫자를 클릭합니다.

   ![mailchimp 8](../../../assets/import-mailchimp-8.png) 가져오기

1. **[!UICONTROL Export]**&#x200B;을(를) 클릭하고 `.csv` 파일을 저장합니다.

   이 파일에 `Primary Key`, `date (mm/dd/yyyy)` 및 `campaign name` 열을 추가해야 합니다.

   ![mailchimp 9](../../../assets/import-mailchimp-9.png) 가져오기

## [!DNL Commerce Intelligence]에 업로드할 파일 준비 {#upload}

각 파일(`Opens`, `Clicks` 및 `Sent`)은 별도의 파일로 [!DNL Commerce Intelligence]에 업로드해야 합니다. Adobe에서는 다음 명명 규칙을 사용하여 파일 이름을 지정할 것을 권장합니다. `MailChimp\_ACTION\_DATE`. `ACTION`을(를) `Open`, `Click` 또는 `Sent`(으)로 바꾸고 `DATE`을(를) 내보낸 날짜로 바꿉니다.

파일을 업로드할 준비가 되면 [`File Upload` 기능](../connecting-data/using-file-uploader.md)을(를) 사용하여 데이터를 Data Warehouse으로 가져옵니다.
