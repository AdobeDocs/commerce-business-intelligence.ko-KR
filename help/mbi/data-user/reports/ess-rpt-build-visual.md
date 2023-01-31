---
title: 시각적 Report Builder
description: Visual Report Builder 사용 방법을 알아봅니다.
exl-id: 1101f43d-e014-4df2-be21-12d90a9d8a56
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# `Visual Report Builder`

`Visual Report Builder` 사전 정의된 지표를 기반으로 빠른 보고서를 쉽게 만들 수 있도록 해줍니다. 각 지표에는 보고서에 대한 데이터 세트를 정의하는 쿼리가 포함되어 있습니다.

다음 예제에서는 간단한 보고서를 만들고, 데이터를 추가 차원으로 그룹화하고, 날짜 및 시간 간격을 설정하고, 차트 유형을 변경하고, 보고서를 대시보드에 저장하는 방법을 보여줍니다.

## 단순 보고서를 만들려면:

1. 에서 [!DNL MBI] 메뉴 아래의 **[!UICONTROL Report Builder]**.

1. 아래 `Visual Report Builder`를 클릭합니다. **[!UICONTROL Create Report]** 다음을 수행합니다.

   * 클릭 **[!UICONTROL Add Metric]**.

      사용 가능한 지표는 알파벳순 또는 테이블별로 나열할 수 있습니다.

      ![시각적 Report Builder](../../assets/magento-bi-visual-report-builder-add-metric.png)

   * 을(를) 선택합니다 [지표](../../data-user/reports/ess-manage-data-metrics.md) 보고서에 사용할 데이터 세트를 설명합니다.

      다음 `New Customers` 이 예제에 사용된 지표는 모든 고객을 계산하고 고객이 계정에 대해 등록한 날짜별로 목록을 정렬합니다. 초기 보고서에는 간단한 선 그래프 다음에 데이터 테이블이 포함됩니다.

      왼쪽의 요약에 현재 지표의 이름이 표시되고, 그 뒤에는 지표에 지정된 열 데이터에 대한 계산 결과가 표시됩니다. 이 예에서는 요약에 총 고객 수가 표시됩니다.

      ![시각적 Report Builder](../../assets/magento-bi-report-builder-untitled.png)

1. 차트에서 줄에서 각 데이터 포인트를 마우스로 가리킵니다. 각 데이터 포인트는 해당 달 동안 등록한 총 신규 고객 수를 보여줍니다.

