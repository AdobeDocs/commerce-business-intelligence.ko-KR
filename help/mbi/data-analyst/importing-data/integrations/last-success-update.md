---
title: 데이터베이스와 SQL 편집기 간의 결과 이해
description: 데이터베이스와 SQL 편집기 간의 결과를 이해하는 방법에 대해 알아봅니다.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# 데이터베이스 결과와 [!DNL SQL Editor]개 결과 비교

`Last successful update began` 페이지 내에 있는 `Integrations` 필드가 무엇인지 궁금하실 수 있습니다.

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## `timestamp` 필드 이해

계정에 대한 `timestamp`마지막 업데이트 주기&#x200B;_의 시작_(계정에 설정된 시간대에서)이 표시됩니다.

- 마지막 업데이트 주기 동안 동기화된 테이블에 문제가 발생한 경우 이 타임스탬프는 *업데이트되지 않음*&#x200B;입니다.
- 따라서 보고서가 새로운 데이터로 업데이트되었지만 *마지막으로 성공한 업데이트가 시작됨*&#x200B;이 여전히 지연되는 경우가 있습니다.

## &quot;실제&quot; 마지막 데이터 포인트 식별

특정 통합에 대한 최신 데이터 포인트는 각 통합의 오른쪽에 있는 `Last Data Point Received` 타임스탬프에 의해 결정됩니다. 해당 타임스탬프는 데이터베이스, API 또는 타사 통합이든 간에 Data Warehouse이 해당 소스에서 데이터 포인트를 성공적으로 받은 마지막 지점을 나타냅니다.

*특정 테이블*&#x200B;의 데이터의 최신 상태를 확인하려면 Adobe에서 계정의 가장 중요한 테이블에서 [[!DNL SQL] 을(를) 수행하는 빠른 ](../../dev-reports/sql-rpt-bldr.md)보고서`MAX(timestamp)`를 만드는 것이 좋습니다. 이 타임스탬프를 `Last Data Point`과(와) 비교하면 문제가 전체 계정에 영향을 주는지 테이블의 하위 집합에 영향을 주는지 여부를 나타냅니다. Adobe에서는 일반적으로 사용되는 3~4개의 중요한 테이블에 대해 이 작업을 수행할 것을 권장합니다.

- `MAX(timestamp)` 값이 `Last Data Point Received`보다 최신인 경우 테이블의 하위 집합이 영향을 받았지만 전체 계정의 업데이트 주기는 안정적입니다.
- `MAX(timestamp)` 값이 `Last Data Point Received`과(와) 같거나 그 이전인 경우 계정의 업데이트 주기가 영향을 받았음을 의미합니다. 이 경우 [지원 티켓을 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ko)하십시오.
