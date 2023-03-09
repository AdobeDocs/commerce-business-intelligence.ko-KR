---
title: Microsoft 연결&reg;&reg; SQL Server
description: Microsoft&reg; SQL 데이터베이스를 연결하는 방법 알아보기 [!DNL MBI] 4단계 프로세스.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Microsoft® SQL Server 연결

>[!NOTE]
>
>필요 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

이 문서에서는 을(를) 연결하는 방법을 설명합니다. `Microsoft SQL` 데이터베이스 대상 [!DNL MBI] 4단계 프로세스. 이 프로세스에는 서버 연결 및 SQL과 관련된 기술 전문 지식이 필요하며 팀의 개발자로부터 지원이 필요할 수 있습니다.

MBI 지원 [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft®; SQL Azure]및 기타 대부분의 클라우드 서버 공급자입니다. 특정 진행자에 대해 궁금한 점이 있다면 [지원 티켓 제출](../../../guide-overview.md) 이 정보를 제공해 달라고 요청합니다.

시스템에서 데이터베이스에서 SELECT 쿼리를 실행해야 합니다. 이 작업은 처음에 데이터베이스 구조의 스냅샷을 가져온 다음 정기적으로 초과 작업을 수행하여 데이터를 최신 상태로 유지합니다. 업데이트는 증분 단위이며 Adobe은 서버에서 원하지 않는 로드를 방지하기 위해 업데이트 빈도와 시간을 제한합니다.

가장 좋은 방법은 TCP/IP를 통해 데이터베이스 서버에 연결하는 것입니다. SELECT 쿼리만 실행할 수 있는 사용자(및 선택적으로 지정한 테이블에서 데이터만 선택할 수 있음)를 만듭니다. 이 작업은 연결 중인 각 서버에 대해 수행해야 합니다 [!DNL MBI].

## 연결 중 `Microsoft SQL` 끝 [!DNL MBI]:

1. 서버가 TCP/IP를 통한 연결 및 혼합 모드 인증을 허용하는지 확인하십시오.

1. 방화벽에서 서버의 전용 IP에 연결할 수 있는지 확인하십시오.

   의 연결 섹션에서 서버에 연결하는 데 사용되는 IP 주소를 찾을 수 있습니다. `Settings` 페이지를 가리키도록 업데이트하는 중입니다.

1. 데이터베이스 서버에 로그인하는 데 사용할 사용자를 만듭니다. 다음 두 가지 옵션이 있습니다. `UI` 또는 를 통해 `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (두 번째 예)

1. 서버 IP 주소, 사용자 이름 및 암호 입력 [!DNL MBI] 아래에 **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. 클릭 **[!UICONTROL Add a Data Source]**.

1. 다음을 연결하려면 선택하십시오. `Microsoft SQL` 데이터베이스 및 새 데이터베이스의 필드에 자격 증명을 입력합니다 `Connections` 페이지를 가리키도록 업데이트하는 중입니다.

   을 사용하는 경우 `Windows Azure`데이터베이스 이름도 지정해야 합니다.
