---
title: Pro용 예상 라이프타임 값(LTV) 분석
description: 고객의 고객 생애 가치 성장 및 예상 생애 가치를 이해하는 데 도움이 되는 대시보드를 설정하는 방법에 대해 알아봅니다.
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# 예상 라이프타임 값 분석

이 문서에서는 고객의 고객 생애 가치 성장 및 예상 생애 가치를 이해하는 데 도움이 되는 대시보드를 설정하는 방법을 보여 줍니다.

![](../../assets/exp-lifetim-value-anyalysis.png)

이 분석은 새 아키텍처에 대한 Pro 계정 고객만 사용할 수 있습니다. 계정에 대한 액세스 권한이 있는 경우 `Persistent Views` 아래 기능 `Manage Data` 사이드바에서는 새 아키텍처를 기반으로 하며 여기에 나열된 지침에 따라 분석을 직접 작성할 수 있습니다.

시작하기 전에 다음을 숙지해야 합니다. [집단 report builder.](../dev-reports/cohort-rpt-bldr.md)

## 계산된 열

에 만들 열 **주문 수** 사용할 경우 테이블 **30일 개월**:

* [!UICONTROL Column name]: `Months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `Seconds between customer's first order date and this order`
* 
   [!UICONTROL Datatype]: `Integer`
* **정의:**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name]: `Months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* 정의: `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

에 만들 열 **`orders`** 사용할 경우 테이블 **달력** 개월:

* [!UICONTROL Column name]: `Calendar months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column inputs]:
   * `A` = `created_at`
   * `B` = `Customer's first order date`

* 
   [!UICONTROL Datatype]: `Integer`
* 정의: `case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`

* [!UICONTROL Column name]: `Calendar months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: `A` = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* **정의:**`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`

* [!UICONTROL Column name]: `Is in current month? (Yes/No)`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* 
   [!UICONTROL Datatype]: `String`
* 정의: `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## 지표

### 지표 지침

생성할 지표

* **첫 번째 주문 날짜별 고유 고객**
   * 게스트 주문을 활성화하면 `customer_email`

* 다음에서 **`orders`** 표
* 이 지표는 다음을 수행합니다. **고유 값 계산**
* 다음에서 **`customer_id`** 열
* 정렬 기준: **`Customer's first order date`** timestamp

>[!NOTE]
>
>다음을 확인하십시오. [새 열을 지표에 차원으로 추가](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에

## 보고서

### 보고서 지침

**월별 고객당 예상 매출**

* 지표 `A`: `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` (예를 들어 24개월과 같이 X에 적합한 숫자를 선택하십시오.)
   * `Is in current month?` = `No`

* 
   [!UICONTROL 지표]: `Revenue`
* [!UICONTROL Filter]:

* 지표 `B`: `All time customers (hide)`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* 지표 `C`: `All time customers by month since first order (hide)`
   * `Calendar months since order` `<= X`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Expected revenue`
* [!UICONTROL Formula]: `A / (B - C)`
* 

   [!UICONTROL Format]: `Currency`

기타 차트 세부 정보

* [!UICONTROL Time period]: `All time`
* 시간 간격: `None`
* [!UICONTROL Group by]: `Calendar months between first order and this order` - 모두 표시
* 변경 `group by` 대상: `All time customers` 지표 옆에 있는 연필 아이콘을 사용하여 독립적입니다. `group by`
* 편집 `Show top/bottom` 다음과 같은 필드:
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**집단에 의한 월별 평균 수익**

* 지표 `A`: `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**집단에 의한 월별 평균 누적 수익**

* 지표 `A`: `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

모든 보고서를 컴파일한 후 원하는 대로 대시보드에서 구성할 수 있습니다. 결과는 페이지 상단에 있는 이미지와 비슷할 수 있습니다.

이 분석을 작성하는 동안 질문이 발생하거나 Professional Services 팀의 도움을 얻고자 하는 경우 [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
