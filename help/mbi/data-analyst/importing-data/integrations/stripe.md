---
title: Stripe 연결
description: 비즈니스 결제 및 송장 데이터를 관리하고 추적하는 방법에 대해 알아봅니다.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/S6-otAlCeS8aKQ6K-xZH2ZaqEjZ-ZZ6fMWXtFFafu6c
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 151
ht-degree: 0%

---

# [!DNL Stripe] 연결

>[!NOTE]
>
>[관리자 권한](../../../administrator/user-management/user-management.md)이 필요합니다.

![Stripe 로고](../../../assets/stripe-logo.png)

[!DNL Stripe]을(를) 통해 회사의 결제 및 송장 데이터를 관리하고 추적할 수 있습니다. [!DNL Stripe] 계정을 [!DNL Commerce Intelligence]에 연결하는 간단한 2단계 프로세스입니다.

1. [ [!DNL Stripe] 에서 데이터 소스로  [!DNL Commerce Intelligence]추가](#stepone)
1. [ [!DNL Commerce Intelligence] 데이터에 대한  [!DNL Stripe] 액세스 허용](#steptwo)

## [!DNL Stripe]을(를) 데이터 소스로 추가 {#stepone}

1. `Connections` 아래의 **[!UICONTROL Admin** > **Connections]** 페이지로 이동합니다.
1. **[!UICONTROL Add a Data Source]** 테이블 위의 화면 오른쪽에 있는 `Data Sources`을(를) 클릭합니다.
1. [!DNL Stripe] 아이콘을 클릭합니다. `[!DNL Stripe] authorization` 페이지가 표시됩니다.
1. **[!UICONTROL Connect with Stripe]**&#x200B;을(를) 클릭합니다.

## [!DNL Commerce Intelligence] 데이터에 대한 [!DNL Stripe] 액세스 허용 {#steptwo}

**[!UICONTROL Connect with Stripe]**&#x200B;을(를) 클릭하면 액세스 요청 페이지가 나타납니다.

1. **[!UICONTROL Sign in with Stripe to Continue]**&#x200B;을(를) 클릭합니다.

1. 자격 증명을 입력하고 **[!UICONTROL Sign in to your account]**&#x200B;을(를) 클릭합니다.

1. 자격 증명이 확인되며 [!DNL Commerce Intelligence]&#x200B;(으)로 다시 이동됩니다.

1. 연결이 성공하면 *연결이 성공합니다!* 메시지가 화면 맨 위에 나타납니다.

## 관련 항목:

[[!DNL Stripe] API 설명서](https://stripe.com/docs/api)는 [!DNL Stripe]을(를) [!DNL Commerce Intelligence]과(와) 통합하는 방법에 대한 자세한 내용을 학습하는 데 유용한 리소스가 될 수 있습니다.

* [ [!DNL Stripe] 데이터가 필요합니다.](../integrations/stripe-data.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
