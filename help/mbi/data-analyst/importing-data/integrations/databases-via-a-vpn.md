---
title: VPN을 통해 데이터베이스 연결
description: SSH 터널 대신 VPN을 통해 데이터베이스를 연결하는 방법에 대해 알아봅니다.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# VPN을 통해 데이터베이스 연결

반면에 Adobe은 다음을 사용하여 데이터베이스를 연결할 것을 권장합니다. `SSH tunnel`, 암호화된 `VPN` 연결을 통해 보안을 유지할 수 있습니다. A `VPN` 는 모든 데이터베이스 통합에 사용할 수 있으며, 프로세스를 단순화하기 위해 를 설정하는 것과 거의 동일합니다. `SSH tunnel`:

1. [만들기 [!DNL Commerce Intelligence] 데이터베이스 사용자](#database)
1. [만들기 [!DNL Commerce Intelligence] VPN 사용자](#vpn)
1. [에 대한 액세스 허용 [!DNL Commerce Intelligence] IP 주소](#allowlist)
1. [Commerce Intelligence에 연결 및 VPN 사용자 정보 입력](#finish)

데이터베이스 자격 증명 외에 VPN 사용자가 작업을 완료할 수 있도록 자격 증명을 입력해야 합니다. 모든 VPN 사용자는 작동하지만 Adobe은 다음을 만들 것을 권장합니다. [!DNL Commerce Intelligence] 사용자: 를 사용하면 계정에서 사용자를 더 쉽게 추적할 수 있습니다.

## 데이터베이스 사용자 생성 [!DNL Commerce Intelligence] {#database}

데이터베이스 사용자를 만드는 프로세스는 연결하는 데이터베이스 유형에 따라 다릅니다. 각 데이터베이스 유형에 대한 지침을 보려면 아래 링크를 클릭하십시오.

* [Microsoft](../integrations/microsoft-sql-server.md)
* [몽고DB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSql](../integrations/postgresql.md)

## 만들기 `VPN` 사용자 [!DNL Commerce Intelligence] {#vpn}

앞에서 언급했듯이 모든 유효한 `VPN` 사용자는 작동하지만, Adobe은 다음 작업에만 사용자를 만들 것을 권장합니다. [!DNL Commerce Intelligence] 를 사용하십시오.

## 에 대한 액세스 허용 [!DNL Commerce Intelligence] IP 주소 {#allowlist}

연결에 성공하려면 IP 주소에서 액세스를 허용하도록 방화벽을 구성해야 합니다. 다음과 같습니다 `54.88.76.97` 및 `34.250.211.151`, 하지만 또한 `credentials` 데이터베이스 통합에 대한 페이지:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 연결 입력 및 `VPN` 사용자 정보 입력 [!DNL Commerce Intelligence] {#finish}

마무리하려면 연결 및 사용자 정보를 입력해야 합니다. [!DNL Commerce Intelligence]. 데이터베이스를 종료했습니까? `credentials` 페이지가 열렸습니까? 그렇지 않으면 다음으로 이동합니다. **[!UICONTROL Manage Data** > **Connections]**. 클릭 **[!UICONTROL Add New Data Source]**&#x200B;을 클릭하고 연결할 데이터베이스의 아이콘을 클릭합니다. 다음 사항을 변경하는 것을 잊지 마십시오. `Encrypted` 전환 대상 `Yes`.

이 페이지에 다음 정보를 입력하십시오. `Database Connection` 섹션:

* `Username`: 의 사용자 이름 [!DNL Commerce Intelligence] 데이터베이스 사용자
* `Password`: 의 암호 [!DNL Commerce Intelligence] 데이터베이스 사용자
* `Port`: 서버에 있는 데이터베이스의 포트입니다. 기본값은 다음과 같습니다.
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: 기본적으로 localhost입니다. `127.0.0.1`서버의 공용 IP 주소 또는 LAN 주소일 수도 있습니다.
* `Database Name (optional)`: 한 데이터베이스(데이터베이스 사용자 생성 단계 중에 지정됨)에만 액세스할 수 있도록 허용한 경우 여기에 해당 데이터베이스의 이름을 입력합니다.

아래 `Encryption Connection` 섹션:

* `Encryption Type`: 다음으로 설정 `Cisco IPsec VPN`
* `Gateway Address`: VPN 서버의 IP 주소
* `Group Name`: 그룹 인증에 사용되는 그룹 이름
* `Group Secret`: 그룹에 해당하는 암호입니다.
* `Username`: [!DNL Commerce Intelligence] `VPN` 사용자 이름
* `Password`: [!DNL Commerce Intelligence] `VPN` 사용자 암호

작업을 마치면 를 클릭합니다. **[!UICONTROL Save & Test]** 설치를 완료합니다.
