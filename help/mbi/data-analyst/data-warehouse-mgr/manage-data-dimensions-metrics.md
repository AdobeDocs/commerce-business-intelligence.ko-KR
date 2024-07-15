---
title: 데이터 차원 관리
description: 차원이 무엇이며 지표를 기반으로 차트를 필터링하거나 세그먼트화하는 데 사용할 수 있는지 알아봅니다.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# 데이터 차원 관리

>[!NOTE]
>
>[관리자 권한](../../administrator/user-management/user-management.md)이 필요합니다.

차원은 해당 지표를 기반으로 차트를 필터링하거나 세그먼트화하는 데 사용할 수 있는 지표와 동일한 테이블의 필드입니다. 예를 들어, 매출 지표에는 도시, 주, 국가, 주문 상태, 쿠폰 코드 및 기타 유형의 차원이 포함될 수 있습니다.

## 여러 지표에 차원 추가

여러 지표에 한 번에 하나 이상의 차원을 추가하려면 다음을 수행하십시오.

1. **[!UICONTROL Manage Data > Metrics]**(으)로 이동합니다.

1. **[!UICONTROL Add Dimensions To Metric(s)]**&#x200B;을(를) 클릭합니다.

1. 차원을 포함하는 테이블을 선택합니다.

1. `Choose Metric(s) to Add Dimensions` 열에서 차원을 추가할 지표를 선택합니다. 선택하면 오른쪽에 `Choose Dimensions to Add` 열이 나타납니다. 선택한 지표에 추가할 차원을 확인합니다.

   ![](../../assets/Add_Dimensions.png)

1. 보고서의 데이터 차원을 세그먼트화하거나 그룹화하려면 _그룹화 가능_&#x200B;을 표시해야 합니다.

1. **[!UICONTROL Add]**&#x200B;을(를) 클릭합니다.

## 여러 지표에서 차원 삭제

여러 지표에서 하나 이상의 차원을 삭제하려면 다음을 수행하십시오.

1. **[!UICONTROL Data > Metrics]**(으)로 이동합니다.

1. **[!UICONTROL Remove Dimensions From Metric(s)]**&#x200B;을(를) 클릭합니다.

1. 차원을 포함하는 테이블을 선택합니다.

1. 왼쪽에서 차원을 제거할 지표를 선택하고 오른쪽에서 제거할 차원을 선택합니다.

1. **[!UICONTROL Remove]**&#x200B;을(를) 클릭합니다.

1. 차원이 보고서에서 사용 중인 경우 차원을 사용 중인 차트 목록과 함께 경고가 표시됩니다. **[!UICONTROL Delete]**&#x200B;을(를) 클릭하여 보고서를 포함하여 선택한 차원과 모든 종속 항목을 삭제합니다.

## 지표의 차원 관리

**지표에 차원을 추가하려면:**

1. **[!UICONTROL Data > Metrics]**(으)로 이동합니다.

1. 새 차원이 필요한 지표에서 **[!UICONTROL Edit]**&#x200B;을(를) 클릭합니다.

1. `Dimensions` 섹션에서 `Add a dimension` 드롭다운을 사용하여 추가할 차원을 선택합니다.

>[!NOTE]
>
>필터링하거나 그룹화할 모든 차원은 [!DNL Commerce Intelligence]에서 이미 추적되어 있어야 합니다. 원하는 차원을 찾지 못한 경우 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) 페이지를 통해 데이터베이스에서 새 데이터 열 추적을 시작해야 할 수 있습니다.


**지표에서 차원을 삭제하려면:**

1. **[!UICONTROL Manage Data > Metrics]**(으)로 이동합니다.

1. 새 차원이 필요한 지표에서 **[!UICONTROL Edit]**&#x200B;을(를) 클릭합니다.

1. `Dimensions` 섹션 아래에서 제거하려는 차원 옆에 있는 삭제 열의 확인란을 선택합니다.

>[!NOTE]
>
>차원을 삭제한 후에도 Data Warehouse의 테이블에 열로 존재합니다. 모든 지표에 다시 추가하고 이러한 차원을 사용하여 새 지표를 작성할 수 있습니다. [!DNL Commerce Intelligence]에서 차원에 해당하는 데이터 열을 제거하려면 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) 페이지를 통해 데이터 열의 추적을 해제하면 됩니다.

## 관련 설명서

* [세분화 및 필터링 우수 사례](../../best-practices/segment-filter.md)
