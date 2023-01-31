---
title: Microsoft SQL Server 연결
description: Microsoft SQL 데이터베이스를 [!DNL MBI] 4단계 프로세스.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Microsoft SQL Server 연결

>[!NOTE]
>
>필요한 경우 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

이 문서에서는 `Microsoft SQL` 데이터베이스 대상 [!DNL MBI] 4단계 프로세스. 이 프로세스는 서버 연결 및 SQL과 관련된 몇 가지 기술 지식이 필요하며, 팀의 개발자의 지원이 필요할 수 있습니다.

Adobe 지원 [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure], 및 대부분의 다른 클라우드 서버 공급자. 특정 호스트에 대한 질문이 있으면 [지원 티켓 제출](../../../guide-overview.md) 이 정보를 제공하도록 요청하고 있습니다.

데이터베이스에서 SELECT 쿼리를 실행해야 합니다. 이 작업은 처음에 데이터베이스 구조의 스냅샷을 가져온 다음 정기적으로 연장하여 데이터를 최신 상태로 유지합니다. Adobe는 증분 업데이트이며 업데이트 빈도와 시간을 제한하여 서버에서 원치 않는 로드를 방지합니다.

가장 좋은 방법은 TCP/IP를 통해 데이터베이스 서버에 연결하는 것입니다. SELECT 질의만 실행할 수 있는 사용자를 생성합니다(또한 선택적으로 지정한 테이블에서 데이터만 선택할 수 있음). 연결할 각 서버에 대해 이 작업을 수행해야 합니다 [!DNL MBI].

## 연결 중 `Microsoft SQL` to [!DNL MBI]:

1. 서버가 TCP/IP 및 혼합 모드 인증을 통해 연결을 허용하는지 확인하십시오.

1. 방화벽이 서버의 전용 IP를 연결할 수 있도록 허용하는지 확인하십시오.

   서버에 연결하는 데 사용할 IP 주소는 사용자의 연결 섹션에서 찾을 수 있습니다 `Settings` 페이지.

1. 데이터베이스 서버에 로그인할 때 사용할 사용자를 만듭니다.  두 가지 선택 사항이 있습니다. 를 통해 `UI` 또는 `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (두 번째 예)

1. 서버 IP 주소, 사용자 이름 및 암호를 입력합니다. [!DNL MBI] 아래에 **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. 클릭 **[!UICONTROL Add a Data Source]**.

1. 연결 선택 `Microsoft SQL` 데이터베이스에 새 페이지의 필드에 자격 증명을 입력하고 `Connections` 페이지.

   사용 중인 경우 `Windows Azure`, 데이터베이스 이름도 지정해야 합니다.
