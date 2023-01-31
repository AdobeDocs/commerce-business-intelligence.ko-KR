---
title: 데이터 연결
description: Data Warehouse 관리자에서 동기화할 수 있는 테이블을 검색하는 방법을 알아봅니다.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# 데이터 연결

in [!DNL MBI], 데이터 소스는 `integrations`. 후 `integration` 이(가) 성공적으로 연결되면 Data Warehouse 관리자에서 동기화할 수 있는 테이블을 찾을 수 있습니다.

통합은 `Connections` 페이지를 클릭합니다. **[!UICONTROL Manage Data** > **Connections]**. 여기에는 계정에 연결된 모든 통합, 통합 유형, 상태 목록이 표시됩니다.[!DNL Google Analytics] 및 [!DNL Data Import API] 연결에는 빈 상태 필드가 있으며 마지막으로 연결 테스트( )가 수행됩니다`Last Connection` 시작됨 열)이 수행되었습니다.

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## 통합 유형

데이터를 가져오는 방법에는 네 가지가 있습니다 [!DNL MBI]: 데이터베이스 연결, SaaS 통합 연결, 업로드 `.csv` 파일 또는 API를 사용합니다.

## 데이터베이스 통합

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL MBI] 에서는 다음과 같은 SQL 기반 및 NoSQL 데이터베이스를 지원합니다 [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md), 및 [PostgreSQL](../integrations/postgresql.md).

데이터베이스를 직접 연결할 수 있는 [!DNL MBI] 데이터베이스 자격 증명을 사용하여 SSH 터널과 같은 검증된 암호화 방법을 사용하는 것이 좋습니다. 이렇게 하면 데이터 웨어하우스로 유입되므로 데이터가 안전하게 유지되고 보안을 유지할 수 있습니다.

연결 방법 및 데이터베이스 유형에 따라 설정을 완료하는 데 일부 기술 전문 지식이 필요할 수 있습니다.

## `SaaS` 통합

![](../../../assets/SaaS_icons.jpg)

`SaaS` 통합 서비스는 다음과 같습니다 [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md), 및 [[!DNL Zendesk]](../integrations/zendesk.md). 타사 데이터는 공급업체 서버에 상주하므로 데이터베이스의 데이터로 할 수 있는 것처럼 직접 액세스할 수 없습니다.

대부분의 경우에서 통합을 설정합니다. [!DNL MBI] 계정 자격 증명을 입력하는 것만큼 쉽습니다. 일부 서비스에서는 인증을 완료하기 위해 API 키가 필요할 수 있습니다. [통합 섹션](../integrations/integrations.md) 필요한 자격 증명을 생성하는 방법에 대한 지침입니다.

## 파일 업로드

보조 소스에서 데이터 웨어하우스에 데이터를 가져오는 방법을 모르시겠습니까? [사용 `File Upload` 기능](../connecting-data/using-file-uploader.md) 는 일상적인 의사 결정 시 필요하지 않은 데이터를 가져오는 좋은 방법입니다. 서식 규칙을 따라 빠르게 업로드할 수 있습니다 `.csv` 파일을 data warehouse로 가져와 다른 데이터 소스와 결합합니다.

## [!DNL MBI] `Import API`

자체 소스 중 하나에서 데이터 검색을 자동화하는 것이 나을 경우 [!DNL MBI] `Import API`. 기본적으로 데이터베이스 또는 `SaaS` 통합, `Import API` 기능이 가장 좋습니다.

API를 사용하려면 기술적인 지식이 필요합니다. 작은 Ruby 또는 PHP 스크립트를 작성하고 유지 관리하는 데 익숙한 사람이 자격을 더 많이 갖출 것입니다.

시작하는 방법에 대해 자세히 알아보려면 `Import API`에서 를 확인하십시오. [개발자 사이트](https://developer.adobe.com/commerce/services/reporting/) 및 [api 키를 생성하는 방법](https://developer.adobe.com/commerce/services/reporting/import-api/).

## 통합 추가

통합을 추가하려면 를 클릭합니다 **[!UICONTROL Manage Data** > **Connections]** 을 클릭한 다음 **[!UICONTROL Add a New Data Source]**. 추가할 통합 아이콘을 클릭하고 도움말 문서의 지침에 따라 설정을 지정합니다.

* [통합 FAQ](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [사용 가능 ](../integrations/integrations.md)
* [테이블 통합](../../../best-practices/consolidating-your-tables.md)
* [데이터베이스에 대한 액세스 제한](../../../administrator/account-management/restrict-db-access.md)

**원하는 통합이 표시되지 않습니까?** 일부 통합을 활성화하여 계정에 표시해야 합니다. 원하는 경우(예: [!DNL Facebook] - 하지만 목록에 표시되지 않았습니다. [지원 티켓 제출](../../../guide-overview.md).

**통합에 대한 오류 상태가 표시되는 경우**, 패닉하지 않음 - 체크아웃 [문제 해결 섹션](https://support.magento.com/hc/en-us/sections/360003078151) 도움이 필요합니다.
