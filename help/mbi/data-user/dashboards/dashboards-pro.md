---
title: 기본 대시보드
description: 비즈니스에 대한 통찰력을 제공하는 기본 제공 대시보드에 대해 알아봅니다.
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '2240'
ht-degree: 0%

---

# 기본 제공 대시보드

[!DNL MBI] 에는 비즈니스에 대한 통찰력을 제공하는 기본 제공 대시보드가 포함되어 있습니다. 대시보드를 사용하면 사용자 라이프타임 수익, 반복 구매 횟수, 지정된 기간 동안 구매한 상위 제품 등과 같은 필수 지표의 상태를 확인할 수 있습니다. 사전 구성된 이러한 대시보드는 정보에 입각한 비즈니스 결정을 내리는 데 도움을 주기 위해 작성되었습니다.

>[!NOTE]
>
>이러한 대시보드에 대한 액세스는 계정 유형 및 액세스 수준에 따라 다릅니다. 이러한 대시보드가 표시되지 않으면 다음으로 문의하십시오. [지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## 보고서 가용성

의 경우 `Customers` 및 `Executive Summary` 대시보드, 일부 보고서는 저장소의 체크아웃 구성에 따라서만 사용할 수 있습니다. 특히 스토어에서 게스트 체크아웃을 허용하거나 게스트 체크아웃을 허용하지 않는 경우.

## 고객(게스트 체크아웃 허용)

고객 (게스트 체크아웃 허용) 대시보드는 구매 행동과 같은 고객 기반에 대한 정보를 제공합니다. 이 대시보드를 사용하면 고객 보유율을 높이고 가장 높은 매출을 올리는 고객을 파악하는 데 도움이 될 수 있습니다.

### 보고서

| 이름 | 설명 |
|---|---|
| `Orders by New Customers (Past 30 Days)` | 이전에 주문한 적이 없는 고객으로부터 지난 30일 동안의 주문. |
| `Orders by Existing Customers (Past 30 Days)` | 이전에 최소 한 개 이상의 주문을 한 고객으로부터 지난 30일 동안의 주문. |
| `Total Unique Customers (Past 30 Days)` | 지난 30일 동안 주문을 한 고유 고객 수. |
| `Orders by New vs Existing Customers` | 이전 주문이 없는 고객과 하나 이상의 이전 주문이 있는 고객의 주문 수. |
| `Subsequent Order Probability (All Time)` | 주문한 고객이 다른 고객을 배치할 가능성. |
| `% of Customers with Multiple Orders (All Time)` | 두 개 이상의 주문을 한 모든 고객의 비율. |
| `Median Time Between Orders (All Time)` | 각 고객이 한 주문과 다음 주문 사이에 걸리는 평균 시간. |
| `Subsequent Order Probability` | 주문을 한 고객이 주문 번호로 분류된 다른 주문을 할 가능성. 즉, 두 번째 주문을 하는 한 고객과 두 번째 주문을 하는 두 번째 주문 고객의 비율, 세 번째 주문을 하는 두 번째 주문 고객 비율 등입니다. |
| `Time Between Orders` | 주문 번호별로 구분된 주문 간 평균 및 중간 시간(즉, 주문 1과 2, 2와 3 사이의 시간). |
| `Number of Customers - Lifetime Orders` | 고객 라이프타임에 지정된 주문 수의 경우 해당 많은 주문을 한 고객의 수와 해당 숫자가 나타내는 전체 고객 기준의 백분율입니다. |
| `One-Time Customers who Bought 3-6 Months Ago` | 3~6개월 전에 처음 구입하고 구입만 한 고객. |
| `Avg LTV by First Order` | 집단 간 누적 평균 고객 생애 매출을 비교합니다. 집단은 고객이 처음 구매한 월로 정의됩니다. 예: `Jan 2020` 코호트는 2020년 1월에 첫 구매가 이루어진 고객의 누적 평균 LTV를 보여 준다. |
| `Customer's First 30 Day vs Lifetime Revenue` | 첫 구매 후 30일 동안의 고객 평균 매출과 전체 라이프타임 간의 평균 매출의 비교. 각 버블은 배송 지역에 해당하며, 각 버블의 크기는 해당 지역에서 취득한 고객의 수를 나타낸다. |

## 고객(게스트 체크아웃이 허용되지 않음)

고객 (게스트 체크아웃 허용 안 함) 대시보드는 구매 행동 및 계정 등록에서 주문 배치로의 전환과 같은 고객 기반에 대한 정보를 제공합니다. 이 대시보드를 사용하면 고객 보유율을 높이고 가장 높은 매출을 올리는 고객을 파악하는 데 도움이 될 수 있습니다.

### 보고서

| 이름 | 설명 |
|---|---|
| 계정 등록(지난 30일) | 지난 30일 동안 스토어에 계정을 등록한 사용자의 수입니다. |
| 1개 이상의 주문과 함께 등록된(지난 30일) 계정 | 지난 30일 동안 스토어에 계정을 등록하고 최소 1개의 주문을 한 사용자의 수. |
| 등록에서 첫 번째 주문으로의 % 전환(지난 30일) | 지난 30일 동안 등록된 주문된 계정의 백분율입니다. |
| 등록에서 1차 주문으로의 % 전환 | 등록 월별로 주문을 한 등록된 계정의 백분율입니다. |
| 신규 및 기존 고객별 주문 | 이전 주문이 없는 고객과 하나 이상의 이전 주문이 있는 고객의 주문 수. |
| 후속 주문 확률(항상) | 주문한 고객이 다른 고객을 배치할 가능성. |
| 여러 개의 주문을 가진 고객 비율(항상) | 두 개 이상의 주문을 한 모든 고객의 비율. |
| 주문 간 평균 시간(모든 시간) | 각 고객이 한 주문과 다음 주문 사이에 걸리는 평균 시간. |
| 후속 주문 확률 | 주문을 한 고객이 주문 번호로 분류된 다른 고객을 배치할 가능성. 즉, 두 번째 주문하는 고객의 %, 세 번째 주문하는 두 명의 고객 % 등입니다. |
| 주문 사이의 시간 | 주문 번호별로 구분된 주문 간 평균 및 중간 시간(즉, 주문 1과 2, 2와 3 사이의 시간). |
| 고객 수 - 라이프타임 주문 | 고객 라이프타임에 지정된 주문 수의 경우 해당 많은 주문을 한 고객의 수와 해당 숫자가 나타내는 전체 고객 기준의 백분율입니다. |
| 3~6개월 전에 구입한 일회성 고객 | 3~6개월 전에 처음 구입하고 구입만 한 고객. |
| 첫 번째 주문별 평균 LTV | 집단 간 누적 평균 고객 생애 매출을 비교합니다. 집단은 고객이 처음 구매한 월로 정의됩니다. 예를 들어 2020년 1월 코호트는 2020년 1월에 첫 구매가 이루어진 고객에 대한 누적 평균 LTV를 표시합니다. |
| 고객의 최초 30일 대 라이프타임 수익 | 첫 구매 후 30일 동안의 고객 평균 매출과 전체 라이프타임 간의 평균 매출의 비교. 각 버블은 배송 지역에 해당하며, 각 버블의 크기는 해당 지역에서 취득한 고객의 수를 나타낸다. |

## 실행 요약(게스트 체크아웃 허용)

실행 요약(게스트 체크아웃 허용) 대시보드는 주문 및 매출 측면에서 비즈니스의 진행 상황을 간결하게 파악할 수 있습니다. 이 대시보드는 경영진이 비즈니스 성과를 전체적으로 이해할 수 있도록 설계되었지만 다른 사용자도 통찰력을 가질 수 있습니다.

### 보고서

| 이름 | 설명 |
|---|---|
| 매출(이번 달) | 스토어에서 이번 달 동안 생성한 매출입니다. 이 경우 매출은 고객이 주문에 대해 지불한 최종 가격으로 정의됩니다. |
| 매출(지난 6개월 일별) | 이전 7일 동안의 평균 일일 매출과 오버레이된 총 일일 매출입니다. 이 경우 매출은 고객이 주문에 대해 지불한 최종 가격으로 정의됩니다. |
| 매출 % 변경(MoM MTD) | 이전 달의 동일한 부분과 현재 월의 수익 비교. |
| 신규 고객과 기존 고객의 매출(이번 달) | 이번 달 매출(지금까지)은 신규(처음) 고객 대 기존 고객(두 번째 또는 이후 주문)으로 인한 것입니다. |
| 평균 주문 가격(현재 월) | 현재 월에 수행한 주문의 일일 평균 값(현재까지)입니다. 주문 가치는 고객이 주문에 대해 지불한 최종 가격으로 정의됩니다. |
| 주문(이번 달) | 현재 월에 스토어에서 수행한 주문 수(현재까지)입니다. |
| 주문 % 변경(MoM MTD) | 현재 월의 주문 수(현재까지)와 이전 달의 동일한 부분 비교. |
| 신규 고객별 주문(이번 달) | 이전에 주문한 적이 없는 고객의 현재 월 주문. |
| 기존 고객별 주문(이번 달) | 이전에 하나 이상의 주문을 한 고객의 현재 월 주문. |
| 신규 및 기존 고객별 주문(현재 주별 연도) | 현재 연도의 각 주에 대한 이전 주문이 없는 고객의 주문 수와 이전 주문이 하나 이상인 고객의 주문 수(현재까지)입니다. |

## 실행 요약(게스트 체크아웃이 허용되지 않음)

실행 요약 (게스트 체크아웃이 허용되지 않음) 대시보드는 주문, 매출 및 계정 등록 측면에서 비즈니스의 운영 방식에 대한 간단한 그림을 제공합니다. 이 대시보드는 경영진이 비즈니스 성과를 전체적으로 이해할 수 있도록 설계되었지만 다른 사용자도 통찰력을 가질 수 있습니다.

### 보고서

| 이름 | 설명 |
|---|---|
| 매출(이번 달) | 이번 달 스토어에서 생성된 매출입니다. 이 경우 매출은 고객이 주문에 대해 지불한 최종 가격으로 정의됩니다. |
| 매출(지난 6개월 일별) | 이전 7일 동안의 평균 일일 매출과 오버레이된 총 일일 매출입니다. 이 경우 매출은 고객이 주문에 대해 지불한 최종 가격으로 정의됩니다. |
| 매출 % 변경(MoM MTD) | 이번 달 동안의 매출과 이전 달의 동일한 부분 비교. |
| 신규 고객과 기존 고객의 매출(이번 달) | 이번 달 매출(지금까지)은 신규(처음) 고객 대 기존 고객(두 번째 또는 이후 주문)으로 인한 것입니다. |
| 평균 주문 가격(현재 월) | 현재 월에 수행한 주문의 일일 평균 값(현재까지)입니다. 주문 가치는 고객이 주문에 대해 지불한 최종 가격으로 정의됩니다. |
| 주문(이번 달) | 현재 월에 스토어에서 수행한 주문 수(현재까지)입니다. |
| 주문 % 변경(MoM MTD) | 현재 월의 주문 수(현재까지)와 이전 달의 동일한 부분 비교. |
| 계정 등록(현재 월) | 이번 달 현재까지 새로 등록된 계좌 수. |
| 등록에서 첫 번째 주문으로의 % 전환(현재 월) | 이번 달 현재까지 등록된 주문된 계정의 백분율입니다. |
| 등록에서 첫 번째 주문으로의 % 전환(현재 주별 연도) | 올해 들어 현재까지 매주 등록한 주문된 계정의 비율입니다. |

## 주문 수

주문 대시보드는 주문의 트랜잭션 양, 주문 상태, 사용된 쿠폰 코드, 생성된 수익 및 사용된 결제 방법에 대한 통찰력을 제공합니다. 예를 들어 이행 프로세스를 추적하고 문제나 병목 현상이 발생하지 않는지 확인할 수 있습니다.

>[!NOTE]
>
>이 대시보드의 보고서는 두 가지 구성 유형(게스트 체크아웃, 게스트 체크아웃 없음)이 있는 저장소에 연결된 계정에 사용할 수 있습니다.

### 보고서

| 이름 | 설명 |
|---|---|
| 주문(지난 30일) | 지난 30일 동안 스토어와 함께 수행한 주문 수. |
| 매출(지난 30일) | 지난 30일 동안 스토어에서 생성된 매출입니다. 매출은 고객이 주문에 대해 지불한 최종 가격으로 정의됩니다. |
| 평균 주문 가격(지난 30일) | 지난 30일 동안의 평균 주문 가격. 주문 가치는 고객이 주문에 대해 지불한 최종 가격으로 정의됩니다. |
| 주문 수 | 매월 스토어에서 수행한 주문 수. |
| 결제 방법별 수익 | 스토어에서 생성된 수익, 결제 방법으로 분할된 수익. 매출은 고객이 주문에 대해 지불한 최종 가격으로 정의됩니다. |
| 신규 및 기존 고객별 AOV | 스토어에서 수행한 주문의 월별 평균 값. 이전 주문이 없는 고객과 하나 이상의 이전 주문이 있는 고객의 주문으로 분할됩니다. 주문 가치는 고객이 주문에 대해 지불한 최종 가격으로 정의됩니다. |
| 상태별 % 주문(지난 30일) | 현재 각 주문 상태에 있는 지난 30일 동안 각 날짜의 주문 비율. |
| 미완료 주문(1일 이상 전에 생성됨) | 하루 이상 전에 수행한 모든 주문 중 아직 미완료 상태(취소되거나 완료되지 않음)에 있는 주문 목록. |
| 시간당 주문 수(지난 7일) | 매시간 주문량. |
| 수익 세부 정보(지난 30일) | 지난 30일 동안의 일일 수익을 총 수익 값의 모든 구성 요소로 분류합니다. |
| 쿠폰 코드별 주문 세부 사항(지난 30일) | 스토어에서 제공하는 각 쿠폰 코드에 대해, 해당 쿠폰 코드가 사용된 방법과 지난 30일 동안 가져온 반환 항목에 대한 세부 정보. |
| 쿠폰 포함 % 주문(지난 30일) | 지난 30일 동안 쿠폰을 사용한 주문 대 사용하지 않은 주문의 백분율. |

## 제품

제품 대시보드에는 주문 제품, 총 상품 가격(GMV) 및 구매 및 환불 상위 제품에 대한 일반 제품 성능이 표시됩니다. 구매와 수익의 균형을 맞추고, 제품의 성공과 인기를 결정하는 데 도움이 될 수 있습니다. 스토어는 다음과 같아야 합니다. [환불을 추적하도록 구성됨](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html) 을 참조하십시오.

>[!NOTE]
>
>이 대시보드의 보고서는 두 가지 구성 유형(게스트 체크아웃, 게스트 체크아웃 없음)이 있는 저장소에 연결된 계정에 사용할 수 있습니다.

### 보고서

| 이름 | 설명 |
|---|---|
| GMV(지난 30일) | 지난 30일 동안 판매된 모든 제품의 총 상품 가치. GMV는 주문수량에 제품별 기준가격을 곱한 것으로 정의된다. |
| % GMV(지난 30일) 환불 | 지난 30일 동안 구매하여 환불이 발생한 제품에 대한 GMV의 백분율. |
| 주문한 제품 수량(지난 30일) | 지난 30일 동안 주문된 항목의 총 수량입니다. |
| % 구매 제품(지난 30일) 환불 | 지난 30일 동안 구매하여 환불된 항목의 비율입니다. |
| 총 상품 가치 | 판매된 모든 제품의 월별 총 상품 가치. GMV는 주문수량에 제품별 기준가격을 곱한 것으로 정의된다. |
| 제품당 구매 및 환급률(지난 30일) | 각 제품에 대해 지난 30일 동안 주문한 총 수와 제품이 환불된 비율을 비교합니다. 각각의 버블 크기는 환급률을 나타낸다. |
| 제품 성능 세부 정보(지난 30일) | 지난 30일 동안의 판매 및 이후 환불 세부 정보(제품 sku 및 제품 이름별). |
| GMV별 주요 구매 제품(지난 30일) | 지난 30일 동안 판매된 제품 중 가장 많은 매출을 올린 제품(상위 10개). |
| GMV별 상위 환불 제품(지난 30일) | 지난 30일 동안 구매한 제품으로 인해 환불(상위 10개)로 인해 가장 많은 GMV가 손실되었습니다. |
| 수량별 상위 구매 제품(지난 30일) | 지난 30일 동안 판매된 제품 수가 가장 많음(상위 10개). |
| 수량별 상위 환불 제품(지난 30일) | 지난 30일 동안 구매하여 환불 수량이 가장 많은 제품(상위 10개). |
