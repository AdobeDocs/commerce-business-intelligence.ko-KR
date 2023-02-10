---
title: 데이터베이스와 SQL 편집기 간의 결과 이해
description: 데이터베이스와 SQL 편집기 간의 결과를 이해하는 방법을 배웁니다.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 데이터베이스 결과와 `SQL Editor` 결과

궁금하실 수도 있습니다 `Last successful update began` 필드 `Integrations` 페이지:

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## 이해 `timestamp` 필드

시작이 표시됩니다 `timestamp` (계정에 설정된 시간대)에서 _마지막 성공 업데이트 주기_ 내 계정에

- 동기화된 테이블 중 마지막 업데이트 주기 동안 문제가 발생하는 경우 이 타임스탬프는 *업데이트되지 않음*.
- 따라서 보고서가 새 데이터로 업데이트되지만 *마지막으로 성공한 업데이트가 시작되었습니다.* 아직 뒤쳐져 있습니다.

## &quot;실제&quot; 마지막 데이터 포인트 식별

특정 통합에 대한 최신 데이터 포인트는 `Last Data Point Received` `timestamp` 각 통합 오른쪽에 있습니다. 해당 타임스탬프는 데이터 웨어하우스가 데이터베이스, API 또는 타사 통합이든 간에 해당 소스에서 데이터 포인트를 성공적으로 수신한 마지막 지점을 나타냅니다.

에서 데이터의 새로 고침 여부를 확인하려면 *특정 테이블*, 빠른 작업 을 수행하는 것이 좋습니다 [SQL 보고서](../../dev-reports/sql-rpt-bldr.md) 다음을 수행합니다 `MAX(timestamp)` 당신의 계좌에 있는 가장 중요한 표에. 이 타임스탬프와 `Last Data Point` 문제가 전체 계정에 영향을 주는지 또는 표의 하위 세트에 영향을 주는지를 나타냅니다. 일반적으로 사용되는 3~4개의 중요한 테이블에 대해 이 작업을 수행하는 것이 좋습니다.

- 만약 `MAX(timestamp)` 값이 보다 최근 값 `Last Data Point Received`즉, 테이블 하위 세트가 영향을 받았지만 전체 계정의 업데이트 주기는 안정적입니다.
- 만약 `MAX(timestamp)` 다음 값 또는 그 이전 `Last Data Point Received`즉, 계정의 업데이트 주기가 영향을 받았음을 의미합니다. 이런 상황에서 [지원 티켓 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
