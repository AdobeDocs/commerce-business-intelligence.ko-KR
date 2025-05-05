---
title: 고객 집중 정의
description: 총 수익이 고객 기반 간에 어떻게 분배되는지 측정하는 데 도움이 되는 대시보드를 설정하는 방법을 알아봅니다.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# 고객 집중

이 항목에서는 총 매출이 고객 기반 간에 분배되는 방식을 측정하는 데 도움이 되는 대시보드를 설정하는 방법을 보여 줍니다. 고객 중 몇 퍼센트가 몇 퍼센트의 매출에 기여하는지 파악하고 가장 좋은 시장 점유율을 위해 세그먼트화된 목록을 만들어 기여도가 높은 고객을 유지하고 있습니다.

이 분석에는 [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md)이(가) 포함되어 있습니다.

## 시작

먼저 값이 1인 기본 키만 포함된 파일을 업로드해야 합니다. 이를 통해 분석에 필요한 몇 가지 계산된 열을 만들 수 있습니다.

[파일 업로더](../importing-data/connecting-data/using-file-uploader.md) 및 아래 이미지를 사용하여 파일 형식을 지정할 수 있습니다.

## 계산된 열

원본 아키텍처를 사용하는 경우(예: `Manage Data` 메뉴 아래에 `Data Warehouse Views` 옵션이 없는 경우) 지원 팀에 연락하여 아래 열을 빌드해야 합니다. 새 아키텍처에서 이러한 열은 `Manage Data > Data Warehouse` 페이지에서 만들 수 있습니다. 자세한 지침은 아래에 나와 있습니다.

귀사에서 고객 주문을 허용한다면 더욱 차별화됩니다. 이 경우 `customer_entity` 테이블의 모든 단계를 무시할 수 있습니다. 게스트 주문이 허용되지 않으면 `sales_flat_order` 테이블에 대한 모든 단계를 무시하십시오.

생성할 열

* `Sales_flat_order/customer_entity` 테이블
* (입력) `reference`
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `entity_id`
* [!UICONTROL Calculation]: - **A가 null이고 Null인 경우 다른 1은(는) end**
* [!UICONTROL Datatype]: - `Integer`

* `Customer concentration` 테이블(이 파일은 `1` 번호로 업로드한 파일입니다.)
* 고객 수
* [!UICONTROL Column type]: - `Many to One > Count Distinct`
* 경로 - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` 또는 `customer_entity.(input)reference > Customer Concentration.Primary Key`
* 선택한 열 - `sales_flat_order.customer_email` 또는 `customer_entity.entity_id`

* `customer_entity` 테이블
* 고객 수
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* 경로 - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* 선택한 열 - `Number of customers`

* (입력) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: - `Same table > Event Number`
* 이벤트 소유자 - `Number of customers`
* 이벤트 순위 - `Customer's lifetime revenue`

* 고객의 수익 백분위수
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **A가 null이고 A/B가 null인 경우* 100 end &#x200B;**
* [!UICONTROL Datatype]: - `Decimal`

* `Sales_flat_order` 테이블
* 고객 수
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* 경로 - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* 선택한 열 - `Number of customers`

* (입력) 고객 생애 수익별 순위
* [!UICONTROL Column type]: - `Same table > Event Number`
* 이벤트 소유자 - `Number of customers`
* 이벤트 순위 - `Customer's lifetime revenue`
* 필터 - `Customer's order number = 1`

* 고객의 수익 백분위수
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **A가 null이고 A/B가 null인 경우* 100 end &#x200B;**
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>사용된 백분위수는 고객의 분할이며, 고객 기반의 X번째 백분위수를 나타냅니다. 각 고객은 1에서 100 사이의 정수와 연결되는데, 이 정수는 라이프타임 매출 *순위*&#x200B;로 생각할 수 있습니다. 예를 들어 특정 고객에 대한 고객의 매출 백분위수가 **5**&#x200B;인 경우 이 고객은 라이프타임 매출 측면에서 모든 고객의 ***5번째 백분위수***&#x200B;에 속합니다.

## 지표

* **총 고객 수명 값**
* `customer_entity` 테이블에서
* 이 지표는 **합계**&#x200B;를 수행합니다.
* `Customer's lifetime revenue` 열에서
* `Customer's first order date` 타임스탬프로 정렬됨

## 보고서

* **고객 집중**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* &#x200B;
  [!UICONTROL 그룹 기준]: `Independent`
* 지표 `A`: `Total customer lifetime revenue by percentile`
* 지표 `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* 위쪽/아래쪽 표시: `100% of Customer's revenue percentile Name`
* &#x200B;
  [!UICONTROL Chart type]: `Line`

* **상위 10% 농도**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* 지표 `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* 차트 숨기기
* &#x200B;
  [!UICONTROL 그룹 기준]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **하위 50% 집중도(한 번만 구매)**

* 지표 `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* 차트 숨기기
* &#x200B;
  [!UICONTROL 그룹 기준]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **하위 10% 농도**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* 지표 `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* 차트 숨기기
* &#x200B;
  [!UICONTROL 그룹 기준]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

모든 보고서를 컴파일한 후 원하는 대로 대시보드에서 구성할 수 있습니다. 결과는 위의 샘플 대시보드와 비슷할 수 있습니다.

이 분석을 작성하는 동안 질문이 있거나 Professional Services 팀에 문의하려는 경우 [지원 팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ko)하십시오.
