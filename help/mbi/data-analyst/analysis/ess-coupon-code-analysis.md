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

* 할인은 `base_grand_total` 금액(Commerce Intelligence의 `Revenue` 지표)에 반영됩니다.
* 쿠폰 코드는 `coupon_code` 필드에 저장됩니다. 이 필드가 NULL(비어 있음)이면 주문에 연결된 쿠폰이 없습니다.
* 할인된 금액이 `base_discount_amount`에 저장됩니다. 구성에 따라 이 값이 음수 또는 양수로 표시될 수 있습니다.

Commerce 2.4.7부터 고객은 주문에 두 개 이상의 쿠폰 코드를 적용할 수 있습니다. 이 경우:

* 적용된 모든 쿠폰 코드는 `sales_order_coupons`의 `coupon_code` 필드에 저장됩니다. 적용된 첫 번째 쿠폰 코드도 `sales_order`의 `coupon_code` 필드에 저장됩니다. 이 필드가 NULL(비어 있음)이면 주문에 연결된 쿠폰이 없습니다.

## 지표 작성

첫 번째 단계는 다음 단계로 새 지표를 구성하는 것입니다.

* **[!UICONTROL Manage Data > Metrics > Create New Metric]**(으)로 이동합니다.

* `sales_order` 선택.
* 이 지표는 **created_at**&#x200B;에 의해 정렬된 **base_discount_amount** 열에서 **Sum**&#x200B;을 수행합니다.
   * [!UICONTROL Filters]:
      * `Orders we count`(저장된 필터 집합) 추가
      * 다음을 추가합니다.
         * `coupon_code`**이(가) 아님**`[NULL]`
      * 지표에 `Coupon discount amount`과(와) 같은 이름을 지정하십시오.

## 대시보드 만들기

* 지표가 생성되면 다음 작업을 수행하십시오.
   * [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**로 이동합니다.
   * 대시보드에 `_Coupon Analysis_` 등의 이름을 지정하십시오.

* 여기서 모든 보고서를 만들고 추가할 수 있습니다.

## 보고서 작성 중

* **새 보고서:**

>[!NOTE]
>
>각 보고서의 [!UICONTROL Time Period]**이(가) `All-time`(으)로 나열됩니다. 분석 요구 사항에 맞게 자유롭게 변경하십시오. Adobe은 `All time`, `Year-to-date` 또는 `Last 365 days`과(와) 같이 이 대시보드에 있는 모든 보고서를 동일한 기간에 포함하도록 권장합니다.

* **쿠폰이 포함된 주문**
   * &#x200B;

     [!UICONTROL 지표]: `Orders`
      * 필터 추가:
         * [`A`] `coupon_code` **이(가) 아님** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;

     [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **쿠폰 없는 주문**
   * &#x200B;

     [!UICONTROL 지표]: `Orders`
      * 필터 추가:
         * [`A`] `coupon_code` **IS** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;

     [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **쿠폰이 포함된 주문 순 수익**
   * &#x200B;

     [!UICONTROL 지표]: `Revenue`
      * 필터 추가:
         * [`A`] `coupon_code` **이(가) 아님** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;

     [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **쿠폰 할인**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;

     [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **평균 라이프타임 수익: 쿠폰을 획득한 고객**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 필터 추가:
         * [`A`] `Customer's first order's coupon_code` **이(가) 아님** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;

     [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **평균 라이프타임 수익: 쿠폰을 받지 않은 고객이 획득한 금액**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 필터 추가:
         * [A] `Customer's first order's coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;

     [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **쿠폰 사용 세부 정보(처음 주문)**
   * 지표 `1`: `Orders`
      * 필터 추가:
         * [`A`] `coupon_code` **이(가) 아님**`[NULL]`
         * [`B`] `Customer's order number` **같음** `1`

   * 지표 `2`: `Revenue`
      * 필터 추가:
         * [`A`] `coupon_code` **이(가) 아님**`[NULL]`
         * [`B`] `Customer's order number` **같음** `1`

      * 이름 바꾸기: `Net revenue`

   * 지표 `3`: `Coupon discount amount`
      * 필터 추가:
         * [`A`] `coupon_code` **이(가) 아님**`[NULL]`
         * [`B`] `Customer's order number` **같음** `1`

   * 수식 만들기: `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * &#x200B;

        [!UICONTROL Format]: `Currency`

   * 수식 만들기: **% 할인**
      * 수식: `(C / (B - C))`
      * &#x200B;

        [!UICONTROL Format]: `Percentage`

   * 수식 만들기: `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * &#x200B;

        [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;

     [!UICONTROL 간격]: `None`
   * &#x200B;

     [!UICONTROL 차트 유형]: `Table`

* **첫 주문 쿠폰별 평균 라이프타임 수익**
   * [!UICONTROL Metric]:**평균 라이프타임 수익**
      * 필터 추가:
         * [`A`] `coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;

     [!UICONTROL 간격]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **쿠폰 사용 세부 정보(처음 주문)**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 필터 추가:
         * [`A`] `Customer's first order's coupon_code` **이(가) 아님** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;

     [!UICONTROL 간격]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * &#x200B;

     [!UICONTROL 차트 유형]: **Column**

* **쿠폰으로 신규 고객/비쿠폰 고객 확보**
   * 지표 `1`: `New customers`
      * 필터 추가:
         * [`A`] `Customer's first order's coupon_code` **이(가) 아님** `[NULL]`

      * [!UICONTROL Rename]: `Coupon acquisition customer`

   * 지표 `2`: `New customers`
      * 필터 추가:
         * [`A`] `coupon_code` **IS**`[NULL]`

      * [!UICONTROL Rename]: `Non-coupon acquisition customer`

   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`

보고서를 작성한 후 대시보드에서 보고서를 구성하는 방법에 대한 자세한 내용은 이 항목 맨 위에 있는 이미지를 참조하십시오.

>[!NOTE]
>
>Adobe Commerce 2.4.7부터 고객은 **quote_coupons** 및 **sales_order_coupons** 테이블을 사용하여 고객이 여러 쿠폰을 사용하는 방법에 대한 통찰력을 얻을 수 있습니다.

![](../../assets/multicoupon_relationship_tables.png)
