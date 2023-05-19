---
title: 직접 연결을 통해 MySQL 연결
description: 연결 방법 알아보기 [!DNL MongoDB] 직접 연결을 통해.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 연결 [!DNL MySQL] 직접 연결

## 이 항목에서

* [에 대한 액세스 허용 [!DNL Commerce Intelligence] IP 주소](#allowlist)
* [만들기 [!DNL MySQL] 사용자 [!DNL Commerce Intelligence]](#steptwo)
* [에 연결 정보 입력 [!DNL Commerce Intelligence]](#stepthree)

## 이동

* [[!DNL MySQL] 경유 ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] 경유 [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] 다음을 사용하도록 권장합니다. [SSH](../integrations/mysql-via-ssh-tunnel.md) 또는 데이터를 보호하기 위한 다른 형태의 암호화! 옵션이 아닌 경우 직접 연결할 수 있습니다 [!DNL Commerce Intelligence] 이 항목의 지침을 사용하여 데이터베이스에 연결합니다.

이 항목에서는 을(를) 직접 연결하는 방법을 설명합니다. [!DNL MySQL] 데이터베이스 대상 [!DNL Commerce Intelligence]. 이러한 설정은 과 함께 사용할 수도 있습니다. [!DNL Adobe Commerce] 또는 MySQL을 사용하는 다른 전자 상거래 데이터베이스.

## 에 대한 액세스 허용 [!DNL Commerce Intelligence] IP 주소 {#allowlist}

연결에 성공하려면 IP 주소에서 액세스를 허용하도록 방화벽을 구성해야 합니다. 다음과 같습니다 `54.88.76.97` 및 `34.250.211.151`, 하지만 또한 [!DNL MySQL] 자격 증명 페이지:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 만들기 [!DNL MySQL] 사용자 [!DNL Commerce Intelligence]

를 만드는 가장 간단한 방법 `MySQL` 사용자 [!DNL Commerce Intelligence] 에 로그인하면 다음 쿼리를 실행합니다 `MySQL` 포함 `GRANT` 권한. 바꾸기 `Commerce Intelligence IP Address` (으)로 [!DNL Commerce Intelligence] 주소 및 바꾸기 `secure password` 보안 암호를 사용하여 다음 작업을 수행하십시오.

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

이 사용자가 특정 데이터베이스, 테이블 또는 열의 데이터에 액세스하지 못하도록 제한하려면 `GRANT` 사용자가 허용하는 데이터에만 액세스할 수 있는 쿼리입니다.

**동일한 사용자 및 암호를 사용하여 필요한 모든 IP에 대해 GRANT 쿼리를 다시 실행하십시오.**

## Commerce Intelligence에 연결 정보 입력

마무리하려면 연결 및 사용자 정보를 입력해야 합니다. [!DNL Commerce Intelligence]. 다음을 떠나셨나요? [!DNL MySQL] 자격 증명 페이지가 열려 있습니까? 그렇지 않으면 다음으로 이동합니다. **[!UICONTROL Data** > **Connections]** 및 클릭 **[!UICONTROL Add New Data Source]**&#x200B;을(를) 클릭하고 [!DNL MySQL] 아이콘. 다음 사항을 변경하는 것을 잊지 마십시오. `Encrypted` 전환 대상 `Yes`.

이 페이지에 다음 정보를 입력하십시오. `Database Connection` 섹션:

* `Connection Nickname`: 통합 이름 입력(예: Ecommerce 스토어)
* `Username`: 의 사용자 이름 [!DNL Commerce Intelligence] [!DNL MySQL] 사용자
* `Password`: 의 암호 [!DNL Commerce Intelligence] [!DNL MySQL] 사용자
* `Port`: 서버에 있는 MySQL의 포트(`3306` (기본적으로)
* `Host`: 기본적으로 localhost입니다. 일반적으로 의 바인드 주소 값입니다. [!DNL MySQL] 서버 - 기본적으로 `127.0.0.1 (localhost)`로컬 네트워크 주소일 수도 있습니다(예: `192.168.0.1`) 또는 서버의 공용 IP 주소입니다.

   값은 다음에서 찾을 수 있습니다. `my.cnf` 파일(위치: `/etc/my.cnf`)를 나타내는 줄 아래에 `\[mysqld\]`. 해당 파일에서 바인드 주소 줄이 주석 처리되면 외부 연결 시도로부터 서버가 보호됩니다.

작업을 마치면 를 클릭합니다. **[!UICONTROL Save & Test]** 설치를 완료합니다.

## 관련 설명서

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
