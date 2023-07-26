---
title: MailChimp 데이터 가져오기
description: MailChimp 데이터를 로 가져오는 방법 알아보기 [!DNL Commerce Intelligence].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 가져오기 [!DNL Mailchimp] 데이터

캠페인 활동을 종합적으로 파악하려면 다음을 가져올 수 있습니다. [!DNL Mailchimp] 캠페인 데이터를에 이메일 보내기 [!DNL Commerce Intelligence]. 가져오기를 완료하려면 각각에 대해 다음 작업을 수행해야 합니다 [!DNL Mailchimp] 보유한 캠페인:

## 열기 데이터 내보내기 {#opens}

1. 에 로그인한 후 [!DNL Mailchimp]로 이동합니다. `Campaigns` 탭.

   ![mailchimp 1 가져오기](../../../assets/import-mailchimp-1.png)

1. 클릭 **[!UICONTROL View Report]**&#x200B;를 클릭합니다.

   ![mailchimp 2 가져오기](../../../assets/import-mailchimp-2.png)

1. 다음을 클릭합니다. **[!UICONTROL Opened]** 숫자.

   ![mailchimp 3 가져오기](../../../assets/import-mailchimp-3.png)

1. 클릭 **[!UICONTROL Export]** 및 저장 `.csv` 파일.

   다음을 추가해야 합니다. `primary key`, `date (mm/dd/yyyy)`, 및 `campaign name` 이 파일에 대한 열입니다. 다음을 확인합니다. `primary keys` 각 행에 고유합니다.

   ![mailchimp 4 가져오기](../../../assets/import-mailchimp-4.png)

## 클릭 수 데이터 내보내기 {#clicks}

1. 다음으로 돌아가기 `View Report` 캠페인을 위한 화면입니다.

1. 번호 클릭: `Clicked`.

   ![mailchimp 5 가져오기](../../../assets/import-mailchimp-5.png)

1. 아래의 숫자를 클릭합니다. `Total Clicks` 또는 `Unique Clicks` 열.

   ![mailchimp 6 가져오기](../../../assets/import-mailchimp-6.png)

1. 클릭 **[!UICONTROL Export]** 및 저장 `.csv` 파일.

   다음을 추가해야 합니다. `Primary Key`, `date (mm/dd/yyyy)`, `campaign name`, 및 `URL` 이 파일에 대한 열입니다. 전체 URL을 추가할 필요는 없으며, 단지 클릭한 내용을 알려주는 것입니다.

   ![mailchimp 7 가져오기](../../../assets/import-mailchimp-7.png)

1. 이메일에서 클릭한 각 URL에 대해 3단계와 4단계를 반복하여 모든 데이터를 동일한 것으로 결합합니다 `.csv` 파일이 완성되었습니다.

## 보낸 데이터 내보내기 {#sent}

1. 로 이동합니다. `Campaigns` 탭 / [!DNL Mailchimp].

1. 클릭 **[!UICONTROL View Report]** 캠페인 이름 옆에 있습니다.

1. 옆에 있는 숫자를 클릭합니다. `Recipients`.

   ![mailchimp 8 가져오기](../../../assets/import-mailchimp-8.png)

1. 클릭 **[!UICONTROL Export]** 및 저장 `.csv` 파일.

   다음을 추가해야 합니다. `Primary Key`, `date (mm/dd/yyyy)`, 및 `campaign name` 이 파일에 대한 열입니다.

   ![mailchimp 9 가져오기](../../../assets/import-mailchimp-9.png)

## 업로드할 파일 준비 [!DNL Commerce Intelligence] {#upload}

각 파일 - `Opens`, `Clicks`, 및 `Sent` - 을(를) (으)로 업로드해야 합니다. [!DNL Commerce Intelligence] 별도의 파일로 사용할 수 있습니다. Adobe은 다음과 같은 명명 규칙을 사용하여 파일 이름을 지정할 것을 권장합니다. `MailChimp\_ACTION\_DATE`. 바꾸기 `ACTION` 포함 `Open`, `Click`, 또는 `Sent`, 및 바꾸기 `DATE` (내보내는 날짜 포함)

파일을 업로드할 준비가 되면 [`File Upload` 기능](../connecting-data/using-file-uploader.md) 데이터를 Data Warehouse으로 가져오기
