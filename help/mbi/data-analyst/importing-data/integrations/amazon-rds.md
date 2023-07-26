---
title: Amazon RDS 연결
description: RDS 인스턴스 연결 단계를 알아봅니다.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# 연결 [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] 는 이미 잘 알고 있을 데이터베이스 엔진에서 실행되는 관리되는 데이터베이스 서비스입니다.

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

에 연결하는 단계 [!DNL RDS] 인스턴스는 사용 중인 데이터베이스 유형과 암호화된 연결(예: [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), 하지만 기본 사항은 다음과 같습니다.

## 승인 [!DNL Commerce Intelligence] 데이터베이스에 액세스하려면

자격 증명 페이지(**[!UICONTROL Manage Data** > **Integrations]**) 각 데이터베이스에 대해 R에 연결할 권한을 부여해야 하는 IP 주소가 들어 있는 상자가 표시됩니다[!DNL RDS] 끝 [!DNL Commerce Intelligence]: `54.88.76.97` 및 `34.250.211.151`. 다음 항목을 살펴보십시오. `MySQL credentials` 페이지에서 IP 주소 상자를 강조 표시한 경우:

![](../../../assets/RDS_IP.png)

대상 [!DNL Commerce Intelligence] 을(를) 통해 성공적으로 연결 [!DNL RDS] 예를 들어 AWS 관리 콘솔을 통해 이러한 IP 주소를 적절한 데이터베이스 보안 그룹에 추가해야 합니다. 이러한 IP 주소는 기존 그룹에 추가하거나 만들 수 있습니다. 중요한 것은 그룹이 연결할 인스턴스에 액세스할 수 있는 권한이 있다는 것입니다 [!DNL Commerce Intelligence].

추가 시 [!DNL Commerce Intelligence] IP 주소입니다. `/32` 을(를) 표시할 주소 끝까지 [!DNL Amazon] 정확한 IP 주소입니다. 걱정하지 마십시오. AWS 인터페이스를 통해 이 기능이 필요하다는 것을 알 수 있습니다.

## 만들기 `Linux` 사용자 [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>이 단계는 암호화된 연결을 사용하는 경우에만 필요합니다. 이 작업을 수행하는 방법에 대한 지침은 사용 중인 데이터베이스에 대한 설정 항목(예: MySQL)을 참조하십시오. 다음 `Linux` 사용자는 다음을 만들 수 있습니다. `SSH tunnel`: 인터넷을 통해 데이터를 전송하는 가장 안전한 방법입니다.

## 데이터베이스 사용자 만들기 [!DNL Commerce Intelligence]

이는 사용 중인 데이터베이스에 따라 단계가 달라지는 프로세스의 일부입니다. 하지만 아이디어는 사용자를 만드는 것과 동일합니다 [!DNL Commerce Intelligence] 데이터베이스에 액세스하는 데 사용됩니다. 데이터베이스 만들기 지침 [!DNL Commerce Intelligence] 사용자는 사용 중인 데이터베이스의 설정 항목에서 찾을 수 있습니다.

## 에 연결 정보 입력 [!DNL Commerce Intelligence]

승인 후 [!DNL Commerce Intelligence] 인스턴스에 액세스하고 사용자를 생성했습니다. 마지막으로 해야 할 작업은 연결 정보를 입력하는 것입니다. [!DNL Commerce Intelligence].

의 자격 증명 페이지 `MySQL`, `Microsoft SQL`, 및 `PostgreSQL` 을 통해 액세스됩니다. `Integrations` 페이지 (**[!UICONTROL Manage Data** > **Integrations]**)을 클릭하여 **[!UICONTROL Add Integration]**. 통합 목록이 표시되면 사용 중인 데이터베이스의 아이콘을 눌러 인증서 페이지로 이동합니다. 현재 필요한 통합에 대한 액세스 권한이 없는 경우 Adobe 계정 팀에 문의하십시오.

연결 만들기를 완료하려면 다음 정보가 필요합니다.

* RDS 인스턴스의 공개 주소: 다음에서 찾을 수 있습니다. [!DNL AWS] 관리 콘솔.
* 데이터베이스 인스턴스가 사용하는 포트: 일부 데이터베이스에는 기본 포트가 있어 자동으로 `Port` 필드. 이 정보는 데이터베이스의 설치 설명서에서도 찾을 수 있습니다.
* 만든 사용자의 사용자 이름과 암호 [!DNL Commerce Intelligence].

암호화된 연결을 사용하는 경우 `Encrypted` [데이터베이스 인증서] 페이지에서 다음 작업을 수행합니다. `Yes`. 암호화 설정을 위한 추가 양식이 표시됩니다.

![](../../../assets/sql-integration-encrypted-yes.png)


