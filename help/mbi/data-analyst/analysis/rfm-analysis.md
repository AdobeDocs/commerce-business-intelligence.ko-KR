---
title: 최신성, 빈도, 통화(RFM) 분석
description: 최신성, 빈도 및 통화 등급별로 고객을 세그먼트화할 수 있는 대시보드를 설정하는 방법을 알아봅니다.
exl-id: 8f0f08fd-710b-4810-9faf-3d0c3cc0a25d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# RFM 분석

이 문서에서는 최신성, 빈도 및 통화 등급별로 고객을 세그먼트화할 수 있는 대시보드를 설정하는 방법을 보여줍니다. RFM 분석은 도달 범위를 위한 세그먼테이션을 결정하는 데 도움이 되도록 고객 행동을 고려하는 마케팅 기법입니다. 세 가지 면을 고려한다. 최근 - 고객이 최근 스토어에서 구입한 빈도, 고객이 고객으로부터 구매한 빈도를 나타내는 빈도, 고객이 지출하는 금액의 통화 등을 보여줍니다.

![](../../assets/blobid0.png)

RFM 분석은 [!DNL MBI] Pro는 새 아키텍처에 대해 계획합니다(예를 들어 &quot;데이터 관리&quot; 메뉴 아래에 &quot;Data Warehouse 보기&quot; 옵션이 있는 경우). 이러한 열은 &quot;데이터 관리 > Data Warehouse&quot; 페이지에서 만들 수 있습니다. 자세한 지침은 아래에 나와 있습니다.

## 시작하기

먼저 값이 1인 기본 키만 포함된 파일을 업로드해야 합니다. 이렇게 하면 분석에 필요한 일부 계산된 열을 만들 수 있습니다.

이를 활용할 수 있습니다 [도움말 센터 문서](../importing-data/connecting-data/using-file-uploader.md) 및 파일 형식을 지정하는 아래 이미지를 참조하십시오.

## 계산된 열

귀사에서 손님 주문을 허용하는 경우 더 차별화된 내용이 있습니다. 그럴 경우 `customer_entity` 테이블. 게스트 주문이 허용되지 않는 경우 `sales_flat_order` 테이블.

만들 열

* **`Sales_flat_order/customer_entity`** 표
* `Customer's last order date`
* [!UICONTROL Column type]: `Many to one > Max`
* [!UICONTROL Pat]: `sales_flat_order.customer_id > customer_entity.entity_id`
* 선택됨 [!UICONTROL column]: `created_at`
* [!UICONTROL Filter]: `Orders we count`

* 

       고객의 마지막 주문 날짜 이후 시간(초)
   * [!UICONTROL Column type]: - &quot;동일한 표 > 연령
* 선택됨 [!UICONTROL column]: `Customer's last order date`

* (입력) 카운트 참조
* [!UICONTROL Column type]: `Same table > Calculation`
* 
   [!UICONTROL 입력]: `entity_id`
* [!UICONTROL Calculation]: `**case when A is null then null else 1 end**`
* 

   [[!UICONTROL 데이터 유형]: `Integer`

* **카운트 참조** 표(방금 업로드한 파일 중 &quot;1&quot; 숫자)
* 고객 수
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `ales_flat_order.(input) reference > Count reference.Primary Key` 또는 `customer_entity.(input)reference > Count Reference`. `Primary Key`
* 선택됨 [!UICONTROL column]: `sales_flat_order.customer_email` 또는 `customer_entity.entity_id`

* **Customer_entity** 표
* 고객 수
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity`.(입력) 참조 > 고객 집중 `Primary Key`
* 선택됨 [!UICONTROL column]: `Number of customers`

* (입력) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime revenue`

* 고객 라이프타임 수입별 순위 지정
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 

   [[!UICONTROL 데이터 유형]: `Integer`

* 고객의 통화 점수(백분위수)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 

   [[!UICONTROL 데이터 유형]: `Integer`

* (입력) 고객 라이프타임 주문 번호별 등급
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime number of orders`

* 고객 라이프타임 주문 수별 순위 지정
* 
   [!UICONTROL 열 유형]: – "동일한 테이블 > 계산"
* [!UICONTROL Inputs]: - **(입력) 고객 라이프타임 주문 번호별 등급**, **고객 수**
* [!UICONTROL Calculation]: - **A가 null이면 null이면 B-(A-1) 끝남**
* [!UICONTROL Datatype]: - 정수

* 고객의 빈도 점수(백분위수)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 

   [[!UICONTROL 데이터 유형]: `Integer`

* 고객의 마지막 주문 날짜 이후(초)별 순위 지정
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Seconds since customer's last order date`

* 고객의 최신성 점수(백분위수)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end`
* 

   [[!UICONTROL 데이터 유형]: `Integer`

* 고객의 최신성 점수(백분위수)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end`
* 

   [[!UICONTROL 데이터 유형]: String

* **카운트 참조** 표
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `sales_flat_order.(input) reference > Customer Concentration. Primary Key` 또는 `customer_entity.(input)reference > Customer Concentration.Primary Key`
* 선택됨 [!UICONTROL column]: `sales_flat_order.customer_email` 또는 `customer_entity.entity_id`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` 000과 같지 않음

* **Customer_entity** 표
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity.(input) reference > Customer Concentration.Primary Key`
* 선택됨 [!UICONTROL column]: - `Number of customers`

* 고객의 최신성 점수 `(R+F+M)`
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: - `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end`
* 

   [[!UICONTROL 데이터 유형]: `Integer`

* (입력) 고객의 전체 RFM 점수별 등급
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's recency score (R+F+M)`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` 000과 같지 않음

* 고객의 전체 RFM 점수별 순위 지정
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer's overall RFM score`, `Number of customers (RFM > 0)`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 

   [[!UICONTROL 데이터 유형]: `Integer`

* 고객의 RFM 그룹
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end`
* 

   [[!UICONTROL 데이터 유형]: `Integer`

>[!NOTE]
>
>사용되는 백분위수는 고객의 분할입니다(예: 1-5를 반환하기 위해 20% 버킷). 이 가중치를 원하는 사용자 지정 방법이 있으면 티켓을 제출할 때 분석가에게 문의하십시오.

## 지표

새 지표가 없습니다!

**참고**: 다음을 확인하십시오 [새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에

## 보고서

* **RFM 그룹별 고객**
* 지표 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's RFM score (by percentiles) Not Equal to 000`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 차트 숨기기
* [!UICONTROL Group by]: `Customer's RFM group`
* 
   [[!UICONTROL 그룹]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **최신성 점수가 5인 고객**
* 지표 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 5`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 
   [!UICONTROL Chart Type]: `Scalar`
* 차트 숨기기
* 
   [[!UICONTROL 그룹]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 

   [!UICONTROL Chart type]: `Table`

* **최신성 점수가 1인 고객**
* 지표 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 1`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 
   [!UICONTROL Chart Type]: `Scalar`
* 차트 숨기기
* 
   [[!UICONTROL 그룹]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 

   [!UICONTROL Chart type]: `Table`

모든 보고서를 컴파일한 후 대시보드에서 원하는 대로 구성할 수 있습니다. 최종 결과는 위의 샘플 대시보드와 비슷할 수 있지만, 생성된 세 개의 테이블은 수행할 수 있는 고객 세그멘테이션 유형의 예입니다.
