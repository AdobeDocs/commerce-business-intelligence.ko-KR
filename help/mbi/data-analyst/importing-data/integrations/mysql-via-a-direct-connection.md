---
title: 직접 연결을 통해 MySQL 연결
description: 직접 연결을 통해  [!DNL MongoDB] 을(를) 연결하는 방법에 대해 알아봅니다.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 직접 연결을 통해 [!DNL MySQL] 연결

## 이 항목에서

* [ [!DNL Commerce Intelligence] IP 주소에 대한 액세스 허용](#allowlist)
* [ [!DNL MySQL] 의  [!DNL Commerce Intelligence]사용자 만들기](#steptwo)
* [ [!DNL Commerce Intelligence]에 연결 정보 입력](#stepthree)

## 이동

* [[!DNL MySQL] 경유 ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL]을(를) 통한  [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe]에서는 데이터를 보호하기 위해 [SSH](../integrations/mysql-via-ssh-tunnel.md) 또는 다른 형태의 암호화를 사용하는 것이 좋습니다. 옵션이 아닌 경우 이 항목의 지침을 사용하여 [!DNL Commerce Intelligence]을(를) 데이터베이스에 직접 연결할 수 있습니다.

이 항목에서는 [!DNL MySQL] 데이터베이스를 [!DNL Commerce Intelligence]에 직접 연결하는 방법을 소개합니다. 이러한 설정은 [!DNL Adobe Commerce] 또는 MySQL을 사용하는 다른 전자 상거래 데이터베이스에서도 사용할 수 있습니다.

## [!DNL Commerce Intelligence] IP 주소에 대한 액세스 허용 {#allowlist}

연결에 성공하려면 IP 주소에서 액세스를 허용하도록 방화벽을 구성해야 합니다. `54.88.76.97` 및 `34.250.211.151`이지만 [!DNL MySQL] 자격 증명 페이지에도 있습니다.

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## [!DNL MySQL]에 대해 [!DNL Commerce Intelligence] 사용자 만들기

`MySQL`에 대해 [!DNL Commerce Intelligence] 사용자를 만드는 가장 간단한 방법은 `MySQL` 권한으로 `GRANT`에 로그인할 때 다음 쿼리를 실행하는 것입니다. `Commerce Intelligence IP Address`을(를) [!DNL Commerce Intelligence] IP 주소로 바꾸고 `secure password`을(를) 선택한 보안 암호로 바꿉니다.

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

이 사용자가 특정 데이터베이스, 테이블 또는 열의 데이터에 액세스하지 못하도록 제한하려면 대신 사용자가 허용하는 데이터에만 액세스를 허용하는 `GRANT` 쿼리를 실행할 수 있습니다.

**동일한 사용자 및 암호를 사용하여 필요한 모든 IP에 대한 GRANT 쿼리를 다시 실행하십시오.**

## Commerce Intelligence에서 연결 정보 입력

마무리하려면 [!DNL Commerce Intelligence]에 연결 및 사용자 정보를 입력해야 합니다. [!DNL MySQL] 자격 증명 페이지를 열어 두셨습니까? 그렇지 않으면 **[!UICONTROL Data** > **Connections]**(으)로 이동하여 **[!UICONTROL Add New Data Source]**&#x200B;을(를) 클릭한 다음 [!DNL MySQL] 아이콘을 클릭합니다. `Encrypted` 토글을 `Yes`(으)로 변경하는 것을 잊지 마십시오.

이 페이지에 `Database Connection` 섹션부터 다음 정보를 입력하십시오.

* `Connection Nickname`: 통합 이름 입력(예: Ecommerce 스토어)
* `Username`: [!DNL Commerce Intelligence] [!DNL MySQL] 사용자의 사용자 이름
* `Password`: [!DNL Commerce Intelligence] [!DNL MySQL] 사용자의 암호
* `Port`: 서버에 있는 MySQL의 포트(기본적으로 `3306`)
* `Host`: 기본적으로 localhost입니다. 일반적으로 이 값은 [!DNL MySQL] 서버에 대한 바인드 주소 값이며 기본적으로 `127.0.0.1 (localhost)`이지만 일부 로컬 네트워크 주소(예: `192.168.0.1`) 또는 서버의 공용 IP 주소일 수도 있습니다.

  이 값은 `my.cnf`을(를) 읽는 줄 아래의 `/etc/my.cnf` 파일(`\[mysqld\]`에 있음)에서 찾을 수 있습니다. 해당 파일에서 바인드 주소 줄이 주석 처리되면 외부 연결 시도로부터 서버가 보호됩니다.

완료되면 **[!UICONTROL Save & Test]**&#x200B;을(를) 클릭하여 설치를 완료합니다.

## 관련 설명서

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ko)
