---
title: 데이터 연결
description: Data Warehouse 관리자에서 동기화에 사용할 수 있는 테이블을 검색하는 방법을 알아봅니다.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 데이터 연결

위치 [!DNL Adobe Commerce Intelligence], 데이터 소스를 호출합니다. `integrations`. 다음 이후 `integration` 이(가) 성공적으로 연결되었습니다. Data Warehouse 관리자에서 동기화에 사용할 수 있는 테이블을 검색할 수 있습니다.

통합을 추가하고 관리하는 방법: `Connections` 페이지 - 다음을 클릭하여 액세스할 수 있음 **[!UICONTROL Manage Data** > **Connections]**. 여기에서 다음을 볼 수 있습니다.

* 계정에 연결된 모든 통합 목록

* 통합 유형

* 상태([!DNL Google Analytics] 및 [!DNL Data Import API] 연결에 빈 상태 필드가 있음)

* 마지막으로 연결을 테스트한 시간(`Last Connection Started` 열)을 수행했습니다.

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## 통합 유형

데이터를 로 가져오는 방법에는 네 가지가 있습니다 [!DNL Commerce Intelligence]: 데이터베이스 연결, SaaS 통합 연결 및 업로드 `.csv` 또는 Adobe API를 사용하십시오.

## 데이터베이스 통합

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] 는 다음과 같은 SQL 기반 및 NoSQL 데이터베이스를 지원합니다. [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft](../integrations/microsoft-sql-server.md), [몽고DB](../integrations/mongodb-via-ssh-tunnel.md), 및 [PostgreSql](../integrations/postgresql.md).

데이터베이스를 직접 연결할 수 있는 동안 [!DNL Commerce Intelligence] Adobe은 데이터베이스 자격 증명을 사용하여 SSH 터널과 같은 검증된 암호화 방법을 사용할 것을 권장합니다. 이렇게 하면 데이터가 Data Warehouse에 들어갈 때 안전하고 안전하게 유지됩니다.

연결 방법 및 데이터베이스 유형에 따라 설정을 완료하는 데 일부 기술 전문 지식이 필요할 수 있습니다.

## `SaaS` 통합

![](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

`SaaS` 통합은 다음과 같은 서비스입니다. [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md), 및 [[!DNL Zendesk]](../integrations/zendesk.md). 타사 데이터는 공급업체 서버에 있으므로 데이터베이스의 데이터로 직접 액세스할 수 없습니다.

일반적으로 의 통합 설정 [!DNL Commerce Intelligence] 은 계정 자격 증명을 입력하는 것만큼 쉽습니다. 인증을 완료하려면 일부 서비스에 API 키가 필요할 수 있습니다. 다음을 확인하십시오. [통합 섹션](../integrations/integrations.md) 필요한 자격 증명을 생성하는 방법에 대한 지침이 제공됩니다.

## 파일 업로드

보조 소스에서 Data Warehouse으로 데이터를 얻는 방법을 잘 모를 수 있습니까? [사용 `File Upload` 기능](../connecting-data/using-file-uploader.md) 은 일상적인 의사 결정에 필요하지 않은 데이터를 가져오는 좋은 방법입니다. 서식 규칙에 따라 빠르게 업로드할 수 있습니다 `.csv` 파일을 Data Warehouse에 저장하고 다른 데이터 소스와 연결합니다.

## [!DNL Commerce Intelligence] `Import API`

소스 중 하나에서 데이터 검색을 자동화하려는 경우 [!DNL Commerce Intelligence] `Import API`. 기본적으로 데이터베이스나 `SaaS` 통합, `Import API` 기능이 최상의 선택입니다.

API를 사용하려면 약간의 기술 전문 지식이 필요합니다. 작은 Ruby 또는 PHP 스크립트를 작성하고 유지 관리하는 데 익숙한 사람은 적격 이상입니다.

시작하기 자세히 알아보기 `Import API`, 다음을 확인하십시오. [개발자 사이트](https://developer.adobe.com/commerce/services/reporting/) 및 [api 키를 생성하는 방법](https://developer.adobe.com/commerce/services/reporting/import-api/).

## 통합 추가

통합을 추가하려면 다음을 클릭합니다. **[!UICONTROL Manage Data** > **Connections]** 그런 다음 을 클릭합니다. **[!UICONTROL Add a New Data Source]**. 추가할 통합의 아이콘을 클릭하고 도움말 항목의 지침을 따라 설정합니다.

* [통합 FAQ](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [사용 가능 ](../integrations/integrations.md)
* [테이블 통합](../../../best-practices/consolidating-your-tables.md)
* [데이터베이스에 대한 액세스 제한](../../../administrator/account-management/restrict-db-access.md)

**원하는 통합이 표시되지 않습니까?** 일부 통합을 활성화해야 계정에 볼 수 있습니다. 다음과 같은 항목을 찾고 계신다면 [!DNL Facebook] 목록에 없는데, [지원 티켓 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

**통합에 대한 오류 상태가 표시되는 경우**, 다음을 확인하십시오. [문제 해결 섹션](https://support.magento.com/hc/en-us/sections/360003078151) 도와주세요.
