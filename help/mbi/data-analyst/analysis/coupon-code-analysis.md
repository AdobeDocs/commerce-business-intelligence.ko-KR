---
title: 쿠폰 성능
description: 쿠폰 성능 분석에 대해 알아보십시오.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: d8fc96a58b72c601a5700f35ea1f3dc982d76571
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# 고급 쿠폰 코드 분석

비즈니스의 쿠폰 성능을 이해하는 것은 주문을 세그먼트화하고 고객을 더 잘 이해할 수있는 흥미로운 방법입니다. 이 항목에서는 쿠폰을 사용하여 획득하는 고객, 일반적인 쿠폰 사용을 어떻게 수행하고 추적하는지를 이해하기 위한 분석을 만드는 단계를 안내합니다.

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

이 분석에는 [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md)이(가) 포함되어 있습니다.

## 시작

첫 번째 단계로, 다음 열이 Data Warehouse에 동기화되어 있는지 확인해야 합니다. 그렇지 않은 경우 계속 진행하여 `Manage Data` > `Data Warehouse`(으)로 이동한 다음 내용을 동기화하여 추적하십시오.

* **sales\_flat\_order** 테이블
* **coupon\_code**
* **base\_discount\_amount**

## 계산된 열

게스트 주문 정책에 관계없이 생성할 열:

* `sales\_flat\_order` 테이블
* **쿠폰이 적용되었습니까?**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`

   * &#x200B;

     [!UICONTROL 데이터 유형]: `String`
   * [!UICONTROL Calculation]: `A`이(가) null인 경우 `No coupon`이(가) 아니면 `Coupon`이(가) 끝남

* **\[INPUT\] customer\_id - 쿠폰 코드**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`

   * [!UICONTROL Datatype] 문자열
   * [!UICONTROL Calculation]: `concat(A,' - ',B)`

* **이 쿠폰이 포함된 주문 수**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * 이벤트 소유자:`INPUT customer_id - coupon code`
   * 이벤트 순위: `created\_at`
   * [!UICONTROL Filters]: `Orders we count` 필터 집합

게스트 주문이 지원되지 않는 경우 생성할 추가 열:

* `customer\_entity` 테이블
   * **고객의 첫 주문에 쿠폰이 포함되었습니까? (쿠폰/쿠폰 없음)**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * [!UICONTROL column] 선택: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`

   * **고객 첫 주문 쿠폰**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL column] 선택: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`

   * **사용된 고객의 라이프타임 쿠폰 수**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`

   * **쿠폰 획득 고객 또는 비쿠폰 획득 고객**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

      * &#x200B;

        [!UICONTROL 데이터 유형]: `String`
      * [!UICONTROL Calculation]: **A=&#39;Coupon&#39;, &#39;Coupon acquisition customer&#39;, 기타 &#39;Non-coupon acquisition customer&#39;인 경우**

   * **쿠폰이 포함된 고객 주문 비율**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`

      * &#x200B;

        [!UICONTROL 데이터 유형]: `Decimal`
      * [!UICONTROL Calculation]: **A가 null이거나 B가 null이거나 B=0인 경우 A/B가 null이 됩니다.**

   * **고객의 쿠폰 사용**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`

      * &#x200B;

        [!UICONTROL 데이터 유형]: `String`
      * [!UICONTROL Calculation]: **A가 null이면 null, A=0이면 &#39;쿠폰 사용 안 함&#39;, A&lt;0.5이면 &#39;주로 전체 가격&#39;, A=0.5이면 &#39;50/50&#39;, A=1이면 &#39;쿠폰만&#39;, A>0.5이면 &#39;주로 쿠폰&#39;, 기타 &#39;정의되지 않음&#39; 종료**

* `sales\_flat\_order` 테이블
   * **고객의 첫 주문에 포함된 쿠폰이 있습니까? (쿠폰/쿠폰 없음)**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL column] 선택: `Customer's first order included a coupon? (Coupon/No coupon)`
^

   * **고객 첫 주문 쿠폰**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL column] 선택: `Customer's first order coupon?`

게스트 주문이 지원되지 않는 경우 생성할 추가 열:

