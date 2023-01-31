---
title: Campaign 패널을 통해 MySQL 연결
description: Campaign 패널을 통해 MySQL을 연결하는 방법을 알아봅니다.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Campaign 패널을 통해 MySQL 연결

* [만들기 [!DNL MBI] Campaign 패널의 MySQL 사용자](#cpanel)
* [MBI에 연결 및 사용자 정보 입력](#finish)

## 이동

* [SSH 터널을 통한 MySQL](../integrations/mysql-via-ssh-tunnel.md)
* [직접 연결을 통한 MySQL](../integrations/mysql-via-a-direct-connection.md)

* **`MySQL via cPanel`**

>[!IMPORTANT]
>
>데이터를 보호하기 위해 SSH 또는 기타 암호화 형식을 사용하는 것이 좋습니다. 이 옵션을 선택하지 않으면 직접 연결할 수 있습니다 [!DNL MBI] 참조하십시오.

이 문서에서는 MySQL 데이터베이스를 [!DNL MBI] &quot;패널&quot;을 사용 중입니다. 이 프로세스를 사용하여 연결할 수도 있습니다 [!DNL Magento] 및 기타 모든 MySQL 기반 eCommerce 데이터베이스를 [!DNL MBI].

1. 만들기 [!DNL MBI] 의 MySQL 사용자 `cPanel`
1. 연결 및 사용자 정보를에 입력합니다. [!DNL MBI]

시작.

## 만들기 [!DNL MBI] 의 MySQL 사용자 `cPanel` {#cpanel}

1. 에 로그인합니다. [`cPanel`](../../../data-analyst/importing-data/integrations/mysql-via-cpanel.md) 호스팅 공급자를 통해 제공됩니다.
1. 클릭 **[!UICONTROL MySQL Databases]**&#x200B;에 위치 `Database` 섹션을 참조하십시오.
1. 아래로 스크롤하여 `Add New User` 섹션 및 사용자 만들기 [!DNL MBI]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. 클릭 **[!UICONTROL Create User]**.
1. 사용자를 만들었으므로 이제 사용자를 데이터베이스에 연결해야 합니다. 로 돌아갑니다. `Add New User` 섹션 - 설정 참조 `Add User to Database?` 그게 우리가 필요한 거야
1. 에서 `User` 이 섹션의 드롭다운에서 생성한 사용자를 선택합니다.
1. 에서 `Database` 이 섹션의 드롭다운에서 연결할 데이터베이스를 선택합니다 [!DNL MBI].
1. 클릭 **[!UICONTROL Add]**.
1. 권한 검사 목록이 나타나면 옆에 있는 상자를 선택합니다 `SELECT` - 이 모든 것 [!DNL MBI] 데이터베이스에 연결해야 합니다.

## 연결 및 사용자 정보를 [!DNL MBI] {#finish}

요약하려면 연결 및 사용자 정보를 [!DNL MBI]. MySQL 인증서 페이지를 열어 두었습니까? 그렇지 않으면 로 이동합니다. **[!UICONTROL Manage Data** > **Connections]** 을(를) 클릭합니다. **[!UICONTROL Add New Data Source]**&#x200B;를 가리킨 다음 MySQL 아이콘을 클릭합니다.

다음 정보를 `Database Connection` 섹션:

* `Username`: 사용자 이름 [!DNL MBI] MySQL 사용자
* `Password`: 의 암호 [!DNL MBI] MySQL 사용자
* `Port`: 서버의 MySQL 포트(`3306` 기본적으로)
* `Host`: 의 공개 주소입니다 `MySQL` server [!DNL MBI] 에 연결됩니다. 일반적으로 로그인하는 데 사용하는 URL입니다 `cPanel`.

를 사용하는 경우 [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)암호화 정보를 입력해야 합니다. 설정 `Encrypted` 전환 `Yes` 를 클릭하여 폼을 표시합니다.

* `Connection Type`: 을(를) (으)로 설정합니다. `SSH Tunnel`
* `Remote Address`: 서버의 IP 주소 또는 호스트 이름 [!DNL MBI] 터널로
* `Username`: 사용자 이름 [!DNL MBI] `SSH (Linux)` user. [지침](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) 아직 수행하지 않았다면 다음을 수행합니다.
* `SSH Port`: 서버의 SSH 포트(`22` 기본적으로)

바로 그거야! 완료되면 를 클릭합니다 **[!UICONTROL Save & Test]** 를 클릭하여 설정을 완료합니다.

## 관련:

* [통합 재인증](https://support.magento.com/hc/en-us/articles/360016733151)
