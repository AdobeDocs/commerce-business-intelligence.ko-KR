---
title: 대시보드 전체 필터링
description: 특정 대시보드에 있는 모든 보고서를 일괄 편집하는 방법을 알아봅니다.
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 대시보드 전체 필터링

대시보드 전체 필터링을 사용하면 특정 대시보드에 있는 모든 보고서를 일괄 편집할 수 있습니다. 서로 다른 기간 동안 또는 서로 다른 스토어에 대해 동일한 분석을 빠르게 볼 수 있습니다. 점포별로 전년도, 월, 주의 실적을 쉽게 비교할 수 있다. 새로 시작한 캠페인을 수용하도록 전체 대시보드를 업데이트할 수 있습니다.

## 날짜 필터

대시보드에서 보고서의 날짜 범위 또는 간격을 변경하려면 오른쪽 위의 달력 아이콘(![달력](../../assets/calendar-button.png))을 클릭합니다.

`Fixed Date Range` 또는 미리 계산된 다양한 `Moving Date Ranges`을(를) 사용하여 데이터를 보도록 선택할 수 있습니다.

![날짜 범위 이동](../../assets/moving_date_ranges.png)

`Last Full...` 이동 범위 옵션은 가장 최근에 완전히 완료된 범위를 나타내고 `This...`은(는) 현재 진행 중인 범위입니다. 예를 들어, 지금이 6월이면 `Last Full Month`은(는) _5월 1일 - 5월 31_&#x200B;이고, `This Month`은(는) _6월 1일 - 지금_&#x200B;입니다.

또는 자신의 `Custom Moving Range`을(를) 만드십시오\:

![사용자 지정 이동 범위](../../assets/custom-moving-range.png)

간격도 변경하도록 선택합니다. 기본 단추(![시간 간격 기본값](../../assets/time_interval_default.png))를 선택하면 날짜 범위만 변경됩니다.

![시간 간격](../../assets/time_interval.png)

모든 보고서를 초기 날짜 범위 및 간격으로 복원하려면 **[!UICONTROL Restore Defaults]**&#x200B;을(를) 클릭하거나 **[!UICONTROL Cancel]**&#x200B;을(를) 클릭합니다.

대시보드에 대한 날짜 필터를 지정하는 경우 해당 필터는 해당 대시보드에만 적용됩니다. 다른 대시보드로 이동하면 적용되지 않습니다.

>[!NOTE]
>
>현재 `Cohort Reports` 및 `SQL Reports`은(는) 대시보드 수준에서 변경 내용을 적용할 때 포함되지 않습니다.

## 필터 저장

특정 스토어의 성능을 분석하려면 오른쪽 상단의 스토어 아이콘(![스토어 필터](../../assets/store-filter.png))을 클릭합니다. 기본적으로 `Store Filter`은(는) `All Stores`(으)로 설정되어 Commerce 사이트에서 사용할 수 있는 모든 [스토어 보기](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html?lang=ko)의 데이터를 표시합니다.

>[!NOTE]
>
>저장소 필터가 전체 [!DNL Commerce Intelligence] 계정에 대해 활성화되거나 비활성화됩니다. 대시보드에 필터의 영향을 받지 않는 보고서(예: [!DNL Adobe Commerce] 데이터에 작성되지 않은 보고서)가 포함되어 있는 경우 저장소 필터가 적용될 때 해당 보고서가 업데이트되지 않습니다. 저장소 선택에 따라 보고서를 업데이트해야 하거나 계정 저장소 필터가 잘못 비활성화되어 있다고 생각되는 경우 [지원 센터에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ko)할 수 있습니다.

`Store Filter`에서 스토어를 선택하면 필터가 대시보드 사이를 이동할 때 선택 내용을 유지합니다. 선택을 유지하면 `All Stores`을(를) 선택할 때까지 선택한 저장소의 데이터를 모든 곳에서 볼 수 있습니다.

## 공유 대시보드용 필터

공유 대시보드의 경우 한 사용자가 날짜 필터를 구성하면 대시보드에 대한 액세스 권한이 있는 다른 사용자에게 동일한 필터가 적용된 것으로 표시됩니다. 단, 이 경우에는 스토어 필터가 적용되지 않습니다. 대시보드 소유자가 저장소 필터를 구성하고 대시보드를 공유하는 경우 구성된 저장소 필터가 다른 사용자에게 지속되지 않습니다. 대시보드 필터를 조정하려면 사용자에게 대시보드에 대한 [편집 액세스 권한](../../data-user/dashboards/share-dashboard-with-users.md)이 있어야 합니다.
