---
title: Connect [!DNL MongoDB] SSH 터널 사용
description: 연결 방법 알아보기 [!DNL MongoDB] SSH 터널을 통해
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Connect [!DNL MongoDB] SSH 터널 사용


연결 [!DNL MongoDB] 데이터베이스 대상 [!DNL MBI] SSH 터널을 통해 귀하(또는 기술자가 아닌 경우 사용자)는 다음과 같은 몇 가지 작업을 수행해야 합니다.

1. [검색 [!DNL MBI] 공개 키](#retrieve)
1. [에 대한 액세스 허용 [!DNL MBI] IP 주소](#allowlist)
1. [MBI용 Linux 사용자 만들기](#linux)
1. [만들기 [!DNL MongoDB] MBI용 사용자](#mongodb)
1. [연결 및 사용자 정보를에 입력합니다. [!DNL MBI]](#finish)

>[!NOTE]
>
>이 설정의 기술적 특성으로 인해 이전에 이 작업을 수행하지 않았다면 개발자로부터 도움을 받는 것이 좋습니다.

## 검색 [!DNL MBI] 공개 키 {#retrieve}

다음 `public key` 는 를 승인하는 데 사용됩니다 [!DNL MBI] `Linux` 사용자. 다음 섹션에서는 사용자를 만들고 키를 가져옵니다.

1. 이동 **[!UICONTROL Data** > **Connections]** 을(를) 클릭합니다. **[!UICONTROL Add New Data Source]**.
1. 을(를) 클릭합니다. [!DNL MONGODB] 아이콘.
1. 다음 이후 [!DNL MongoDB] 자격 증명 페이지가 열립니다. `Encrypted` 전환 `Yes`. SSH 설정 양식이 표시됩니다.
1. 다음 `public key` 는 이 양식 아래에 있습니다.

이 페이지를 자습서 전체에서 열어 둡니다. 이 페이지는 다음 섹션과 끝에 필요합니다.

약간 유실되면, 여기 탐색 방법이 있습니다 [!DNL MBI] 키를 검색하려면 다음을 수행하십시오.

![RJMetrics 공개 키 검색](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## 에 대한 액세스 허용 [!DNL MBI] IP 주소 {#allowlist}

연결에 성공하려면 IP 주소에서 액세스할 수 있도록 방화벽을 구성해야 합니다. 그렇습니다 `54.88.76.97` 및 `34.250.211.151`하지만, 또한 [!DNL MongoDB] 자격 증명 페이지:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 만들기 `Linux` 사용자 [!DNL MBI] {#linux}

>[!IMPORTANT]
>
>만약 `sshd_config` 서버와 연결된 파일이 기본 옵션으로 설정되어 있지 않고 특정 사용자만 서버 액세스 권한이 있습니다. 이렇게 하면 에 성공적으로 연결할 수 없습니다 [!DNL MBI]. 이러한 경우 다음과 같은 명령을 실행해야 합니다 `AllowUsers` 허용 `rjmetric` 서버에 대한 사용자 액세스 권한.

실시간(또는 자주 업데이트되는) 데이터가 포함된 경우 프로덕션 또는 보조 시스템일 수 있습니다. 이 사용자는에 연결할 권한이 있는 한 원하는 방식으로 제한할 수 있습니다 [!DNL MongoDB] server.

새 사용자를 추가하려면 다음 명령을 `Linux` server:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

다음 사항을 기억하십시오 `public key` 첫 번째 섹션에서 검색했습니까? 사용자가 데이터베이스에 액세스할 수 있도록 하려면 키를 `authorized_keys`. 전체 키를 `authorized_keys` 파일:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

사용자 만들기를 완료하려면 SSH를 통해 액세스할 수 있도록 /home/rjmetric 디렉토리의 권한을 변경합니다.

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## 만들기 [!DNL MBI] [!DNL MongoDB] 사용자 {#mongodb}

[!DNL MongoDB] 서버는 두 가지 실행 모드를 갖습니다. [&quot;auth&quot; 옵션이 있는 옵션](#auth) `(mongod -- auth)` 한 명 없이 [기본값은 입니다.](#default). 만들기 단계 [!DNL MongoDB] 사용자는 서버의 사용 모드에 따라 약간 다르므로 계속하기 전에 모드를 확인하십시오.

### 서버에서 `Auth` 옵션: {#auth}

여러 데이터베이스에 연결할 때 로그인하여 사용자를 추가할 수 있습니다 [!DNL MongoDB] 관리자 권한으로 다음 명령을 실행합니다.

>[!NOTE]
>
>사용 가능한 모든 데이터베이스를 보려면 [!DNL MBI] 사용자에게 실행할 권한이 필요합니다. `listDatabases.`

이 명령은 [!DNL MBI] 사용자 액세스 `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

이 명령을 사용하여 [!DNL MBI] 사용자 액세스 `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

이렇게 하면 다음과 같은 응답이 인쇄됩니다.

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### 서버에서 기본 옵션을 사용하는 경우 {#default}

서버가 `auth` 모드, [!DNL MongoDB] 사용자 이름과 암호가 없어도 서버에 액세스할 수 있습니다. 그러나 다음을 확인해야 합니다 `mongodb.conf` 파일 `(/etc/mongodb.conf)` 에는 다음 줄이 있습니다. 그렇지 않으면 서버를 추가한 후 서버를 다시 시작합니다.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

를 바인딩하려면 [!DNL MongoDB] 서버가 다른 주소로 이동하여 다음 단계의 데이터베이스 호스트 이름을 적절히 조정합니다.

## 연결 및 사용자 정보를 [!DNL MBI] {#finish}

요약하려면 연결 및 사용자 정보를 [!DNL MBI]. 여기 나가셨어요? [!DNL MongoDB] 자격 증명 페이지가 열려 있습니까? 그렇지 않으면 로 이동합니다. **[!UICONTROL Data > Connections]** 을(를) 클릭합니다. **[!UICONTROL Add New Data Source]**, 그런 다음 [!DNL MongoDB] 아이콘. 변경 사항을 잊지 마십시오 `Encrypted` 전환 `Yes`.

다음 정보를 이 페이지에 입력하고 `Database Connection` 섹션:

* `Host`: `127.0.0.1`
* `Username`: 다음 [!DNL MBI] [!DNL MongoDB] 사용자 이름 (반드시 `rjmetric`)
* `Password`: 다음 [!DNL MBI] [!DNL MongoDB] 암호
* `Port`: 서버에 있는 MongoDB의 포트(`27017` 기본적으로)
* `Database Name` (선택 사항): 하나의 데이터베이스에만 액세스를 허용하는 경우 여기에서 해당 데이터베이스의 이름을 지정합니다.

아래에 `SSH Connection` 섹션:

* `Remote Address`: SSH를 사용할 서버의 IP 주소 또는 호스트 이름
* `Username`: 다음 [!DNL MBI] Linux(SSH) 사용자 이름(rjmetric이어야 함)
* `SSH Port`: 서버의 SSH 포트(기본적으로 22)

바로 그거야! 완료되면 를 클릭합니다 **[!UICONTROL Save Test]** 를 클릭하여 설정을 완료합니다.

### 관련

* [통합 재인증](https://support.magento.com/hc/en-us/articles/360016733151)
