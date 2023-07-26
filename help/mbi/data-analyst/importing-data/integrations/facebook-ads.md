---
title: facebook 광고 연결
description: 광고 지출 데이터를 분석하고 비용이 효과적으로 지출되는지 확인하는 방법을 알아봅니다.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 연결 [!DNL Facebook Ads]

>[!NOTE]
>
>필요 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/facebook-ads-logo.png)

조사, 광고 제작, 캠페인 시작 시기 [!DNL Facebook]. 이제 광고 지출 데이터를 분석하고 비용이 효과적으로 지출되고 있는지 확인할 차례입니다. 광고 지출 데이터를 사용하여 다음과 같은 작업을 수행할 수 있습니다 [광고 비용과 고객 생애 가치(CLV)를 결합하여 캠페인 ROI를 측정합니다.](../../../data-analyst/analysis/roi-ad-camp.md) 캠페인에서 획득한 사용자 수

연결 중 [!DNL Facebook Ad] 데이터 받는 사람 [!DNL Commerce Intelligence] 는 간단한 3단계 프로세스입니다.

1. [추가 [!DNL Facebook] 의 데이터 소스로서의 [!DNL Commerce Intelligence]](#stepone)
1. [허용 [!DNL Commerce Intelligence] 다음에 대한 액세스 권한: [!DNL Facebook Ads] 데이터](#steptwo)
1. [선택 [!DNL Facebook Ads] 데이터 가져오기 계정](#stepthree)

## 추가 [!DNL Facebook] 의 데이터 소스로서의 [!DNL Commerce Intelligence] {#stepone}

1. 을(를) 추가하려면 [!DNL Facebook] 에 통합 [!DNL Commerce Intelligence]계정, 다음으로 이동 `Connections` 아래 페이지 **[!UICONTROL Manage Data** > **Integrations]**.
1. 클릭 **[!UICONTROL Add Integration]**, 오른쪽에 있습니다.
1. 다음을 클릭합니다. [!DNL Facebook] 아이콘. 그러면 [!DNL Facebook] 인증 페이지입니다.
1. 클릭 **[!UICONTROL Authorize]**.

## 허용 [!DNL Commerce Intelligence] 다음에 대한 액세스 권한: [!DNL Facebook Ads] 데이터 {#steptwo}

클릭 후 **[!DNL Facebook Authorize]**&#x200B;작은 팝업 창이 표시됩니다.

![](../../../assets/Facebook_Access_Popup.png)

허용할 일련의 단계를 따릅니다. [!DNL Commerce Intelligence] 공개 프로필의 데이터에 액세스하려면 다음을 수행하십시오. [!DNL Facebook Ads] 및 관련 통계. 클릭 **[!UICONTROL OK]** 계속하려면 이 단계를 수행하십시오.

## 선택 [!DNL Facebook Ads] 데이터 가져오기 계정 {#stepthree}

1. 인증이 완료되면 다음을 선택하라는 메시지가 표시됩니다. [!DNL Facebook Ads] 데이터를 가져올 계정입니다. 에서 확인란을 클릭하여 원하는 계정을 선택합니다. `Connect` 열.

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. 클릭 **[!UICONTROL Save Connections]**.

   정상적으로 연결되면 *연결 성공!* 메시지가 페이지 맨 위에 표시됩니다.

## 다음은 무엇입니까? {#next}

추적하고 있는지 확인하십시오 [!DNL Facebook] 의 캠페인 [!DNL Google Analytics]. 이렇게 하면 `utm\_campaign` 의 필드 [!DNL Google Analytics] 이(가) 다음에 대해 적절히 채워집니다. [!DNL Facebook] 캠페인.

## 관련 항목

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [연결 [!DNL Google Adwords] account](../integrations/google-ecommerce.md)
* [다음을 통해 주문 참조 소스 추적 [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [데이터베이스에서 사용자 조회 소스 추적](../../analysis/google-track-user-acq.md)
* [데이터베이스에서 사용자 장치, 브라우저 및 OS 데이터 추적](../../analysis/track-usr-dev-browser.md)
* [가장 가치 있는 확보 소스 및 채널 살펴보기](../../analysis/most-value-source-channel.md)
* [광고 캠페인에 대한 ROI 향상](../../analysis/roi-ad-camp.md)
* [은 어떻게 합니까? [!DNL Google Analytics] UTM 속성이 작동합니까?](../../analysis/utm-attributes.md)
