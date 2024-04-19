---
title: 쿠폰 코드 분석(기본)
description: 귀하의 사업의 쿠폰 성과에 대해 알아보는 것은 주문을 세분화하고 고객 습관을 더 잘 이해하는 흥미로운 방법입니다.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: d8fc96a58b72c601a5700f35ea1f3dc982d76571
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# 기본 쿠폰 코드 분석

귀하의 비즈니스의 쿠폰 성과를 이해하는 것은 주문을 세분화하고 고객 습관을 더 잘 이해할 수있는 흥미로운 방법입니다.

이 항목에서는 쿠폰을 구입한 고객이 수행하는 방법을 이해하고, 추세를 확인하고, 개별 쿠폰 코드 사용을 추적하는 데 필요한 이러한 분석을 만드는 데 필요한 단계를 설명합니다.

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## 시작

먼저, 쿠폰 코드를 추적하는 방법에 대한 참고 사항. 고객이 주문에 쿠폰을 적용하면 다음 세 가지 상황이 발생합니다.

* 할인은 다음에 반영됩니다. `base_grand_total` 금액(본인) `Revenue` Commerce Intelligence의 지표)
* 쿠폰 코드는 `coupon_code` 필드. 이 필드가 NULL(비어 있음)이면 주문에 연결된 쿠폰이 없습니다.
* 할인된 금액은에 저장됩니다. `base_discount_amount`. 구성에 따라 이 값이 음수 또는 양수로 표시될 수 있습니다.

Commerce 2.4.7부터 고객은 주문에 두 개 이상의 쿠폰 코드를 적용할 수 있습니다. 이 경우:

* 적용되는 모든 쿠폰 코드는 `coupon_code` 필드 `sales_order_coupons`. 적용된 첫 번째 쿠폰 코드도 `coupon_code` 필드 `sales_order`. 이 필드가 NULL(비어 있음)이면 주문에 연결된 쿠폰이 없습니다.

## 지표 작성

첫 번째 단계는 다음 단계로 새 지표를 구성하는 것입니다.

* 다음으로 이동 **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* 다음 항목 선택 `sales_order`.
* 이 지표는 다음을 수행합니다. **합계** 다음에 있음 **base_discount_mount** 열, 정렬 기준 **created_at**.
   * [!UICONTROL Filters]:
      * 추가 `Orders we count` (저장된 필터 세트)
      * 다음을 추가합니다.
         * `coupon_code`**아님**`[NULL]`
      * 지표에 다음과 같은 이름을 지정합니다. `Coupon discount amount`.

## 대시보드 만들기

* 지표가 생성되면 다음 작업을 수행하십시오.
   * 다음으로 이동 [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
   * 대시보드에 다음과 같은 이름을 지정합니다. `_Coupon Analysis_`.

* 여기서 모든 보고서를 만들고 추가할 수 있습니다.

## 보고서 작성 중

* **새 보고서:**

>[!NOTE]
>
>다음 [!UICONTROL Time Period]각 보고서에 대한 ** 목록은 다음과 같습니다. `All-time`. 분석 요구 사항에 맞게 자유롭게 변경하십시오. Adobe은 이 대시보드에 있는 모든 보고서가 동일한 기간을 다루는 것을 권장합니다. 예: `All time`, `Year-to-date`, 또는 `Last 365 days`.

* **쿠폰이 포함된 주문**
   * 
     [!UICONTROL 지표]: `Orders`
      * 필터 추가:
         * [`A`] `coupon_code` **아님** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **쿠폰이 없는 주문**
   * 
     [!UICONTROL 지표]: `Orders`
      * 필터 추가:
         * [`A`] `coupon_code` **다음과 같음** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **쿠폰이 포함된 주문 순 수익**
   * 
     [!UICONTROL 지표]: `Revenue`
      * 필터 추가:
         * [`A`] `coupon_code` **아님** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **쿠폰 할인**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **평균 라이프타임 수익: 쿠폰 획득 고객**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 필터 추가:
         * [`A`] `Customer's first order's coupon_code` **아님** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **평균 라이프타임 수익: 비쿠폰 획득 고객**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 필터 추가:
         * [A] `Customer's first order's coupon_code` **다음과 같음**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **쿠폰 사용 세부 정보(최초 주문)**
   * 지표 `1`: `Orders`
      * 필터 추가:
         * [`A`] `coupon_code` **아님**`[NULL]`
         * [`B`] `Customer's order number` **다음과 같음** `1`

   * 지표 `2`: `Revenue`
      * 필터 추가:
         * [`A`] `coupon_code` **아님**`[NULL]`
         * [`B`] `Customer's order number` **다음과 같음** `1`

      * 이름 바꾸기:  `Net revenue`

   * 지표 `3`: `Coupon discount amount`
      * 필터 추가:
         * [`A`] `coupon_code` **아님**`[NULL]`
         * [`B`] `Customer's order number` **다음과 같음** `1`

   * 수식 만들기: `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * 
        [!UICONTROL Format]: `Currency`

   * 수식 만들기:**% 할인**
      * 공식: `(C / (B - C))`
      * 
        [!UICONTROL Format]: `Percentage`

   * 수식 만들기: `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
        [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 간격]: `None`
   * 
     [!UICONTROL 차트 유형]: `Table`

* **1순위 쿠폰별 평균 라이프타임 수익**
   * [!UICONTROL Metric]:**평균 라이프타임 수익**
      * 필터 추가:
         * [`A`] `coupon_code` **다음과 같음**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **쿠폰 사용 세부 정보(최초 주문)**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 필터 추가:
         * [`A`] `Customer's first order's coupon_code` **아님** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 간격]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 
     [!UICONTROL 차트 유형]: **Column**

* **쿠폰 / 비 쿠폰 획득에 의한 새로운 고객**
   * 지표 `1`: `New customers`
      * 필터 추가:
         * [`A`] `Customer's first order's coupon_code` **아님** `[NULL]`

      * [!UICONTROL Rename]: `Coupon acquisition customer`

   * 지표 `2`: `New customers`
      * 필터 추가:
         * [`A`] `coupon_code` **다음과 같음**`[NULL]`

      * [!UICONTROL Rename]: `Non-coupon acquisition customer`

   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`

보고서를 작성한 후 대시보드에서 보고서를 구성하는 방법에 대한 자세한 내용은 이 항목 맨 위에 있는 이미지를 참조하십시오.

>[!NOTE]
>
>Adobe Commerce 2.4.7부터 고객은 **quote_coupns** 및 **sales_order_coupins** 고객이 여러 쿠폰을 사용하는 방법에 대한 통찰력을 얻을 수 있는 표

![](../../assets/multicoupon_relationship_tables.png)
