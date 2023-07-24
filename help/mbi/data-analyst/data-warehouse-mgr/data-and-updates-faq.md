---
title: 데이터 및 업데이트 정보
description: 업데이트 주기 상태를 확인하는 방법을 알아봅니다.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 데이터 및 업데이트 정보

* [데이터가 변경된 이유는 무엇입니까?](#datachange)
* [정기 업데이트와 강제 업데이트의 차이점은 무엇입니까?](#regularforcedupdates)
* [업데이트 주기가 오래 걸리는 이유는 무엇입니까?](#updatecycletime)
* [업데이트 주기가 완료되면 알림을 받을 수 있습니까?](#notifyupdate)
* [이유는 다음과 같습니다 [!DNL Google ECommerce] 내 데이터베이스와 다른 데이터?](#ecommdatabase)
* [데이터 불일치 문제를 해결하려면 어떻게 합니까?](#datadiscrepancy)

## 데이터가 변경된 이유는 무엇입니까? {#datachange}

새 데이터가 Data Warehouse에 동기화되어 차트 값이 하루 종일 변경될 수 있습니다. 또한 기존 데이터 열의 값은 [재확인](../data-warehouse-mgr/cfg-data-rechecks.md). 재검사는 데이터 열에서 변경된 값(예: 다음에서 이동하는 주문 상태)을 찾는 프로세스입니다. `open` 끝 `shipped`.

몇 가지 다른 방법이 있습니다 [업데이트 주기 상태를 확인하려면](../../best-practices/check-update-cycle.md)사용자의 권한 설정에 따라 다릅니다.

## 정기 업데이트와 강제 업데이트의 차이점은 무엇입니까? {#regularforcedupdates}

정기적인 업데이트는 다음과 같습니다 **예약됨** 강제 업데이트가 있는 동안의 프로세스 **사용자가 시작한 수동 프로세스**. 일시 중단 시간(또는 [!DNL Commerce Intelligence] 가 데이터를 업데이트하지 않아야 함). 강제로 업데이트를 수행하면 일시 중단 기간의 제한을 준수하지 않는 주기가 시작됩니다.

## 업데이트 주기가 오래 걸리는 이유는 무엇입니까? {#updatecycletime}

많은 요인으로 인해 이미 긴 업데이트 시간이 추가될 수 있습니다. 확실하 [복제 메서드](../data-warehouse-mgr/cfg-replication-methods.md), [높은 재검사 빈도](../data-warehouse-mgr/cfg-data-rechecks.md), 대시보드 및 차트 수는 소수의 기여자에 불과합니다. Adobe 추천 [일부 설정 다시 구성](../../best-practices/reduce-update-cycle-time.md) 및 [분석을 위해 데이터베이스 최적화](../../best-practices/opt-db-analysis.md) 업데이트 시간을 줄이십시오.

## 업데이트 주기가 완료되면 알림을 받을 수 있습니까? {#notifyupdate}

업데이트가 진행 중이면 `Connections` 주기가 완료되면 이메일 알림을 요청하는 데 사용할 수 있는 페이지입니다.

## 이유는 다음과 같습니다[!DNL Google ECommerce]내 데이터베이스와 다른 데이터? {#ecommdatabase}

불일치 [!DNL Google Analytics] 그리고 데이터베이스는 다양한 이유로 발생할 수 있습니다. 추적이 제대로 활성화되지 않음, 사용자가 시크릿 방문 및 클릭 이벤트가 제대로 작동하지 않는 것은 몇 가지 예에 불과합니다. 매출과 주문이 제대로 표시되지 않으면, [이 항목 보기](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) 문제를 진단합니다.

## 데이터 불일치 문제를 해결하려면 어떻게 합니까? {#datadiscrepancy}

Adobe은 일관되지 않은 데이터를 보는 것이 답답한 경험이 될 수 있다는 것을 알고 있습니다. 다음을 사용해 보십시오. [데이터 불일치 검사 목록](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html) 또는 [데이터 내보내기 자습서](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html) 문제를 진단합니다. 아직 당황하셨다면, [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
