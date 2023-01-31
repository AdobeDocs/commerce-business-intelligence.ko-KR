---
title: Amazon RDS 연결
description: RDS 인스턴스를 연결하는 단계를 알아봅니다.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Amazon RDS 연결

Amazon Relational Database Services(RDS)는 이미 익숙한 데이터베이스 엔진에서 실행되는 관리 데이터베이스 서비스입니다. [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md), [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md), 및 [[!DNL PostgreSQ]](../integrations/postgresql.md).

RDS 인스턴스를 연결하는 단계는 사용 중인 데이터베이스 유형(각 데이터베이스에 대한 자세한 지침은 위의 링크 사용)과 암호화된 연결(예: [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)).

## 권한 부여 [!DNL MBI] 데이터베이스에 액세스하려면

자격 증명 페이지(**[!UICONTROL Manage Data** > **Integrations]**) 각 데이터베이스에 대해 RDS를 MBI에 연결하기 위해 인증해야 하는 IP 주소가 포함된 상자가 표시됩니다. `54.88.76.97` 및 `34.250.211.151`. 다음은 `MySQL credentials` 페이지에서 IP 주소 상자를 강조 표시한 경우:

![](../../../assets/RDS_IP.png)

대상 [!DNL MBI] RDS 인스턴스와 연결하려면 AWS 관리 콘솔을 통해 해당 데이터베이스 보안 그룹에 이러한 IP 주소를 추가해야 합니다. 이러한 IP 주소를 기존 그룹에 추가하거나 새 IP 주소를 만들 수 있습니다. 중요한 것은 연결할 인스턴스에 액세스할 수 있는 권한이 그룹에 부여되었다는 것입니다 [!DNL MBI].

를 추가할 때 [!DNL MBI] IP 주소, `/32` 주소 끝에 가 정확한 IP 주소임을 Amazon에 나타낼 수 있습니다. 걱정하지 마십시오. AWS 인터페이스를 통해 이 작업이 필수임을 알 수 있습니다.

## 만들기 `Linux` 사용자 [!DNL MBI] {#linux}

>[!NOTE]
>
>이 단계는 암호화된 연결을 사용하는 경우에만 필요합니다. 이 작업을 수행하는 방법에 대한 지침은 사용 중인 데이터베이스에 대한 설정 문서를 참조하십시오(예: MySQL). 다음 `Linux` 사용자가 `SSH tunnel`- 인터넷을 통해 데이터를 전송하는 가장 안전한 방법입니다.

## MBI용 데이터베이스 사용자 만들기

사용 중인 데이터베이스에 따라 단계가 달라지는 프로세스의 일부입니다. 하지만, 그 생각은 같다: 다음에 대한 사용자를 만듭니다. [!DNL MBI] 데이터베이스에 액세스하는 데 사용됩니다. 데이터베이스 만들기 지침 [!DNL MBI] 사용자는 사용 중인 데이터베이스의 설정 문서에 있습니다.

## MBI에 연결 정보 입력

당신이 허락한 후에 [!DNL MBI] 인스턴스에 액세스하고 사용자를 생성할 때 마지막으로 해야 할 작업은 연결 정보를 [!DNL MBI].

에 대한 자격 증명 페이지 `MySQL`, `Microsoft SQL`, 및 `PostgreSQL` 는 `Integrations` 페이지 (**[!UICONTROL Manage Data** > **Integrations]**). **[!UICONTROL Add Integration]**. 통합 목록이 표시되면 사용 중인 데이터베이스의 아이콘을 클릭하여 인증서 페이지로 이동합니다. 현재 필요한 통합에 액세스할 수 없는 경우 CSM에 문의하십시오.

연결 만들기를 완료하려면 다음 정보가 필요합니다.

* RDS 인스턴스의 공개 주소: AWS 관리 콘솔에서 찾을 수 있습니다.
* 데이터베이스 인스턴스가 사용하는 포트: 일부 데이터베이스에는 자동으로 `Port` 필드. 이 정보는 데이터베이스의 설정 설명서에서도 찾을 수 있습니다.
* 만든 사용자의 사용자 이름 및 암호입니다 [!DNL MBI].

암호화된 연결을 사용하는 경우 `Encrypted` 데이터베이스 인증서 페이지에서 `Yes`. 암호화 설정을 위한 추가 양식이 표시됩니다.

![](../../../assets/sql-integration-encrypted-yes.png)

그게 전부야! RDS 인스턴스 연결이 완료되었습니다.
