---
title: 데이터 및 업데이트 정보
description: 업데이트 주기 상태를 확인하는 방법을 알아봅니다.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# 데이터 및 업데이트 정보

* [데이터가 변경된 이유는 무엇입니까?](#datachange)
* [정기 업데이트와 강제 업데이트의 차이점은 무엇입니까?](#regularforcedupdates)
* [업데이트 주기가 오래 걸리는 이유는 무엇입니까?](#updatecycletime)
* [업데이트 주기가 완료되면 알림을 받을 수 있습니까?](#notifyupdate)
* [&#x200B; [!DNL Google ECommerce] 데이터가 내 데이터베이스와 다른 이유는 무엇입니까?](#ecommdatabase)
* [데이터 불일치 문제를 해결하려면 어떻게 합니까?](#datadiscrepancy)

## 데이터가 변경된 이유는 무엇입니까? {#datachange}

새 데이터가 Data Warehouse에 동기화되어 차트 값이 하루 종일 변경될 수 있습니다. 또한 [다시 확인](../data-warehouse-mgr/cfg-data-rechecks.md)으로 인해 기존 데이터 열의 값이 변경될 수 있습니다. 다시 검사는 `open`에서 `shipped`(으)로 이동하는 주문 상태와 같이 데이터 열에서 변경된 값을 찾는 프로세스입니다.

사용자의 권한 설정에 따라 [업데이트 주기 상태를 확인](../../best-practices/check-update-cycle.md)하는 여러 가지 방법이 있습니다.

## 정기 업데이트와 강제 업데이트의 차이점은 무엇입니까? {#regularforcedupdates}

일반 업데이트는 **예약됨** 프로세스이고 강제 업데이트는 **수동 프로세스 시작**&#x200B;입니다. 일시 중단 시간(또는 [!DNL Commerce Intelligence]에서 데이터를 업데이트하지 말아야 하는 기간)이 있는 경우 강제로 업데이트를 수행하면 일시 중단 기간의 제한을 준수하지 않는 주기가 시작됩니다.

## 업데이트 주기가 오래 걸리는 이유는 무엇입니까? {#updatecycletime}

많은 요인으로 인해 이미 긴 업데이트 시간이 추가될 수 있습니다. 특정 [복제 메서드](../data-warehouse-mgr/cfg-replication-methods.md), [더 높은 재확인 빈도](../data-warehouse-mgr/cfg-data-rechecks.md) 및 대시보드 및 차트 수가 몇 가지 기여자에 불과합니다. Adobe에서는 업데이트 시간을 줄이려면 [일부 설정을 다시 구성](../../best-practices/reduce-update-cycle-time.md)하고 [분석을 위해 데이터베이스를 최적화](../../best-practices/opt-db-analysis.md)하는 것이 좋습니다.

## 업데이트 주기가 완료되면 알림을 받을 수 있습니까? {#notifyupdate}

업데이트가 진행 중인 경우 주기가 완료되면 이메일 알림을 요청하는 데 사용할 수 있는 링크가 `Connections` 페이지에 있습니다.

## [!DNL Google ECommerce]데이터가 내 데이터베이스와 다른 이유는 무엇입니까? {#ecommdatabase}

[!DNL Google Analytics]과(와) 데이터베이스 간의 불일치는 여러 가지 이유로 발생할 수 있습니다. 추적이 제대로 활성화되지 않음, 사용자가 시크릿 방문 및 클릭 이벤트가 제대로 작동하지 않는 것은 몇 가지 예에 불과합니다. 매출과 주문이 올바르게 표시되지 않으면 [이 항목을 참조](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=ko)하여 문제를 진단하십시오.

## 데이터 불일치 문제를 해결하려면 어떻게 합니까? {#datadiscrepancy}

Adobe은 일관되지 않은 데이터를 보는 것이 답답한 경험이 될 수 있다는 것을 알고 있습니다. [데이터 불일치 검사 목록](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=ko) 또는 [데이터 내보내기 자습서](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=ko)를 사용하여 문제를 진단해 보십시오. 여전히 문제가 있으면 [지원팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ko)하세요.
