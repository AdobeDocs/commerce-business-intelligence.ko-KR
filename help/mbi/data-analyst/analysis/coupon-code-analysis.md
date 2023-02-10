---
title: 쿠폰 성능
description: 쿠폰 성과 분석에 대해 알아봅니다.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 0%

---

# 고급 쿠폰 코드 분석

비즈니스의 쿠폰 성능을 이해하는 것은 주문을 세분화하고 고객을 더 잘 이해할 수 있는 흥미로운 방법입니다. 이 문서는 쿠폰 사용을 통해 어떤 고객이 쿠폰을 사용하는지, 쿠폰 사용방법을 수행하고, 일반적인 쿠폰 사용을 추적하는 분석을 만드는 단계를 안내합니다.

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

이 분석에는 다음이 포함됩니다 [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md).

## 시작하기

첫 번째 단계에서는 다음 열이 Data Warehouse에 동기화되었는지 확인해야 합니다. 표시되지 않으면 &quot;데이터 관리&quot; > &quot;Data Warehouse&quot;으로 이동하여 다음을 동기화하여 계속 추적합니다.

* **sales\_flat\_order** 표
* **coupon\_code**
* **base\_discount\_amount**

## 계산된 열

게스트 주문 정책에 관계없이 생성할 열:

* `sales\_flat\_order` 표
* **주문서에 쿠폰이 적용되어 있습니까?**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]: 케이스 `A` 이면 null입니다. `No coupon` else `Coupon` end


* **\[INPUT\] customer\_id - 쿠폰 코드**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`
   * [!UICONTROL Datatype]: 문자열
   * [!UICONTROL Calculation]:: `concat(A,' - ',B)`


* **이 쿠폰이 있는 주문 수**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * 이벤트 소유자:`INPUT customer_id - coupon code`
   * 이벤트 등급: `created\_at`
   * [!UICONTROL Filters]: `Orders we count` 필터 세트

게스트 주문이 지원되지 않는 경우 생성할 추가 열:

* `customer\_entity` 표
   * **고객의 첫 주문에는 쿠폰이 포함되어 있나요? (쿠폰/쿠폰 없음)**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * 선택 [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`
   * **고객의 최초 주문 쿠폰**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 선택 [!UICONTROL column]: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`
   * **사용된 고객의 라이프타임 쿠폰 수**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`
   * **쿠폰 획득 고객 또는 쿠폰 획득 고객**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
      * [!UICONTROL Datatype]:: `String`
      * [!UICONTROL Calculation]: **대/소문자 A=&#39;Coupon&#39;, &#39;Coupon 획득 고객&#39;, &#39;Non-coupon acquisition customer&#39; 종료**
   * **쿠폰이 있는 고객 주문 비율**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`
      * [!UICONTROL Datatype]:: `Decimal`
      * [!UICONTROL Calculation]: **A가 null이거나 B가 null이거나 B=0이고 Null else A/B 종료일 경우**
   * **고객의 쿠폰 사용**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`
      * [!UICONTROL Datatype]:: `String`
      * [!UICONTROL Calculation]: **A가 null이면 A=0이면 null이고, A=0.5이면 &#39;주로 전체 가격&#39;이고, A=0.5이면 &#39;50/50&#39;이면 &#39;주로 전체 가격&#39;이면 A=0.5이면 &#39;주로 전체 가격&#39;이고, A>0.5에서 &#39;주로 쿠폰&#39;, &#39;대부분 정의되지 않음&#39;이 끝나는 경우 A=0이면 null이면 null입니다**









* `sales\_flat\_order` 표
   * **고객의 첫 번째 주문에는 쿠폰이 포함되어 있습니까? (쿠폰/쿠폰 없음)**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 선택 [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^
   * **고객의 최초 주문 쿠폰**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 선택 [!UICONTROL column]: `Customer's first order coupon?`


게스트 주문이 지원되지 않는 경우 생성할 추가 열:

* `sales\_flat\_order` 표
   * **고객의 첫 주문에는 쿠폰이 포함되어 있나요? (쿠폰/쿠폰 없음)** **-** 분석가가 \[COUPON ANALYSIS\] 티켓의 일부로 만들었습니다.
   * **고객의 최초 주문 쿠폰**{::}**-** 분석가가 \[COUPON ANALYSIS\] 티켓의 일부로 만들었습니다.

* **사용된 고객의 라이프타임 쿠폰 수**{::}**-** 분석가가 \[COUPON ANALYSIS\] 티켓의 일부로 만들었습니다.
* **쿠폰 획득 고객 또는 쿠폰 획득 고객**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]: **대/소문자 A=&#39;Coupon&#39;, &#39;Coupon 획득 고객&#39;, &#39;Non-coupon acquisition customer&#39; 종료**


