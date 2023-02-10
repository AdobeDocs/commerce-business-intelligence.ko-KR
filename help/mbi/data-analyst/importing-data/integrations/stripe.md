---
title: 스트라이프 연결
description: 비즈니스 결제 및 송장 데이터를 관리하고 추적하는 방법을 알아봅니다.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# 스트라이프 연결

>[!NOTE]
>
>필요한 경우 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/stripe-logo.png)

[!DNL Stripe] 을(를) 통해 비즈니스 결제 및 송장 데이터를 관리하고 추적할 수 있습니다. 연결 [!DNL Stripe] 계정 대상 [!DNL MBI] 는 간단한 2단계 프로세스입니다.

1. [추가 [!DNL Stripe] 의 데이터 소스로 사용 [!DNL MBI]](#stepone)
1. [허용 [!DNL MBI] 액세스 권한 [!DNL Stripe] 데이터](#steptwo)

## 추가 [!DNL Stripe] 데이터 소스로 사용 {#stepone}

1. 로 이동합니다. `Connections` 아래의 페이지 **[!UICONTROL Admin** > **Connections]**.
1. 클릭 **[!UICONTROL Add a Data Source]**- 화면 오른쪽 위의 `Data Sources` 테이블.
1. 을(를) 클릭합니다. [!DNL Stripe] 아이콘. 그러면 `[!DNL Stripe] authorization` 페이지.
1. 클릭 **[!UICONTROL Connect with Stripe]**.

## 허용 [!DNL MBI] 액세스 권한 [!DNL Stripe] 데이터 {#steptwo}

클릭 후 **[!UICONTROL Connect with Stripe]**&#x200B;에 액세스 요청 페이지가 나타납니다.

1. 클릭 **[!UICONTROL Sign in with Stripe to Continue]**.

1. 자격 증명을 입력하고 **[!UICONTROL Sign in to your account]**.

1. 을(를) 클릭하면 자격 증명의 유효성이 확인되고 다시 [!DNL MBI].

1. 연결에 성공하면 *연결에 성공했습니다!* 메시지가 화면 상단에 표시됩니다.

## 관련:

만약 당신이 좀 더 기술적인 지식이 있다면, [[!DNL Stripe] API 설명서](https://stripe.com/docs/api) 는 방법에 대한 자세한 학습을 위해 유용한 리소스일 수 있습니다. [!DNL Stripe] 는 [!DNL MBI].

* [예상됨 [!DNL Stripe] 데이터](../integrations/stripe-data.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
