---
title: 전자 상거래 데이터 형식 지정 및 가져오기
description: 전자 상거래 데이터를 업로드 하는 데 사용할 이상적인 데이터 형식에 대해 알아보십시오.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# 데이터 서식 지정 및 가져오기

현재 지원 [!DNL Adobe Commerce Intelligence] 되지 않는 통합을 사용 하는 경우에도 [ [ 파일 업로드] 기능 ](using-file-uploader.md) 을 사용 하 여 데이터를 데이터 웨어하우스로 가져올 수 있습니다. 이 항목에서는 전자 상거래 데이터를 업로드 하는 데 사용할 이상적인 데이터 형식을 설명 합니다.

## `Orders` 테이블

이 테이블에 `orders` 는 비즈니스가 수행한 모든 트랜잭션에 대해 하나의 행이 포함 되어야 합니다. 잠재적 열은 다음과 같습니다.

| 열 이름 | 설명 |
|----|----|
| `Order ID` | 주문 ID는 테이블의 모든 행에 대해 고유 해야 합니다. 또한 일반적으로 테이블에 대 한 기본 키입니다. |
| `Customer` | 주문이 접수 된 고객입니다. |
| `Order total` | 주문의 합계입니다. 이 열은 부분합 및 배송료와 같은 다른 열의 값이이 열의 합계를 구성 하는 계산 기반 열입니다. |
| `Currency` | 주문이 지불 된 통화입니다. 관련성이 있는 경우 포함 합니다. |
| ` Order status` | 주문 상태 (예: `In Progress` , `Refunded` , 또는 `Complete` ) 이 열의 값이 완료 되지 않은 경우 변경 됩니다. 새로 만들기 및 업데이트 된 데이터는 페이지에서 `File Uploads` 데이터 추가 기능 ](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 을 [ 사용 하 여 가져올 수 있습니다. |
| `Acquisition/marketing channel` | 주문이 접수 된 고객이 언급 한 확보 또는 마케팅 채널입니다. |
| `Order datetime` | 주문이 만들어진 날짜 및 시간입니다. |
| `Order updated at` | 주문 레코드가 마지막으로 수정 된 날짜와 시간입니다. |

{style="table-layout:auto"}

## `Order detail/items` 테이블 {#itemstable}

테이블에 `order_detail / items` 는 모든 주문에서 각 개별 항목에 대 한 행이 하나씩 포함 되어야 합니다. 잠재적 열은 다음과 같습니다.

| 열 이름 | 설명 |
|----|----|
| `Order item ID` | 주문 항목 ID는 테이블의 모든 행에 대해 고유 해야 합니다. 이는 일반적으로 테이블의 경우에도 해당 `primary key` 됩니다. |
| `Order ID` | 주문의 ID입니다. |
| `Product ID` | 제품의 ID입니다. |
| `Product name` | 제품의 이름입니다. |
| `Product's unit price` | 제품의 단일 단위 가격입니다. |
| `Quantity` | 주문에 있는 제품의 수량입니다. |

## `Customers` 테이블 {#customerstable}

이 표에는 `customers` 각 고객 계정에 대 한 행이 하나씩 들어 있어야 합니다. 잠재적 열은 다음과 같습니다.

| 열 이름 | 설명 |
|----|----|
| `Customer ID` | 고객 ID는 테이블의 모든 행에 대해 고유 해야 합니다. 또한 일반적으로 테이블에 대 한 기본 키입니다. |
| `Customer created at` | 고객의 계정를 만든 날짜와 시간입니다. |
| `Customer modified at` | 고객의 계정 마지막으로 수정한 날짜와 시간입니다. |
| `Acquisition/marketing channel source` | 고객이 참조 한 확보 또는 마케팅 채널입니다. |
| `Demographic info` | 연령 범위 및 성별과 같은 인구 통계 정보를 사용 하 여 보고서를 세그먼트 수 있습니다. |
| `Acquisition/marketing channel` | 주문이 접수 된 고객이 언급 한 확보 또는 마케팅 채널입니다. |

## `Subscription payments` 테이블

테이블에 `subscriptions` 는 각 가입 지불에 대해 하나의 행이 포함 되어야 합니다. 잠재적 열은 다음과 같습니다.

| 열 이름 | 설명 |
|----|----|
| `Subscription ID` | 구독 ID는 테이블의 모든 행에 대해 고유 해야 합니다. 또한 일반적으로 테이블에 대 한 기본 키입니다. |
| `Customer ID` | 지불을 한 고객의 ID입니다. |
| `Payment amount` | 가입 지불 금액입니다. |
| `Start date` | 지불이 덮고 있는 기간의 시작 날짜/시간입니다. |
| `End date` | 지불이 덮고 있는 기간의 종료 날짜/시간입니다. |
