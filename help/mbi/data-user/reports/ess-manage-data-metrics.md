---
title: 지표 만들기
description: 지표를 사용하여 차트를 만드는 방법을 알아봅니다.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# 지표 만들기

>[!NOTE]
>
>[관리자 권한](../../administrator/user-management/user-management.md)이 필요합니다.

지표는 측정입니다. SQL 및 데이터베이스 구조에서 지표는 변수 기간에 대한 저장된 쿼리와 같습니다.

[!DNL Commerce Intelligence]에서 지표를 사용하여 [차트를 만들기](../../data-user/reports/ess-rpt-build-visual.md)할 수 있습니다. 예를 들어 지표 `revenue`은(는) 총 주문 수입니다. 지표 `average customer revenue per order`은(는) 주문당 평균 고객이 소비하는 지표입니다.

보고서에서 사용할 경우 지정된 기간 동안 지표를 분석하고 [다른 카테고리로 필터링 또는 분할](../../best-practices/segment-filter.md)할 수 있습니다. 성별로 그룹화된 평균 고객 매출을 분석해 보십시오. 이 경우 `average customer revenue per order`이(가) 지표이고 성별이 그룹입니다.

## 지표 정의 {#define}

1. 지표를 만들려면 **[!UICONTROL Data** > **Metrics]**&#x200B;을(를) 클릭합니다.

1. **[!UICONTROL Create New Metric]**&#x200B;을(를) 클릭합니다.

1. 드롭다운에서 지표에 사용할 기본 또는 계산된 열을 포함하는 표를 클릭합니다.

1. 지표 이름을 지정합니다.

   Adobe은 지표가 무엇인지 한눈에 알 수 있도록 이름을 권장합니다. 예: `Average Order Revenue`.

1. 다음 단계는 지표가 수행하는 작업을 정의하는 것입니다. 드롭다운 메뉴를 사용하여 지표의 작업, `operation` 열 및 `date` 차원을 정의합니다.

   * 작업 선택:
      * `Count` - 이 작업은 데이터 테이블의 행 수를 계산합니다.
      * `Max` - 최대값은 특정 데이터 열의 최대값을 반환합니다.
      * `Min` - Min이 특정 데이터 열의 최소값을 반환합니다.
      * `Sum` - 이 작업은 특정 데이터 열의 값을 합합니다.
      * `Average` - 이 작업은 데이터 열 값의 평균을 계산합니다.
      * `Count Distinct Value` - 특정 데이터 열의 고유 값 수를 계산합니다.
      * `Median` - 이 작업은 데이터 열 값의 중간값을 계산합니다.
      * `First and Third Quartiles` - 이 연산은 데이터 열 값의 25번째 및 75번째 백분위수를 각각 계산합니다.
      * `Tenth and Ninetieth Percentiles` - 이 작업은 데이터 열 값의 10번째 및 90번째 백분위수를 각각 계산합니다.

   * 작업을 수행할 열을 선택합니다. 예를 들어 총 매출을 찾으려면 `order total` 열에서 합계 작업을 수행합니다.

     기존 지표를 편집하는 경우 이 섹션에서 [지표의 작업 테이블을 변경](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md)할 수도 있습니다.

   * 지표의 트렌드를 분석하는 데 사용할 수 있는 날짜 차원을 선택합니다. 예: `order date`.

## 필터 추가 {#filters}

`Filter` 섹션에서 필터를 만들거나 [저장된 필터 집합](../../data-user/reports/ess-manage-data-filters.md)을 지표에 적용할 수 있습니다.

`average order revenue` 지표의 경우 스토어를 설정하는 동안 수행되었을 수 있는 테스트 주문을 포함하지 않으려 할 것입니다. 이렇게 하면 부정확한 결과를 얻을 수 있습니다. 필터 세트를 적용하여 데이터 세트에서 해당 주문을 제거할 수 있습니다. 필터가 생성되면 이 지표를 사용하여 빌드된 모든 차트에 적용됩니다.

`Filter Logic` 섹션에서 지표의 동작 방식을 추가로 정의할 수 있습니다.

* &quot;\[`A`\] 또는 \[`B`\]&quot;에서는 \[`A`\] 또는 \[`B`\] 필터를 충족하는 모든 데이터를 허용합니다
* &quot;\[`A`\] 및 \[`B`\]&quot;에서는 \[`A`\] 및 \[`B`\] 필터를 모두 충족하는 데이터만 허용합니다
* &quot;(\[`A`\] 및 \[`B`\]) 또는 \[`C`\]&quot;은(는) \[`A`\] 및 \[`B`\] 필터를 모두 충족하거나 \[`C`\] 필터를 단독으로 충족하는 데이터만 허용합니다

## 차원 추가 {#dimensions}

[`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 섹션에는 필터링 또는 그룹화에 사용 가능한 모든 데이터 차원이 표시됩니다. 기본적으로 사용 가능한 모든 데이터 열은 차원으로 나열됩니다. 예를 계속 진행하여 조회 출처별로 매출을 세그먼트화하려는 경우 여기에서 세그먼트화할 수 있습니다.

사용 가능한 모든 데이터 열을 차원으로 나열할 뿐만 아니라 [!DNL Commerce Intelligence]에서 그룹화할 수 있는 열을 추측합니다. *보고서에 데이터를 세그먼트화하거나 그룹화하려면* 열을 그룹화 가능으로 표시해야 합니다.

## 마무리 중 {#finish}

지표의 동작 방식을 정의하는 것 외에도 `User Rights` 섹션에서 권한 수준을 설정할 수도 있습니다. `Admin`명의 사용자가 모든 지표에 액세스할 수 있지만 해당 그룹 옆의 확인란을 선택하여 이 지표를 사용할 수 있는 사용자를 표시해야 합니다.

기존 지표를 편집하는 경우 `Dependent Charts` 섹션에서 이 지표를 사용하는 차트 목록(및 해당 지표를 소유한 사용자)을 볼 수 있습니다.

변경 사항이 자동으로 저장되고 이제 지표를 사용할 수 있습니다.
