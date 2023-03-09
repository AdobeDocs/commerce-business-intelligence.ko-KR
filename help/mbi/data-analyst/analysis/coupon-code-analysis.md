---
title: 쿠폰 성능
description: 쿠폰 성능 분석에 대해 알아보십시오.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 0%

---

# 고급 쿠폰 코드 분석

비즈니스의 쿠폰 성능을 이해하는 것은 주문을 세그먼트화하고 고객을 더 잘 이해할 수있는 흥미로운 방법입니다. 이 문서에서는 쿠폰을 사용하여 획득하는 고객, 일반적인 쿠폰 사용을 수행하고 추적하는 방법을 이해하는 분석을 만드는 단계를 안내합니다.

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

이 분석에는 다음이 포함됩니다. [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md).

## 시작

첫 번째 단계로, 다음 열이 Data Warehouse에 동기화되어 있는지 확인해야 합니다. 그렇지 않은 경우 계속 진행하여 &quot;데이터 관리&quot; > &quot;Data Warehouse&quot;로 이동한 다음 다음을 동기화하여 추적하십시오.

* **sales\_flat\_order** 표
* **coupon\_code**
* **base\_discount\_amount**

## 계산된 열

게스트 주문 정책에 관계없이 생성할 열:

* `sales\_flat\_order` 표
* **쿠폰이 적용되었습니까?**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`
   * 
      [!UICONTROL 데이터 유형]: `String`
   * [!UICONTROL Calculation]: 다음의 경우 `A` 이(가) null이면 `No coupon` else `Coupon` 종료


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
   * 이벤트 등급: `created\_at`
   * [!UICONTROL Filters]: `Orders we count` 필터 세트

게스트 주문이 지원되지 않는 경우 생성할 추가 열:

* `customer\_entity` 표
   * **고객의 첫 주문에 쿠폰이 포함되었습니까? (쿠폰/쿠폰 없음)**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * 선택 [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`
   * **고객 퍼스트 오더 쿠폰**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 선택 [!UICONTROL column]: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`
   * **사용된 고객 라이프타임 쿠폰 수**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`
   * **쿠폰 획득 고객 또는 비쿠폰 획득 고객**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
      * 
         [!UICONTROL 데이터 유형]: `String`
      * [!UICONTROL Calculation]: **A=&#39;쿠폰&#39;, &#39;쿠폰취득고객&#39;, 기타 &#39;비쿠폰취득고객&#39;이 종료되는 경우**
   * **쿠폰이 포함된 고객 주문 비율**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`
      * 
         [!UICONTROL 데이터 유형]: `Decimal`
      * [!UICONTROL Calculation]: **A가 null이거나 B가 null이거나 B=0인 경우 A/B가 종료되고 A/B가 종료됨**
   * **고객의 쿠폰 사용**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`
      * 
         [!UICONTROL 데이터 유형]: `String`
      * [!UICONTROL Calculation]: **A가 null일 때 A=0이면 &#39;쿠폰을 사용하지 않음&#39;이 되고 A&lt;0.5이면 &#39;주로 전체 가격&#39;이 되고 A=0.5이면 &#39;50/50&#39;이 되고 A=1이면 &#39;쿠폰만&#39;이 되고 A>0.5이면 &#39;주로 쿠폰&#39; 기타 &#39;정의되지 않음&#39;이 종료됨**









