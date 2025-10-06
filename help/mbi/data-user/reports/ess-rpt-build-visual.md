---
title: Visual Report Builder
description: Visual Report Builder 사용 방법을 알아봅니다.
exl-id: 1101f43d-e014-4df2-be21-12d90a9d8a56
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 0%

---

# [!DNL Visual Report Builder]

[!DNL Visual Report Builder]을(를) 사용하면 사전 정의된 지표를 기반으로 빠른 보고서를 쉽게 만들 수 있습니다. 각 지표에는 보고서에 대한 데이터 세트를 정의하는 쿼리가 포함됩니다.

다음 예에서는 간단한 보고서를 생성하고, 데이터를 추가 차원으로 그룹화하고, 날짜 및 시간 간격을 설정하고, 차트 유형을 변경하고, 보고서를 대시보드에 저장하는 방법을 보여 줍니다.

## 간단한 보고서를 만들려면 다음 작업을 수행하십시오.

1. [!DNL Commerce Intelligence] 메뉴에서 **[!UICONTROL Report Builder]**&#x200B;을(를) 클릭합니다.

1. [!UICONTROL Visual Report Builder]에서 **[!UICONTROL Create Report]**&#x200B;을(를) 클릭하고 다음을 수행합니다.

   * **[!UICONTROL Add Metric]**&#x200B;을(를) 클릭합니다.

     사용 가능한 지표는 알파벳순 또는 표별로 나열할 수 있습니다.

     ![시각적 Report Builder](../../assets/magento-bi-visual-report-builder-add-metric.png)

   * 보고서에 사용할 데이터 집합을 설명하는 [지표](../../data-user/reports/ess-manage-data-metrics.md)을(를) 선택하십시오.

     이 예제에 사용된 `New Customers` 지표는 모든 고객을 계산하고 고객이 계정에 등록한 날짜별로 목록을 정렬합니다. 초기 보고서에는 간단한 선 그래프가 포함되며 그 뒤에 데이터 테이블이 옵니다.

     왼쪽의 요약에는 현재 지표의 이름이 표시되며, 그 뒤에는 지표에 지정된 열 데이터에 대한 계산 결과가 표시됩니다. 이 예에서는 요약에 총 고객 수가 표시됩니다.

     ![시각적 Report Builder](../../assets/magento-bi-report-builder-untitled.png)

1. 차트에서 선의 각 데이터 포인트 위로 마우스를 가져갑니다. 각 데이터 포인트는 해당 달 동안 등록한 총 신규 고객 수를 보여 줍니다.