1. 다음 지침에 따라 데이터를 그룹화하고, 날짜 범위 및 차트 유형을 변경합니다.

   **`Group By`**

   다음 `Group By` 컨트롤을 사용하면 그룹 또는 세그먼트별로 여러 차원을 추가할 수 있습니다. Dimension은 데이터를 그룹화하는 데 사용할 수 있는 테이블의 열입니다.

   * 다음 목록에서 사용 가능한 차원 중 하나를 선택합니다 `Group By` 옵션.

      이 예에서는 고객이 첫 번째 주문을 하면서 사용한 5개의 쿠폰 코드를 발견했습니다.

      ![그룹화 기준](../../assets/magento-bi-report-builder-group-by-dimensions.png)

      다음 `Group By` 세부 정보에는 고객이 사용하는 각 쿠폰이 나열됩니다. 초기 주문을 배치하는 데 사용된 쿠폰에는 확인란이 표시됩니다. 이제 차트에는 첫 번째 주문에 사용된 각 쿠폰을 나타내는 여러 색상 선이 있습니다. 범례는 각 데이터 행에 일치하도록 색상으로 구분됩니다.

   * 클릭 **[!UICONTROL Apply]** 그룹 세부 사항을 닫으려면 다음을 수행합니다.

      ![여러 Dimension](../../assets/magento-bi-report-builder-group-by-dimension-detail.png)

   * 각 줄에 있는 몇 개의 데이터 포인트를 마우스로 가리키면 첫 번째 주문을 하면서 해당 쿠폰을 사용한 개월 동안의 고객 수를 볼 수 있습니다.

   * 이제 데이터 테이블에 월별 열 및 각 쿠폰 코드에 대한 행이 포함된 추가 차원이 있습니다.

      ![테이블 데이터별 그룹](../../assets/magento-bi-report-builder-group-by-table-data.png)

   * 이동(![](../../assets/magento-bi-btn-transpose.png)) 테이블의 오른쪽 위 모서리에 있는 컨트롤을 사용하여 데이터 방향을 변경합니다.

      데이터의 축이 뒤집어지고, 이제 테이블에는 각 쿠폰 코드에 대한 열과 각 달에 대한 행이 있습니다. 이 방향을 읽기 쉽게 찾을 수 있습니다.

      ![전송 데이터](../../assets/magento-bi-report-builder-group-by-table-data-transposed.png)
   **`Date Range`**

   다음 `Date Range` 컨트롤은 현재 날짜 범위 및 시간 간격 설정을 보여주며 오른쪽의 차트 바로 위에 있습니다.

   * 을(를) 클릭합니다. `Date Range` 이 예에서 `All-Time by Month`.

      ![날짜 범위](../../assets/magento-bi-report-builder-date-range.png)

   * 다음 사항을 변경합니다.

      * 자세히 보려면 날짜 범위를 로 변경하십시오 `Last Full Quarter`.
      * 아래 `Select Time Interval`, 선택 `Week`.
      * 완료되면 를 클릭합니다. **[!UICONTROL Save]**.

      이제 보고서에는 지난 분기, 주별 데이터만 포함됩니다.

      ![주별 최근 분기 보고서](../../assets/magento-bi-report-builder-date-range-quarter-by-week-chart.png)
   **차트 유형**

   * 오른쪽 위 모서리의 컨트롤을 클릭하여 데이터에 가장 적합한 차트를 찾습니다.

      일부 차트 유형은 다차원 데이터와 호환되지 않습니다.

      |  |  |
      |-----|-----|
      | ![](../../assets/magento-bi-btn-chart-line.png) | 선 그래프 |
      | ![](../../assets/magento-bi-btn-chart-horz-bar.png) | 가로 막대형 |
      | ![](../../assets/magento-bi-btn-chart-horz-stacked-bar.png) | 가로 누적 막대 |
      | ![](../../assets/magento-bi-btn-chart-vert-bar.png) | 세로 막대 |
      | ![](../../assets/magento-bi-btn-chart-vert-stacked-bar.png) | 세로 누적 막대 |
      | ![](../../assets/magento-bi-btn-chart-pie.png) | 파이 |
      | ![](../../assets/magento-bi-btn-chart-area.png) | 영역 |
      | ![](../../assets/magento-bi-btn-chart-funnel.png) | 단계 |

      {style=&quot;table-layout:auto&quot;}




1. 보고서를 `title`를 바꿉니다. `Untitled Report` 설명적인 제목을 사용하여 페이지 맨 위에 있는 텍스트입니다.

1. 오른쪽 위 모서리에서 **[!UICONTROL Save]** 다음을 수행합니다.

   * 대상 `Type`, 기본 설정을 수락합니다. `Chart`.

   * 을(를) 선택합니다 `Dashboard` 보고서를 사용할 수 있는 위치입니다.

   * 클릭 **[!UICONTROL Save to Dashboard]**.

      ![대시보드에 저장](../../assets/magento-bi-report-builder-save-to-dashboard.png)

1. 대시보드에서 차트를 보려면 다음 중 하나를 수행합니다.

   * 클릭 **[!UICONTROL Go to Dashboard]** 를 입력합니다.

   * 메뉴에서 `Dashboards` 을 클릭하고 현재 대시보드의 이름을 클릭하여 목록을 표시합니다. 그런 다음 보고서를 저장한 대시보드의 이름을 클릭합니다.

      ![대시보드의 보고서](../../assets/magento-bi-report-builder-my-dashboard.png)
