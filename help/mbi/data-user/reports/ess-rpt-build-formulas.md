---
title: 공식
description: 수식 사용 방법을 알아봅니다.
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
source-git-commit: df81d2b036d00cd53274ec1ae22031dbf06cc948
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 공식

공식은 질문에 답하기 위해 여러 지표와 수학적 논리를 결합합니다. 예를 들어, 휴가철 동안 신규 고객이 창출한 제품당 매출은 얼마나 됩니까?

![대시보드의 휴일 판매](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 1단계: 기본 보고서 만들기

1. 메뉴에서 다음을 선택합니다. `Report Builder`.

1. 클릭 **[!UICONTROL Add Metric]** 보고서에 대한 첫 번째 지표를 선택합니다.

   이 예제의 경우 `Revenue by products ordered` 지표가 사용됩니다.

1. 클릭 **[!UICONTROL Add Metric]** 다시 한 번 보고서에 대한 두 번째 지표를 선택합니다.

   이 예제의 경우 `New Customers` 지표가 사용됩니다.

1. 사이드바에서 를 클릭합니다. **[!UICONTROL Details]** 각 지표에 대한 정보를 표시합니다.

   ![주문한 제품별 매출](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. 사이드바에서 각 지표의 이름을 클릭하여 새 브라우저 탭에서 설정 페이지를 엽니다. 아래로 스크롤하여 지표 쿼리, 필터 및 차원을 포함한 지표의 각 구성 요소를 확인합니다.

   ![지표 설정](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. 보고서로 돌아가려면 이전 브라우저 탭을 클릭합니다.

1. 차트에서 각 선의 몇 개 데이터 포인트 위로 마우스를 가져가 각 지표와 연관된 금액을 확인합니다.

## 2단계: 공식 추가

1. 사이드바 상단에서 를 클릭합니다. **[!UICONTROL Add Formula]**.

   공식 상자에는 지표가 사용 가능한 입력으로 표시됩니다 `A` 및 `B`에는 공식을 입력할 수 있는 입력 상자가 포함되어 있습니다.

   다음을 수행합니다.

   * 다음에서 `Enter your Formula` 입력 상자, 입력 `A/B`.

      이는 매출을 신규 고객 수로 주문한 제품별로 나눕니다.

   * 설정 `Select format` 끝 `123Number`.

   * 사이드바에서 바꾸기 `Untitled` (공식 이름 포함)

   ![공식 설정](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. 완료되면 다음을 클릭하십시오. **[!UICONTROL Apply]**.

   이제 보고서에 공식에 대한 새 라인이 있습니다. `New Customer Revenue`및 사이드바에는 신규 고객이 생성한 총 매출액이 표시됩니다.

   ![수식을 사용한 보고서](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## 3단계: 날짜 범위 추가

1. 클릭 **[!UICONTROL Date Range]** 오른쪽 상단 모서리입니다.

1. 다음에서 `Fixed Date Range` 탭에서 다음을 수행합니다.

   * 달력에서 날짜 범위를 선택합니다.

      이 예에서는 휴가철이 다음과 같습니다. `November 1` 에서 `December 31`.

   * 아래 `Select Time Interval`, 선택 `Day`.

      ![고정 날짜 범위](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * 완료되면 다음을 클릭하십시오. **[!UICONTROL Apply]**.

   이제 보고서는 휴가철로 제한되며, 각 날의 데이터 포인트가 있습니다.

   ![고정 날짜 범위](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## 4단계: 보고서 저장

이 단계에서는 보고서를 차트 및 표로 저장합니다.

1. 클릭 `Untitled Report` 페이지 맨 위에 수사적 제목을 입력합니다. 이 예제에서 보고서 제목은 다음과 같습니다. `2017 Holiday Sales`.

   그런 다음 다음을 수행합니다.

   * 오른쪽 상단에서 **[!UICONTROL Save]**.

   * 대상 `Type`, 기본값을 사용합니다. `Chart` 설정.

   * 다음을 선택합니다. `Dashboard` 보고서를 사용할 수 있는 위치입니다.

   * 클릭 **[!UICONTROL Save to Dashboard]**.

1. 보고서 제목을 클릭하고 이름을 변경합니다. 이 예의 경우 보고서 제목이 (으)로 변경됩니다. `2017 Holiday Sales Data`.

   그런 다음 다음을 수행합니다.

   * 오른쪽 위 모서리에서 을(를) 클릭합니다. **[!UICONTROL Save a Copy]**.

   * 설정 `Type` 끝 `Table`.

   * 다음을 선택합니다. `Dashboard` 보고서를 사용할 수 있는 위치입니다.

   * 클릭 **[!UICONTROL Save a Copy to Dashboard]**.

1. 대시보드에서 보고서를 보려면 다음 중 하나를 수행하십시오.

   * 클릭 **[!UICONTROL Go to Dashboard]** 을 참조하십시오.

   * 메뉴에서 다음을 선택합니다. **[!UICONTROL Dashboards]**. 현재 대시보드의 이름을 클릭하여 목록을 표시합니다. 그런 다음 보고서가 저장된 대시보드의 이름을 클릭합니다.
