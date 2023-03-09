---
title: 데이터베이스와 SQL 편집기 간의 결과 이해
description: 데이터베이스와 SQL 편집기 간의 결과를 이해하는 방법에 대해 알아봅니다.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# 데이터베이스 결과와 `SQL Editor` 결과

다음 내용이 궁금하실 수 있습니다. `Last successful update began` 필드는 내 안에 있습니다. `Integrations` 페이지:

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## 이해 `timestamp` 필드

시작이 표시됩니다. `timestamp` (계정에 설정된 시간대에) _마지막으로 성공한 업데이트 주기_ 계정에서.

- 마지막 업데이트 주기 동안 동기화된 테이블에 문제가 발생한 경우 이 타임스탬프는 다음과 같습니다. *업데이트되지 않음*.
- 따라서 보고서가 새로운 데이터로 업데이트된 경우가 있을 수 있지만 *마지막으로 성공한 업데이트가 시작됨* 아직 늦어지고 있습니다.

## &quot;실제&quot; 마지막 데이터 포인트 식별

특정 통합에 대한 최신 데이터 포인트는 다음을 통해 결정됩니다. `Last Data Point Received` `timestamp` 각 통합의 오른쪽에 있습니다. 해당 타임스탬프는 Data Warehouse이 데이터베이스, API 또는 서드파티 통합이든 간에 해당 소스에서 데이터 포인트를 성공적으로 받은 마지막 지점을 나타냅니다.

에서 데이터의 최신 상태를 확인하려면 *특정 테이블*, Adobe은 빠른 만들기를 권장합니다 [SQL 보고서](../../dev-reports/sql-rpt-bldr.md) 다음을 수행합니다. `MAX(timestamp)` 계정에서 가장 중요한 테이블에. 이 타임스탬프를 와 비교 중 `Last Data Point` 문제가 전체 계정에 영향을 주는지 테이블의 하위 집합에 영향을 주는지 여부를 나타냅니다. Adobe 일반적으로 사용되는 3~4개의 중요한 테이블에 대해 이 작업을 수행하는 것이 좋습니다.

- 다음과 같은 경우 `MAX(timestamp)` 값이 다음보다 최신입니다. `Last Data Point Received`즉, 테이블의 하위 집합이 영향을 받았지만 전체 계정의 업데이트 주기는 안정적입니다.
- 다음과 같은 경우 `MAX(timestamp)` 값은 다음 또는 이전과 같습니다. `Last Data Point Received`즉, 계정의 업데이트 주기가 영향을 받았습니다. 이런 상황에서는 [지원 티켓 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
