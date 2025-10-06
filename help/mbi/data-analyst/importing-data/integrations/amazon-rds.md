---
title: Amazon RDS 연결
description: RDS 인스턴스 연결 단계를 알아봅니다.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---

# [!DNL Amazon RDS] 연결

[!DNL Amazon Relational Database Services (RDS)]은(는) 이미 잘 알고 있는 데이터베이스 엔진에서 실행되는 관리되는 데이터베이스 서비스입니다.

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

[!DNL RDS] 인스턴스를 연결하는 단계는 사용 중인 데이터베이스 유형과 암호화된 연결(예: [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md))을 사용하고 있는지 여부에 따라 다르지만, 기본 사항은 다음과 같습니다.

## 데이터베이스에 액세스할 수 있도록 [!DNL Commerce Intelligence] 승인

각 데이터베이스의 자격 증명 페이지(**[!UICONTROL Manage Data** > **Integrations]**)에 R[!DNL RDS]을(를) [!DNL Commerce Intelligence]에 연결하기 위해 승인해야 하는 IP 주소가 들어 있는 상자가 표시됩니다. `54.88.76.97` 및 `34.250.211.151`. 다음은 `MySQL credentials` 페이지에서 IP 주소 상자를 강조 표시한 보기입니다.

![IP 주소 구성을 표시하는 Amazon RDS 보안 그룹 설정](../../../assets/RDS_IP.png)

[!DNL Commerce Intelligence]이(가) [!DNL RDS] 인스턴스와 성공적으로 연결하려면 AWS 관리 콘솔을 통해 이러한 IP 주소를 적절한 데이터베이스 보안 그룹에 추가해야 합니다. 이러한 IP 주소를 기존 그룹에 추가하거나 만들 수 있습니다. 중요한 것은 그룹이 [!DNL Commerce Intelligence]에 연결할 인스턴스에 액세스할 수 있는 권한이 있다는 것입니다.

[!DNL Commerce Intelligence] IP 주소를 추가할 때 주소 끝에 `/32`을(를) 추가하여 [!DNL Amazon]에 정확한 IP 주소임을 나타내십시오. 걱정하지 마십시오. AWS 인터페이스를 통해 이 기능이 필요하다는 것을 알 수 있습니다.

## `Linux`에 대해 [!DNL Commerce Intelligence] 사용자 만들기 {#linux}

>[!NOTE]
>
>이 단계는 암호화된 연결을 사용하는 경우에만 필요합니다. 이 작업을 수행하는 방법에 대한 지침은 사용 중인 데이터베이스에 대한 설정 항목(예: MySQL)을 참조하십시오. `Linux` 사용자는 인터넷을 통해 데이터를 보내는 가장 안전한 방법인 `SSH tunnel`을(를) 만들 수 있도록 허용합니다.

## [!DNL Commerce Intelligence]에 대한 데이터베이스 사용자 만들기

이는 사용 중인 데이터베이스에 따라 단계가 달라지는 프로세스의 일부입니다. 그러나 데이터베이스에 액세스하는 데 사용되는 [!DNL Commerce Intelligence]의 사용자를 만드는 아이디어는 동일합니다. 데이터베이스 [!DNL Commerce Intelligence] 사용자를 만드는 방법은 사용 중인 데이터베이스에 대한 설치 항목에서 찾을 수 있습니다.

## [!DNL Commerce Intelligence]에 연결 정보 입력

인스턴스에 대한 [!DNL Commerce Intelligence] 액세스 권한을 부여하고 사용자를 만든 후에는 [!DNL Commerce Intelligence]에 연결 정보를 입력할 필요가 없습니다.

`MySQL`을(를) 클릭하여 `Microsoft SQL`, `PostgreSQL` 및 `Integrations`의 자격 증명 페이지에 **[!UICONTROL Manage Data** > **Integrations]** 페이지(**[!UICONTROL Add Integration]**)를 통해 액세스할 수 있습니다. 통합 목록이 표시되면 사용 중인 데이터베이스의 아이콘을 눌러 인증서 페이지로 이동합니다. 현재 필요한 통합에 대한 액세스 권한이 없는 경우 Adobe 계정 팀에 문의하십시오.

연결 만들기를 완료하려면 다음 정보가 필요합니다.

* RDS 인스턴스의 공개 주소: [!DNL AWS] 관리 콘솔에서 찾을 수 있습니다.
* 데이터베이스 인스턴스가 사용하는 포트: 일부 데이터베이스에는 `Port` 필드를 자동으로 채우는 기본 포트가 있습니다. 이 정보는 데이터베이스의 설치 설명서에서도 찾을 수 있습니다.
* [!DNL Commerce Intelligence]에 대해 만든 사용자의 사용자 이름과 암호입니다.

암호화된 연결을 사용하는 경우 데이터베이스 자격 증명 페이지의 `Encrypted` 토글을 `Yes`(으)로 변경합니다. 암호화 설정을 위한 추가 양식이 표시됩니다.

암호화를 사용할 수 있는 ![SQL 통합 양식에서 [예] 옵션을 표시함](../../../assets/sql-integration-encrypted-yes.png)