1. 다음 지침에 따라 데이터를 그룹화하고 날짜 범위 및 차트 유형을 변경합니다.

   **`Group By`**

   `Group By` 컨트롤은 그룹 또는 세그먼트별로 여러 차원을 추가할 수 있는 기능을 제공합니다. 차원은 데이터를 그룹화하는 데 사용할 수 있는 테이블의 열입니다.

   * `Group By` 옵션 목록에서 사용 가능한 차원 중 하나를 선택합니다.

     예를 들어 고객이 첫 주문을 할 때 사용한 쿠폰 코드 5개를 찾은 것이다.

     ![그룹화 기준](../../assets/magento-bi-report-builder-group-by-dimensions.png)

     `Group By` 세부 정보에는 고객이 사용하는 각 쿠폰이 나열됩니다. 최초 주문에 사용된 쿠폰에는 확인란이 표시됩니다. 이제 차트에는 첫 번째 주문에 사용된 각 쿠폰을 나타내는 여러 색상 선이 있습니다. 범례는 각 데이터 행에 대응하도록 색상으로 구분됩니다.

   * 그룹화 기준 세부 정보를 닫으려면 **[!UICONTROL Apply]**&#x200B;을(를) 클릭하십시오.

     ![여러 차원](../../assets/magento-bi-report-builder-group-by-dimension-detail.png)

   * 첫 번째 주문을 하는 동안 해당 쿠폰을 사용한 달의 고객 수를 보려면 각 라인의 몇 개 데이터 포인트를 마우스로 가리킵니다.

   * 이제 데이터 표에는 추가 차원이 있으며, 각 달에 대한 열과 각 쿠폰 코드에 대한 행이 있습니다.

     ![테이블 데이터별 그룹화](../../assets/magento-bi-report-builder-group-by-table-data.png)

   * 표의 오른쪽 위 모서리에 있는 바꾸기(![바꾸기 아이콘](../../assets/magento-bi-btn-transpose.png)) 컨트롤을 클릭하여 데이터 방향을 변경합니다.

     데이터의 축이 플립되며, 이제 테이블에는 각 쿠폰 코드에 대한 열과 각 달에 대한 행이 있습니다. 이 방향을 읽기가 더 쉬울 수 있습니다.

     ![전치된 데이터](../../assets/magento-bi-report-builder-group-by-table-data-transposed.png)

   **`Date Range`**

   `Date Range` 컨트롤은 현재 날짜 범위 및 시간 간격 설정을 보여주며 오른쪽 차트 바로 위에 있습니다.

   * 이 예제에서 `Date Range`(으)로 설정된 `All-Time by Month` 컨트롤을 클릭합니다.

     ![날짜 범위](../../assets/magento-bi-report-builder-date-range.png)

   * 다음과 같이 변경합니다.

      * 더 가깝게 보려면 날짜 범위를 `Last Full Quarter`(으)로 변경하십시오.
      * `Select Time Interval`에서 `Week`을(를) 선택합니다.
      * 완료되면 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

     이제 보고서에는 주별로 마지막 분기에 대한 데이터만 포함됩니다.

     ![주별 지난 분기 보고서](../../assets/magento-bi-report-builder-date-range-quarter-by-week-chart.png)

   **차트 종류**

   * 오른쪽 위 모서리에 있는 컨트롤을 클릭하여 데이터에 가장 적합한 차트를 찾습니다.

     일부 차트 유형은 다차원 데이터와 호환되지 않습니다.

     | | |
     |-----|-----|
     | ![선 그래프 아이콘](../../assets/magento-bi-btn-chart-line.png) | 선 그래프 |
     | ![가로 막대 아이콘](../../assets/magento-bi-btn-chart-horz-bar.png) | 가로 막대형 |
     | ![가로 누적 막대 아이콘](../../assets/magento-bi-btn-chart-horz-stacked-bar.png) | 가로 누적 막대 |
     | ![세로 막대 아이콘](../../assets/magento-bi-btn-chart-vert-bar.png) | 세로 막대 |
     | ![세로 스택 막대 아이콘](../../assets/magento-bi-btn-chart-vert-stacked-bar.png) | 세로 누적 막대 |
     | ![원형 차트 아이콘](../../assets/magento-bi-btn-chart-pie.png) | 파이 |
     | ![영역 차트 아이콘](../../assets/magento-bi-btn-chart-area.png) | 영역 |
     | ![Funnel 차트 아이콘](../../assets/magento-bi-btn-chart-funnel.png) | 단계 |

     {style="table-layout:auto"}

1. 보고서에 `title`을(를) 지정하려면 페이지 상단의 `Untitled Report` 텍스트를 설명 제목으로 바꾸십시오.

1. 오른쪽 상단 모서리에서 **[!UICONTROL Save]**&#x200B;을(를) 클릭하고 다음을 수행합니다.

   * `Type`의 경우 기본 설정인 `Chart`을(를) 사용합니다.

   * 보고서를 사용할 수 있는 `Dashboard`을(를) 선택하십시오.

   * **[!UICONTROL Save to Dashboard]**&#x200B;을(를) 클릭합니다.

     ![대시보드에 저장](../../assets/magento-bi-report-builder-save-to-dashboard.png)

1. 대시보드에서 차트를 보려면 다음 중 하나를 수행하십시오.

   * 페이지 맨 위에 있는 메시지에서 **[!UICONTROL Go to Dashboard]**&#x200B;을(를) 클릭합니다.

   * 메뉴에서 `Dashboards`을(를) 선택하고 현재 대시보드의 이름을 클릭하여 목록을 표시합니다. 그런 다음 보고서가 저장된 대시보드의 이름을 클릭합니다.

     ![대시보드의 보고서](../../assets/magento-bi-report-builder-my-dashboard.png)
