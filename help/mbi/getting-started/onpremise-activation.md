---
title: 활성화 [!DNL MBI] 온-프레미스 구독 계정
description: 귀하의 활성화에 대해 알아보기 [!DNL MBI] 온-프레미스 구독에 대한 계정입니다.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
source-git-commit: 6f018ab220f2ae573cbc9016f9efb83c27a254be
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 활성화 [!DNL MBI] 온-프레미스 구독 계정

활성화하려면 [!DNL MBI] 온-프레미스 구독의 경우 먼저 [!DNL MBI] 계정, 연결 [!DNL MBI] 상거래 데이터베이스로 이동합니다. 의 활성화에 대한 자세한 내용 `Cloud Starter` 프로젝트, 참조 [활성화 [!DNL MBI] 계정 `Cloud Starter` 구독](../getting-started/cloud-activation.md).

1. 사용자 만들기 [!DNL MBI] 계정.

   - 다음으로 이동 [Adobe Commerce 계정 로그인](https://account.magento.com/customer/account/login)

   - 다음으로 이동 **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - 클릭 **[!UICONTROL Create Instance]**. 이 단추가 표시되지 않으면 Adobe 계정 팀이나 고객 기술 관리자에게 문의하십시오.

   - 계정을 만들려면 정보를 입력하십시오.

   ![](../assets/create-account-2.png)

   - 받은 편지함으로 이동하여 이메일 주소를 확인합니다. 이메일을 받지 못한 경우 [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

   - 암호를 만듭니다.

   ![](../assets/create-account-4.png)

   - 계정을 만든 후에는 새 계정에 사용자를 추가할 수 있습니다. 이제 기술 관리자를 추가하여 다음 단계를 수행할 수 있습니다.

   ![](../assets/create-account-5.png)

1. 환경 설정을 지정할 스토어에 대한 정보를 입력하십시오.

   ![](../assets/create-account-6.png)

1. 연결 [!DNL MBI] 암호화된 연결을 사용하여 Commerce 데이터베이스에 연결합니다.

   Commerce에서는 다음을 사용하여 연결하는 것이 좋습니다 [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md). 그러나 옵션이 아닌 경우 계속 연결할 수 있습니다 [!DNL MBI] 을 사용하여 데이터베이스에 [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

1. 을(를) 연결한 후 [!DNL MBI] 상거래 데이터베이스로 통합 설정 및 기타 구성 단계와 같은 다음 단계를 조정하려면 Adobe 계정 팀에 문의하십시오.

1. 구성을 마치면 다음 작업을 수행할 수 있습니다 [로그인](../getting-started/sign-in.md) (으)로 [!DNL MBI] 계정입니다.
