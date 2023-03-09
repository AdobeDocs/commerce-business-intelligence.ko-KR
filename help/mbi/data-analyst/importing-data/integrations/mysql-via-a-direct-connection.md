---
title: 직접 연결을 통해 MySQL 연결
description: 연결 방법 알아보기 [!DNL MongoDB] 직접 연결을 통해.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# 연결 [!DNL MongoDB] 직접 연결

## 이 문서에서

* [에 대한 액세스 허용 [!DNL MBI] IP 주소](#allowlist)
* [만들기 ](#steptwo)
* [에 연결 정보 입력 [!DNL MBI]](#stepthree)

## 이동

* [&#39;SSH 터널을 통한 MySQL&#39;](../integrations/mysql-via-ssh-tunnel.md)
* `MySQL via direct connection`
* [&#39;MySQL via cPanel&#39;](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>Adobe은 다음을 권장합니다. [SSH](../integrations/mysql-via-ssh-tunnel.md) 또는 데이터를 보호하기 위한 다른 형태의 암호화! 옵션이 아닌 경우 직접 연결할 수 있습니다 [!DNL MBI] 이 문서의 지침에 따라 데이터베이스에 복사합니다.

이 문서는에 MySQL 데이터베이스를 직접 연결하는 방법을 설명합니다. [!DNL MBI]. 이러한 설정은 Commerce 또는 MySQL을 사용하는 다른 eCommerce 데이터베이스에서도 사용할 수 있습니다.

## 에 대한 액세스 허용 [!DNL MBI] IP 주소 {#allowlist}

연결에 성공하려면 IP 주소에서 액세스를 허용하도록 방화벽을 구성해야 합니다. 다음과 같습니다 `54.88.76.97` 및 `34.250.211.151`또한 MySQL 자격 증명 페이지에도 있습니다.

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 다음에 대한 MySQL 사용자 만들기 [!DNL MBI]

를 만드는 가장 간단한 방법 `MySQL` 사용자 [!DNL MBI] 에 로그인하면 다음 쿼리를 실행합니다 `MySQL` 포함 `GRANT` 권한. 바꾸기 `MBI IP Address` (으)로 [!DNL MBI] 주소 및 바꾸기 `secure password` 보안 암호를 사용하여 다음 작업을 수행하십시오.

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

이 사용자가 특정 데이터베이스, 테이블 또는 열의 데이터에 액세스하지 못하도록 제한하려면 `GRANT` 사용자가 허용하는 데이터에만 액세스할 수 있는 쿼리입니다.

**동일한 사용자 및 암호를 사용하여 필요한 모든 IP에 대해 GRANT 쿼리를 다시 실행하십시오.**

## MBI에 연결 정보 입력

마무리하려면 연결 및 사용자 정보를 입력해야 합니다. [!DNL MBI]. MySQL 자격 증명 페이지를 열어 두셨습니까? 그렇지 않으면 다음으로 이동합니다. **[!UICONTROL Data** > **Connections]** 및 클릭 **[!UICONTROL Add New Data Source]**&#x200B;을 클릭한 다음 MySQL 아이콘을 클릭합니다. 다음 사항을 변경하는 것을 잊지 마십시오. `Encrypted` 전환 대상 `Yes`.

이 페이지에 다음 정보를 입력하십시오. `Database Connection` 섹션:

* `Connection Nickname`: 통합 이름 입력(예: Ecommerce 스토어)
* `Username`: 의 사용자 이름 [!DNL MBI] MySQL 사용자
* `Password`: 의 암호 [!DNL MBI] MySQL 사용자
* `Port`: 서버에 있는 MySQL의 포트(`3306` (기본적으로)
* `Host`: 기본적으로 localhost입니다. 일반적으로 MySQL 서버의 바인드 주소 값이며 기본값은 입니다. `127.0.0.1 (localhost)`로컬 네트워크 주소일 수도 있습니다(예: `192.168.0.1`) 또는 서버의 공용 IP 주소입니다.

   값은 다음에서 찾을 수 있습니다. `my.cnf` 파일(위치: `/etc/my.cnf`)를 나타내는 줄 아래에 `\[mysqld\]`. 해당 파일에서 바인드 주소 줄이 주석 처리되면 외부 연결 시도로부터 서버가 보호됩니다.

바로 그거야! 작업을 마치면 를 클릭합니다. **[!UICONTROL Save & Test]** 설치를 완료합니다.

## 관련 설명서

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
