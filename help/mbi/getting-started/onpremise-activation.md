---
title: 활성화 [!DNL MBI] 온-프레미스 구독 계정
description: 활성화 방법에 대해 알아보기 [!DNL MBI] 온-프레미스 가입을 위한 계정.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 활성화 [!DNL MBI] 온-프레미스 구독 계정

활성화하려면 [!DNL MBI] 온-프레미스 구독의 경우, 먼저 [!DNL MBI] account, connect [!DNL MBI] 전자 상거래 데이터베이스에 추가합니다. 의 활성화에 대한 자세한 정보 `Cloud Starter` 프로젝트, [활성화 [!DNL MBI] 계정 `Cloud Starter` 구독](../getting-started/cloud-activation.md).

1. 만들기 [!DNL MBI] 계정.

   - 이동 [https://account.magento.com/customer/account/login](https://account.magento.com/customer/account/login)

   - 이동 **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - 클릭 **[!UICONTROL Create Instance]**. 이 단추가 표시되지 않으면 고객 성공 관리자 또는 고객 기술 관리자에게 문의하십시오.

   - 계정을 만들려면 정보를 입력합니다.

   ![](../assets/create-account-2.png)

   - 받은 편지함으로 이동하여 이메일 주소를 확인합니다. 이메일을 받지 않았다면 [연락처 지원](../guide-overview.md).

   - 암호를 만듭니다.

   ![](../assets/create-account-4.png)

   - 계정을 만든 후에는 새 계정에 사용자를 추가하는 옵션이 있습니다. 이제 기술 관리자를 추가하여 다음 단계를 수행할 수 있습니다.

   ![](../assets/create-account-5.png)

1. 저장소에 대한 정보를 입력하여 기본 설정을 지정합니다.

   ![](../assets/create-account-6.png)

1. Connect [!DNL MBI] 암호화된 연결을 사용하여 상거래 데이터베이스에 추가합니다.

   Commerce에서는 [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md). 그러나 이 옵션이 아닌 경우에도 계속 연결할 수 있습니다 [!DNL MBI] 를 사용하여 데이터베이스에 [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

1. 성공적으로 접속한 후 [!DNL MBI] commerce 데이터베이스에 대해서는 고객 성공 관리자에게 문의하여 통합 설정 및 기타 구성 단계와 같은 다음 단계를 조정하십시오.

1. 구성을 마치면 다음을 수행할 수 있습니다 [로그인](../getting-started/sign-in.md) 아래와 같이 [!DNL MBI] 계정이 필요합니다.
