---
title: 공식
description: 공식을 사용하는 방법을 알아봅니다.
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# 공식

수식은 여러 지표와 수학 논리를 결합하여 질문에 답합니다. 예를 들어, 휴일 시즌 동안 제품당 매출액 중 신규 고객이 생성한 양은 얼마입니까?

![대시보드의 휴일 판매](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 1단계: 기본 보고서 만들기

1. 메뉴에서 `Report Builder`.

1. 클릭 **[!UICONTROL Add Metric]** 보고서에 대한 첫 번째 지표를 선택합니다.

   이 예제에서는 `Revenue by products ordered` 지표가 사용됩니다.

1. 클릭 **[!UICONTROL Add Metric]** 다시 선택하고 보고서에 대한 두 번째 지표를 선택합니다.

   이 예제에서는 `New Customers` 지표가 사용됩니다.

1. 사이드바에서 **[!UICONTROL Details]** 각 지표에 대한 정보를 표시하기 위해

   ![주문된 제품별 매출](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. 사이드바에서 각 지표의 이름을 클릭하여 새 브라우저 탭에서 설정 페이지를 엽니다. 아래로 스크롤하여 지표 쿼리, 필터 및 차원을 포함한 지표의 각 구성 요소를 확인합니다.

   ![지표 설정](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. 보고서로 돌아가려면 이전 브라우저 탭을 클릭합니다.

1. 차트에서 각 행의 몇 개의 데이터 포인트 위로 마우스를 가져가면 각 지표와 연관된 금액이 표시됩니다.

## 2단계: 수식 추가

1. 사이드바 상단에서 **[!UICONTROL Add Formula]**.

   공식 상자는 지표를 사용 가능한 입력으로 표시합니다 `A` 및 `B`, 그리고 공식을 입력할 수 있는 입력 상자가 포함됩니다.

   다음을 수행합니다.

   * 에서 `Enter your Formul` 입력 상자, 입력 `A/B`.

      이렇게 하면 매출을 신규 고객 수로 나눈 제품별로 나누게 됩니다.

   * 설정 `Select format` to `123Number`.

   * 사이드바에서 `Untitled` 공식 이름으로 지정합니다.

   ![수식 설정](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. 완료되면 를 클릭합니다. **[!UICONTROL Apply]**.

   이제 보고서에 배합표에 대한 새 줄이 생겼고 `New Customer Revenue`및 사이드바는 새 고객이 생성한 총 매출액을 보여줍니다.

   ![배합표가 있는 보고서](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## 3단계: 날짜 범위 추가

1. 클릭 **[!UICONTROL Date Range]** 오른쪽 상단 모서리에서

1. 설정 `Fixed Date Range` 탭에서 다음을 수행합니다.

   * 달력에서 날짜 범위를 선택합니다.

      예를 들어, 휴가철은 11월 1일부터 12월 31일까지입니다.

   * 아래 `Select Time Interval`, 선택 `Day`.

      ![고정 날짜 범위](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * 완료되면 를 클릭합니다. **[!UICONTROL Apply]**.

   이제 보고서는 휴가철으로 제한되며 매일 데이터 포인트가 제공됩니다.

   ![고정 날짜 범위](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## 4단계: 보고서 저장

이 단계에서는 보고서를 차트로 저장하고 테이블로도 저장합니다.

1. 클릭 `Untitled Report` 페이지 상단에서 수사적 제목을 입력합니다. 이 예제에서 보고서 제목은 `2017 Holiday Sales`.

   그런 다음 다음을 수행합니다.

   * 오른쪽 위 모서리에서 **[!UICONTROL Save]**.

   * 대상 `Type`, 기본값을 그대로 사용합니다 `Chart` 설정

   * 을(를) 선택합니다 `Dashboard` 보고서를 사용할 수 있는 위치입니다.

   * 클릭 **[!UICONTROL Save to Dashboard]**.

1. 보고서 제목을 클릭하고 이름을 변경합니다. 이 예제에서 보고서 제목은 `2017 Holiday Sales Data`.

   그런 다음 다음을 수행합니다.

   * 오른쪽 위 모서리에서 을(를) 클릭합니다. **[!UICONTROL Save a Copy]**.

   * 설정 `Type` to `Table`.

   * 을(를) 선택합니다 `Dashboard` 보고서를 사용할 수 있는 위치입니다.

   * 클릭 **[!UICONTROL Save a Copy to Dashboard]**.

1. 대시보드에서 보고서를 보려면 다음 중 하나를 수행합니다.

   * 클릭 **[!UICONTROL Go to Dashboard]** 를 입력합니다.

   * 메뉴에서 **[!UICONTROL Dashboards]**. 목록을 표시하려면 현재 대시보드의 이름을 클릭합니다. 그런 다음 보고서를 저장한 대시보드의 이름을 클릭합니다.
