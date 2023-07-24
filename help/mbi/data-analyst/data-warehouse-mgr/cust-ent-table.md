---
title: customer_entity 테이블
description: 등록된 모든 계정의 레코드에 액세스하는 방법을 알아봅니다.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# customer_entity 테이블

다음 `customer_entity` 테이블에는 등록된 모든 계정의 기록이 들어 있습니다. 구매 완료 여부와 관계없이 계정에 등록하면 계정이 등록된 것으로 간주됩니다. 각 행은 해당 계정에 의해 식별되는 하나의 등록된 고유 계정에 해당합니다. `entity_id`.

이 표에는 게스트 체크아웃을 통해 주문한 고객의 기록이 들어 있지 않습니다. 스토어에서 게스트 체크아웃을 수락하는 경우 [게스트 주문 처리 방법](../data-warehouse-mgr/guest-orders.md) 주문을위한.

## 공통 열

| **열 이름** | **설명** |
|---|---|
| `created_at` | 계정의 등록 날짜에 해당하는 타임스탬프가 UTC로 로컬에 저장됩니다. 의 구성에 따라 [!DNL Commerce Intelligence], 이 타임스탬프는에서 보고 시간대로 변환될 수 있습니다. [!DNL Commerce Intelligence] 데이터베이스 시간대와 다릅니다. |
| `email` | 계정과 연결된 이메일 주소 |
| `entity_id` (PK) | 테이블에 대한 고유 식별자로, 조인 시 일반적으로 사용됩니다. `customer_id` 인스턴스 내의 다른 테이블에서 |
| `group_id` | 와(과) 연결된 외래 키 `customer_group` 테이블. 가입 대상 `customer_group.customer_group_id` 등록된 계정과 연계된 고객 그룹 확인 |
| `store_id` | 와(과) 연결된 외래 키 `store` 테이블. 가입 대상 `store`.`store_id` 등록된 계정과 연결된 Commerce 스토어 보기를 확인하려면 |

{style="table-layout:auto"}

## 공통 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Customer's first 30 day revenue` | 고객의 첫 번째 주문 일자로부터 30일 이내에 이 고객이 수행한 모든 주문의 총 매출액 합계. 조인으로 계산됨 `customer_entity.entity_id` 끝 `sales_order.customer_id` 및 합계 `base_grand_total` 모든 주문에 대한 필드 `sales_order.Seconds between customer's first order date and this order` ≤ 2592000: 30일 동안의 초 수입니다. |
| `Customer's first order date` | 해당 고객이 주문한 첫 번째 주문의 타임스탬프. 조인으로 계산됨 `customer_entity.entity_id` 끝 `sales_order.customer_id` 최소값 반환 `sales_order`.`created_at` 값 |
| `Customer's first order's billing region` | 고객의 첫 번째 주문과 연계된 청구 지역. 조인으로 계산됨 `customer_entity.entity_id` 끝 `sales_order.customer_id` 및 반환 `Billing address region` 위치 `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | 고객의 첫 번째 주문과 연계된 쿠폰 코드. 조인으로 계산됨 `customer_entity.entity_id` 끝 `sales_order.customer_id` 및 반환 `sales_order.coupon_code` 위치 `sales_order.Customer's order number` = 1 |
| `Customer's group code` | 등록된 고객의 그룹 이름. 조인으로 계산됨 `customer_entity.group_id` 끝 `customer_group`.`customer_group_id` 및 반환 `customer_group_code` 필드 |
| `Customer's lifetime number of coupons` | 이 고객이 수행한 모든 주문에 적용된 총 쿠폰 수입니다. 조인으로 계산됨 `customer_entity.entity_id` 끝 `sales_order.customer_id` 주문 수 계산 `sales_order.coupon_code` 은(는) 아님 `NULL` |
| `Customer's lifetime number of orders` | 이 고객이 수행한 총 주문 수. 조인으로 계산됨 `customer_entity.entity_id` 끝 `sales_order.customer_id` 및 계산 `sales_order` 표 |
| `Customer's lifetime revenue` | 이 고객이 수행한 모든 주문에 대한 총 매출액 합계. 조인으로 계산됨 `customer_entity.entity_id` 끝 `sales_order.customer_id` 및 합계 `base_grand_total` 이 고객이 수행한 모든 주문에 대한 필드 |
| `Seconds since customer's first order date` | 고객의 첫 번째 주문 일자와 지금 사이의 경과 시간. 빼서 계산됨 `Customer's first order date` 쿼리가 실행될 때의 서버 타임스탬프에서 정수로 반환됩니다 |
| `Store name` | 등록된 이 계정과 연결된 상거래 저장소의 이름입니다. 조인으로 계산됨 `customer_entity.store_id` 끝 `store.store_id` 및 반환 `name` 필드 |

{style="table-layout:auto"}

## 일반 지표

| **지표 이름** | **설명** | **구성** |
|---|---|---|
| `Avg first 30 day revenue` | 고객의 첫 번째 주문 후 30일 이내에 수행한 주문의 고객당 평균 매출액 | 공정: 평균<br/>피연산자: `Customer's first 30 day revenue`<br/>타임스탬프: `created_at`<br/>필터:<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000(첫 주문 후 아직 30일에 도달하지 않은 고객 제외) |
| `Avg lifetime coupons` | 라이프타임 동안 고객당 주문에 적용된 평균 쿠폰 수 | 공정: 평균<br/>피연산자: `Customer's lifetime number of coupons`<br/>타임스탬프: `created_at` |
| `Avg lifetime orders` | 라이프타임 동안 고객당 수행한 평균 주문 수 | 공정: 평균<br/>피연산자: `Customer's lifetime number of orders`<br/>타임스탬프: `created_at` |
| `Avg lifetime revenue` | 라이프타임 동안 수행한 모든 주문에 대한 고객당 평균 총 매출액 | 공정: 평균<br/>피연산자: `Customer's lifetime revenue`<br/>타임스탬프: `created_at` |
| `New customers` | 첫 번째 주문 날짜에 계산되는 하나 이상의 주문이 있는 고객 수입니다. 등록하지만 주문하지 않은 계정 제외 | 작업: 카운트<br/>피연산자: `entity_id`<br/>타임스탬프: `Customer's first order date` |
| `Registered accounts` | 등록된 계정 수. 계정이 주문을 했는지 여부에 관계없이 등록된 모든 계정을 포함합니다. | 작업: 카운트<br/>피연산자: `entity_id`<br/>타임스탬프: `created_at` |

{style="table-layout:auto"}

## 외래 키 조인 경로

`customer_group`

* 가입 대상 `customer_group` 등록된 계정의 고객 그룹 이름을 반환하는 열을 만드는 테이블입니다.
   * 경로: `customer_entity.group_id` (다) => `customer_group.customer_group_id` (1)

`store`

* 가입 대상 `store` 등록된 계정과 연결된 저장소 관련 세부 정보를 반환하는 열을 만드는 테이블입니다.
   * 경로: `customer_entity.store_id` (다) => `store.store_id` (1)
