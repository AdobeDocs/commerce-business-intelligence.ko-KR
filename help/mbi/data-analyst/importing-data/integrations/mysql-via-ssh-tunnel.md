---
title: 연결 중 [!DNL MySQL] SSH 터널 사용
description: 연결 방법 알아보기 [!DNL MySQL] SSH 터널을 통해
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# 연결 [!DNL MySQL] 경유 [!DNL SSH Tunnel]

* [검색 [!DNL Commerce Intelligence] 공개 키](#retrieve)
* [에 대한 액세스 허용 [!DNL Commerce Intelligence] IP 주소](#allowlist)
* [Linux 사용자 만들기 [!DNL Commerce Intelligence]](#linux)
* [만들기 [!DNL MySQL] 사용자 [!DNL Commerce Intelligence]](#mysql)
* [에 연결 및 사용자 정보 입력 [!DNL Commerce Intelligence]](#finish)

## 이동

* [[!DNL MySQL] 경유 ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] 경유 [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

을(를) 연결하려면 [!DNL MySQL] 데이터베이스 대상 [!DNL Commerce Intelligence] 을 통해 `SSH tunnel`, 다음 몇 가지 작업을 수행해야 합니다.

1. 검색 [!DNL Commerce Intelligence] `public key`
1. 에 대한 액세스 허용 [!DNL Commerce Intelligence] `IP address`
1. 만들기 `Linux` 사용자 [!DNL Commerce Intelligence]
1. 만들기 `MySQL` 사용자 [!DNL Commerce Intelligence]
1. 에 연결 및 사용자 정보 입력 [!DNL Commerce Intelligence]


## 검색 중 [!DNL Commerce Intelligence] 공개 키 {#retrieve}

다음 `public key` 을(를) 승인하는 데 사용됩니다. [!DNL Commerce Intelligence] `Linux` 사용자. 다음 섹션에서 사용자를 만들고 키를 가져옵니다.

1. 다음으로 이동 **[!UICONTROL Manage Data** > **Connections]** 및 클릭 **[!UICONTROL Add New Data Source]**.
1. 다음을 클릭합니다. `MySQL` 아이콘.
1. 다음 이후 `MySQL credentials` 페이지가 열리고 `Encrypted` 전환 대상 `Yes`. SSH 설정 양식이 표시됩니다.
1. 다음 `public key` 은(는) 이 양식 아래에 있습니다.

자습서 전체에서 이 페이지를 열어 두십시오. 다음 섹션과 끝에서 필요합니다.

탐색 방법은 다음과 같습니다 [!DNL Commerce Intelligence] 키를 검색하려면 다음을 수행하십시오.

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## 에 대한 액세스 허용 [!DNL Commerce Intelligence] IP 주소 {#allowlist}

연결에 성공하려면 IP 주소에서 액세스를 허용하도록 방화벽을 구성해야 합니다. 다음과 같습니다 `54.88.76.97` 및 `34.250.211.151` 하지만 다음 항목에도 있습니다. `MySQL credentials` 페이지를 가리키도록 업데이트하는 중입니다. 위의 GIF에 있는 파란색 상자를 참조하십시오.

## 만들기 [!DNL Linux] 사용자 [!DNL Commerce Intelligence] {#linux}

실시간(또는 자주 업데이트되는) 데이터가 포함되어 있는 한 프로덕션 또는 보조 시스템일 수 있습니다. 다음을 수행할 수 있습니다. [이 사용자 제한](../../../administrator/account-management/restrict-db-access.md) 에 연결할 수 있는 권한이 유지되는 한 원하는 대로 `MySQL` 서버입니다.

1. 새 사용자를 추가하려면 다음 명령을 루트로 실행합니다. [!DNL Linux] 서버:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 다음을 기억하십시오. `public key` 첫 번째 섹션에서 검색하셨습니까? 사용자가 데이터베이스에 액세스할 수 있도록 하려면 키를 로 가져와야 합니다 `authorized\_keys`.

   전체 키를 `authorized\_keys` 파일을 다음과 같이 지정합니다.

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. 사용자 만들기를 완료하려면 `/home/rjmetric` 를 통한 액세스를 허용할 디렉터리 `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>다음과 같은 경우 `sshd\_config` 서버와 연결된 파일이 기본 옵션으로 설정되지 않고 특정 사용자만 서버에 액세스할 수 있으므로 [!DNL Commerce Intelligence]. 이러한 경우 다음과 같은 명령을 실행해야 합니다. `AllowUsers` 허용 `rjmetric` 서버에 대한 사용자 액세스 권한.

## 만들기 [!DNL MySQL] 사용자 [!DNL Commerce Intelligence] {#mysql}

조직에서는 다른 프로세스가 필요할 수 있지만 로그인할 때 다음 쿼리를 실행하는 것이 이 사용자를 만드는 가장 간단한 방법입니다 [!DNL MySQL] 권한을 부여할 권한이 있는 사용자:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

바꾸기 `secure password here` 와 다를 수 있는 보안 암호를 사용합니다. `SSH` 암호.

이 사용자가 특정 데이터베이스, 테이블 또는 열의 데이터에 액세스하지 못하도록 제한하려면 대신 사용자가 허용하는 데이터에만 액세스를 허용하는 GRANT 쿼리를 실행할 수 있습니다.

## 에 연결 및 사용자 정보 입력 [!DNL Commerce Intelligence] {#finish}

마무리하려면 연결 및 사용자 정보를 입력해야 합니다. [!DNL Commerce Intelligence]. 다음을 떠나셨나요? `MySQL credentials` 페이지가 열렸습니까? 그렇지 않으면 다음으로 이동합니다. **[!UICONTROL Data** > **Connections]** 및 클릭 **[!UICONTROL Add New Data Source]**, 그런 다음 [!DNL MySQL] 아이콘. 다음을 설정하는 것을 잊지 마십시오. `Encrypted` 전환 대상 `Yes`.

이 페이지에 다음 정보를 입력하십시오. `Database Connection` 섹션:

* `Username`: 의 사용자 이름 [!DNL Commerce Intelligence] [!DNL MySQL] 사용자
* `Password`: 의 암호 [!DNL Commerce Intelligence] [!DNL MySQL] 사용자
* `Port`: [!DNL MySQL] 서버의 포트(기본적으로 3306)
* `Host` 기본적으로 localhost입니다. 일반적으로 의 바인드 주소 값입니다. [!DNL MySQL] 서버 - 기본적으로 `127.0.0.1 (localhost)`로컬 네트워크 주소일 수도 있습니다(예: `192.168.0.1`) 또는 서버의 공용 IP 주소입니다.

   값은 다음에서 찾을 수 있습니다. `my.cnf` 파일(위치: `/etc/my.cnf`)를 나타내는 줄 아래에 `\[mysqld\]`. 해당 파일에서 바인드 주소 줄이 주석 처리되면 외부 연결 시도로부터 서버가 보호됩니다.

다음에서 `SSH Connection` 섹션:

* `Remote Address`: 서버의 IP 주소 또는 호스트 이름 [!DNL Commerce Intelligence] 다음으로 터널링됨
* `Username`: 의 사용자 이름 [!DNL Commerce Intelligence] SSH ([!DNL Linux]) 사용자
* `SSH Port`: 서버의 SSH 포트(기본적으로 22)

작업을 마치면 를 클릭합니다. **[!UICONTROL Save & Test]** 설치를 완료합니다.

## 관련 항목:

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
