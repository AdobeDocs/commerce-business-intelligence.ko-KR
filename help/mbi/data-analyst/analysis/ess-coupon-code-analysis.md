---
title: 쿠폰 코드 분석(기본)
description: 비즈니스의 쿠폰 성능에 대해 알아보려면 주문을 세분화하고 고객 습관을 이해하는 흥미로운 방법입니다.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 기본 쿠폰 코드 분석

비즈니스의 쿠폰 성능을 이해하는 것은 주문을 세분화하고 고객 습관을 더 잘 이해할 수 있는 흥미로운 방법입니다.

쿠폰으로 획득한 고객이 수행하는 방식을 이해하고, 트렌드를 확인하고, 개별 쿠폰 코드 사용을 추적하는 데 필요한 단계를 문서화했습니다.

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## 시작하기

먼저 쿠폰 코드를 추적하는 방법에 대한 노트입니다. 고객이 주문에 쿠폰을 적용하면 다음과 같은 세 가지 상황이 발생합니다.

* 할인은 `base_grand_total` 금액( `Revenue` mbi의 지표)
* 쿠폰 코드는 `coupon_code` 필드. 이 필드가 NULL(비어 있음)이면 주문에 쿠폰이 연결되어 있지 않습니다.
* 할인된 금액은 다음 위치에 저장됩니다. `base_discount_amount`. 구성에 따라 이 값은 음수 또는 양수로 표시될 수 있습니다.

## 지표 작성

첫 번째 단계는 다음 단계로 새 지표를 구성하는 것입니다.

* 다음으로 이동 **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* 을(를) 선택합니다 `sales_order`.
* 이 지표는 다음을 수행합니다 **합계** on **base_discount_amount** 열, 정렬 기준 **created_at**.
   * [!UICONTROL Filters]:
      * 추가 `Orders we count` (저장된 필터 세트)
      * 다음을 추가합니다.
         * `coupon_code`**아님**`[NULL]`
      * 지표에 다음과 같은 이름을 지정합니다. `Coupon discount amount`.

## 대시보드 만들기

* 지표가 만들어지면:
   * 다음으로 이동 [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
   * 대시보드에 다음과 같은 이름을 지정합니다. `_Coupon Analysis_`.

* 이 단계에서 모든 보고서를 만들고 추가합니다.

## 보고서 작성

* **새 보고서:**

>[!NOTE]
>
>다음 [!UICONTROL Time Period]각 보고서에 대해 **은 `All-time`. 분석 요구 사항에 맞게 자유롭게 변경할 수 있습니다. 이 대시보드의 모든 보고서는 다음과 같은 동일한 기간을 포함하는 것이 좋습니다 `All time`, `Year-to-date`, 또는 `Last 365 days`.

* **쿠폰이 있는 주문**
   * 
      [[!UICONTROL 지표]: `Orders`
      * 필터 추가:
         * [`A`] `coupon_code` **아님** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **쿠폰 없는 주문**
   * 
      [[!UICONTROL 지표]: `Orders`
      * 필터 추가:
         * [`A`] `coupon_code` **IS** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **쿠폰이 있는 주문의 순 매출**
   * 
      [[!UICONTROL 지표]: `Revenue`
      * 필터 추가:
         * [`A`] `coupon_code` **아님** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **쿠폰에서 할인**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **평균 라이프타임 매출: 쿠폰 인수 고객**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 필터 추가:
         * [`A`] `Customer's first order's coupon_code` **아님** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **평균 라이프타임 매출: 쿠폰이 아닌 획득 고객**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 필터 추가:
         * [A] `Customer's first order's coupon_code` **IS**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **쿠폰 사용 세부 정보(최초 주문)**
   * 지표 `1`: `Orders`
      * 필터 추가:
         * [`A`] `coupon_code` **아님**`[NULL]`
         * [`B`] `Customer's order number` **같음** `1`
   * 지표 `2`: `Revenue`
      * 필터 추가:
         * [`A`] `coupon_code` **아님**`[NULL]`
         * [`B`] `Customer's order number` **같음** `1`
      * 이름 변경:  `Net revenue`
   * 지표 `3`: `Coupon discount amount`
      * 필터 추가:
         * [`A`] `coupon_code` **아님**`[NULL]`
         * [`B`] `Customer's order number` **같음** `1`
   * 새 수식 만들기: `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * 
         [!UICONTROL Format]: `Currency`
   * 새 수식 만들기:**% 할인**
      * 공식: `(C / (B - C))`
      * 
         [!UICONTROL Format]: `Percentage`
   * 새 수식 만들기: `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
         [!UICONTROL Format]: `Percentage`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 간격]: `None`
   * 

      [!UICONTROL 차트 유형]: `Table`








* **첫 번째 주문 쿠폰별 평균 라이프타임 매출**
   * [!UICONTROL Metric]:**평균 라이프타임 매출**
      * 필터 추가:
         * [`A`] `coupon_code` **IS**`[NULL]`
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


* **쿠폰/비쿠폰 획득별 신규 고객**
   * 지표 `1`: `New customers`
      * 필터 추가:
         * [`A`] `Customer's first order's coupon_code` **아님** `[NULL]`
      * [!UICONTROL Rename]: `Coupon acquisition customer`
   * 지표 `2`: `New customers`
      * 필터 추가:
         * [`A`] `coupon_code` **IS**`[NULL]`
      * [!UICONTROL Rename]: `Non-coupon acquisition customer`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`





보고서를 작성한 후 대시보드에서 보고서를 구성하는 방법에 대해서는 이 항목 상단의 이미지를 참조하십시오.