* **쿠폰이 있는 고객 주문 비율**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`
   * [!UICONTROL Datatype]:: `Decimal`
   * [!UICONTROL Calculation]: **A가 null이거나 B가 null이거나 B=0이고 Null else A/B 종료일 경우**


* **고객의 쿠폰 사용**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]: **A가 null이면 A=0이면 null이고, A=0.5이면 &#39;주로 전체 가격&#39;이고, A=0.5이면 &#39;50/50&#39;이면 &#39;주로 전체 가격&#39;이면 A=0.5이면 &#39;주로 전체 가격&#39;이고, A>0.5에서 &#39;주로 쿠폰&#39;, &#39;대부분 정의되지 않음&#39;이 끝나는 경우 A=0이면 null이면 null입니다**


## 지표

* **쿠폰 할인 금액**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* 에서 `sales\_flat\_order` 표
* 이 지표는 다음을 수행합니다 **합계**
* 설정 `discount\_amount` 열
* 정렬 기준 `created\_at` timestamp
* [!UICONTROL Filter]:

* **사용된 쿠폰 수**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* 에서 `sales\_flat\_order` 표
* 이 지표는 다음을 수행합니다 **카운트**
* 설정 `entity\_id` 열
* 정렬 기준 `created\_at` timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>다음을 확인하십시오 [새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에

## 보고서

* **쿠폰 획득 및 쿠폰 미획득 고객 %**
   * [!UICONTROL Metric]: `New customers`

* 지표 `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` 또는 `Non coupon acquisition customer`
* 

   [!UICONTROL 차트 유형]: `Pie`

* **쿠폰 획득 및 쿠폰 미획득 고객 수**
   * [!UICONTROL Metric]: `New customers`

* 지표 A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` 또는 `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **평균 라이프타임 매출: 쿠폰 Acq. (90일 이상 연령)**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 쿠폰(쿠폰/쿠폰 없음) = 쿠폰 포함

* 지표 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Scalar`

* **평균 라이프타임 매출: 쿠폰 Acq가 아닙니다. (90일 이상 연령)**
   * [!UICONTROL Metric]: 평균 라이프타임 매출
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 쿠폰(쿠폰/쿠폰 없음) = 쿠폰 없음

* 지표 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Scalar`

* **첫 번째 주문 쿠폰별 평균 라이프타임 매출**
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
>많은 수의 쿠폰 코드가 있는 경우, 대부분의 클라이언트가 하는 것처럼 평균 라이프타임 매출로 정렬된 상위 10위와 같은 상위/하위를 적용하려고 합니다

* **반복 주문 가능성: 쿠폰 인수**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 쿠폰(쿠폰/쿠폰 없음) = 쿠폰 포함
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 쿠폰(쿠폰/쿠폰 없음) = 쿠폰 포함
      * 고객의 마지막 주문입니까? = 아니요
   * 
      [[!UICONTROL 공식]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * 통계적으로 중요한 숫자를 선택합니다. `Customer's by lifetime orders` 차트. 차트를 볼 때, 좋은 규칙으로, 일반적으로 버킷에 30명 이상의 고객이 있는 주문 번호를 찾습니다. 데이터 세트에 따라 숫자가 많을 수 있으므로 1-10을 자유롭게 추가할 수 있습니다.


