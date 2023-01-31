---
title: VPN을 통해 데이터베이스 연결
description: SSH 터널 대신 VPN을 통해 데이터베이스를 연결하는 방법을 알아봅니다.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# VPN을 통해 데이터베이스 연결

SSH 터널을 사용하여 데이터베이스를 연결하는 것이 좋지만 암호화된 VPN 연결을 사용하여 보안을 유지할 수도 있습니다. A `VPN` 모든 데이터베이스 통합에 사용할 수 있으며, 작업을 단순화하기 위해 프로세스는 를 설정하는 것과 거의 같습니다 `SSH tunnel`:

1. [만들기 [!DNL MBI] 데이터베이스 사용자](#database)
1. [만들기 [!DNL MBI] VPN 사용자](#vpn)
1. [에 대한 액세스 허용 [!DNL MBI] IP 주소](#allowlist)
1. [MBI에 연결 및 VPN 사용자 정보를 입력하십시오.](#finish)

데이터베이스 자격 증명 외에 VPN 사용자가 내용을 정리하기 위한 자격 증명을 입력해야 합니다. 모든 VPN 사용자가 작동하지만 [!DNL MBI] 사용자 - 계정에서 사용자를 쉽게 추적할 수 있습니다.

시작해 보겠습니다.

## 데이터베이스 사용자 생성 [!DNL MBI] {#database}

데이터베이스 사용자 생성 프로세스는 연결 중인 데이터베이스 유형에 따라 달라집니다. 각 데이터베이스 유형에 대한 지침을 보려면 아래 링크를 클릭하십시오.

* [Microsoft SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## 만들기 `VPN` 사용자 [!DNL MBI] {#vpn}

전에 언급했듯이 모든 유효한 `VPN` 사용자가 작동하지만, [!DNL MBI] 사용.

## 에 대한 액세스 허용 [!DNL MBI] IP 주소 {#allowlist}

연결에 성공하려면 IP 주소에서 액세스할 수 있도록 방화벽을 구성해야 합니다. 그렇습니다 `54.88.76.97` 및 `34.250.211.151`하지만, 또한 `credentials` 모든 데이터베이스 통합에 대한 페이지

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 연결 입력 및 `VPN` 사용자 정보 [!DNL MBI] {#finish}

요약하려면 연결 및 사용자 정보를 [!DNL MBI]. 데이터베이스를 그대로 두셨나요 `credentials` 페이지를 열어? 그렇지 않으면 로 이동합니다. **[!UICONTROL Manage Data** > **Connections]** 을(를) 클릭합니다. **[!UICONTROL Add New Data Source]**&#x200B;을 눌러 연결하는 데이터베이스의 아이콘을 선택합니다. 변경 사항을 잊지 마십시오 `Encrypted` 전환 `Yes`.

다음 정보를 이 페이지에 입력하고 `Database Connection` 섹션:

* `Username`: 사용자 이름 [!DNL MBI] 데이터베이스 사용자
* `Password`: 의 암호 [!DNL MBI] 데이터베이스 사용자
* `Port`: 서버의 데이터베이스 포트입니다. 기본값은 다음과 같습니다.
* `MicrosoftSQL`: `1433`
* `MongoDB`: `27017`
* `MySQL`: `3306`
* `PostgreSQL`: `5432`
* `Host`: 기본적으로 localhost입니다. `127.0.0.1`그러나 서버의 공용 IP 주소 또는 로컬 영역 네트워크 주소일 수도 있습니다.
* `Database Name (optional)`: 데이터베이스 사용자 생성 단계에서 지정한 데이터베이스에 대한 액세스 권한만 허용하는 경우 여기에서 해당 데이터베이스의 이름을 입력합니다.

아래에 `Encryption Connection` 섹션:

* `Encryption Type`: 을(를) (으)로 설정합니다. `Cisco IPsec VPN`
* `Gateway Address`: VPN 서버의 IP 주소
* `Group Name`: 그룹 인증에 사용되는 그룹의 이름입니다
* `Group Secret`: 그룹에 해당하는 암호입니다.
* `Username`: 다음 [!DNL MBI] `VPN` 사용자 이름
* `Password`: 다음 [!DNL MBI] `VPN` 사용자 암호

바로 그거야! 완료되면 를 클릭합니다 **[!UICONTROL Save & Test]** 를 클릭하여 설정을 완료합니다.
