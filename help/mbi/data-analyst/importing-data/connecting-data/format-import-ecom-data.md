---
title: eCommerce 데이터 형식 지정 및 가져오기
description: eCommerce 데이터를 업로드하는 데 사용할 이상적인 데이터 형식을 알아봅니다.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 데이터 형식 지정 및 가져오기

현재 지원되지 않는 통합을 사용하고 있는 경우 [!DNL MBI]를 사용할 수도 있습니다. [파일 업로드 기능](using-file-uploader.md) 데이터를 data warehouse로 가져오기. 이 문서에서는 eCommerce 데이터를 업로드하는 데 사용할 이상적인 데이터 형식을 살펴봅니다.

## `Orders` 표

다음 `orders` 테이블에는 비즈니스가 수행한 모든 트랜잭션에 대해 하나의 행이 포함되어야 합니다. 가능한 열에는 다음이 포함됩니다.

| 열 이름 | 설명 |
|----|----|
| `Order ID` | 주문 ID는 테이블의 모든 행에 대해 고유해야 합니다. 또한 이 키는 일반적으로 테이블의 기본 키입니다. |
| `Customer` | 주문을 한 고객입니다. |
| `Order total` | 주문의 합계입니다. 이 열은 계산 기반 열일 수 있으며, 이때 소계 및 배송과 같은 다른 열의 값이 이 열에 대한 합계를 구성합니다. |
| `Currency` | 주문이 지급된 통화입니다. 관련된 경우 포함합니다. |
| ` Order status` | 주문 상태(예: ) `In Progress`, `Refunded`, 또는 `Complete`. 이 열의 값이 변경될 수 있습니다(완료되지 않은 경우). 새 데이터와 업데이트된 데이터를 [데이터 추가 기능](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) on `File Uploads` 페이지. |
| `Acquisition/marketing channel` | 주문을 수행한 고객이 참조한 획득 또는 마케팅 채널입니다. |
| `Order datetime` | 주문을 만든 날짜 및 시간입니다. |
| `Order updated at` | 주문 레코드에 대한 마지막 수정 날짜 및 시간입니다. |

{style=&quot;table-layout:auto&quot;}

## `Order detail/items` 표 {#itemstable}

다음 `order_detail / items` 테이블에는 모든 순서로 각 개별 항목에 대해 하나의 행이 포함되어야 합니다. 가능한 열에는 다음이 포함됩니다.

| 열 이름 | 설명 |
|----|----|
| `Order item ID` | 주문 항목 ID는 테이블의 모든 행에 대해 고유해야 합니다. 또한 일반적으로 다음과 같습니다 `primary key` 참조하십시오. |
| `Order ID` | 주문 ID입니다. |
| `Product ID` | 제품의 ID입니다. |
| `Product name` | 제품의 이름입니다. |
| `Product's unit price` | 제품의 단품가격. |
| `Quantity` | 주문 제품의 수량입니다. |

## `Customers` 표 {#customerstable}

다음 `customers` 테이블에는 각 고객 계정에 대해 하나의 행이 포함되어야 합니다. 가능한 열에는 다음이 포함됩니다.

| 열 이름 | 설명 |
|----|----|
| `Customer ID` | 고객 ID는 테이블의 모든 행에 대해 고유해야 합니다. 또한 이 키는 일반적으로 테이블의 기본 키입니다. |
| `Customer created at` | 고객의 계정이 생성된 날짜 및 시간입니다. |
| `Customer modified at` | 고객의 계정이 마지막으로 수정된 날짜 및 시간입니다. |
| `Acquisition/marketing channel source` | 고객이 참조한 획득 또는 마케팅 채널입니다. |
| `Demographic info` | 연령 범위 및 성별 등의 인구 통계 정보를 사용하여 보고서를 세그먼트화할 수 있습니다. |
| `Acquisition/marketing channel` | 주문을 수행한 고객이 참조한 획득 또는 마케팅 채널입니다. |

## `Subscription payments` 표

다음 `subscriptions` 테이블에는 각 구독 지불에 대해 하나의 행이 포함되어야 합니다. 가능한 열에는 다음이 포함됩니다.

| 열 이름 | 설명 |
|----|----|
| `Subscription ID` | 구독 ID는 테이블의 모든 행에 대해 고유해야 합니다. 또한 이 키는 일반적으로 테이블의 기본 키입니다. |
| `Customer ID` | 지급을 한 고객의 ID입니다. |
| `Payment amount` | 구독 지불 금액입니다. |
| `Start date` | 지급에 적용되는 기간의 시작 날짜/시간입니다. |
| `End date` | 지급에 적용되는 기간의 종료 날짜/시간입니다. |
