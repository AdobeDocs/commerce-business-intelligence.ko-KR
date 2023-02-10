---
title: SSH 터널을 통해 MySQL 연결
description: SSH 터널을 통해 MySQL을 연결하는 방법을 알아봅니다.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# Connect `MySQL` via `SSH Tunnel`

* [검색 [!DNL MBI] 공개 키](#retrieve)
* [에 대한 액세스 허용 [!DNL MBI] IP 주소](#allowlist)
* [용 Linux 사용자 생성 [!DNL MBI]](#linux)
* [에 대한 MySQL 사용자 만들기 [!DNL MBI]](#mysql)
* [연결 및 사용자 정보를에 입력합니다. [!DNL MBI]](#finish)

## 이동

* `MySQL via SSH tunnel`
* [&#39;MySQL&#39;](../integrations/mysql-via-a-direct-connection.md)
* [&#39;MySQL&#39;](../integrations/mysql-via-cpanel.md)

연결 `MySQL` 데이터베이스 대상 [!DNL MBI] 를 통해 `SSH tunnel`, 사용자(또는 기술자가 아닌 경우 사용자 팀)는 다음 몇 가지 작업을 수행해야 합니다.

1. 검색 [!DNL MBI] `public key`
1. 에 대한 액세스 허용 [!DNL MBI] `IP address`
1. 만들기 `Linux` 사용자 [!DNL MBI]
1. 만들기 `MySQL` 사용자 [!DNL MBI]
1. 연결 및 사용자 정보를에 입력합니다. [!DNL MBI]

그것은 들리는 것만큼 복잡하지 않다. 시작해 보겠습니다.

## 검색 [!DNL MBI] 공개 키 {#retrieve}

다음 `public key` 는 를 승인하는 데 사용됩니다 [!DNL MBI] `Linux` 사용자. 다음 섹션에서는 사용자를 만들고 키를 가져옵니다.

1. 이동 **[!UICONTROL Manage Data** > **Connections]** 을(를) 클릭합니다. **[!UICONTROL Add New Data Source]**.
1. 을(를) 클릭합니다. `MySQL` 아이콘.
1. 다음 이후 `MySQL credentials` 페이지가 열리고 `Encrypted` 전환 `Yes`. SSH 설정 양식이 표시됩니다.
1. 다음 `public key` 는 이 양식 아래에 있습니다.

이 페이지를 자습서 전체에서 열어 둡니다. 이 페이지는 다음 섹션과 끝에 필요합니다.

만약 여러분이 약간 길을 잃는다면, 여기 어떻게 탐색해야 할지 알려드리겠습니다 [!DNL MBI] 키를 검색하려면 다음을 수행하십시오.

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## 에 대한 액세스 허용 [!DNL MBI] IP 주소 {#allowlist}

연결에 성공하려면 IP 주소에서 액세스할 수 있도록 방화벽을 구성해야 합니다. 그렇습니다 `54.88.76.97` 및 `34.250.211.151` 하지만 그들은 또한 `MySQL credentials` 페이지. 위의 GIF에 있는 파란색 상자가 보입니까? 바로 그거야!

## 만들기 `Linux` 사용자 [!DNL MBI] {#linux}

실시간(또는 자주 업데이트되는) 데이터가 포함된 경우 프로덕션 또는 보조 시스템일 수 있습니다. 다음을 수행할 수 있습니다 [이 사용자 제한](../../../administrator/account-management/restrict-db-access.md) 원하는 방식대로, 원하는 방법으로 `MySQL` server.

1. 새 사용자를 추가하려면 다음 명령을 `Linux` server:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 다음 사항을 기억하십시오 `public key` 첫 번째 섹션에서 검색했습니까? 사용자가 데이터베이스에 액세스할 수 있도록 하려면 키를 `authorized\_keys`.

   전체 키를 `authorized\_keys` 파일:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. 사용자 만들기를 완료하려면 `/home/rjmetric` 을 통해 액세스를 허용하는 디렉토리 `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>만약 `sshd\_config` 서버와 연결된 파일이 기본 옵션으로 설정되어 있지 않고 특정 사용자만 서버 액세스 권한이 있습니다. 이렇게 하면 에 성공적으로 연결할 수 없습니다 [!DNL MBI]. 이러한 경우 다음과 같은 명령을 실행해야 합니다 `AllowUsers` 허용 `rjmetric` 서버에 대한 사용자 액세스 권한.

## 만들기 `MySQL` 사용자 [!DNL MBI] {#mysql}

조직에서 다른 프로세스를 필요로 할 수 있지만, 이 사용자를 만드는 가장 간단한 방법은 로그인한 경우 다음 쿼리를 실행하는 것입니다 `MySQL` 권한을 부여할 수 있는 권한이 있는 사용자로서:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

바꾸기 `secure password here` 보안 암호가 있는 경우 `SSH` 암호.

이 사용자가 특정 데이터베이스, 테이블 또는 열의 데이터에 액세스하지 못하도록 제한하려면 사용자가 허용하는 데이터에 대해서만 액세스를 허용하는 GRANT 쿼리를 실행할 수 있습니다.

## 연결 및 사용자 정보를 [!DNL MBI] {#finish}

요약하려면 연결 및 사용자 정보를 [!DNL MBI]. 여기 나가셨어요? `MySQL credentials` 페이지를 열어? 그렇지 않으면 로 이동합니다. **[!UICONTROL Data** > **Connections]** 을(를) 클릭합니다. **[!UICONTROL Add New Data Source]**&#x200B;를 가리킨 다음 MySQL 아이콘을 클릭합니다. 을 설정하는 것을 잊지 마십시오 `Encrypted` 전환 `Yes`.

데이터베이스 연결 섹션부터 시작하여 다음 정보를 이 페이지에 입력합니다.

* `Username`: 사용자 이름 [!DNL MBI] MySQL 사용자
* `Password`: 의 암호 [!DNL MBI] MySQL 사용자
* `Port`: 서버의 MySQL 포트(기본적으로 3306)
* `Host` 기본적으로 localhost입니다. 일반적으로 MySQL 서버의 바인드 주소 값이며 기본값은 입니다. `127.0.0.1 (localhost)`그러나 일부 로컬 네트워크 주소(예: `192.168.0.1`) 또는 서버의 공용 IP 주소입니다.

   값은 `my.cnf` 파일(일반적으로 `/etc/my.cnf`)를 읽습니다 `\[mysqld\]`. 해당 파일에서 바인드 주소 라인을 주석 처리하면 외부 연결 시도에서 서버가 보안됩니다.

에서 `SSH Connection` 섹션:

* `Remote Address`: 서버의 IP 주소 또는 호스트 이름 [!DNL MBI] 터널로
* `Username`: 사용자 이름 [!DNL MBI] SSH(Linux) 사용자
* `SSH Port`: 서버의 SSH 포트(기본적으로 22)

바로 그거야! 완료되면 를 클릭합니다 **[!UICONTROL Save & Test]** 를 클릭하여 설정을 완료합니다.

## 관련:

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
