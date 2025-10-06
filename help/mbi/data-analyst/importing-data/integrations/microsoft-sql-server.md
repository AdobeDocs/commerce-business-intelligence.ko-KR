---
title: Microsoft SQL Server 연결
description: 4단계 프로세스를 통해 Microsoft SQL 데이터베이스를  [!DNL Commerce Intelligence] 에 연결하는 방법을 알아봅니다.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# [!DNL Microsoft SQL] 서버 연결

>[!NOTE]
>
>[관리자 권한](../../../administrator/user-management/user-management.md)이 필요합니다.

![Microsoft SQL Server 로고](../../../assets/MicrosoftSQLServer-logo.png)

이 항목에서는 4단계 프로세스를 통해 [!DNL Microsoft SQL] 데이터베이스를 [!DNL Commerce Intelligence]에 연결하는 방법을 설명합니다. 이 프로세스에는 서버 연결 및 SQL과 관련된 기술 전문 지식이 필요하며 팀의 개발자로부터 지원이 필요할 수 있습니다.

[!DNL Commerce Intelligence]은(는) [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure] 및 대부분의 다른 클라우드 서버 공급자를 지원합니다. 특정 호스트에 대한 질문이 있는 경우 [지원 티켓을 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ko)하여 이 정보를 제공하십시오.

시스템에서 데이터베이스에서 SELECT 쿼리를 실행해야 합니다. 이 작업은 처음에 데이터베이스 구조의 스냅샷을 가져온 다음 정기적으로 초과 작업을 수행하여 데이터를 최신 상태로 유지합니다. 업데이트는 증분 단위이며 Adobe은 서버에서 원하지 않는 로드를 방지하기 위해 업데이트 빈도와 시간을 제한합니다.

가장 좋은 방법은 TCP/IP를 통해 데이터베이스 서버에 연결하는 것입니다. SELECT 쿼리만 실행할 수 있는 사용자(및 선택적으로 지정한 테이블에서 데이터만 선택할 수 있음)를 만듭니다. [!DNL Commerce Intelligence]에 연결하는 각 서버에 대해 이 작업을 수행해야 합니다.

## `Microsoft SQL`에 [!DNL Commerce Intelligence] 연결 중:

1. 서버가 TCP/IP를 통한 연결 및 혼합 모드 인증을 허용하는지 확인하십시오.

1. 방화벽에서 서버의 전용 IP에 연결할 수 있는지 확인하십시오.

   `Settings` 페이지의 연결 섹션에서 서버에 연결하는 데 사용되는 IP 주소를 찾을 수 있습니다.

1. 데이터베이스 서버에 로그인하는 데 사용할 사용자를 만듭니다. `UI` 또는 `query`을(를) 통해 두 가지 옵션이 있습니다.
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user)&#x200B;(두 번째 예)

1. [!DNL Commerce Intelligence]의 **[!UICONTROL Manage Data** > **Connections]**&#x200B;에 서버 IP 주소, 사용자 이름 및 암호를 입력하십시오.

   ![데이터베이스 통합을 표시하는 데이터 연결 관리 페이지](../../../assets/manage-data-connections.png)

1. **[!UICONTROL Add a Data Source]**&#x200B;을(를) 클릭합니다.

1. `Microsoft SQL` 데이터베이스에 연결하고 새 `Connections` 페이지의 필드에 자격 증명을 입력하려면 선택하십시오.

   `Windows Azure`을(를) 사용하는 경우 데이터베이스 이름도 지정해야 합니다.