* `sales\_flat\_order` 표
   * **고객의 첫 주문에 쿠폰이 포함되었습니까? (쿠폰/쿠폰 없음)**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 선택 [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^
   * **고객 퍼스트 오더 쿠폰**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 선택 [!UICONTROL column]: `Customer's first order coupon?`


게스트 주문이 지원되지 않는 경우 생성할 추가 열:

* `sales\_flat\_order` 표
   * **고객의 첫 주문에 쿠폰이 포함되었습니까? (쿠폰/쿠폰 없음)** **-** 분석가가 \[COUPON ANALYSIS\] 티켓의 일부로 생성함
   * **고객 퍼스트 오더 쿠폰**{::}**-** 분석가가 \[COUPON ANALYSIS\] 티켓의 일부로 생성함

* **사용된 고객 라이프타임 쿠폰 수**{::}**-** 분석가가 \[COUPON ANALYSIS\] 티켓의 일부로 생성함
* **쿠폰 획득 고객 또는 비쿠폰 획득 고객**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
   * 
      [!UICONTROL 데이터 유형]: `String`
   * [!UICONTROL Calculation]: **A=&#39;쿠폰&#39;, &#39;쿠폰취득고객&#39;, 기타 &#39;비쿠폰취득고객&#39;이 종료되는 경우**


* **쿠폰이 포함된 고객 주문 비율**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`
   * 
      [!UICONTROL 데이터 유형]: `Decimal`
   * [!UICONTROL Calculation]: **A가 null이거나 B가 null이거나 B=0인 경우 A/B가 종료되고 A/B가 종료됨**


* **고객의 쿠폰 사용**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`
   * 
      [!UICONTROL 데이터 유형]: `String`
   * [!UICONTROL Calculation]: **A가 null일 때 A=0이면 &#39;쿠폰을 사용하지 않음&#39;이 되고 A&lt;0.5이면 &#39;주로 전체 가격&#39;이 되고 A=0.5이면 &#39;50/50&#39;이 되고 A=1이면 &#39;쿠폰만&#39;이 되고 A>0.5이면 &#39;주로 쿠폰&#39; 기타 &#39;정의되지 않음&#39;이 종료됨**


## 지표

* **쿠폰 할인 금액**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* 다음에서 `sales\_flat\_order` 표
* 이 지표는 다음을 수행합니다. **합계**
* 다음에서 `discount\_amount` 열
* 정렬 기준: `created\_at` timestamp
* [!UICONTROL Filter]:

* **사용된 쿠폰 수**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* 다음에서 `sales\_flat\_order` 표
* 이 지표는 다음을 수행합니다. **카운트**
* 다음에서 `entity\_id` 열
* 정렬 기준: `created\_at` timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>다음을 확인하십시오. [새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에

## 보고서

* **쿠폰 획득 및 비쿠폰 획득 고객의 %**
   * [!UICONTROL Metric]: `New customers`

* 지표 `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` 또는 `Non coupon acquisition customer`
* 

   [!UICONTROL 차트 유형]: `Pie`

* **쿠폰 획득 및 비쿠폰 획득 고객 수**
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
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Scalar`

* **평균 라이프타임 수익: 비쿠폰 Acq. (90일 이상)**
   * [!UICONTROL Metric]: 평균 라이프타임 수익
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 포함된 쿠폰 (쿠폰 / 쿠폰 없음) = 쿠폰 없음

* 지표 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Scalar`

* **1순위 쿠폰별 평균 라이프타임 수익**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 지표 `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* 

   [!UICONTROL 차트 유형]: `Column`

>[!NOTE]
>
>많은 쿠폰 코드가 있는 경우, 많은 클라이언트가 하는 것처럼, 평균 라이프타임 수익별로 정렬된 상위 10과 같은 상위/하위를 적용하려고 합니다.

* **반복 주문 가능성: 쿠폰 획득**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 포함 쿠폰 (쿠폰 / 쿠폰 없음) = 쿠폰
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 포함 쿠폰 (쿠폰 / 쿠폰 없음) = 쿠폰
      * 고객의 마지막 주문입니까? = 아니요
   * 
      [!UICONTROL 공식]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * 다음에서 통계적으로 중요한 숫자 선택: `Customer's by lifetime orders` 차트. 차트를 볼 때 버킷에 30명 이상의 고객이 있는 주문 번호를 찾는 것이 좋습니다. 데이터 세트에 따라, 이는 많은 수일 수 있으므로 1-10을 자유롭게 추가할 수 있습니다.


* 지표 `A`: `Number of orders`
* 지표 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
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
   * 
      [!UICONTROL 공식]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * 다음에서 통계적으로 중요한 숫자 선택: `Customer's by lifetime orders` chart 또는 1-5.



* 지표 `A`: `Number of orders`
* 지표 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
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
   * 
      [!UICONTROL 공식]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* 지표 `A`: `Coupon-acquired customers`
* 지표 `B`: `Number of repeat orders`
* 지표 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Table` (더 나은 시각화를 위해 이 테이블의 위치를 바꿀 수 있음)

* **비쿠폰 획득 고객의 쿠폰 사용률(반복 주문)**
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
   * 
      [!UICONTROL 공식]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* 지표 `A`: `Non-coupon-acquired customers`
* 지표 `B`: `Number of repeat orders`
* 지표 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Table` (더 나은 시각화를 위해 이 테이블의 위치를 바꿀 수 있음)

* **쿠폰 사용 세부 정보(최초 주문)**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 = 1
      * 이 쿠폰이 포함된 주문 수 > 10
   * 
      [!UICONTROL 지표]: `Revenue`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 = 1
      * 이 쿠폰이 포함된 주문 수 > 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 = 1
      * 이 쿠폰이 포함된 주문 수 > 10
   * [!UICONTROL Formula]: `B-C` (C가 음수인 경우), B+C (C가 양인 경우)
   * 

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
* 
   [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `coupon code`
* 

   [!UICONTROL 차트 유형]: `Table`
>[!NOTE]
>
>&quot;이 쿠폰으로 주문 수&quot;에 대한 10개 수량은 임의적입니다. 이 필터에 가장 적합한 수량을 자유롭게 사용하십시오.

* **쿠폰이 포함된 주문 수(항상)**
   * [!UICONTROL Metric]: `Number of coupons used`

* 지표 `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Scalar`

* **쿠폰이 포함된 주문의 순 수익(항상)**
   * 
      [!UICONTROL 지표]: `Revenue`
   * [!UICONTROL Filter]:
      * 쿠폰이 적용되었습니까? (쿠폰/쿠폰 없음) = 쿠폰

* 지표 `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Scalar`

* **쿠폰 할인(항상)**
   * [!UICONTROL Metric]: `Number of coupons used`

* 지표 `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Scalar`

* **쿠폰이 포함된 주문 및 없는 주문 수**
   * [!UICONTROL Metric]: `Number of orders`

* 지표 `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
   [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **반복 사용자 간 쿠폰 사용**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 고객의 라이프타임 주문 수 > 1

* 지표 `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* 

   [!UICONTROL 차트 유형]: `Pie`

* **쿠폰 사용 세부 정보**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * 이 쿠폰이 포함된 주문 수 > 10
   * 
      [!UICONTROL 지표]: `Revenue`
   * [!UICONTROL Filter]:
      * 이 쿠폰이 포함된 주문 수 > 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 이 쿠폰이 포함된 주문 수 > 10
   * [!UICONTROL Formula]: `B-C` (if `C` 음수); `B+C` (if `C` 긍정적임)
   * 

      [!UICONTROL 형식]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` (if `C` 음수); `C/(B+C)` (if `C` 긍정적임)
   * 

      [!UICONTROL 형식]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * 이 쿠폰이 포함된 주문 수 > 10
   * 
      [!UICONTROL 공식]: `C/A`
   * 

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
* 
   [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
   [!UICONTROL 차트 유형]: `Table`

>[!NOTE]
>
>&quot;이 쿠폰으로 주문 수&quot;에 대한 10개 수량은 임의적입니다. 이 필터에 가장 적합한 수량을 자유롭게 사용하십시오.

모든 보고서를 컴파일한 후 원하는 대로 대시보드에서 구성할 수 있습니다. 결과는 페이지 상단에 있는 이미지와 비슷할 수 있습니다.

이 분석을 작성하는 동안 질문이 발생하거나 Professional Services 팀의 도움을 얻고자 하는 경우 [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
