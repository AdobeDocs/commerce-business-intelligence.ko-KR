---
title: 데이터 및 업데이트 정보
description: 업데이트 주기를 확인하는 방법을 알아봅니다.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
source-git-commit: 09b6983c3e06a1f18035542dfa3b9de9ac3ceb38
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# 데이터 및 업데이트 정보

* [데이터가 변경된 이유는 무엇입니까?](#datachange)
* [정기적인 업데이트와 강제 업데이트 간의 차이점은 무엇입니까?](#regularforcedupdates)
* [업데이트 주기를 오래 걸리는 이유는 무엇입니까?](#updatecycletime)
* [업데이트 주기가 완료되면 알림을 받을 수 있습니까?](#notifyupdate)
* [이유는 무엇입니까? [!DNL Google ECommerce] 데이터와 내 데이터베이스가 다른 데이터?](#ecommdatabase)
* [데이터 불일치를 해결하려면 어떻게 해야 합니까?](#datadiscrepancy)

## 데이터가 변경된 이유는 무엇입니까? {#datachange}

데이터 웨어하우스에 동기화되는 새로운 데이터로 인해 차트 값이 하루 종일 변경될 수 있습니다. 또한 기존 데이터 열의 값은 [재검사](../data-warehouse-mgr/cfg-data-rechecks.md). 재확인은 데이터 열에서 변경된 값을 찾는 프로세스입니다. 예를 들어 다음 위치에서 이동하는 주문 상태 `open` to `shipped`.

다음과 같은 몇 가지 방법이 있습니다 [업데이트 주기 상태를 확인하려면](../../best-practices/check-update-cycle.md)보유한 사용자 권한 유형에 따라 달라집니다.

## 정기적인 업데이트와 강제 업데이트 간의 차이점은 무엇입니까? {#regularforcedupdates}

일반 업데이트는 다음과 같습니다 **예약됨** 강제 업데이트 중 프로세스 **사용자가 시작한 수동 프로세스**. 일시 중단 시간이 있거나 [!DNL MBI] 데이터를 업데이트하면 안 됩니다. 업데이트를 수행하면 일시 중단 기간의 제한을 준수하지 않는 주기가 시작됩니다.

## 업데이트 주기를 오래 걸리는 이유는 무엇입니까? {#updatecycletime}

많은 요소가 이미 오래 업데이트되는 시간을 가중시킬 수 있습니다. 특정 [복제 방법](../data-warehouse-mgr/cfg-replication-methods.md), [높은 재검사 빈도](../data-warehouse-mgr/cfg-data-rechecks.md), 그리고 대시보드 및 차트의 수는 몇 명의 기여자에 불과합니다. 추천합니다 [일부 설정 재구성](../../best-practices/reduce-update-cycle-time.md) 및 [분석을 위한 데이터베이스 최적화](../../best-practices/opt-db-analysis.md) 업데이트 시간을 단축합니다.

## 업데이트 주기가 완료되면 알림을 받을 수 있습니까? {#notifyupdate}

당연하지! 현재 업데이트가 진행 중인 경우, `Connections` 주기가 완료되면 이메일 알림을 요청하는 데 사용할 수 있는 페이지입니다.

## 이유는 무엇입니까?[!DNL Google ECommerce]데이터와 내 데이터베이스가 다른 데이터? {#ecommdatabase}

불일치 [!DNL Google Analytics] 그리고 데이터베이스는 많은 이유로 발생할 수 있습니다. 제대로 활성화되지 않은 추적에서는 Incognito를 방문하는 사용자와 작동하지 않는 클릭 이벤트가 몇 가지 예일 수 있습니다. 매출과 주문이 제대로 되지 않으면, [이 문서 사용](https://support.magento.com/hc/en-us/articles/360016505232) 문제를 진단하기 위해

## 데이터 불일치를 해결하려면 어떻게 해야 합니까? {#datadiscrepancy}

일관성 없는 데이터를 보는 것이 좌절스러운 경험이 될 수 있다는 것을 알고 있습니다. 사용 시도 [데이터 불일치 검사 목록](https://support.magento.com/hc/en-us/articles/360016731271) 또는 [데이터 내보내기 자습서](https://support.magento.com/hc/en-us/articles/360016730631) 문제를 진단하기 위해 아직 넘어지셨다면, [연락처 지원](../../guide-overview.md).