* `sales\_flat\_order` 테이블
   * **고객의 첫 주문에 쿠폰이 포함되었습니까? (쿠폰/쿠폰 없음)** **-** 분석가가 \[COUPON ANALYSIS\] 티켓의 일부로 만들었습니다.
   * **고객의 첫 번째 주문 쿠폰**{:}**-** 분석가가 \[COUPON ANALYSIS\] 티켓의 일부로 만들었습니다.

* **고객의 라이프타임 쿠폰 수**{:}**-** 분석가가 \[COUPON ANALYSIS\] 티켓의 일부로 만든 쿠폰
* **쿠폰 획득 고객 또는 비쿠폰 획득 고객**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

   * &#x200B;

     [!UICONTROL 데이터 유형]: `String`
   * [!UICONTROL Calculation]: **A=&#39;Coupon&#39;, &#39;Coupon acquisition customer&#39;, 기타 &#39;Non-coupon acquisition customer&#39;인 경우**

* **쿠폰이 포함된 고객 주문 비율**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`

   * &#x200B;

     [!UICONTROL 데이터 유형]: `Decimal`
   * [!UICONTROL Calculation]: **A가 null이거나 B가 null이거나 B=0인 경우 A/B가 null이 됩니다.**

* **고객의 쿠폰 사용**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`

   * &#x200B;

     [!UICONTROL 데이터 유형]: `String`
   * [!UICONTROL Calculation]: **A가 null이면 null, A=0이면 &#39;쿠폰 사용 안 함&#39;, A&lt;0.5이면 &#39;주로 전체 가격&#39;, A=0.5이면 &#39;50/50&#39;, A=1이면 &#39;쿠폰만&#39;, A>0.5이면 &#39;주로 쿠폰&#39;, 기타 &#39;정의되지 않음&#39; 종료**

## 지표

* **쿠폰 할인 금액**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* `sales\_flat\_order` 테이블에서
* 이 지표는 **합계**&#x200B;를 수행합니다.
* `discount\_amount` 열에서
* `created\_at` 타임스탬프로 정렬됨
* [!UICONTROL Filter]:

* **사용된 쿠폰 수**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* `sales\_flat\_order` 테이블에서
* 이 지표는 **Count**&#x200B;을 수행합니다.
* `entity\_id` 열에서
* `created\_at` 타임스탬프로 정렬됨
* [!UICONTROL Filter]:

>[!NOTE]
>
>새 보고서를 작성하기 전에 [모든 새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md)하십시오.

## 보고서

* **%의 쿠폰 획득 및 비쿠폰 획득 고객**
   * [!UICONTROL Metric]: `New customers`

* 지표 `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` 또는 `Non coupon acquisition customer`
* &#x200B;
  [!UICONTROL 차트 유형]: `Pie`

* **쿠폰을 획득하거나 쿠폰을 획득하지 않은 고객 수**
   * [!UICONTROL Metric]: `New customers`

* 지표 A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` 또는 `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **평균 라이프타임 수익: 쿠폰 Acq. (90일 이상)**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 포함 쿠폰 (쿠폰 / 쿠폰 없음) = 쿠폰

* 지표 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* &#x200B;
  [!UICONTROL 간격]: `None`
* &#x200B;
  [!UICONTROL 차트 유형]: `Scalar`

* **평균 라이프타임 수익: 비쿠폰 Acq. (90일 이상)**
   * [!UICONTROL Metric]: 평균 라이프타임 수익
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 포함된 쿠폰 (쿠폰 / 쿠폰 없음) = 쿠폰 없음

* 지표 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* &#x200B;
  [!UICONTROL 간격]: `None`
* &#x200B;
  [!UICONTROL 차트 유형]: `Scalar`

