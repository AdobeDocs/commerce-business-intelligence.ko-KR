---
title: 무료 배송 임계값
description: 무료 배송 임계값의 성능을 추적하는 대시보드를 설정하는 방법에 대해 알아봅니다.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
role: Admin,  User
feature: Data Warehouse Manager, Dashboards, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# 무료 배송

>[!NOTE]
>
>이 항목에는 원래 아키텍처와 새 아키텍처를 사용하는 클라이언트에 대한 지침이 포함되어 있습니다. 기본 도구 모음에서 `Data Warehouse Views`을(를) 선택한 후 `Manage Data` 섹션을 사용할 수 있는 경우 새 아키텍처를 사용합니다.

이 항목에서는 무료 배송 임계값의 성능을 추적하는 대시보드를 설정하는 방법을 보여 줍니다. 아래 표시된 이 대시보드는 A/B에서 두 개의 무료 배송 임계값을 테스트할 수 있는 좋은 방법입니다. 예를 들어 귀사는 50달러 또는 100달러에 무료 배송을 제공해야 하는지 확신할 수 없습니다. 고객의 임의 하위 집합 두 개에 대한 A/B 테스트를 수행하고 [!DNL Commerce Intelligence]에서 분석을 수행해야 합니다.

시작하기 전에 상점의 무료 배송 임계값에 대한 값이 다른 두 개의 개별 기간을 식별하려고 합니다.

![무료 배송 임계값 분석 및 주문 값 분포를 보여 주는 차트](../../assets/free_shipping_threshold.png)

이 분석에는 [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md)이(가) 포함되어 있습니다.

## 계산된 열

원본 아키텍처를 사용하는 경우(예: `Data Warehouse Views` 메뉴 아래에 `Manage Data` 옵션이 없는 경우) 지원 팀에 연락하여 아래 열을 빌드해야 합니다. 새 아키텍처에서 이러한 열은 `Manage Data > Data Warehouse` 페이지에서 만들 수 있습니다. 자세한 지침은 아래에 나와 있습니다.

* **`sales_flat_order`** 테이블
   * 이 계산은 일반적인 장바구니 크기에 비례하여 증분으로 버킷을 만듭니다. 5, 10, 50, 100을 포함하는 증분의 범위일 수 있습니다.

* **`Order subtotal (buckets)`** 원본 아키텍처: 분석가가 `[FREE SHIPPING ANALYSIS]` 티켓의 일부로 만들었습니다.
* **`Order subtotal (buckets)`**&#x200B;개의 새 아키텍처:
   * 위에서 언급했듯이 이 계산은 일반적인 장바구니 크기에 비례하여 증분으로 버킷을 생성합니다. `base_subtotal`과(와) 같은 기본 소계 열이 있는 경우 이 새 열의 기반으로 사용할 수 있습니다. 그렇지 않은 경우 매출에서 출하 및 할인을 제외하는 계산된 열이 될 수 있습니다.

  >[!NOTE]
  >
  >버킷 크기는 클라이언트로서 적합한 항목에 따라 다릅니다. `average order value`(으)로 시작하여 해당 양보다 작거나 큰 버킷을 만들 수 있습니다. 아래 계산을 살펴볼 때 쿼리의 일부를 쉽게 복사하고, 편집하고, 추가 버킷을 만드는 방법을 알 수 있습니다. 이 예제는 50씩 증가하여 수행됩니다.

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal` 또는 `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
`A< 200` 및 `A <= 250`일 때 `201 - 250`
`A<251` 및 `A<= 300`일 때 `251 - 300`
`A<301` 및 `A<= 350`일 때 `301 - 350`
`A<351` 및 `A<=400`일 때 `351 - 400`
`A<401` 및 `A<=450`일 때 `401 - 450`
450개 이상
종료


## 지표

새 지표가 없습니다!!!

>[!NOTE]
>
>새 보고서를 작성하기 전에 [모든 새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md)하십시오.

## 보고서

* **배송 규칙 A의 평균 주문 가격**
   * [!UICONTROL Metric]: `Average order value`

* 지표 `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **배달 규칙 A가 있는 소계 버킷별 주문 수**
   * [!UICONTROL Metric]: `Number of orders`

  >[!NOTE]
  >
  >`X`에 상위 `sorted by` `Order subtotal` `Show top/bottom`(버킷)을 표시하여 끝 부분을 차단할 수 있습니다.

* 지표 `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]: `Column`

* 배송 규칙 A가 있는 소계별 주문 비율 **퍼센트**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * &#x200B;
     [!UICONTROL 그룹 기준]: `Independent`
   * [!UICONTROL Formula]: `(A / B)`
   * &#x200B;
     [!UICONTROL Format]: `%`

* 지표 `A`: `Number of orders by subtotal (hide)`
* 지표 `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`

* 소계가 배송 규칙 A를 초과하는 주문의 **퍼센트**
   * [!UICONTROL Metric]: `Number of orders`
   * &#x200B;
     [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]: `Number of orders`
   * &#x200B;
     [!UICONTROL 그룹 기준]: `Independent`

   * [!UICONTROL Formula]: `1- (A / B)`
   * &#x200B;
     [!UICONTROL Format]: `%`

* 지표 `A`: `Number of orders by subtotal`
* 지표 `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`


운송 규칙 B가 있는 기간 및 운송 B에 대해 위의 단계와 보고서를 반복합니다.

모든 보고서를 컴파일한 후 원하는 대로 대시보드에서 구성할 수 있습니다. 결과는 이 페이지 상단에 있는 이미지와 비슷할 수 있습니다.
