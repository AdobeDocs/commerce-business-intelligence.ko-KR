---
title: eCommerce 데이터 서식 지정 및 가져오기
description: eCommerce 데이터를 업로드하는 데 사용할 이상적인 데이터 형식에 대해 알아봅니다.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# 데이터 서식 지정 및 가져오기

현재 다음에서 지원하지 않는 통합을 사용하는 경우: [!DNL Adobe Commerce Intelligence], 여전히 다음을 사용할 수 있습니다 [파일 업로드 기능](using-file-uploader.md) 을 클릭하여 데이터를 Data Warehouse으로 가져옵니다. 이 주제에서는 전자 상거래 데이터를 업로드하는 데 사용할 이상적인 데이터 형식을 다룹니다.

## `Orders` 표

다음 `orders` 테이블에는 비즈니스가 수행한 모든 트랜잭션에 대해 하나의 행이 포함되어야 합니다. 잠재적 열에는 다음이 포함됩니다.

| 열 이름 | 설명 |
|----|----|
| `Order ID` | 주문 ID는 테이블의 모든 행에 대해 고유해야 합니다. 또한 이는 일반적으로 테이블의 기본 키입니다. |
| `Customer` | 주문한 고객. |
| `Order total` | 총 주문 수. 이 열은 계산 기반 열일 수 있으며, 다른 열의 값(예: 소계 및 배송)은 이 열의 합계를 구성합니다. |
| `Currency` | 주문이 지불된 통화. 관련 있는 경우 포함. |
| ` Order status` | 주문 상태(예: ) `In Progress`, `Refunded`, 또는 `Complete`. 이 열의 값이 변경됩니다(완료되지 않은 경우). 새 데이터 및 업데이트된 데이터는 [데이터 추가 기능](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 다음에 있음 `File Uploads` 페이지를 가리키도록 업데이트하는 중입니다. |
| `Acquisition/marketing channel` | 주문한 고객이 참조한 획득 또는 마케팅 채널. |
| `Order datetime` | 주문이 생성된 날짜와 시간입니다. |
| `Order updated at` | 주문 레코드를 마지막으로 수정한 날짜 및 시간입니다. |

{style="table-layout:auto"}

## `Order detail/items` 표 {#itemstable}

다음 `order_detail / items` 테이블에는 모든 주문에서 각 개별 항목에 대해 하나의 행이 포함되어야 합니다. 잠재적 열에는 다음이 포함됩니다.

| 열 이름 | 설명 |
|----|----|
| `Order item ID` | 주문 항목 ID는 테이블의 모든 행에 대해 고유해야 합니다. 또한 일반적으로 `primary key` 테이블로요. |
| `Order ID` | 주문 ID입니다. |
| `Product ID` | 제품 ID입니다. |
| `Product name` | 제품 이름. |
| `Product's unit price` | 제품 단일 단위의 가격입니다. |
| `Quantity` | 주문된 제품의 수량입니다. |

## `Customers` 표 {#customerstable}

다음 `customers` 테이블에는 각 고객 계정에 대해 하나의 행이 포함되어야 합니다. 잠재적 열에는 다음이 포함됩니다.

| 열 이름 | 설명 |
|----|----|
| `Customer ID` | 고객 ID는 테이블의 모든 행에 대해 고유해야 합니다. 또한 이는 일반적으로 테이블의 기본 키입니다. |
| `Customer created at` | 고객 계정이 생성된 날짜와 시간입니다. |
| `Customer modified at` | 고객 계정을 마지막으로 수정한 날짜 및 시간입니다. |
| `Acquisition/marketing channel source` | 고객이 참조한 획득 또는 마케팅 채널. |
| `Demographic info` | 연령 범위 및 성별과 같은 인구 통계학적 정보를 사용하여 보고서를 세그먼트화할 수 있습니다. |
| `Acquisition/marketing channel` | 주문한 고객이 참조한 획득 또는 마케팅 채널. |

## `Subscription payments` 표

다음 `subscriptions` 테이블에는 각 구독 결제에 대해 하나의 행이 포함되어야 합니다. 잠재적 열에는 다음이 포함됩니다.

| 열 이름 | 설명 |
|----|----|
| `Subscription ID` | 구독 ID는 테이블의 모든 행에 대해 고유해야 합니다. 또한 이는 일반적으로 테이블의 기본 키입니다. |
| `Customer ID` | 결제를 수행한 고객의 ID입니다. |
| `Payment amount` | 구독 결제 금액. |
| `Start date` | 지급이 적용되는 기간의 시작 날짜/시간입니다. |
| `End date` | 지급이 적용되는 기간의 종료 날짜/시간입니다. |