* 지표 `A`: `Number of orders`
* 지표 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **반복 순서 확률: 쿠폰 미획득**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 쿠폰(쿠폰/쿠폰 없음) = 쿠폰 없음
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 첫 번째 주문에 쿠폰(쿠폰/쿠폰 없음) = 쿠폰 없음
      * 고객의 마지막 주문입니까? = 아니요
   * 
      [[!UICONTROL 공식]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * 통계적으로 중요한 숫자를 선택합니다. `Customer's by lifetime orders` 차트 또는 1-5.



* 지표 `A`: `Number of orders`
* 지표 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **쿠폰 획득 고객의 쿠폰 사용율(반복 주문)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 쿠폰 획득 고객 또는 쿠폰 획득 고객 = 쿠폰 획득
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 > 1
      * 고객의 첫 주문에는 쿠폰이 포함되어 있나요? (쿠폰/쿠폰 없음) = 쿠폰
   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 > 1
      * 고객의 첫 주문에는 쿠폰이 포함되어 있나요? (쿠폰/쿠폰 없음) = 쿠폰
      * 주문서에 쿠폰이 적용되어 있습니까? (쿠폰/쿠폰 없음) = 쿠폰
   * 
      [[!UICONTROL 공식]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* 지표 `A`: `Coupon-acquired customers`
* 지표 `B`: `Number of repeat orders`
* 지표 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Table` (더 나은 시각화를 위해 이 표를 다른 테이블로 전환할 수 있음)

* **쿠폰이 획득되지 않은 고객의 쿠폰 사용율(반복 주문)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 쿠폰 획득 고객 또는 쿠폰 획득 고객 = 쿠폰 미획득
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 > 1
      * 고객의 첫 주문에는 쿠폰이 포함되어 있나요? (쿠폰/쿠폰 없음) = 쿠폰 없음
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 > 1
      * 고객의 첫 주문에는 쿠폰이 포함되어 있나요? (쿠폰/쿠폰 없음) = 쿠폰 없음
      * 주문서에 쿠폰이 적용되어 있습니까? (쿠폰/쿠폰 없음) = 쿠폰
   * 
      [[!UICONTROL 공식]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* 지표 `A`: `Non-coupon-acquired customers`
* 지표 `B`: `Number of repeat orders`
* 지표 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Table` (더 나은 시각화를 위해 이 표를 다른 테이블로 전환할 수 있음)

* **쿠폰 사용 세부 정보(최초 주문)**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 = 1
      * 이 쿠폰이 있는 주문 수 10 이상
   * 
      [[!UICONTROL 지표]: `Revenue`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 = 1
      * 이 쿠폰이 있는 주문 수 10 이상
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 = 1
      * 이 쿠폰이 있는 주문 수 10 이상
   * [!UICONTROL Formula]: `B-C` 다. 음수인 경우) B+C(C가 양수인 경우)
   * 

      [!UICONTROL 형식]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * 고객의 주문 번호 = 1
      * 이 쿠폰이 있는 주문 수 10 이상




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
>&quot;이 쿠폰이 있는 주문 수&quot;에 대한 10의 수량은 임의의 수량입니다. 이 필터에 가장 적절한 양을 자유롭게 사용하십시오.

* **쿠폰이 있는 주문 수(모든 시간)**
   * [!UICONTROL Metric]: `Number of coupons used`

* 지표 `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Scalar`

* **쿠폰이 있는 주문에서 순 수익(항상)**
   * 
      [[!UICONTROL 지표]: `Revenue`
   * [!UICONTROL Filter]:
      * 주문서에 쿠폰이 적용되어 있습니까? (쿠폰/쿠폰 없음) = 쿠폰

* 지표 `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Scalar`

* **쿠폰에서 할인(항상)**
   * [!UICONTROL Metric]: `Number of coupons used`

* 지표 `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL 간격]: `None`
* 

   [!UICONTROL 차트 유형]: `Scalar`

* **쿠폰이 있는 주문 및 없는 주문 수**
   * [!UICONTROL Metric]: `Number of orders`

* 지표 `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
   [!UICONTROL 간격]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **반복 사용자 간의 쿠폰 사용**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 고객의 주문 라이프타임 번호 > 1

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
      * 이 쿠폰이 있는 주문 수 10 이상
   * 
      [[!UICONTROL 지표]: `Revenue`
   * [!UICONTROL Filter]:
      * 이 쿠폰이 있는 주문 수 10 이상
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 이 쿠폰이 있는 주문 수 10 이상
   * [!UICONTROL Formula]: `B-C` (다음과 같은 경우) `C` 는 음수입니다. `B+C` (다음과 같은 경우) `C` is positive)
   * 

      [!UICONTROL 형식]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` (다음과 같은 경우) `C` 는 음수입니다. `C/(B+C)` (다음과 같은 경우) `C` is positive)
   * 

      [!UICONTROL 형식]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * 이 쿠폰이 있는 주문 수 10 이상
   * 
      [[!UICONTROL 공식]: `C/A`
   * 

      [!UICONTROL 형식]: `Currency`

   * [!UICONTROL Metric]: `Distinct buyers`
   * [!UICONTROL Filter]:
      * 이 쿠폰이 있는 주문 수 10 이상





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
>&quot;이 쿠폰이 있는 주문 수&quot;에 대한 10의 수량은 임의의 수량입니다. 이 필터에 가장 적절한 양을 자유롭게 사용하십시오.

모든 보고서를 컴파일한 후 대시보드에서 원하는 대로 구성할 수 있습니다. 최종 결과는 페이지 상단에 있는 이미지와 같을 수 있습니다.

이 분석을 작성하는 동안 질문이 있거나 전문 서비스 팀에 참여하려는 경우 [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
