---
title: 공식
description: 수식 사용 방법을 알아봅니다.
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# 공식

공식은 질문에 답하기 위해 여러 지표와 수학적 논리를 결합합니다. 예를 들어, 휴가철 동안 신규 고객이 창출한 제품당 매출은 얼마나 됩니까?

![대시보드의 휴일 판매](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 1단계: 기본 보고서 만들기

1. 메뉴에서 `Report Builder`을(를) 선택합니다.

1. **[!UICONTROL Add Metric]**&#x200B;을(를) 클릭하고 보고서에 대한 첫 번째 지표를 선택합니다.

   이 예에서는 `Revenue by products ordered` 지표가 사용됩니다.

1. **[!UICONTROL Add Metric]**&#x200B;을(를) 다시 클릭하고 보고서에 대한 두 번째 지표를 선택합니다.

   이 예에서는 `New Customers` 지표가 사용됩니다.

1. 사이드바에서 **[!UICONTROL Details]**&#x200B;을(를) 클릭하여 각 지표에 대한 정보를 표시합니다.

   ![주문한 제품별 매출](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. 사이드바에서 각 지표의 이름을 클릭하여 새 브라우저 탭에서 설정 페이지를 엽니다. 아래로 스크롤하여 지표 쿼리, 필터 및 차원을 포함한 지표의 각 구성 요소를 확인합니다.

   ![지표 설정](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. 보고서로 돌아가려면 이전 브라우저 탭을 클릭합니다.

1. 차트에서 각 선의 몇 개 데이터 포인트 위로 마우스를 가져가 각 지표와 연관된 금액을 확인합니다.

## 2단계: 공식 추가

1. 사이드바 상단에서 **[!UICONTROL Add Formula]**&#x200B;을(를) 클릭합니다.

   수식 상자에는 사용 가능한 입력 `A` 및 `B`(으)로 지표가 표시되며 수식을 입력할 수 있는 입력 상자가 포함됩니다.

   다음을 수행합니다.

   * `Enter your Formula` 입력란에 `A/B`을(를) 입력하십시오.

     이는 매출을 신규 고객 수로 주문한 제품별로 나눕니다.

   * `Select format`을(를) `123Number`(으)로 설정합니다.

   * 사이드바에서 `Untitled`을(를) 수식의 이름으로 바꾸십시오.

   ![수식 설정](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. 완료되면 **[!UICONTROL Apply]**&#x200B;을(를) 클릭합니다.

   이제 보고서에 수식 `New Customer Revenue`에 대한 새 줄이 있으며 사이드바에 새 고객이 생성한 총 매출액이 표시됩니다.

   ![수식을 사용한 보고서](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## 3단계: 날짜 범위 추가

1. 오른쪽 상단의 **[!UICONTROL Date Range]**&#x200B;을(를) 클릭합니다.

1. `Fixed Date Range` 탭에서 다음을 수행합니다.

   * 달력에서 날짜 범위를 선택합니다.

     이 예제에서 휴일 기간은 `November 1`부터 `December 31`까지입니다.

   * `Select Time Interval`에서 `Day`을(를) 선택합니다.

     ![고정 날짜 범위](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * 완료되면 **[!UICONTROL Apply]**&#x200B;을(를) 클릭합니다.

   이제 보고서는 휴가철로 제한되며, 각 날의 데이터 포인트가 있습니다.

   ![고정 날짜 범위](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## 4단계: 보고서 저장

이 단계에서는 보고서를 차트 및 표로 저장합니다.

1. 페이지 상단의 `Untitled Report`을(를) 클릭하고 설명 제목을 입력합니다. 이 예제에서 보고서 제목은 `2017 Holiday Sales`입니다.

   그런 다음 다음을 수행합니다.

   * 오른쪽 상단에서 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

   * `Type`의 경우 기본 `Chart` 설정을 사용합니다.

   * 보고서를 사용할 수 있는 `Dashboard`을(를) 선택하십시오.

   * **[!UICONTROL Save to Dashboard]**&#x200B;을(를) 클릭합니다.

1. 보고서 제목을 클릭하고 이름을 변경합니다. 이 예에서는 보고서 제목이 `2017 Holiday Sales Data`(으)로 변경되었습니다.

   그런 다음 다음을 수행합니다.

   * 오른쪽 상단에서 **[!UICONTROL Save a Copy]**&#x200B;을(를) 클릭합니다.

   * `Type`을(를) `Table`(으)로 설정합니다.

   * 보고서를 사용할 수 있는 `Dashboard`을(를) 선택하십시오.

   * **[!UICONTROL Save a Copy to Dashboard]**&#x200B;을(를) 클릭합니다.

1. 대시보드에서 보고서를 보려면 다음 중 하나를 수행하십시오.

   * 페이지 맨 위에 있는 메시지에서 **[!UICONTROL Go to Dashboard]**&#x200B;을(를) 클릭합니다.

   * 메뉴에서 **[!UICONTROL Dashboards]**&#x200B;을(를) 선택합니다. 현재 대시보드의 이름을 클릭하여 목록을 표시합니다. 그런 다음 보고서가 저장된 대시보드의 이름을 클릭합니다.
