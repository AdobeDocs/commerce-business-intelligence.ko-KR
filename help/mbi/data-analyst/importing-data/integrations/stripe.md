---
title: 스트라이프 연결
description: 비즈니스 결제 및 송장 데이터를 관리하고 추적하는 방법에 대해 알아봅니다.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# 스트라이프 연결

>[!NOTE]
>
>필요 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/stripe-logo.png)

[!DNL Stripe] 비즈니스 결제 및 송장 데이터를 관리하고 추적할 수 있습니다. 연결 중 [!DNL Stripe] 계정 위치: [!DNL MBI] 는 간단한 2단계 프로세스입니다.

1. [추가 [!DNL Stripe] 의 데이터 소스로서의 [!DNL MBI]](#stepone)
1. [허용 [!DNL MBI] 다음에 대한 액세스 권한: [!DNL Stripe] 데이터](#steptwo)

## 추가 [!DNL Stripe] 데이터 소스 {#stepone}

1. 로 이동 `Connections` 아래 페이지 **[!UICONTROL Admin** > **Connections]**.
1. 클릭 **[!UICONTROL Add a Data Source]**, 위의 화면 오른쪽에 있음 `Data Sources` 테이블.
1. 다음을 클릭합니다. [!DNL Stripe] 아이콘. 그러면 `[!DNL Stripe] authorization` 페이지를 가리키도록 업데이트하는 중입니다.
1. 클릭 **[!UICONTROL Connect with Stripe]**.

## 허용 [!DNL MBI] 다음에 대한 액세스 권한: [!DNL Stripe] 데이터 {#steptwo}

클릭 후 **[!UICONTROL Connect with Stripe]**&#x200B;에 액세스 요청 페이지가 나타납니다.

1. 클릭 **[!UICONTROL Sign in with Stripe to Continue]**.

1. 자격 증명을 입력하고 **[!UICONTROL Sign in to your account]**.

1. 을(를) 클릭하면 자격 증명의 유효성을 검사하고 다음 위치로 돌아갑니다. [!DNL MBI].

1. 정상적으로 연결되면 *연결 성공!* 메시지가 화면 맨 위에 나타납니다.

## 관련 항목:

좀 더 기술에 정통한 사람이라면 [[!DNL Stripe] API 설명서](https://stripe.com/docs/api) 은(는) 방법에 대한 자세한 내용을 학습하는 데 유용한 리소스가 될 수 있습니다. [!DNL Stripe] 와 통합됨 [!DNL MBI].

* [예상 [!DNL Stripe] 데이터](../integrations/stripe-data.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
