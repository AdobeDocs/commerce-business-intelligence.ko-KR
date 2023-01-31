---
title: 직접 연결을 통해 MySQL 연결
description: 연결 방법 알아보기 [!DNL MongoDB] 직접 연결을 통해
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Connect [!DNL MongoDB] 직접 연결 사용

## 이 문서에서

* [에 대한 액세스 허용 [!DNL MBI] IP 주소](#allowlist)
* [만들기 ](#steptwo)
* [연결 정보에 을 입력합니다. [!DNL MBI]](#stepthree)

## 이동

* [&#39;SSH 터널을 통한 MySQL&#39;](../integrations/mysql-via-ssh-tunnel.md)
* `MySQL via direct connection`
* [&#39;cPanel을 통한 MySQL&#39;](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>을 사용하는 것이 좋습니다 [SSH](../integrations/mysql-via-ssh-tunnel.md) 또는 데이터를 보호하기 위해 다른 형태의 암호화가 필요합니다! 이 옵션을 선택하지 않으면 직접 연결할 수 있습니다 [!DNL MBI] 참조하십시오.

이 문서에서는 MySQL 데이터베이스를 [!DNL MBI]. 이러한 설정은 Commerce 또는 MySQL을 사용하는 다른 모든 eCommerce 데이터베이스에서도 사용할 수 있습니다.

## 에 대한 액세스 허용 [!DNL MBI] IP 주소 {#allowlist}

연결에 성공하려면 IP 주소에서 액세스할 수 있도록 방화벽을 구성해야 합니다. 그렇습니다 `54.88.76.97` 및 `34.250.211.151`그러나 MySQL 자격 증명 페이지에도 표시됩니다.

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 에 대한 MySQL 사용자 만들기 [!DNL MBI]

를 만드는 가장 간단한 방법 `MySQL` 사용자 [!DNL MBI] 은 로그인한 경우 다음 쿼리를 실행하는 것입니다 `MySQL` with `GRANT` 권한. 바꾸기 `MBI IP Address` 사용 [!DNL MBI] IP 주소 및 바꾸기 `secure password` 원하는 보안 암호 사용:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

이 사용자가 특정 데이터베이스, 테이블 또는 열의 데이터에 액세스하지 못하도록 제한하려면 대신 실행할 수 있습니다 `GRANT` 허용하는 데이터에 대해서만 액세스를 허용하는 쿼리

**동일한 사용자 및 암호를 사용하여 모든 필수 IP에 대한 GRANT 쿼리를 다시 실행합니다.**

## MBI에 연결 정보 입력

요약하려면 연결 및 사용자 정보를 [!DNL MBI]. MySQL 인증서 페이지를 열어 두었습니까? 그렇지 않으면 로 이동합니다. **[!UICONTROL Data** > **Connections]** 을(를) 클릭합니다. **[!UICONTROL Add New Data Source]**&#x200B;를 가리킨 다음 MySQL 아이콘을 클릭합니다. 을 변경하는 것을 잊지 마십시오 `Encrypted` 전환 `Yes`.

다음 정보를 이 페이지에 입력하고 `Database Connection` 섹션:

* `Connection Nickname`: 통합 이름(예: Ecommerce Store)을 입력합니다
* `Username`: 사용자 이름 [!DNL MBI] MySQL 사용자
* `Password`: 의 암호 [!DNL MBI] MySQL 사용자
* `Port`: 서버의 MySQL 포트(`3306` 기본적으로)
* `Host`: 기본적으로 localhost입니다. 일반적으로 MySQL 서버의 바인드 주소 값이며 기본값은 입니다. `127.0.0.1 (localhost)`그러나 일부 로컬 네트워크 주소(예: `192.168.0.1`) 또는 서버의 공용 IP 주소입니다.

   값은 `my.cnf` 파일(일반적으로 `/etc/my.cnf`)를 읽습니다 `\[mysqld\]`. 해당 파일에서 바인드 주소 라인을 주석 처리하면 외부 연결 시도에서 서버가 보안됩니다.

바로 그거야! 완료되면 를 클릭합니다 **[!UICONTROL Save & Test]** 를 클릭하여 설정을 완료합니다.

## 관련 설명서

* [통합 재인증](https://support.magento.com/hc/en-us/articles/360016733151)
