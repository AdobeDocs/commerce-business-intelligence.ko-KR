---
title: cPanel을 통해 MySQL 연결
description: cPanel을 통해 MySQL을 연결하는 방법에 대해 알아봅니다.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# [!DNL MySQL]을(를) 통해 [!DNL cPanel] 연결

* [&#x200B; [!DNL Commerce Intelligence] [!DNL MySQL]에서  [!DNL cPanel] 사용자 만들기](#cpanel)
* [&#x200B; [!DNL Commerce Intelligence]에 연결 및 사용자 정보 입력](#finish)

## 이동

* [SSH 터널을 통한 [!DNL MySQL]](../integrations/mysql-via-ssh-tunnel.md)
* [직접 연결을 통한 [!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe]은(는) SSH 또는 다른 형태의 암호화를 사용하여 데이터를 보호하는 것을 권장합니다! 옵션이 아닌 경우 이 항목의 지침을 사용하여 [!DNL Commerce Intelligence]을(를) 데이터베이스에 직접 연결할 수 있습니다.

이 항목에서는 [!DNL MySQL]을(를) 사용하여 [!DNL Commerce Intelligence] 데이터베이스를 [!DNL cPanel]에 직접 연결하는 과정을 안내합니다. 이 프로세스를 사용하여 [!DNL Adobe Commerce] 및 기타 MySQL 기반 전자 상거래 데이터베이스를 [!DNL Commerce Intelligence]에 연결할 수도 있습니다.

1. [!DNL Commerce Intelligence]에서 [!DNL MySQL] [!DNL cPanel] 사용자 만들기
1. [!DNL Commerce Intelligence]에 연결 및 사용자 정보 입력

시작합니다.

## [!DNL Commerce Intelligence]에서 [!DNL MySQL] [!DNL cPanel] 사용자를 만드는 중 {#cpanel}

1. 호스팅 공급자를 통해 [!DNL cPanel]에 로그인합니다.
1. **[!UICONTROL [!DNL MySQL] Databases]** 섹션에 있는 `Database`을(를) 클릭합니다.
1. `Add New User` 섹션까지 아래로 스크롤하고 [!DNL Commerce Intelligence]에 대한 사용자를 만드십시오.

   사용자 양식 만들기를 표시하는 ![cPanel MySQL 데이터베이스 인터페이스](../../../assets/create-mbi-mysql-user-cpanel.png)

1. **[!UICONTROL Create User]**&#x200B;을(를) 클릭합니다.
1. 이제 사용자를 만들었으므로 이 사용자를 데이터베이스에 연결해야 합니다. `Add New User` 섹션으로 돌아가서 필요한 `Add User to Database?`에 대한 설정을 확인하십시오.
1. 이 섹션의 `User` 드롭다운에서 만든 사용자를 선택합니다.
1. 이 섹션의 `Database` 드롭다운에서 [!DNL Commerce Intelligence]에 연결할 데이터베이스를 선택합니다.
1. **[!UICONTROL Add]**&#x200B;을(를) 클릭합니다.
1. 권한 검사 목록이 나타나면 `SELECT` 옆의 확인란을 선택합니다. [!DNL Commerce Intelligence]에서 데이터베이스에 연결하는 데 필요한 모든 항목입니다.

## [!DNL Commerce Intelligence]에 연결 및 사용자 정보 입력 {#finish}

마무리하려면 [!DNL Commerce Intelligence]에 연결 및 사용자 정보를 입력해야 합니다. [!DNL MySQL] 자격 증명 페이지를 열어 두셨습니까? 그렇지 않으면 **[!UICONTROL Manage Data** > **Connections]**(으)로 이동하여 **[!UICONTROL Add New Data Source]**&#x200B;을(를) 클릭한 다음 [!DNL MySQL] 아이콘을 클릭합니다.

`Database Connection` 섹션의 이 페이지에 다음 정보를 입력하십시오.

* `Username`: [!DNL Commerce Intelligence] [!DNL MySQL] 사용자의 사용자 이름
* `Password`: [!DNL Commerce Intelligence] [!DNL MySQL] 사용자의 암호
* `Port`: 서버에 있는 MySQL의 포트(기본적으로 `3306`)
* `Host`: `MySQL` 서버 [!DNL Commerce Intelligence]이(가) 연결하는 공용 주소입니다. 일반적으로 `[!DNL cPanel]`에 로그인하는 데 사용하는 URL입니다.

[`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)을(를) 사용하는 경우 암호화 정보를 입력해야 합니다. 양식을 표시하려면 `Encrypted` 전환을 `Yes`(으)로 설정하십시오.

* `Connection Type`: `SSH Tunnel`(으)로 설정
* `Remote Address`: [!DNL Commerce Intelligence] 서버의 IP 주소 또는 호스트 이름이
* `Username`: [!DNL Commerce Intelligence] `SSH (Linux)` 사용자의 사용자 이름입니다. 아직 수행하지 않았다면 이 작업을 수행하는 방법에 대한 [지침](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md)을 참조하십시오.)
* `SSH Port`: 서버의 SSH 포트(기본적으로 `22`)

완료되면 **[!UICONTROL Save & Test]**&#x200B;을(를) 클릭하여 설치를 완료합니다.

## 관련 항목:

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ko)
