---
title: cPanel을 통해 MySQL 연결
description: cPanel을 통해 MySQL을 연결하는 방법에 대해 알아봅니다.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 1%

---

# 연결 [!DNL MySQL] 경유 [!DNL cPanel]

* [만들기 [!DNL Commerce Intelligence] [!DNL MySQL] 의 사용자 [!DNL cPanel]](#cpanel)
* [에 연결 및 사용자 정보 입력 [!DNL Commerce Intelligence]](#finish)

## 이동

* [[!DNL MySQL] SSH 터널 사용](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] 직접 연결](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] ssh 또는 다른 형태의 암호화를 사용하여 데이터를 보호하는 것이 좋습니다! 옵션이 아닌 경우 직접 연결할 수 있습니다 [!DNL Commerce Intelligence] 이 항목의 지침을 사용하여 데이터베이스에 연결합니다.

이 항목에서는 을(를) 직접 연결하는 방법을 설명합니다. [!DNL MySQL] 데이터베이스 대상 [!DNL Commerce Intelligence] 사용 [!DNL cPanel]. 이 프로세스를 사용하여 연결할 수도 있습니다. [!DNL Adobe Commerce] 및 기타 MySQL 기반 eCommerce 데이터베이스를 사용하여 [!DNL Commerce Intelligence].

1. 만들기 [!DNL Commerce Intelligence] [!DNL MySQL] 의 사용자 [!DNL cPanel]
1. 에 연결 및 사용자 정보 입력 [!DNL Commerce Intelligence]

시작.

## 만들기 [!DNL Commerce Intelligence] [!DNL MySQL] 의 사용자 [!DNL cPanel] {#cpanel}

1. 에 로그인 [!DNL cPanel] 호스팅 공급자를 통해
1. 클릭 **[!UICONTROL [!DNL MySQL] Databases]**, 위치: `Database` 섹션.
1. 아래로 스크롤하여 `Add New User` 섹션 및 사용자 만들기 [!DNL Commerce Intelligence]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. 클릭 **[!UICONTROL Create User]**.
1. 이제 사용자를 만들었으므로 이 사용자를 데이터베이스에 연결해야 합니다. 로 돌아가기 `Add New User` 섹션 - 다음에 대한 설정 참조 `Add User to Database?` 그게 네가 필요한 거야
1. 다음에서 `User` 이 섹션의 드롭다운에서 생성한 사용자를 선택합니다.
1. 다음에서 `Database` 이 섹션의 드롭다운에서 연결할 데이터베이스를 선택합니다. [!DNL Commerce Intelligence].
1. 클릭 **[!UICONTROL Add]**.
1. 권한 체크리스트가 나타나면 옆에 있는 상자를 선택합니다 `SELECT` - 이것이 전부입니다. [!DNL Commerce Intelligence] 을(를) 데이터베이스에 연결해야 합니다.

## 에 연결 및 사용자 정보 입력 [!DNL Commerce Intelligence] {#finish}

마무리하려면 연결 및 사용자 정보를 입력해야 합니다. [!DNL Commerce Intelligence]. 다음을 떠나셨나요? [!DNL MySQL] 자격 증명 페이지가 열려 있습니까? 그렇지 않으면 다음으로 이동합니다. **[!UICONTROL Manage Data** > **Connections]** 및 클릭 **[!UICONTROL Add New Data Source]**, 그런 다음 [!DNL MySQL] 아이콘.

의 이 페이지에 다음 정보를 입력합니다. `Database Connection` 섹션:

* `Username`: 의 사용자 이름 [!DNL Commerce Intelligence] [!DNL MySQL] 사용자
* `Password`: 의 암호 [!DNL Commerce Intelligence] [!DNL MySQL] 사용자
* `Port`: 서버에 있는 MySQL의 포트(`3306` (기본적으로)
* `Host`: 의 공개 주소 `MySQL` server [!DNL Commerce Intelligence] 에 연결합니다. 일반적으로 로그인하는 데 사용하는 URL입니다 `[!DNL cPanel]`.

을(를) 사용하는 경우 [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)암호화 정보를 입력해야 합니다. 설정 `Encrypted` 전환 대상 `Yes` 을 눌러 양식을 표시합니다.

* `Connection Type`: 다음으로 설정 `SSH Tunnel`
* `Remote Address`: 서버의 IP 주소 또는 호스트 이름 [!DNL Commerce Intelligence] 다음으로 터널링됨
* `Username`: 의 사용자 이름 [!DNL Commerce Intelligence] `SSH (Linux)` 사용자, 참조 [지침](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) 을(를) 수행하는 방법에 대해 설명합니다(아직 수행하지 않은 경우).
* `SSH Port`: 서버의 SSH 포트(`22` (기본적으로)

작업을 마치면 를 클릭합니다. **[!UICONTROL Save & Test]** 설치를 완료합니다.

## 관련 항목:

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
