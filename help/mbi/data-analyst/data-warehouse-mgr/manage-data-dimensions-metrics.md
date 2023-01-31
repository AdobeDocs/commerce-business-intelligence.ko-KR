---
title: 데이터 차원 관리
description: 데이터 생성 방법, 새 행이 Core Commerce 중 하나에 삽입되는 정확한 원인을 알아보고, 구매 또는 상거래 데이터베이스에 기록된 계정을 만드는 등의 작업을 어떻게 수행하는지 알아봅니다.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 데이터 차원 관리

>[!NOTE]
>
>필요한 경우 [관리자 권한](../../administrator/user-management/user-management.md).

차원은 해당 지표를 기반으로 차트를 필터링하거나 세그먼트화하는 데 사용할 수 있는 지표와 동일한 테이블의 필드입니다. 예를 들어, 매출 지표에는 도시, 주, 국가, 주문 상태, 쿠폰 코드 및 기타 유형의 차원이 포함될 수 있습니다.

## 여러 지표에 차원 추가

한 번에 하나 이상의 차원을 여러 지표에 추가하려면:

1. 기본 탐색 막대에서 **[!UICONTROL Manage Data > Metrics]**.

1. 페이지 상단에서 **[!UICONTROL Add Dimensions To Metric(s)]**.

1. 차원을 포함하는 테이블을 선택합니다.

1. 에서 `Choose Metric(s) to Add Dimensions` 열에서 차원을 추가할 지표를 선택합니다. 선택하면 `Choose Dimensions to Add` 열이 오른쪽에 나타납니다. 선택한 지표에 추가할 차원을 선택합니다.

   ![](../../assets/Add_Dimensions.png)

1. 보고서의 데이터 차원별로 세그먼트화하거나 그룹화하려면 해당 차원이 아닌지 확인해야 합니다 _그룹 가능_.

1. 클릭 **[!UICONTROL Add]**.

## 여러 지표에서 차원 삭제

여러 지표에서 하나 이상의 차원을 삭제하려면

1. 기본 탐색 막대에서 **[!UICONTROL Data > Metrics]**.

1. 페이지 상단에서 **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. 차원을 포함하는 테이블을 선택합니다.

1. 왼쪽의 차원을 제거할 지표와 오른쪽에서 제거할 차원을 선택합니다.

1. 클릭 **[!UICONTROL Remove]**.

1. 보고서에서 차원을 사용 중인 경우, 해당 차원을 사용 중인 차트 목록과 경고가 표시됩니다. 클릭 **[!UICONTROL Delete]** 선택된 차원 및 보고서를 포함하여 모든 종속 항목을 삭제하려면

## 지표의 차원 관리

**지표에 차원을 추가하려면**

1. 기본 탐색 막대에서 **[!UICONTROL Data > Metrics]**.

1. 클릭 **[!UICONTROL Edit]** 지표에서 새 차원을 가져옵니다.

1. 아래에 `Dimensions` 섹션에서 `Add a dimension` 드롭다운을 클릭하여 추가할 차원을 선택합니다.

>[!NOTE]
>
>필터링하거나 그룹화할 모든 차원은 이미 추적해야 합니다 [!DNL MBI]. 원하는 차원을 찾을 수 없는 경우, [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) 페이지.


**지표에서 차원을 삭제하려면**

1. 기본 탐색 막대에서 **[!UICONTROL Manage Data > Metrics]**.

1. 클릭 **[!UICONTROL Edit]** 지표에서 새 차원을 가져옵니다.

1. 아래에 `Dimensions` 섹션에서 제거할 차원 옆에 있는 삭제 열에서 확인란을 선택합니다.

>[!NOTE]
>
>차원을 삭제한 후에도 데이터 웨어하우스에서 테이블의 열로 여전히 존재합니다. 지표를 다시 지표에 추가하고 이러한 차원을 사용하여 새 지표를 만들 수 있습니다. 데이터 열을 제거하려면 차원이 차원에 해당하는 [!DNL MBI]를 통해 데이터 열의 추적을 해제하면 됩니다 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) 페이지.

## 관련 설명서

* [세그먼테이션 및 필터링 우수 사례](../../best-practices/segment-filter.md)
