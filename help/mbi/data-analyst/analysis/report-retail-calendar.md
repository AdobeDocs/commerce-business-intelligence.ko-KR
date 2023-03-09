---
title: 소매 달력 보고
description: 내에서 4-5-4 소매 달력을 사용하도록 구조를 설정하는 방법에 대해 알아봅니다. [!DNL MBI] 계정입니다.
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# 소매 달력 보고

이 문서에서는 [4-5-4 소매 달력](https://nrf.com/resources/4-5-4-calendar) 내 [!DNL MBI] 계정입니다. 시각적 리포트 빌더는 놀라울 정도로 유연한 시간 범위, 간격 및 독립 설정을 제공합니다. 그러나 이러한 모든 설정은 기존의 월별 달력을 사용하여 작동합니다.

많은 고객이 소매 또는 회계 날짜를 사용하도록 달력을 변경하기 때문에 아래 단계에서는 데이터를 사용하고 소매 날짜를 사용하여 보고서를 만드는 방법을 보여줍니다. 아래 지침은 4-5-4 소매 달력을 참조하지만, 재무 달력이든 사용자 정의 시간대이든 팀이 사용하는 특정 달력에 대해 변경할 수 있습니다.

시작하기 전에 다음을 숙지해야 합니다. [파일 업로더](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 및 을(를) 늘려 `.csv` 파일. 이렇게 하면 날짜가 모든 이전 데이터를 포함하고 날짜를 미래로 푸시할 수 있습니다.

이 분석에는 다음이 포함됩니다. [고급 계산 열](../data-warehouse-mgr/adv-calc-columns.md).

## 시작

다음을 수행할 수 있습니다. [다운로드](../../assets/454-calendar.csv) a `.csv` 2014년부터 2017년까지 소매 연도에 대한 4-5-4 소매 달력 버전. 내부 소매 일정에 따라 이 파일을 조정하고 날짜 범위를 확장하여 기록 및 현재 시간대를 지원할 수 있습니다. 파일을 다운로드한 후 File Uploader를 사용하여 [!DNL MBI] Data Warehouse. 4-5-4 소매 달력의 변경되지 않은 버전을 사용하는 경우 이 표에 있는 필드의 구조 및 데이터 유형이 다음과 일치하는지 확인하십시오.

| 열 이름 | 열 데이터 유형 | 기본 키 |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (최대 255자) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## 생성할 열

* **sales\_order** 표
   * `INPUT` `created\_at` (yyyy-mm-dd 00:00:00)
      * [!UICONTROL Column type]: – `Same table > Calculation`
      * [!UICONTROL Inputs]: – `created\_at`
      * [!UICONTROL Datatype]: – `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **소매 달력** 파일 업로드 테이블
   * **현재 날짜**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
         [!UICONTROL 데이터 유형]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

         >[!NOTE]
         >
         >다음 `now()` 위의 함수는 PostgreSQL에만 해당됩니다. 대부분 [!DNL MBI] 데이터 웨어하우스는 PostgreSQL에서 호스팅되며 일부는 Redshift에서 호스팅될 수 있습니다. 위의 계산에서 오류가 반환되면 Redshift 함수를 사용해야 할 수도 있습니다 `getdate()` 대신 `now()`.
   * **현재 소매 연도** (지원 분석가가 작성해야 함)
      * [!UICONTROL Column type]: 전자`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
         [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **현재 소매 연도에 포함됩니까? (예/아니요)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL 데이터 유형]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **이전 소매 연도에 포함됩니까? (예/아니요)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL 데이터 유형]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`


* **sales\_order** 표
   * **Created\_at (소매 연도)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 경로 -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * 선택 [!UICONTROL table]: `Retail Calendar`
      * 선택 [!UICONTROL column]: `Year Retail`
   * **Created\_at (소매 주)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 경로 -
         * [!UICONTROL Many]: sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00
         * [!UICONTROL One]: 소매 Calendar.Date 소매
      * 선택 [!UICONTROL table]: `Retail Calendar`
      * 선택 [!UICONTROL column]: `Week Retail`
   * **Created\_at (소매 월)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 경로
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * 선택 [!UICONTROL table]: `Retail Calendar`
      * 선택 [!UICONTROL column]: `Month Number Retail`
   * **이전 소매 연도에 포함하시겠습니까? (예/아니요)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 경로 -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: 소매 `Calendar.Date Retail`
      * 선택 [!UICONTROL table]: `Retail Calendar`
      * 선택 [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **현재 소매 연도에 포함하시겠습니까? (예/아니요)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 경로 -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: 소매 `Calendar.Date Retail`
      * 선택 [!UICONTROL table]: `Retail Calendar`
      * 선택 [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## 지표

참고: 이 분석에는 새 지표가 필요하지 않습니다. 그러나 다음을 확인하십시오. [sales\_order 테이블에 작성한 새 열을 차원으로 추가합니다.](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 보고서를 계속 진행하기 전에 sales\_order 테이블의 모든 지표에 대해 설명합니다.

## 보고서

* **주별 주문 - 소매 달력(전년 대비)**
   * 지표 `A`: `2017`
      * [!UICONTROL Metric]: 주문 수
      * [!UICONTROL Filter]:
         * Created\_at (소매 연도) = 2017
   * 지표 `B`: `2016`
      * [!UICONTROL Metric]: 주문 수
      * [!UICONTROL Filter]:
         * Created\_at (소매 연도) = 2016
   * 지표 `C`: `2015`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail week)
   * 
      [!UICONTROL Chart type]: `Line`
      * 끄기 `multiple Y-axes`

* **소매 달력 개요(현재 월별 소매 연도)**
   * 지표 `A`: `Revenue`
      * 
         [!UICONTROL 지표]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 지표 `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 지표 `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail month)
   * 

      [!UICONTROL Chart type]: `Line`

* **소매 달력 개요(이전 월별 소매 연도)**
   * 지표 `A`: `Revenue`
      * 
         [!UICONTROL 지표]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 지표 `B`: `Orders`
      * [!UICONTROL Metric]: 주문 수
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 지표 `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail month)
   * 

      [!UICONTROL Chart type]: `Line`

## 다음 단계

위의 설명은에 빌드된 모든 지표와 호환되도록 소매 일정을 구성하는 방법을 설명합니다. `sales\_order` 표(예: `Revenue` 또는 `Orders`). 모든 표에 작성된 지표에 대한 소매 일정을 지원하도록 확장할 수도 있습니다. 유일한 요구 사항은 이 테이블에 소매 달력 테이블에 조인하는 데 사용할 수 있는 유효한 날짜/시간 필드가 있다는 것입니다.

따라서 예를 들어 4-5-4 소매 달력에서 고객 수준 지표를 보려면 `Same Table` 계산 `customer\_entity` 표, 유사 `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` 위에서 설명했습니다. 그런 다음 이 열을 사용하여 `One to Many` JOINED\_COLUMN 계산(예: `Created_at (retail year)` 및 `Include in previous retail year? (Yes/No)` 을(를) 참여시켜 `customer\_entity` 테이블 대상 `Retail Calendar` 테이블.

잊지 말고 [새 열을 지표에 차원으로 추가](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에
