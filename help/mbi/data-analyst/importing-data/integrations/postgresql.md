---
title: SSH 터널을 통해 PostgreSQL 연결
description: PostgreSQL 데이터베이스를 [!DNL MBI] SSH 터널을 통해
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Connect `PostgreSQL` via `SSH` 터널

연결 `PostgreSQL` 데이터베이스 대상 [!DNL MBI] 를 통해 `SSH tunnel`, 사용자(또는 기술자가 아닌 경우 사용자 팀)는 다음 몇 가지 작업을 수행해야 합니다.

1. [검색 [!DNL MBI] 공개 키](#retrieve)
1. [에 대한 액세스 허용 [!DNL MBI] IP 주소](#allowlist)
1. [용 Linux 사용자 생성 [!DNL MBI] ](#linux)
1. [다음에 대한 Postgres 사용자 만들기 [!DNL MBI] ](#postgres)
1. [MBI에 연결 및 사용자 정보를 입력합니다](#finish)

그것은 들리는 것만큼 복잡하지 않다. 시작.

## 검색 [!DNL MBI] `public key` {#retrieve}

다음 `public key` 는 를 승인하는 데 사용됩니다 [!DNL MBI] Linux 사용자. 다음 섹션에서는 사용자를 만들고 키를 가져옵니다.

1. 이동 **[!UICONTROL Manage Data** > **Connections]** 을(를) 클릭합니다. **[!UICONTROL Add a Data Source]**.
1. 을(를) 클릭합니다. `PostgreSQL` 아이콘.
1. 다음 이후 `PostgreSQL credentials` 페이지가 열리고 `Encrypted` 전환 `Yes`. 그러면 `SSH` 설정 양식.
1. 다음 `public key` 는 이 양식 아래에 있습니다.

이 페이지를 자습서 전체에서 열어 둡니다. 이 페이지는 다음 섹션과 끝에 필요합니다.

약간 손실된 경우 이 방법으로 탐색합니다 [!DNL MBI] 키를 검색하려면 다음을 수행하십시오.

![RJMetrics 공개 키 검색](../../../assets/get-mbi-public-key.gif)

## 에 대한 액세스 허용 [!DNL MBI] IP 주소 {#allowlist}

연결에 성공하려면 IP 주소에서 액세스할 수 있도록 방화벽을 구성해야 합니다. 그것은 `54.88.76.97/32`하지만, 또한 `PostgreSQL` 자격 증명 페이지. 위의 GIF에 있는 파란색 상자가 보입니까? 바로 그거야!

## 만들기 `Linux` 사용자 [!DNL MBI] {#linux}

실시간(또는 자주 업데이트되는) 데이터가 포함된 경우 프로덕션 또는 보조 시스템일 수 있습니다. 다음을 수행할 수 있습니다 [이 사용자 제한](../../../administrator/account-management/restrict-db-access.md) 원하는 방식으로, PostgreSQL 서버에 연결할 수 있는 권한이 있는 한.

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
```

>[!IMPORTANT]
>
>만약 `sshd\_config` 서버와 연결된 파일이 기본 옵션으로 설정되어 있지 않고 특정 사용자만 서버 액세스 권한이 있습니다. 이렇게 하면 에 성공적으로 연결할 수 없습니다 [!DNL MBI]. 이러한 경우 다음과 같은 명령을 실행해야 합니다 `AllowUsers` rjmetric 사용자가 서버에 액세스할 수 있도록 하기 위한 것입니다.

## 만들기 [!DNL MBI] Postgres 사용자 {#postgres}

조직에서 다른 프로세스를 필요로 할 수 있지만, 이 사용자를 만드는 가장 간단한 방법은 권한을 부여할 수 있는 권한이 있는 사용자로 Postgres에 로그인할 때 다음 쿼리를 실행하는 것입니다. 또한 사용자는 [!DNL MBI] 에 대한 액세스 권한이 부여됩니다.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

바꾸기 `secure password` 보안 암호를 직접 사용(SSH 암호와 다를 수 있음). 또한 `database name` 및 `schema name` 데이터베이스에 해당 이름을 입력합니다.

여러 데이터베이스 또는 스키마를 연결하려면 필요에 따라 이 프로세스를 반복합니다.

## 연결 및 사용자 정보를 [!DNL MBI] {#finish}

요약하려면 연결 및 사용자 정보를 [!DNL MBI]. PostgreSQL 인증서 페이지를 열어 두었습니까? 그렇지 않으면 로 이동합니다. **[!UICONTROL Manage Data > Connections]** 을(를) 클릭합니다. **[!UICONTROL Add a Data Source]**&#x200B;를 클릭한 다음 PostgreSQL 아이콘을 클릭합니다. 을 설정하는 것을 잊지 마십시오 `Encrypted` 전환 `Yes`.

데이터베이스 연결 섹션부터 시작하여 다음 정보를 이 페이지에 입력합니다.

* `Username`: RJMetrics Postgres 사용자 이름(rjmetric이어야 함)
* `Password`: RJMetics Postgres 암호
* `Port`: 서버의 PostgreSQL 포트(기본적으로 5432)
* `Host`: 127.0.0.1

아래 `SSH Connection`:

* `Remote Address`: SSH를 사용할 서버의 IP 주소 또는 호스트 이름
* `Username`: SSH 로그인 이름(rjmetric이어야 함)
* `SSH Port`: 서버의 SSH 포트(기본적으로 22)

바로 그거야! 완료되면 를 클릭합니다 **저장 및 테스트** 를 클릭하여 설정을 완료합니다.

### 관련

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
