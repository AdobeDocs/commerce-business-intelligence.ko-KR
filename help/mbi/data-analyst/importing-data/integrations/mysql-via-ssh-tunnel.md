---
title: SSH 터널을 통해  [!DNL MySQL] 연결 중
description: SSH 터널을 통해 [!DNL MySQL] 연결하는 방법에 대해 알아봅니다.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# [!DNL MySQL]을(를) 통해 [!DNL SSH Tunnel] 연결

* [ [!DNL Commerce Intelligence] 공개 키 검색](#retrieve)
* [ [!DNL Commerce Intelligence] IP 주소에 대한 액세스 허용](#allowlist)
* [ [!DNL Commerce Intelligence]에 대한 Linux 사용자 만들기](#linux)
* [ [!DNL MySQL] 의  [!DNL Commerce Intelligence]사용자 만들기](#mysql)
* [ [!DNL Commerce Intelligence]에 연결 및 사용자 정보 입력](#finish)

## 이동

* [[!DNL MySQL] 경유 ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL]을(를) 통한  [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

[!DNL MySQL]을(를) 통해 [!DNL Commerce Intelligence] 데이터베이스를 `SSH tunnel`에 연결하려면 다음을 수행해야 합니다.

1. [!DNL Commerce Intelligence] `public key` 검색
1. [!DNL Commerce Intelligence] `IP address`에 대한 액세스 허용
1. `Linux`에 대해 [!DNL Commerce Intelligence] 사용자 만들기
1. `MySQL`에 대해 [!DNL Commerce Intelligence] 사용자 만들기
1. [!DNL Commerce Intelligence]에 연결 및 사용자 정보 입력


## [!DNL Commerce Intelligence] 공개 키 검색 중 {#retrieve}

`public key`은(는) [!DNL Commerce Intelligence] `Linux` 사용자를 승인하는 데 사용됩니다. 다음 섹션에서 사용자를 만들고 키를 가져옵니다.

1. **[!UICONTROL Manage Data** > **Connections]**(으)로 이동하여 **[!UICONTROL Add New Data Source]**&#x200B;을(를) 클릭합니다.
1. `MySQL` 아이콘을 클릭합니다.
1. `MySQL credentials` 페이지가 열린 후 `Encrypted` 전환을 `Yes`(으)로 설정합니다. SSH 설정 양식이 표시됩니다.
1. `public key`은(는) 이 양식 아래에 있습니다.

자습서 전체에서 이 페이지를 열어 두십시오. 다음 섹션과 끝에서 필요합니다.

키를 검색하기 위해 [!DNL Commerce Intelligence]을(를) 탐색하는 방법은 다음과 같습니다.

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## [!DNL Commerce Intelligence] IP 주소에 대한 액세스 허용 {#allowlist}

연결에 성공하려면 IP 주소에서 액세스를 허용하도록 방화벽을 구성해야 합니다. `54.88.76.97` 및 `34.250.211.151`이지만 `MySQL credentials` 페이지에도 있습니다. 위의 GIF에 있는 파란색 상자를 참조하십시오.

## [!DNL Linux]에 대해 [!DNL Commerce Intelligence] 사용자를 만드는 중 {#linux}

실시간(또는 자주 업데이트되는) 데이터가 포함되어 있는 한 프로덕션 또는 보조 시스템일 수 있습니다. [ 서버에 연결할 수 있는 권한이 있는 한 원하는 방식으로 ](../../../administrator/account-management/restrict-db-access.md)이 사용자를 제한`MySQL`할 수 있습니다.

1. 새 사용자를 추가하려면 [!DNL Linux] 서버에서 다음 명령을 root로 실행합니다.

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 첫 번째 섹션에서 검색한 `public key`을(를) 기억하십니까? 사용자가 데이터베이스에 액세스할 수 있도록 하려면 키를 `authorized\_keys`(으)로 가져와야 합니다.

   다음과 같이 전체 키를 `authorized\_keys` 파일에 복사합니다.

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. 사용자 만들기를 완료하려면 `/home/rjmetric`을(를) 통해 액세스할 수 있도록 `SSH` 디렉터리에 대한 권한을 변경하십시오.

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>서버와 연결된 `sshd\_config` 파일이 기본 옵션으로 설정되지 않은 경우 특정 사용자만 서버에 액세스할 수 있으므로 [!DNL Commerce Intelligence]에 연결할 수 없습니다. 이러한 경우 `AllowUsers` 사용자가 서버에 액세스할 수 있도록 하려면 `rjmetric`과(와) 같은 명령을 실행해야 합니다.

## [!DNL MySQL]에 대해 [!DNL Commerce Intelligence] 사용자를 만드는 중 {#mysql}

조직에 다른 프로세스가 필요할 수 있지만 이 사용자를 만드는 가장 간단한 방법은 권한을 부여할 수 있는 권한이 있는 사용자로 [!DNL MySQL]에 로그인한 경우 다음 쿼리를 실행하는 것입니다.

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

`secure password here`을(를) `SSH` 암호와 다른 보안 암호로 바꾸십시오.

이 사용자가 특정 데이터베이스, 테이블 또는 열의 데이터에 액세스하지 못하도록 제한하려면 대신 사용자가 허용하는 데이터에만 액세스를 허용하는 GRANT 쿼리를 실행할 수 있습니다.

## [!DNL Commerce Intelligence]에 연결 및 사용자 정보 입력 {#finish}

마무리하려면 [!DNL Commerce Intelligence]에 연결 및 사용자 정보를 입력해야 합니다. `MySQL credentials` 페이지를 열어 두셨습니까? 그렇지 않으면 **[!UICONTROL Data** > **Connections]**(으)로 이동하여 **[!UICONTROL Add New Data Source]**&#x200B;을(를) 클릭한 다음 [!DNL MySQL] 아이콘을 클릭합니다. `Encrypted` 토글을 `Yes`(으)로 설정하는 것을 잊지 마십시오.

이 페이지에 `Database Connection` 섹션부터 다음 정보를 입력하십시오.

* `Username`: [!DNL Commerce Intelligence] [!DNL MySQL] 사용자의 사용자 이름
* `Password`: [!DNL Commerce Intelligence] [!DNL MySQL] 사용자의 암호
* `Port`: 서버의 [!DNL MySQL] 포트(기본적으로 3306)
* `Host` 기본적으로 localhost입니다. 일반적으로 이 값은 [!DNL MySQL] 서버에 대한 바인드 주소 값이며 기본적으로 `127.0.0.1 (localhost)`이지만 일부 로컬 네트워크 주소(예: `192.168.0.1`) 또는 서버의 공용 IP 주소일 수도 있습니다.

  이 값은 `my.cnf`을(를) 읽는 줄 아래의 `/etc/my.cnf` 파일(`\[mysqld\]`에 있음)에서 찾을 수 있습니다. 해당 파일에서 바인드 주소 줄이 주석 처리되면 외부 연결 시도로부터 서버가 보호됩니다.

`SSH Connection` 섹션에서:

* `Remote Address`: [!DNL Commerce Intelligence] 서버의 IP 주소 또는 호스트 이름이
* `Username`: [!DNL Commerce Intelligence] SSH([!DNL Linux]) 사용자의 사용자 이름
* `SSH Port`: 서버의 SSH 포트(기본적으로 22)

완료되면 **[!UICONTROL Save & Test]**&#x200B;을(를) 클릭하여 설치를 완료합니다.

## 관련 항목:

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ko)
