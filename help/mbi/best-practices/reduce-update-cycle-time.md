---
title: 업데이트 주기 단축
description: 업데이트 주기 시간을 줄이는 방법에 대해 알아봅니다.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# 업데이트 주기 처리 시간 단축

[!DNL Adobe Commerce Intelligence]은(는) 하루 종일 데이터베이스와 동기화하여 새 데이터를 복제하므로 대시보드에 항상 최신 정보가 표시되도록 합니다.

많은 요인으로 인해 이미 긴 업데이트 시간이 추가될 수 있습니다. 특정 복제 방법, 더 높은 재확인 빈도, 대시보드 및 차트 수는 소수의 기여자에 불과합니다. 이 항목에서는 업데이트 시간을 줄이기 위한 몇 가지 모범 사례에 대해 설명합니다.

## 재검사 빈도 감소

데이터베이스 테이블에는 변경 가능한 값이 있는 데이터 열이 있을 수 있습니다. 예를 들어 **orders** 테이블에 **status**(이)라는 열이 있을 수 있습니다. 주문이 데이터베이스에 처음 기록되면 상태 열에 값 `pending`이(가) 포함될 수 있습니다. 이 `pending` 값으로 [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md)에서 순서가 복제됩니다.

변경 가능한 열은 시간이 지남에 따라 [업데이트된 값에 대해 다시 확인](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md)해야 합니다. 기본적으로 [!DNL Commerce Intelligence]은(는) 업데이트할 때마다 이러한 열을 다시 확인하지만, 다시 확인하고 복제해야 할 데이터가 많은 경우 업데이트 시간에 부정적인 영향을 줄 수 있습니다. Adobe은 업데이트할 때마다 다시 검사를 실행하는 대신 재검사 빈도를 매일, 매주 또는 매월 설정하는 것이 좋습니다.

## 증분 복제 방법 사용

위에서 언급했듯이 긴 업데이트 시간은 다시 확인하고 복제해야 하는 데이터의 양과 직접적인 관련이 있습니다. [증분 복제 방법](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md)을 사용하면 업데이트 주기 동안 처리되는 데이터의 양을 크게 줄일 수 있습니다. Adobe 가능한 경우 이러한 방법을 사용하거나 증분 방법을 지원하도록 데이터베이스를 수정하는 것이 좋습니다.

## 대시보드에서 사용되지 않은 차트 제거

업데이트 주기가 끝날 때 [!DNL Commerce Intelligence]은(는) 모든 차트에 대해 캐시 작업을 수행합니다. 캐시는 데이터를 저장하므로 향후 정보 요청을 더 빨리 완료할 수 있습니다. [!DNL Commerce Intelligence]에서 차트는 로드할 때마다 데이터를 쿼리할 필요가 없으므로 대시보드가 빠르게 로드됩니다.

[!DNL Commerce Intelligence]은(는) 대시보드에 있는 차트에 대해서만 캐시 작업을 수행하기 때문에 사용하지 않는 차트를 대시보드에서 제거하면 업데이트 시간이 줄어듭니다. 동일한 차트가 여러 대시보드에 있을 수 있다는 점을 유의하십시오. 팀에 문의하여 사용하지 않는 차트도 제거했는지 확인하십시오.

>[!NOTE]
>
>대시보드에서 차트를 제거해도 차트가 삭제되지 않습니다. 언제든지 [다시 추가할 수 있습니다](../data-user/dashboards/add-charts-dashboard.md).

## 분석을 위해 데이터베이스 최적화

빈도, 복제 방법 및 차트 유용성을 다시 확인하는 것 외에도 [분석을 위해 데이터베이스를 최적화](../best-practices/opt-db-analysis.md)할 수 있습니다.

## 요약

이러한 권장 사항을 구현한 후에도 업데이트 시간이 느린 것 같으면 [지원 팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ko)하십시오.
