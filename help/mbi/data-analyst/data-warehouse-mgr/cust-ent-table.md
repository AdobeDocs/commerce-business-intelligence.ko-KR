---
title: customer_entity 테이블
description: 등록된 모든 계정의 레코드에 액세스하는 방법을 알아봅니다.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# customer_entity 테이블

다음 `customer_entity` 테이블에는 등록된 모든 계정의 레코드가 포함되어 있습니다. 구매가 완료되었는지 여부에 상관없이 계정에 등록하는 경우 계정이 등록된 것으로 간주됩니다. 각 행은 해당 계정의 `entity_id`.

이 표에는 게스트 체크아웃을 통해 주문을 수행하는 고객의 레코드가 포함되어 있지 않습니다. 손님 체크아웃을 수락하시면, [계정 방법 알아보기](../data-warehouse-mgr/guest-orders.md) 해당 고객에 대한 것입니다.

## 공통 열

| **열 이름** | **설명** |
|---|---|
| `created_at` | 계정의 등록 날짜에 해당하는 타임스탬프이며 일반적으로 UTC에 로컬로 저장됩니다. 의 구성에 따라 [!DNL MBI]로 지정하는 경우 이 타임스탬프가 [!DNL MBI] 데이터베이스 시간대와 다른 |
| `email` | 계정과 연결된 이메일 주소 |
| `entity_id` (PK) | 테이블의 고유 식별자이며, 일반적으로 `customer_id` 인스턴스 내의 다른 테이블에서 |
| `group_id` | 와 연결된 외부 키 `customer_group` 테이블. 가입 대상 `customer_group.customer_group_id` 등록된 계정과 연결된 고객 그룹을 확인하려면 |
| `store_id` | 와 연결된 외부 키 `store` 테이블. 가입 대상 `store`.`store_id` 등록된 계정과 연결된 상거래 스토어 보기를 확인하려면 |

{style=&quot;table-layout:auto&quot;}

## 일반적인 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Customer's first 30 day revenue` | 고객의 첫 번째 주문 일자로부터 30일 이내에 이 고객이 수행한 모든 주문에 대한 총 매출입니다. 가입으로 계산됨 `customer_entity.entity_id` to `sales_order.customer_id` 그리고 합하여 `base_grand_total` 모든 주문에 대한 필드 `sales_order.Seconds between customer's first order date and this order` ≤ 2592000: 30일 동안의 초 수입니다 |
| `Customer's first order date` | 이 고객이 수행한 첫 번째 주문의 타임스탬프입니다. 가입으로 계산됨 `customer_entity.entity_id` to `sales_order.customer_id` 최소값 반환 `sales_order`.`created_at` value |
| `Customer's first order's billing region` | 고객의 첫 번째 주문과 연관된 청구 영역입니다. 가입으로 계산됨 `customer_entity.entity_id` to `sales_order.customer_id` 재방문 `Billing address region` 여기서 `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | 고객의 첫 번째 주문과 연관된 쿠폰 코드입니다. 가입으로 계산됨 `customer_entity.entity_id` to `sales_order.customer_id` 재방문 `sales_order.coupon_code` 여기서 `sales_order.Customer's order number` = 1 |
| `Customer's group code` | 등록된 고객의 그룹 이름입니다. 가입으로 계산됨 `customer_entity.group_id` to `customer_group`.`customer_group_id` 재방문 `customer_group_code` 필드 |
| `Customer's lifetime number of coupons` | 이 고객이 수행한 모든 주문에 적용된 총 쿠폰 수입니다. 가입으로 계산됨 `customer_entity.entity_id` to `sales_order.customer_id` 그리고 `sales_order.coupon_code` is not `NULL` |
| `Customer's lifetime number of orders` | 이 고객이 수행한 총 주문 수입니다. 가입으로 계산됨 `customer_entity.entity_id` to `sales_order.customer_id` 및 `sales_order` 표 |
| `Customer's lifetime revenue` | 이 고객이 수행한 모든 주문에 대한 총 매출액. 가입으로 계산됨 `customer_entity.entity_id` to `sales_order.customer_id` 그리고 합하여 `base_grand_total` 이 고객이 수행한 모든 주문에 대한 필드 |
| `Seconds since customer's first order date` | 고객의 첫 번째 주문 날짜와 현재 사이의 경과 시간입니다. 빼서 계산됨 `Customer's first order date` 쿼리 실행 시 서버 타임스탬프에서 정수(초)로 반환됩니다 |
| `Store name` | 이 등록된 계정과 연결된 상거래 저장소의 이름입니다. 가입으로 계산됨 `customer_entity.store_id` to `store.store_id` 재방문 `name` 필드 |

{style=&quot;table-layout:auto&quot;}

## 일반 지표

| **지표 이름** | **설명** | **건설** |
|---|---|---|
| `Avg first 30 day revenue` | 고객의 첫 번째 주문 후 30일 이내에 수행한 주문에 대한 고객당 평균 매출액 | 작업: 평균<br/>피연산자: `Customer's first 30 day revenue`<br/>타임스탬프: `created_at`<br/>필터:<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000(최초 주문 후 30일이 경과하지 않은 고객 제외) |
| `Avg lifetime coupons` | 평생 동안 고객당 주문에 적용된 평균 쿠폰 수 | 작업: 평균<br/>피연산자: `Customer's lifetime number of coupons`<br/>타임스탬프: `created_at` |
| `Avg lifetime orders` | 고객당 라이프타임 동안 수행한 평균 주문 수 | 작업: 평균<br/>피연산자: `Customer's lifetime number of orders`<br/>타임스탬프: `created_at` |
| `Avg lifetime revenue` | 라이프타임 동안 수행한 모든 주문에 대한 고객당 평균 총 매출액 | 작업: 평균<br/>피연산자: `Customer's lifetime revenue`<br/>타임스탬프: `created_at` |
| `New customers` | 첫 번째 주문 날짜에 계산되는 하나 이상의 주문이 있는 고객 수입니다. 등록을 했지만 주문을 하지 않는 계정을 제외합니다. | 작업: 카운트<br/>피연산자: `entity_id`<br/>타임스탬프: `Customer's first order date` |
| `Registered accounts` | 등록된 계정 수입니다. 계정이 주문을 했는지 여부에 관계없이 등록된 모든 계정을 포함합니다 | 작업: 카운트<br/>피연산자: `entity_id`<br/>타임스탬프: `created_at` |

{style=&quot;table-layout:auto&quot;}

## 외래 키 연결 경로

`customer_group`

* 가입 대상 `customer_group` 등록된 계정의 고객 그룹 이름을 반환하는 새 열을 만들 수 있습니다.
   * 경로: `customer_entity.group_id` (다) => `customer_group.customer_group_id` (1)

`store`

* 가입 대상 `store` 등록된 계정과 연결된 저장소와 관련된 세부 정보를 반환하는 새 열을 만들 수 있습니다.
   * 경로: `customer_entity.store_id` (다) => `store.store_id` (1)
