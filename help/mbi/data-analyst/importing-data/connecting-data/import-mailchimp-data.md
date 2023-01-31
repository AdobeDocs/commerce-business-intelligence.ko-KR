---
title: MailChimp 데이터 가져오기
description: MailChimp 데이터를 로 가져오는 방법을 알아봅니다. [!DNL MBI].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# 가져오기 `MailChimp` 데이터

캠페인 활동에 대한 포괄적인 그림을 가져오려면 을(를) 가져올 수 있습니다 `MailChimp` 이메일 캠페인 데이터를 [!DNL MBI]. 가져오기를 완료하려면 각 항목에 대해 다음을 수행해야 합니다 `MailChimp` 캠페인:

## 데이터 내보내기 열기 {#opens}

1. 로그인한 후 `MailChimp`로 이동합니다. `Campaigns` 탭.

   ![mailchimp 1 가져오기](../../../assets/import-mailchimp-1.png)

1. 클릭 **[!UICONTROL View Report]**&#x200B;를 입력합니다.

   ![mailchimp 2 가져오기](../../../assets/import-mailchimp-2.png)

1. 을(를) 클릭합니다. **[!UICONTROL Opened]** 번호.

   ![mailchimp 3 가져오기](../../../assets/import-mailchimp-3.png)

1. 클릭 **[!UICONTROL Export]** 저장하고 `.csv` 파일.

   을(를) 추가해야 합니다. `primary key`, `date (mm/dd/yyyy)`, 및 `campaign name` 열을 파일에 추가합니다. 다음을 확인합니다. `primary keys` 는 각 행에 고유합니다.

   ![mailchimp 4 가져오기](../../../assets/import-mailchimp-4.png)

## 클릭 수 데이터 내보내기 {#clicks}

1. 로 돌아갑니다. `View Report` 캠페인에 대한 화면.

1. 해당 숫자를 클릭합니다. `Clicked`.

   ![mailchimp 5 가져오기](../../../assets/import-mailchimp-5.png)

1. 다음 중 하나를 클릭하여 `Total Clicks` 또는 `Unique Clicks` 열.

   ![mailchimp 6 가져오기](../../../assets/import-mailchimp-6.png)

1. 클릭 **[!UICONTROL Export]** 저장하고 `.csv` 파일.

   을(를) 추가해야 합니다. `Primary Key`, `date (mm/dd/yyyy)`, `campaign name`, 및 `URL` 열을 파일에 추가합니다. 클릭한 내용을 알 수 있도록 전체 URL을 추가할 필요는 없습니다.

   ![mailchimp 7 가져오기](../../../assets/import-mailchimp-7.png)

1. 이메일에서 클릭한 각 URL에 대해 3단계와 4단계를 반복하여 모든 데이터를 동일한 위치에 결합합니다 `.csv` 완료되면 파일을 확인합니다.

## 보낸 데이터 내보내기 {#sent}

1. 로 이동합니다. `Campaigns` MailChimp의 탭입니다.

1. 클릭 **[!UICONTROL View Report]** 캠페인 이름 옆에 표시됩니다.

1. 옆에 있는 숫자를 클릭합니다 `Recipients`.

   ![mailchimp 8 가져오기](../../../assets/import-mailchimp-8.png)

1. 클릭 **[!UICONTROL Export]** 저장하고 `.csv` 파일.

   을(를) 추가해야 합니다. `Primary Key`, `date (mm/dd/yyyy)`, 및 `campaign name` 열을 파일에 추가합니다.

   ![mailchimp 9 가져오기](../../../assets/import-mailchimp-9.png)

## 업로드 파일 준비 [!DNL MBI] {#upload}

각 파일 - `Opens`, `Clicks`, 및 `Sent` - 업로드 대상 [!DNL MBI] 를 별도의 파일로 사용합니다. 또한 다음 명명 규칙을 사용하여 파일 이름을 지정하는 것이 좋습니다. `MailChimp\_ACTION\_DATE`. 바꾸기 `ACTION` with `Open`, `Click`, 또는 `Sent`, 및 바꾸기 `DATE` 내보낼 날짜로 표시합니다.

파일을 업로드할 준비가 되면 [`File Upload` 기능](../connecting-data/using-file-uploader.md) 데이터를 data warehouse로 가져오기.
