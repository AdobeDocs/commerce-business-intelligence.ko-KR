---
title: 대시보드 전체 필터링
description: 특정 대시보드에서 모든 보고서를 일괄적으로 편집하는 방법을 알아봅니다.
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# 대시보드 전체 필터링

대시보드 전체 필터링을 사용하여 특정 대시보드에서 모든 보고서를 벌크 편집할 수 있습니다. 다른 기간 또는 다른 저장소에 대해 동일한 분석을 빠르게 볼 수 있습니다. 스토어당 이전 연도, 월 또는 주의 성과를 쉽게 비교할 수 있습니다. 또한 새로 시작한 캠페인을 수용하도록 전체 대시보드를 업데이트할 수 있습니다.

## 날짜 필터

대시보드에서 보고서 날짜 범위 또는 간격을 변경하려면 오른쪽 상단 모서리에서 달력 아이콘을 클릭합니다(![달력](../../assets/calendar-button.png)).

을 사용하여 데이터를 표시하도록 선택할 수 있습니다 `Fixed Date Range` 또는 사전 계산된 다양한 `Moving Date Ranges`:

![날짜 범위 이동](../../assets/moving_date_ranges.png)

다음 `Last Full...` 이동 범위 옵션은 가장 최근에 완전히 완료된 범위를 나타내고 `This...` 는 현재 진행 중인 범위입니다. 예를 들어 현재 6월이면 `Last Full Month` is _5월 1일 - 5월 31일_&#x200B;에 대해 `This Month` is _6월 1일 - 지금_.

직접 만들 수도 있습니다 `Custom Moving Range`\:

![사용자 지정 이동 범위](../../assets/custom-moving-range.png)

간격을 변경할 수도 있습니다. 기본 단추 선택(![시간 간격 기본](../../assets/time_interval_default.png))은 날짜 범위만 변경됨을 의미합니다.

![시간 간격](../../assets/time_interval.png)

모든 보고서를 초기 날짜 범위 및 간격으로 복원하려면 다음을 클릭합니다 **[!UICONTROL Restore Defaults]** 또는 **[!UICONTROL Cancel]**.

대시보드에 대한 날짜 필터를 지정하면 해당 대시보드에만 해당 필터가 적용됩니다. 다른 대시보드로 이동해도 적용되지 않습니다.

>[!NOTE]
>
>지금, `Cohort Reports` 및 `SQL Reports` 대시보드 수준에서 변경 사항을 적용할 때에는 포함되지 않습니다.

## 저장 필터

특정 스토어의 수행 방식을 분석하려면 오른쪽 상단 모서리에서 저장소 아이콘(![저장소 필터](../../assets/store-filter.png)). 기본적으로 `Store Filter` 가 로 설정되어 있습니다. `All Stores`- 모든 항목의 데이터를 표시합니다 [보기 저장](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) 커머스 사이트에서 사용할 수 있습니다.

>[!NOTE]
>
>저장소 필터가 전체 [!DNL MBI] 계정이 필요합니다. 대시보드에 상거래 데이터에 빌드되지 않은 보고서와 같이 필터의 영향을 받지 않는 보고서가 포함되어 있는 경우 스토어 필터가 적용되면 해당 보고서가 업데이트되지 않습니다. 다음을 수행할 수 있습니다 [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 보고서가 저장소 선택에 따라 업데이트되어야 한다고 생각되거나 계정 저장소 필터가 잘못 비활성화되었다고 생각되는 경우.

에서 저장소를 선택하는 경우 `Store Filter`을 지정하면 대시보드 간을 탐색할 때 필터가 선택 사항을 유지합니다. 선택 내용을 유지하면 선택할 때까지 선택한 저장소에 대한 데이터를 모든 위치에 볼 수 있습니다 `All Stores`.

## 공유 대시보드에 대한 필터

공유 대시보드의 경우, 한 사용자가 날짜 필터를 구성하면 대시보드에 액세스할 수 있는 다른 사용자에게 동일한 필터가 적용된 것을 보게 됩니다. 그러나 이 경우에는 저장소 필터가 적용되지 않습니다. 대시보드 소유자가 저장소 필터를 구성하고 대시보드를 공유하는 경우 구성된 저장소 필터가 다른 사용자에게 지속되지 않습니다. 사용자에게 [액세스 편집](../../data-user/dashboards/share-dashboard-with-users.md) 대시보드 필터를 조정하기 위해 를 대시보드에 추가합니다.
