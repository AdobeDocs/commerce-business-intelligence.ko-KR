---
title: 데이터 연결
description: Data Warehouse Manager에서 동기화에 사용할 수 있는 표를 검색하는 방법을 알아봅니다.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: d683f1362d87eee16c41ba9a8a83a9ff533b14aa
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 데이터 연결

[!DNL Adobe Commerce Intelligence]에서 데이터 원본을 `integrations`(으)로 호출합니다. `integration`이(가) 연결되면 Data Warehouse 관리자에서 동기화에 사용할 수 있는 테이블을 검색할 수 있습니다.

`Connections`을(를) 클릭하여 액세스할 수 있는 **[!UICONTROL Manage Data** > **Connections]** 페이지를 사용하여 통합을 추가하고 관리합니다. 여기에서 다음을 볼 수 있습니다.

* 계정에 연결된 모든 통합 목록

* 통합 유형

* 상태([!DNL Google Analytics] 및 [!DNL Data Import API] 연결에 빈 상태 필드가 있음)

* 연결 테스트(`Last Connection Started` 열)를 마지막으로 수행한 시간

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## 통합 유형

데이터를 [!DNL Commerce Intelligence]에 가져오는 방법에는 데이터베이스 연결, SaaS 통합 연결, `.csv` 파일 업로드 또는 Adobe API 사용 등 네 가지가 있습니다.

## 데이터베이스 통합

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence]은(는) [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md) 및 [PostgreSQL](../integrations/postgresql.md)과 같은 SQL 기반 및 NoSQL 데이터베이스를 지원합니다.

데이터베이스 자격 증명을 사용하여 데이터베이스를 [!DNL Commerce Intelligence]에 직접 연결할 수 있지만 Adobe에서는 SSH 터널과 같은 검증된 암호화 방법을 사용하는 것이 좋습니다. 이렇게 하면 Data Warehouse에 데이터가 유입될 때 데이터가 안전하게 보호됩니다.

연결 방법 및 데이터베이스 유형에 따라 설정을 완료하는 데 일부 기술 전문 지식이 필요할 수 있습니다.

## `SaaS` 통합

![지원되는 다양한 플랫폼을 보여주는 SaaS 통합 아이콘](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

`SaaS` 통합은 [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md) 및 [[!DNL Zendesk]](../integrations/zendesk.md)과(와) 같은 서비스입니다. 타사 데이터는 공급업체 서버에 있으므로 데이터베이스의 데이터로 직접 액세스할 수 없습니다.

일반적으로 [!DNL Commerce Intelligence]에서 통합을 설정하는 것은 계정 자격 증명을 입력하는 것만큼 쉽습니다. 인증을 완료하려면 일부 서비스에 API 키가 필요할 수 있습니다. 필요한 자격 증명을 생성하는 방법에 대한 지침은 [통합 섹션](../integrations/integrations.md)을 확인하십시오.

## 파일 업로드

보조 소스에서 Data Warehouse으로 데이터를 얻는 방법을 잘 모를 수 있습니까? [`File Upload` 기능 사용](../connecting-data/using-file-uploader.md)을 사용하면 일상적인 의사 결정에 필요하지 않은 데이터를 가져올 수 있습니다. 서식 규칙에 따라 `.csv`개의 파일을 Data Warehouse에 빠르게 업로드하고 다른 데이터 소스와 연결할 수 있습니다.

## [!DNL Commerce Intelligence] `Import API`

원본 중 하나에서 데이터 검색을 자동화하려는 경우 [!DNL Commerce Intelligence] `Import API`을(를) 사용할 수 있습니다. 기본적으로 데이터베이스 또는 `SaaS` 통합에 없는 경우 `Import API` 함수를 사용하는 것이 가장 좋습니다.

API를 사용하려면 약간의 기술 전문 지식이 필요합니다. 작은 Ruby 또는 PHP 스크립트를 작성하고 유지 관리하는 데 익숙한 사람은 적격 이상입니다.

`Import API` 시작하기에 대한 자세한 내용은 [개발자 사이트](https://developer.adobe.com/commerce/services/reporting/) 및 [API 키를 생성하는 방법](https://developer.adobe.com/commerce/services/reporting/import-api/)을 참조하세요.

## 통합 추가

통합을 추가하려면 **[!UICONTROL Manage Data** > **Connections]**&#x200B;을(를) 클릭한 다음 **[!UICONTROL Add a New Data Source]**&#x200B;을(를) 클릭합니다. 추가할 통합의 아이콘을 클릭하고 도움말 항목의 지침을 따라 설정합니다.

* [통합 FAQ](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [사용 가능 ](../integrations/integrations.md)
* [테이블 통합](../../../best-practices/consolidating-your-tables.md)
* [데이터베이스에 대한 액세스 제한](../../../administrator/account-management/restrict-db-access.md)

**원하는 통합이 표시되지 않습니까?** 일부 통합을 활성화해야 계정에 표시됩니다. [!DNL Facebook]과(와) 같은 항목을 찾고 있지만 나열되지 않은 경우 [지원 티켓을 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)하십시오.

**통합에 대한 오류 상태가 표시되면** [문제 해결 섹션](https://support.magento.com/hc/en-us/sections/360003078151)에서 도움말을 확인하세요.

## 업데이트 상태 모니터링(선택 사항)

소스를 연결한 후 기본 상태 검사를 자동화하여 전체 업데이트가 완료되고 있는지 확인할 수 있습니다. 개발자 설명서에서 [업데이트 주기 상태 API](https://developer.adobe.com/commerce/services/reporting/update-cycle-status-api/)를 사용하여 클라이언트에 대해 가장 최근에 완료된 업데이트 주기를 가져와서 내부 대시보드 또는 경고에 표시합니다.
