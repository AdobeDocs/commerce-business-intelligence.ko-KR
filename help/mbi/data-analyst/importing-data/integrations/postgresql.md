---
title: SSH 터널을 통해 PostgreSQL 연결
description: SSH 터널을 통해 PostgreSQL 데이터베이스를 Commerce Intelligence에 연결하는 방법을 알아봅니다.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# 연결 [!DNL PostgreSQL] 경유 [!DNL SSH Tunnel]

을(를) 연결하려면 [!DNL PostgreSQL] 데이터베이스 대상 [!DNL Commerce Intelligence] 을 통해 `SSH tunnel`, 다음 몇 가지 작업을 수행해야 합니다.

1. [검색 [!DNL Commerce Intelligence] 공개 키](#retrieve)
1. [에 대한 액세스 허용 [!DNL Commerce Intelligence] IP 주소](#allowlist)
1. [만들기 [!DNL Linux] 사용자 [!DNL Commerce Intelligence]](#linux)
1. [만들기 [!DNL PostgreSQL] 사용자 [!DNL Commerce Intelligence]](#postgres)
1. [에 연결 및 사용자 정보 입력 [!DNL Commerce Intelligence]](#finish)

## 검색 중 [!DNL Commerce Intelligence] [!DNL public key] {#retrieve}

다음 `public key` 을(를) 승인하는 데 사용됩니다. [!DNL Commerce Intelligence] [!DNL Linux] 사용자. 이제 사용자를 만들고 키를 가져옵니다.

1. 다음으로 이동 **[!UICONTROL Manage Data** > **Connections]** 및 클릭 **[!UICONTROL Add a Data Source]**.
1. 다음을 클릭합니다. [!DNL PostgreSQL] 아이콘.
1. 다음 이후 `PostgreSQL credentials` 페이지가 열리고 `Encrypted` 전환 대상 `Yes`. 그러면 `SSH` 양식 설정.
1. 다음 `public key` 은(는) 이 양식 아래에 있습니다.

자습서 전체에서 이 페이지를 열어 두십시오. 다음 섹션과 끝에서 필요합니다.

아래에서는 을 통해 탐색하는 방법을 보여 줍니다 [!DNL Commerce Intelligence] 키를 검색하려면 다음을 수행하십시오.

![RJMetrics 공개 키 검색](../../../assets/get-mbi-public-key.gif)

## 에 대한 액세스 허용 [!DNL Commerce Intelligence] IP 주소 {#allowlist}

연결에 성공하려면 IP 주소에서 액세스를 허용하도록 방화벽을 구성해야 합니다. 다음과 같습니다. `54.88.76.97/32`, 하지만 또한 `PostgreSQL` 자격 증명 페이지입니다. 위의 GIF에 있는 파란색 상자를 참조하십시오.

## 만들기 [!DNL Linux] 사용자 [!DNL Commerce Intelligence] {#linux}

실시간(또는 자주 업데이트되는) 데이터가 포함되어 있는 한 프로덕션 또는 보조 시스템일 수 있습니다. 다음을 수행할 수 있습니다. [이 사용자 제한](../../../administrator/account-management/restrict-db-access.md) 에 연결할 수 있는 권한이 유지되는 한 원하는 대로 [!DNL PostgreSQL] 서버입니다.

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
```

>[!IMPORTANT]
>
>다음과 같은 경우 `sshd\_config` 서버와 연결된 파일이 기본 옵션으로 설정되지 않고 특정 사용자만 서버에 액세스할 수 있으므로 [!DNL Commerce Intelligence]. 이러한 경우 다음과 같은 명령을 실행해야 합니다. `AllowUsers` rjmetric 사용자가 서버에 액세스할 수 있도록 허용합니다.

## 만들기 [!DNL Commerce Intelligence] [!DNL Postgres] 사용자 {#postgres}

조직에서는 다른 프로세스가 필요할 수 있지만 이 사용자를 생성하는 가장 간단한 방법은 권한을 부여할 수 있는 권한이 있는 사용자로 Postgres에 로그인할 때 다음 쿼리를 실행하는 것입니다. 사용자는 다음과 같은 스키마도 소유해야 합니다. [!DNL Commerce Intelligence] 에 대한 액세스 권한이 부여됩니다.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

바꾸기 `secure password` ssh 암호와 다를 수 있는 자체 보안 암호를 사용합니다. 또한 다음을 교체해야 합니다. `database name` 및 `schema name` 를 데이터베이스에 추가합니다.

여러 데이터베이스 또는 스키마를 연결하려면 필요에 따라 이 프로세스를 반복합니다.

## 에 연결 및 사용자 정보 입력 [!DNL Commerce Intelligence] {#finish}

마무리하려면 연결 및 사용자 정보를 입력해야 합니다. [!DNL Commerce Intelligence]. 다음을 떠나셨나요? [!DNL PostgreSQL] 자격 증명 페이지가 열려 있습니까? 그렇지 않으면 다음으로 이동합니다. **[!UICONTROL Manage Data > Connections]** 및 클릭 **[!UICONTROL Add a Data Source]**, 그런 다음 [!DNL PostgreSQL] 아이콘. 다음을 설정하는 것을 잊지 마십시오. `Encrypted` 전환 대상 `Yes`.

이 페이지에 다음 정보를 입력하십시오. `Database Connection` 섹션:

* `Username`: RJMetrics Postgres 사용자 이름(rjmetric이어야 함)
* `Password`: RJMetrics Postgres 암호
* `Port`: 서버의 PostgreSQL 포트(기본값: 5432)
* `Host`: 127.0.0.1

아래 `SSH Connection`:

* `Remote Address`: SSH를 사용할 서버의 IP 주소 또는 호스트 이름
* `Username`: SSH 로그인 이름(rjmetric이어야 함)
* `SSH Port`: 서버의 SSH 포트(기본적으로 22)

작업을 마치면 를 클릭합니다. **저장 및 테스트** 설치를 완료합니다.

### 관련 항목

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
