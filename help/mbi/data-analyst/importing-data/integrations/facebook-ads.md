---
title: Facebook 광고 연결
description: 광고 지출 데이터를 분석하고 비용이 효과적으로 지출되는지 확인하는 방법을 알아봅니다.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/6TR559YyeTHT3KWl3oA4Bdnpr-HCowTXTTkvmP0I0tg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 313
ht-degree: 0%

---

# [!DNL Facebook Ads] 연결

>[!NOTE]
>
>[관리자 권한](../../../administrator/user-management/user-management.md)이 필요합니다.

![Facebook 광고 로고](../../../assets/facebook-ads-logo.png)

조사를 했고, 광고를 만들었으며, [!DNL Facebook]에 캠페인을 시작했습니다. 이제 광고 지출 데이터를 분석하고 비용이 효과적으로 지출되고 있는지 확인할 차례입니다. 광고 지출 데이터를 사용하여 [광고 비용과 캠페인에서 획득한 사용자의 CLV(고객 생애 가치)를 합산하여 캠페인 ROI를 측정할 수 있습니다](../../../data-analyst/analysis/roi-ad-camp.md).

[!DNL Facebook Ad] 데이터를 [!DNL Commerce Intelligence]에 연결하는 간단한 3단계 프로세스입니다.

1. [&#x200B; [!DNL Facebook] 에서 데이터 소스로  [!DNL Commerce Intelligence]추가](#stepone)
1. [&#x200B; [!DNL Commerce Intelligence] 데이터에 대한  [!DNL Facebook Ads] 액세스 허용](#steptwo)
1. [데이터를 가져올  [!DNL Facebook Ads] 계정 선택](#stepthree)

## [!DNL Facebook]을(를) [!DNL Commerce Intelligence]의 데이터 소스로 추가 {#stepone}

1. [!DNL Facebook] 계정에 [!DNL Commerce Intelligence] 통합을 추가하려면 `Connections` 아래의 **[!UICONTROL Manage Data** > **Integrations]** 페이지로 이동하십시오.
1. 오른쪽에 있는 **[!UICONTROL Add Integration]**&#x200B;을(를) 클릭합니다.
1. [!DNL Facebook] 아이콘을 클릭합니다. [!DNL Facebook] 인증 페이지가 표시됩니다.
1. **[!UICONTROL Authorize]**&#x200B;을(를) 클릭합니다.

## [!DNL Commerce Intelligence] 데이터에 대한 [!DNL Facebook Ads] 액세스 허용 {#steptwo}

**[!DNL Facebook Authorize]**&#x200B;을(를) 클릭하면 작은 팝업 창이 표시됩니다.

![Commerce Intelligence에 대한 Facebook 액세스 권한 대화 상자](../../../assets/Facebook_Access_Popup.png)

[!DNL Commerce Intelligence]이(가) 공개 프로필, [!DNL Facebook Ads] 및 관련 통계의 데이터에 액세스할 수 있도록 허용하는 일련의 단계를 따릅니다. 계속하려면 이 단계에서 **[!UICONTROL OK]**&#x200B;을(를) 클릭하십시오.

## 데이터를 가져올 [!DNL Facebook Ads] 계정 선택 {#stepthree}

1. 인증이 완료되면 데이터를 가져올 [!DNL Facebook Ads] 계정을 선택하라는 메시지가 표시됩니다. `Connect` 열의 확인란을 클릭하여 원하는 계정을 선택합니다.

   ![Facebook 광고 계정 선택 인터페이스](../../../assets/Facebook_Ad_Accounts.png)

1. **[!UICONTROL Save Connections]**&#x200B;을(를) 클릭합니다.

   연결이 성공하면 *연결이 성공합니다!* 메시지가 페이지 맨 위에 표시됩니다.

## 다음은 무엇입니까? {#next}

[!DNL Facebook]에서 [!DNL Google Analytics]개의 캠페인을 추적하고 있는지 확인하십시오. 이렇게 하면 `utm\_campaign`의 [!DNL Google Analytics] 필드가 [!DNL Facebook] 캠페인에 대해 올바르게 채워집니다.

## 관련 항목

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [&#x200B; [!DNL Google Adwords] 계정 연결](../integrations/google-ecommerce.md)
* [&#x200B; [!DNL Google eCommerce]을(를) 통해 주문 참조 원본 추적](../integrations/google-ecommerce.md)
* [데이터베이스에서 사용자 조회 소스 추적](../../analysis/google-track-user-acq.md)
* [데이터베이스에서 사용자 장치, 브라우저 및 OS 데이터 추적](../../analysis/track-usr-dev-browser.md)
* [가장 가치 있는 확보 소스 및 채널 살펴보기](../../analysis/most-value-source-channel.md)
* [광고 캠페인에 대한 ROI 향상](../../analysis/roi-ad-camp.md)
* [&#x200B; [!DNL Google Analytics] UTM 속성은 어떻게 작동합니까?](../../analysis/utm-attributes.md)