* **첫 주문 쿠폰별 평균 라이프타임 수익**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 지표 `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* &#x200B;
  [!UICONTROL 차트 유형]: `Column`

>[!NOTE]
>
>많은 쿠폰 코드가 있는 경우, 많은 클라이언트가 하는 것처럼, 평균 라이프타임 수익별로 정렬된 상위 10과 같은 상위/하위를 적용하려고 합니다.

* **순서 반복 가능성: 쿠폰 획득**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 포함 쿠폰 (쿠폰 / 쿠폰 없음) = 쿠폰

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 포함 쿠폰 (쿠폰 / 쿠폰 없음) = 쿠폰
      * 고객의 마지막 주문입니까? = 아니요
   * &#x200B;

     [!UICONTROL 공식]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * `Customer's by lifetime orders` 차트에서 통계적으로 중요한 숫자를 선택하십시오. 차트를 볼 때 버킷에 30명 이상의 고객이 있는 주문 번호를 찾는 것이 좋습니다. 데이터 세트에 따라, 이는 많은 수일 수 있으므로 1-10을 자유롭게 추가할 수 있습니다.

* 지표 `A`: `Number of orders`
* 지표 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **반복 주문 확률: 비쿠폰 획득**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 포함 쿠폰 (쿠폰 / 쿠폰 없음) = 쿠폰 없음

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 포함 쿠폰 (쿠폰 / 쿠폰 없음) = 쿠폰 없음
      * 고객의 마지막 주문입니까? = 아니요

   * &#x200B;

     [!UICONTROL 공식]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * `Customer's by lifetime orders` 차트 또는 1-5에서 통계적으로 중요한 숫자를 선택하세요.

* 지표 `A`: `Number of orders`
* 지표 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **쿠폰을 획득한 고객의 쿠폰 사용률(반복 주문)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 쿠폰 획득 고객 또는 비쿠폰 획득 고객 = 쿠폰 획득

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객 주문 번호 > 1
      * 고객의 첫 주문에 쿠폰이 포함되었습니까? (쿠폰/쿠폰 없음) = 쿠폰

   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * 고객 주문 번호 > 1
      * 고객의 첫 주문에 쿠폰이 포함되었습니까? (쿠폰/쿠폰 없음) = 쿠폰
      * 쿠폰이 적용되었습니까? (쿠폰/쿠폰 없음) = 쿠폰

   * &#x200B;

     [!UICONTROL 공식]: `C/B`
   * [!UICONTROL Format]: `Percentage %`

* 지표 `A`: `Coupon-acquired customers`
* 지표 `B`: `Number of repeat orders`
* 지표 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 간격]: `None`
* &#x200B;
  [!UICONTROL 차트 유형]: `Table` (더 나은 시각화를 위해 이 테이블의 위치를 바꿀 수 있음)

* **쿠폰을 받지 않은 고객의 쿠폰 사용 비율(반복 주문)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 쿠폰 획득 고객 또는 비쿠폰 획득 고객 = 비쿠폰 획득

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객 주문 번호 > 1
      * 고객의 첫 주문에 쿠폰이 포함되었습니까? (쿠폰/쿠폰 없음) = 쿠폰 없음

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객 주문 번호 > 1
      * 고객의 첫 주문에 쿠폰이 포함되었습니까? (쿠폰/쿠폰 없음) = 쿠폰 없음
      * 쿠폰이 적용되었습니까? (쿠폰/쿠폰 없음) = 쿠폰

   * &#x200B;

     [!UICONTROL 공식]: `C/B`
   * [!UICONTROL Format]: `Percentage %`

* 지표 `A`: `Non-coupon-acquired customers`
* 지표 `B`: `Number of repeat orders`
* 지표 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 간격]: `None`
* &#x200B;
  [!UICONTROL 차트 유형]: `Table` (더 나은 시각화를 위해 이 테이블의 위치를 바꿀 수 있음)

* **쿠폰 사용 세부 정보(처음 주문)**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 = 1
      * 이 쿠폰이 포함된 주문 수 > 10

   * &#x200B;

     [!UICONTROL 지표]: `Revenue`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 = 1
      * 이 쿠폰이 포함된 주문 수 > 10

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 = 1
      * 이 쿠폰이 포함된 주문 수 > 10

   * [!UICONTROL Formula]: `B-C`(C가 음수인 경우), B+C(C가 양수인 경우)
   * &#x200B;

     [!UICONTROL 형식]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 = 1
      * 이 쿠폰이 포함된 주문 수 > 10

