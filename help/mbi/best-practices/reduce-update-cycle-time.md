---
title: 업데이트 주기 시간 단축
description: 업데이트 주기 시간을 줄이는 방법에 대해 알아봅니다.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 업데이트 주기 처리 시간 단축

[!DNL Adobe Commerce Intelligence] 하루 종일 데이터베이스와 동기화하여 새 데이터를 복제하고 대시보드에 항상 최신 정보가 표시되도록 합니다.

많은 요인이 이미 오래 된 업데이트 시간에 추가 될 수 있습니다. 특정 복제 메서드, 다시 확인 빈도 및 대시보드 및 차트의 수는 소수의 기여자 일 뿐입니다. 이 항목에서는 업데이트 시간을 줄이는 몇 가지 모범 사례에 대해 설명 합니다.

## 재확인 빈도 감소

데이터베이스 테이블에서 변경 가능한 값이 있는 데이터 열이 있을 수 있습니다. 예를 들어 orders **테이블에서** 상태 **라는** 열이 있을 수 있습니다. 처음에 주문이 데이터베이스에 기록 되 면 상태 열에 값 `pending` 이 포함 될 수 있습니다. 이 `pending` 값을 사용 하 여 주문이 데이터 웨어하우스에서 ](../data-analyst/data-warehouse-mgr/tour-dwm.md) 복제 [ 됩니다.

변경 가능한 열은 [ 시간이 지남에 따라 업데이트 된 값 ](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 에 대해 rechecked 해야 합니다. 기본적으로 모든 업데이트 중에 이러한 열을 [!DNL Commerce Intelligence] 다시 검사 하지만 rechecked 및 복제할 데이터가 많은 경우 업데이트 시간에 부정적인 영향을 줄 수 있습니다. 모든 Adobe Systems 업데이트 중에는 재확인을 실행 하는 대신, [다시 검사 빈도를 일별, 주별 또는 월별로 설정 하는 것이 좋습니다.

## 증분 복제 메서드 사용

위에서 언급 한 대로 긴 업데이트 시간은 rechecked 하 고 복제 해야 하는 데이터의 양과 직접적인 관계가 있습니다. [증분 복제 방법](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) 는 업데이트 주기 동안 처리되는 데이터의 양을 크게 줄일 수 있습니다. Adobe 가능한 경우 이러한 방법을 사용하거나 증분 방법을 지원하도록 데이터베이스를 수정하는 것이 좋습니다.

## 대시보드에서 사용 하지 않는 차트 제거

업데이트 주기가 [!DNL Commerce Intelligence] 끝나면 모든 차트에 대해 캐시 작업을 수행 합니다. 캐시에는 나중에 정보 요청을 더 빠르게 완료할 수 있도록 데이터가 저장 됩니다. [!DNL Commerce Intelligence]이는 차트가 로드할 때마다 데이터를 쿼리할 필요가 없으므로 대시보드를 빠르게 로드 하는 것입니다.

대시보드에 있는 차트에 대해서만 캐시 작업을 수행 하므로 [!DNL Commerce Intelligence] 대시보드에서 사용 하지 않는 차트를 제거 하면 업데이트 시간이 줄어듭니다. 동일한 차트가 여러 대시보드에 있을 수 있으므로, 사용 하지 않은 차트도 제거 되었는지 확인 하려면 팀 확인 하십시오.

>[!NOTE]
>
>대시보드에서 차트를 제거 해도 차트는 삭제 되지 않습니다. 언제 든 지 ](../data-user/dashboards/add-charts-dashboard.md) 다시 추가할 수 [ 있습니다.

## 분석을 위해 데이터베이스 최적화

재 확인 빈도, 복제 방법 및 차트 유용성을 다시 평가 하는 것 외에도 [ 분석 ](../best-practices/opt-db-analysis.md) 을 위해 데이터베이스를 최적화할 수 있습니다.

## 래핑

이러한 권장 사항을 구현한 후에도 업데이트 시간이 느린 것처럼 보이는 경우 [지원 팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
