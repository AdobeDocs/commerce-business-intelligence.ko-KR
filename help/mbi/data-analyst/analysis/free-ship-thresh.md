---
title: 무료 배송 임계값
description: 무료 배송 임계값의 성능을 추적하는 대시보드를 설정하는 방법에 대해 알아봅니다.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# 무료 배송

>[!NOTE]
>
>이 항목에는 원래 아키텍처와 새 아키텍처를 사용하는 클라이언트에 대한 지침이 포함되어 있습니다. 다음과 같은 경우 새 아키텍처를 사용합니다. `Data Warehouse Views` 선택 후 사용 가능한 섹션 `Manage Data` 기본 도구 모음에서

이 항목에서는 무료 배송 임계값의 성능을 추적하는 대시보드를 설정하는 방법을 보여 줍니다. 아래 표시된 이 대시보드는 A/B에서 두 개의 무료 배송 임계값을 테스트할 수 있는 좋은 방법입니다. 예를 들어 귀사는 50달러 또는 100달러에 무료 배송을 제공해야 하는지 확신할 수 없습니다. 고객의 두 임의 하위 집합에 대한 A/B 테스트를 수행하고 분석을 수행해야 합니다 [!DNL Commerce Intelligence].

시작하기 전에 상점의 무료 배송 임계값에 대한 값이 다른 두 개의 개별 기간을 식별하려고 합니다.

![](../../assets/free_shipping_threshold.png)

이 분석에는 다음이 포함됩니다. [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md).

## 계산된 열

원본 아키텍처를 사용하고 있는 경우(예: `Data Warehouse Views` 옵션 아래에 있는 `Manage Data` 메뉴)에서 아래 열을 빌드하려면 지원 팀에 문의하십시오. 새 아키텍처에서 이러한 열을 만들 수 있는 `Manage Data > Data Warehouse` 페이지를 가리키도록 업데이트하는 중입니다. 자세한 지침은 아래에 나와 있습니다.

* **`sales_flat_order`** 표
   * 이 계산은 일반적인 장바구니 크기에 비례하여 증분으로 버킷을 만듭니다. 5, 10, 50, 100을 포함하는 증분의 범위일 수 있습니다.

* **`Order subtotal (buckets)`** 원래 아키텍처: 분석가가 `[FREE SHIPPING ANALYSIS]` 티켓
* **`Order subtotal (buckets)`** 새로운 아키텍처:
   * 위에서 언급했듯이 이 계산은 일반적인 장바구니 크기에 비례하여 증분으로 버킷을 생성합니다. 다음과 같은 기본 소계 열이 있는 경우 `base_subtotal`: 이 새 열의 기반으로 사용할 수 있습니다. 그렇지 않은 경우 매출에서 출하 및 할인을 제외하는 계산된 열이 될 수 있습니다.
   >[!NOTE]
   >
   >버킷 크기는 클라이언트로서 적합한 항목에 따라 다릅니다. 다음으로 시작할 수 있습니다. `average order value` 그리고 해당 양보다 작거나 큰 버킷을 만듭니다. 아래 계산을 살펴볼 때 쿼리의 일부를 쉽게 복사하고, 편집하고, 추가 버킷을 만드는 방법을 알 수 있습니다. 이 예제는 50씩 증가하여 수행됩니다.

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`, 또는 `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
다음과 같은 경우 `A< 200` 및 `A <= 250` 그러면 `201 - 250`
조건 `A<251` 및 `A<= 300` 그러면 `251 - 300`
조건 `A<301` 및 `A<= 350` 그러면 `301 - 350`
조건 `A<351` 및 `A<=400` 그러면 `351 - 400`
조건 `A<401` 및 `A<=450` 그러면 `401 - 450`
450을 넘는 다른 끝



## 지표

새 지표가 없습니다!!!

>[!NOTE]
>
>다음을 확인하십시오. [새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에

## 보고서

* **운송 규칙 A의 평균 주문 가격**
   * [!UICONTROL Metric]: `Average order value`

* 지표 `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **운송 규칙 A가 있는 소계 버켓별 주문 수**
   * [!UICONTROL Metric]: `Number of orders`

   >[!NOTE]
   >
   >윗부분을 보여줌으로써 꼬리 끝을 자를 수 있다 `X` `sorted by` `Order subtotal` (버킷) `Show top/bottom`.

* 지표 `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Column`

* **운송 규칙 A가 있는 소계별 주문 비율**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 
      [!UICONTROL 그룹 기준]: `Independent`
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `%`

* 지표 `A`: `Number of orders by subtotal (hide)`
* 지표 `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Line`

* **소계가 운송 규칙 A를 초과하는 주문의 퍼센트**
   * [!UICONTROL Metric]: `Number of orders`
   * 

      [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]: `Number of orders`
   * 

      [!UICONTROL 그룹 기준]: `Independent`

   * [!UICONTROL Formula]: `1- (A / B)`
   * 

      [!UICONTROL Format]: `%`

* 지표 `A`: `Number of orders by subtotal`
* 지표 `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Line`


운송 규칙 B가 있는 기간 및 운송 B에 대해 위의 단계와 보고서를 반복합니다.

모든 보고서를 컴파일한 후 원하는 대로 대시보드에서 구성할 수 있습니다. 결과는 이 페이지 상단에 있는 이미지와 비슷할 수 있습니다.
