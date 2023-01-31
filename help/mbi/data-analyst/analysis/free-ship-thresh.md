---
title: 무료 배송 임계값
description: 무료 배송 임계값의 성능을 추적할 대시보드를 설정하는 방법을 알아봅니다.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# 무료 배송

>[!NOTE]
>
>이 문서에는 원래 아키텍처와 새로운 아키텍처를 활용하는 고객을 위한 지침이 포함되어 있습니다. 기본 도구 모음에서 &quot;데이터 관리&quot;를 선택한 후 &quot;Data Warehouse 보기&quot; 섹션을 사용할 수 있는 경우 새 아키텍처에 있습니다.

이 문서에서는 무료 배송 임계값의 성과를 추적할 대시보드를 설정하는 방법을 보여줍니다. 아래 표시된 이 대시보드는 A/B 테스트를 통해 두 가지 다른 무료 배송 임계값을 테스트할 수 있는 좋은 방법입니다. 예를 들어 귀사는 50달러 또는 100달러로 무료 배송을 제공할지 확실하지 않을 수 있습니다. 고객의 임의 하위 세트 두 개에 대한 A/B 테스트를 수행하고, [!DNL MBI].

시작하기 전에, 스토어의 무료 배송 임계값에 대해 다른 값이 있는 두 개의 개별 기간을 식별하려고 합니다.

![](../../assets/free_shipping_threshold.png)

이 분석에는 다음이 포함됩니다 [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md).

## 계산된 열

원래 아키텍처를 사용하는 경우(예: `Data Warehouse Views` 아래의 옵션 `Manage Data` 메뉴)에서 지원 팀에 연락하여 아래 열을 작성하십시오. 새 아키텍처에서는 `Manage Data > Data Warehouse` 페이지. 자세한 지침은 아래에 나와 있습니다.

* **`sales_flat_order`** 표
   * 이 계산은 일반적인 장바구니 크기에 비례하여 증분으로 버킷을 생성합니다. 이 범위는 5, 10, 50, 100을 포함한 증분으로 구성될 수 있습니다

* **`Order subtotal (buckets)`** 원래 아키텍처: 분석가가 의 일부로 `[FREE SHIPPING ANALYSIS]` 티켓
* **`Order subtotal (buckets)`** 새로운 아키텍처:
   * 위에서 언급했듯이 이 계산에서는 일반적인 장바구니 크기에 대해 증가분의 버킷을 만듭니다. 다음과 같은 기본 하위 합계 열이 있는 경우 `base_subtotal`를 사용 할 수 있습니다. 그렇지 않은 경우 매출에서 운송 및 할인을 제외하는 계산된 열일 수 있습니다.
   >[!NOTE]
   >
   >&quot;버킷&quot; 크기는 고객으로서 적합한 항목에 따라 달라집니다. 먼저 `average order value` 및 해당 양보다 작거나 같은 특정 수의 버킷을 만듭니다. 아래 계산을 보면 쿼리의 일부를 쉽게 복사하고 편집하고 추가 버킷을 만드는 방법을 볼 수 있습니다. 이 예제는 50씩 증가합니다.

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`, 또는 `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
when `A< 200` 및 `A <= 250` 그런 다음 `201 - 250`
when `A<251` 및 `A<= 300` 그런 다음 `251 - 300`
when `A<301` 및 `A<= 350` 그런 다음 `301 - 350`
when `A<351` 및 `A<=400` 그런 다음 `351 - 400`
when `A<401` 및 `A<=450` 그런 다음 `401 - 450`
다른 &#39;450&#39; 끝



## 지표

새 지표 없음!!!

>[!NOTE]
>
>다음을 확인하십시오 [새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에

## 보고서

* **운송 규칙 A가 있는 평균 주문 가격**
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
   >맨 위를 표시하여 꼬리 끝을 잘라낼 수 있습니다 `X` `sorted by` `Order subtotal` (버킷)을 `Show top/bottom`.

* 지표 `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Column`

* **출하 규칙 A가 있는 소계 주문별 비율**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 
      [[!UICONTROL 그룹]: `Independent`
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

* **하위 합계가 출하 규칙 A를 초과하는 주문 비율**
   * [!UICONTROL Metric]: `Number of orders`
   * 

      [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]: `Number of orders`
   * 

      [[!UICONTROL 그룹]: `Independent`

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


운송 규칙 B와 운송 규칙 B에 대해 위의 단계 및 보고서를 반복합니다.

모든 보고서를 컴파일한 후 대시보드에서 원하는 대로 구성할 수 있습니다. 최종 결과는 이 페이지의 맨 위에 있는 이미지와 같을 수 있습니다.