* 지표 `A`: `First time orders (FTO)`
* 지표 `B`: `Revenue from FTO`
* 지표 `C`: `Discounts applied to FTO`
* [!UICONTROL Formula]: `Gross revenue from FTO`
* 지표 `E`: `Average order value for FTO`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `coupon code`
* &#x200B;
  [!UICONTROL 차트 유형]: `Table`
>[!NOTE]
>
>&quot;이 쿠폰으로 주문 수&quot;에 대한 10개 수량은 임의적입니다. 이 필터에 가장 적합한 수량을 자유롭게 사용하십시오.

* **쿠폰이 포함된 주문 수(항상)**
   * [!UICONTROL Metric]: `Number of coupons used`

* 지표 `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 간격]: `None`
* &#x200B;
  [!UICONTROL 차트 유형]: `Scalar`

* **쿠폰이 있는 주문의 순 매출액(항상)**
   * &#x200B;

     [!UICONTROL 지표]: `Revenue`
   * [!UICONTROL Filter]:
      * 쿠폰이 적용되었습니까? (쿠폰/쿠폰 없음) = 쿠폰

* 지표 `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 간격]: `None`
* &#x200B;
  [!UICONTROL 차트 유형]: `Scalar`

* **쿠폰 할인(항상)**
   * [!UICONTROL Metric]: `Number of coupons used`

* 지표 `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 간격]: `None`
* &#x200B;
  [!UICONTROL 차트 유형]: `Scalar`

* **쿠폰이 포함된 주문 수 및 없는 주문 수**
   * [!UICONTROL Metric]: `Number of orders`

* 지표 `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* &#x200B;
  [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **반복 사용자 간 쿠폰 사용**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 고객의 라이프타임 주문 수 > 1

* 지표 `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* &#x200B;
  [!UICONTROL 차트 유형]: `Pie`

* **쿠폰 사용 세부 정보**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * 이 쿠폰이 포함된 주문 수 > 10

   * &#x200B;

     [!UICONTROL 지표]: `Revenue`
   * [!UICONTROL Filter]:
      * 이 쿠폰이 포함된 주문 수 > 10

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 이 쿠폰이 포함된 주문 수 > 10

   * [!UICONTROL Formula]: `B-C`(`C`이(가) 음수인 경우), `B+C`(`C`이(가) 양수인 경우)
   * &#x200B;

     [!UICONTROL 형식]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)`(`C`이(가) 음수인 경우), `C/(B+C)`(`C`이(가) 양수인 경우)
   * &#x200B;

     [!UICONTROL 형식]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * 이 쿠폰이 포함된 주문 수 > 10

   * &#x200B;

     [!UICONTROL 공식]: `C/A`
   * &#x200B;

     [!UICONTROL 형식]: `Currency`

   * [!UICONTROL Metric]: `Distinct buyers`
   * [!UICONTROL Filter]:
      * 이 쿠폰이 포함된 주문 수 > 10

* 지표 `A`: `Number of orders`
* 지표 `B`: `Net revenue from orders`
* 지표 `C`: `Total discounts applied`
* [!UICONTROL Formula]: `Gross revenue`
* [!UICONTROL Formula]: `% discounted`
* 지표 `F`: `Average net order value`
* [!UICONTROL Formula]: `Average order discount`
* 지표 `H`: `Distinct buyers`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `coupon code`
* &#x200B;
  [!UICONTROL 차트 유형]: `Table`

>[!NOTE]
>
>&quot;이 쿠폰으로 주문 수&quot;에 대한 10개 수량은 임의적입니다. 이 필터에 가장 적합한 수량을 자유롭게 사용하십시오.

모든 보고서를 컴파일한 후 원하는 대로 대시보드에서 구성할 수 있습니다. 결과는 페이지 상단에 있는 이미지와 비슷할 수 있습니다.

이 분석을 작성하는 동안 질문이 있거나 Professional Services 팀에 문의하려는 경우 [지원 팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)하십시오.

>[!NOTE]
>
>Adobe Commerce 2.4.7부터 고객은 **quote_coupons** 및 **sales_order_coupons** 테이블을 사용하여 고객이 여러 쿠폰을 사용하는 방법에 대한 통찰력을 얻을 수 있습니다.

![](../../assets/multicoupon_relationship_tables.png)
