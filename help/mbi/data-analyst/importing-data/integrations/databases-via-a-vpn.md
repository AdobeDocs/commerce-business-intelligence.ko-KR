---
title: VPN을 통해 데이터베이스 연결
description: SSH 터널 대신 VPN을 통해 데이터베이스를 연결하는 방법에 대해 알아봅니다.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# VPN을 통해 데이터베이스 연결

Adobe에서는 `SSH tunnel`을(를) 사용하여 데이터베이스를 연결하는 것이 좋지만 암호화된 `VPN` 연결을 사용하여 보안을 유지할 수도 있습니다. `VPN`은(는) 모든 데이터베이스 통합에 사용할 수 있으며, 프로세스를 단순화하기 위해 `SSH tunnel`을(를) 설정하는 것과 거의 동일합니다.

1. [&#x200B; [!DNL Commerce Intelligence] 데이터베이스 사용자 만들기](#database)
1. [&#x200B; [!DNL Commerce Intelligence] VPN 사용자 만들기](#vpn)
1. [&#x200B; [!DNL Commerce Intelligence] IP 주소에 대한 액세스 허용](#allowlist)
1. [Commerce Intelligence에 연결 및 VPN 사용자 정보 입력](#finish)

데이터베이스 자격 증명 외에 VPN 사용자가 작업을 완료할 수 있도록 자격 증명을 입력해야 합니다. Adobe 모든 VPN 사용자가 작동하지만, 계정에서 사용자를 더 쉽게 추적할 수 있도록 [!DNL Commerce Intelligence] 사용자를 만드는 것이 좋습니다.

## [!DNL Commerce Intelligence]에 대한 데이터베이스 사용자를 만드는 중 {#database}

데이터베이스 사용자를 만드는 프로세스는 연결하는 데이터베이스 유형에 따라 다릅니다. 각 데이터베이스 유형에 대한 지침을 보려면 아래 링크를 클릭하십시오.

* [Microsoft](../integrations/microsoft-sql-server.md)
* [몽고DB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSql](../integrations/postgresql.md)

## `VPN`에 대해 [!DNL Commerce Intelligence] 사용자를 만드는 중 {#vpn}

앞에서 언급했듯이 모든 유효한 `VPN` 사용자가 작동하지만, Adobe에서는 [!DNL Commerce Intelligence]용으로만 사용자를 만들 것을 권장합니다.

## [!DNL Commerce Intelligence] IP 주소에 대한 액세스 허용 {#allowlist}

연결에 성공하려면 IP 주소에서 액세스를 허용하도록 방화벽을 구성해야 합니다. `54.88.76.97` 및 `34.250.211.151`이지만 데이터베이스 통합을 위한 `credentials` 페이지에도 있습니다.

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 연결 및 `VPN` 사용자 정보를 [!DNL Commerce Intelligence]에 입력 중 {#finish}

마무리하려면 [!DNL Commerce Intelligence]에 연결 및 사용자 정보를 입력해야 합니다. 데이터베이스 `credentials` 페이지를 열어 두셨습니까? 그렇지 않으면 **[!UICONTROL Manage Data** > **Connections]**(으)로 이동합니다. **[!UICONTROL Add New Data Source]**&#x200B;을(를) 클릭한 다음 연결 중인 데이터베이스의 아이콘을 클릭합니다. `Encrypted` 토글을 `Yes`(으)로 변경하는 것을 잊지 마십시오.

이 페이지에 `Database Connection` 섹션부터 다음 정보를 입력하십시오.

* `Username`: [!DNL Commerce Intelligence] 데이터베이스 사용자의 사용자 이름
* `Password`: [!DNL Commerce Intelligence] 데이터베이스 사용자의 암호
* `Port`: 서버에 있는 데이터베이스의 포트입니다. 기본값은 다음과 같습니다.
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: 기본적으로 localhost `127.0.0.1`이지만 서버의 공용 IP 주소 또는 LAN 주소일 수도 있습니다.
* `Database Name (optional)`: 한 데이터베이스(데이터베이스 사용자 만들기 단계에서 지정됨)에 대한 액세스만 허용한 경우 여기에 해당 데이터베이스의 이름을 입력하십시오.

`Encryption Connection` 섹션 아래:

* `Encryption Type`: `Cisco IPsec VPN`(으)로 설정
* `Gateway Address`: VPN 서버의 IP 주소
* `Group Name`: 그룹 인증에 사용되는 그룹 이름
* `Group Secret`: 그룹에 해당하는 암호입니다.
* `Username`: [!DNL Commerce Intelligence] `VPN` 사용자 이름
* `Password`: [!DNL Commerce Intelligence] `VPN` 사용자 암호

완료되면 **[!UICONTROL Save & Test]**&#x200B;을(를) 클릭하여 설치를 완료합니다.
