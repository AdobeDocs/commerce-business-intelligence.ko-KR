---
title: 고객 집중 정의
description: 고객 기반에 총 매출이 어떻게 분산되는지를 측정하는 데 도움이 되는 대시보드를 설정하는 방법을 알아봅니다.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# 고객 집중

이 문서에서는 고객 기반에 총 매출이 어떻게 배포되는지를 측정하는 데 도움이 되는 대시보드를 설정하는 방법을 보여줍니다. 고객 중 어느 비율이 어느 수익률을 기여하는지 파악하고 세그먼트화된 목록을 만들어 높은 기여 고객을 최상의 마케팅으로 유지하고 있습니다.

이 분석에는 다음이 포함됩니다 [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md).

## 시작하기

먼저 값이 1인 기본 키만 포함된 파일을 업로드해야 합니다. 이렇게 하면 분석에 필요한 일부 계산된 열을 만들 수 있습니다.

활용할 수 있습니다 [파일 업로더](../importing-data/connecting-data/using-file-uploader.md) 및 파일 형식을 지정하는 아래 이미지를 참조하십시오.

## 계산된 열

원래 아키텍처를 사용하는 경우(예: `Data Warehouse Views` 아래의 옵션 `Manage Data` 메뉴)에서 지원 팀에 연락하여 아래 열을 작성하십시오. 새 아키텍처에서는 `Manage Data > Data Warehouse` 페이지. 자세한 지침은 아래에 나와 있습니다.

귀사에서 손님 주문을 허용하는 경우 더 차별화된 내용이 있습니다. 그럴 경우 `customer_entity` 테이블. 게스트 주문이 허용되지 않는 경우 `sales_flat_order` 테이블.

만들 열

* `Sales_flat_order/customer_entity` 표
* (입력) `reference`
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `entity_id`
* [!UICONTROL Calculation]: - **A가 null이면 대/소문자, null이면 나머지 1 종료**
* [!UICONTROL Datatype]: - `Integer`

* `Customer concentration` 표(방금 업로드한 파일과 숫자입니다.) `1`)
* 고객 수
* [!UICONTROL Column type]: - `Many to One > Count Distinct`
* 경로 - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` 또는 `customer_entity.(input)reference > Customer Concentration.Primary Key`
* 선택한 열 - `sales_flat_order.customer_email` 또는 `customer_entity.entity_id`

* `customer_entity` 표
* 고객 수
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* 경로 - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* 선택한 열 - `Number of customers`

* (입력) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: - `Same table > Event Number`
* 이벤트 소유자 - `Number of customers`
* 이벤트 등급 - `Customer's lifetime revenue`

* 고객의 수익 백분위수
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **A가 null이면 null, 다른 경우(A/B)* 100개 끝&#x200B;**
* [!UICONTROL Datatype]: - `Decimal`

* `Sales_flat_order` 표
* 고객 수
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* 경로 - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* 선택한 열 - `Number of customers`

* (입력) 고객 라이프타임 수입별 등급
* [!UICONTROL Column type]: - `Same table > Event Number`
* 이벤트 소유자 - `Number of customers`
* 이벤트 등급 - `Customer's lifetime revenue`
* 필터 - `Customer's order number = 1`

* 고객의 수익 백분위수
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **A가 null이면 null, 다른 경우(A/B)* 100개 끝&#x200B;**
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>사용되는 백분위수는 고객 기반의 Xth 백분위수를 나타내는 고객의 분할입니다. 각 고객은 1에서 100까지의 정수와 연결되며, 이것은 평생 매출로 생각할 수 있습니다 *등급*. 예를 들어 특정 고객에 대한 고객의 매출 백분위수가 **5개**&#x200B;로 설정되면 이 고객은 ***5번째 백분위수*** 라이프타임 매출 측면에서 모든 고객 중

## 지표

* **총 고객 라이프타임 값**
* 에서 `customer_entity` 표
* 이 지표는 다음을 수행합니다 **합계**
* 설정 `Customer's lifetime revenue` 열
* 정렬 기준 `Customer's first order date` timestamp

## 보고서

* **고객 집중**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* 
   [[!UICONTROL 그룹]: `Independent`
* 지표 `A`: `Total customer lifetime revenue by percentile`
* 지표 `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* 위쪽/아래쪽 표시: `100% of Customer's revenue percentile Name`
* 

   [!UICONTROL Chart type]: `Line`

* **상위 10% 농도**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* 지표 `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 차트 숨기기
* 
   [[!UICONTROL 그룹]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **하위 50% 농도, 단 하나의 구매만**

* 지표 `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 차트 숨기기
* 
   [[!UICONTROL 그룹]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **하위 10% 농도**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* 지표 `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 차트 숨기기
* 
   [[!UICONTROL 그룹]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

모든 보고서를 컴파일한 후 대시보드에서 원하는 대로 구성할 수 있습니다. 최종 결과는 위의 샘플 대시보드와 비슷합니다.

이 분석을 작성하는 동안 질문이 있거나 전문 서비스 팀에 참여하려는 경우 [연락처 지원](../../guide-overview.md).
