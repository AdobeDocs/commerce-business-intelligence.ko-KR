---
title: sales_order 테이블
description: sales_order 테이블을 사용하여 작업하는 방법을 알아봅니다.
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 0%

---

# `sales_order` 표

다음 `sales_order` 테이블 (`sales_flat_order` M1)에서 각 주문이 캡처됩니다. 주문을 개별 행으로 분할하는 Commerce의 일부 사용자 지정 구현이 있지만, 대부분의 경우 각 행은 하나의 고유한 순서를 나타냅니다.

이 표에는 게스트 체크아웃을 통해 해당 주문이 처리되었는지 여부에 관계없이 모든 고객 주문이 포함되어 있습니다. 스토어에서 게스트 체크아웃을 수락하면 이에 대한 자세한 정보를 찾을 수 있습니다 [사용 사례](../data-warehouse-mgr/guest-orders.md).

## 공통 열

| **열 이름** | **설명** |
|---|---|
| `base_currency_code` | 캡처된 모든 값에 대한 통화 `base_*` 필드(즉, `base_grand_total`, `base_subtotal`, 등). 일반적으로 상거래 저장소의 기본 통화를 반영합니다 |
| `base_discount_amount` | 주문에 적용된 할인 값 |
| `base_grand_total` | 모든 세금, 배송 및 할인이 적용된 후 고객이 주문에서 지불한 최종 가격. 정확한 계산은 일반적으로 사용자 지정할 수 있지만 `base_grand_total` 는 `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | 주문에 포함된 모든 품목의 총 상품 값입니다. 세금, 배송, 할인 등은 포함되지 않습니다 |
| `base_shipping_amount` | 주문에 적용된 배송 값 |
| `base_tax_amount` | 주문에 적용된 세금 값 |
| `billing_address_id` | `Foreign key` 관련 `sales_order_address` 테이블. 가입 대상 `sales_order_address.entity_id` 주문과 연관된 청구 주소 상세내역을 확인하려면 |
| `coupon_code` | 주문에 적용된 쿠폰입니다. 쿠폰이 적용되지 않으면 이 필드는 `NULL` |
| `created_at` | 주문의 생성 타임스탬프이며, 일반적으로 UTC에 로컬로 저장됩니다. 의 구성에 따라 [!DNL MBI]로 지정하는 경우 이 타임스탬프가 [!DNL MBI] 데이터베이스 시간대와 다른 |
| `customer_email` | 주문하는 고객의 이메일 주소입니다. 이 값은 게스트 체크아웃을 통해 처리된 주문을 포함하여 모든 상황에서 채워집니다 |
| `customer_group_id` | 와 연결된 외부 키 `customer_group` 테이블. 가입 대상 `customer_group.customer_group_id` 주문과 연관된 고객 그룹을 확인하려면 |
| `customer_id` | `Foreign key` 관련 `customer_entity` 테이블(고객이 등록된 경우) 가입 대상 `customer_entity.entity_id` 를 눌러 주문과 연관된 고객 속성을 결정합니다. 게스트 체크아웃을 통해 주문을 수행한 경우 이 필드는 `NULL` |
| `entity_id` (PK) | 테이블의 고유 식별자이며, 상거래 인스턴스 내의 다른 테이블에 대한 조인에 일반적으로 사용됩니다 |
| `increment_id` | 주문에 대한 고유 식별자 및 일반적으로 `order_id` Adobe Commerce 내에서 사용할 수 있습니다. 다음 `increment_id` 과 같이 외부 소스에 대한 조인에 가장 많이 사용됩니다. [!DNL Google Ecommerce] |
| `shipping_address_id` | 와 연결된 외부 키 `sales_order_address` 테이블. 가입 대상 `sales_order_address.entity_id` 주문과 연관된 배송 주소 상세내역을 확인하려면 |
| `status` | 주문 상태 상거래 인스턴스에 구현된 사용자 지정 상태 뿐만 아니라 &#39;complete&#39;, &#39;processing&#39;, &#39;cancelled&#39;, &#39;revolved&#39; 등의 값을 반환할 수 있습니다. 주문이 처리되면 변경될 수 있습니다 |
| `store_id` | `Foreign key` 관련 `store` 테이블. 가입 대상 `store`.`store_id` 주문과 연결된 상거래 스토어 보기를 확인하려면 |

{style=&quot;table-layout:auto&quot;}

## 일반적인 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Billing address city` | 주문에 대한 청구 시입니다. 가입으로 계산됨 `sales_order`.`billing_address_id` to `sales_order_address`.`entity_id` 재방문 `city` 필드 |
| `Billing address country` | 주문에 대한 청구 국가 코드입니다. 가입으로 계산됨 `sales_order`.`billing_address_id` to `sales_order_address`.`entity_id` 재방문 `country_id` |
| `Billing address region` | 주문에 대한 청구 지역(대부분의 경우 주 또는 도)입니다. 가입으로 계산됨 `sales_order`.`billing_address_id` to `sales_order_address`.`entity_id` 재방문 `region` 필드 |
| `Customer's first order date` | 이 고객이 수행한 첫 번째 주문의 타임스탬프입니다. 종종 고객에 대한 &quot;획득 날짜&quot;로 간주됩니다. 최소값을 반환하여 계산됩니다 `sales_order`.`created_at` 각 고유 고객의 가치 |
| `Customer's first order's billing region` | 주문을 수행한 고객의 획득 청구 영역입니다. 를 반환하여 계산됩니다. `Billing address region` 고객의 첫 번째 주문과 연관됨 |
| `Customer's first order's coupon_code` | 이 주문을 한 고객에 대한 획득 쿠폰 코드입니다. 를 반환하여 계산됩니다. `coupon_code` 고객의 첫 번째 주문과 연관됨 |
| `Customer's group code` | 이 주문을 수행한 고객의 그룹 이름입니다. 가입으로 계산됨 `sales_order`.`customer_group_id` to `customer_group`.`customer_group_id` 재방문 `customer_group_code` 필드 |
| `Customer's lifetime number of coupons` | 이 고객이 수행한 모든 주문에 적용된 쿠폰의 총 수량입니다. 다음 위치에서 주문 수를 계산하여 계산됩니다. `coupon_code` is not `NULL` 각 고유 고객에 대해 |
| `Customer's lifetime number of orders` | 이 고객이 수행한 총 주문 수입니다. 에서 행 수를 계산하여 계산됩니다 `sales_order` 각 고유 고객에 대한 테이블 |
| `Customer's lifetime revenue` | 이 고객이 수행한 모든 주문에 대한 총 매출액. 를 합하여 계산됩니다. `base_grand_total` 각 고유 고객의 모든 주문에 대한 필드 |
| `Customer's order number` | 이 고객의 주문에 대한 순차적 순서 등급입니다. 고객이 수행한 모든 주문을 식별하여 `created_at` 타임스탬프 및 각 주문에 증분 정수 값 할당 예를 들어 고객의 첫 번째 주문에 대해 `Customer's order number` 1. 두 번째 주문은 `Customer's order number` 2. 기타 |
| `Customer's order number (previous-current)` | 이 순서의 순서와 연결된 고객의 이전 순서의 등급에서 `-` 문자. 연결(&quot;`Customer's order number` - &quot;)가 있는 경우`-`&quot; 다음에 &quot;`Customer's order number`&quot;. 예를 들어, 고객의 두 번째 구매와 연결된 주문에 대해 이 열은 값을 반환합니다 `1-2`. 대부분의 경우 두 주문 이벤트 사이의 시간(즉, &quot;주문 사이의 시간&quot; 차트에서)을 나타낼 때 사용됩니다 |
| `Is customer's last order?` | 주문이 고객의 마지막 주문인지 가장 최근 주문인지 여부를 결정합니다. 를 비교하여 계산됩니다. `Customer's order number` 다음 값 `Customer's lifetime number of orders`. 이 두 필드가 지정된 순서에 대해 같으면 이 열은 &quot;예&quot;를 반환합니다. 그렇지 않으면 &quot;No&quot;를 반환합니다 |
| `Number of items in order` | 주문에 포함된 항목의 총 수량입니다. 가입으로 계산됨 `sales_order`.`entity_id` to `sales_order_item`.`order_id` 그리고 합하여 `sales_order_item`.`qty_ordered` 필드 |
| `Seconds between customer's first order date and this order` | 이 주문과 고객의 첫 번째 주문 사이의 경과 시간입니다. 빼서 계산됨 `Customer's first order date` 에서 `created_at` 각 주문에 대해 정수(초)로 반환됩니다 |
| `Seconds since previous order` | 이 주문과 고객의 바로 이전 주문 사이의 경과 시간. 을(를) 뺀 숫자 `created_at` 이전 주문에서 `created_at` 이 순서 중 정수(초)로 반환됩니다. 예를 들어, 고객의 세 번째 주문에 해당하는 주문 레코드의 경우, 이 열은 고객의 두 번째 주문과 세 번째 주문 사이의 시간(초)을 반환합니다. 고객의 첫 번째 주문에 대해 이 필드는 반환됩니다 `NULL` |
| `Shipping address city` | 주문시 배송도시입니다 가입으로 계산됨 `sales_order`.`shipping_address_id` to `sales_order_address`.`entity_id` 재방문 `city` 필드 |
| `Shipping address country` | 주문에 대한 배송 국가 코드입니다. 가입으로 계산됨 `sales_order`.`Shipping_address_id` to `sales_order_address`.`entity_id` 재방문 `country_id` |
| `Shipping address region` | 주문에 대한 운송 지역(대부분의 경우 주 또는 도)입니다. 가입으로 계산됨 `sales_order`.`shipping_address_id` to `sales_order_address`.`entity_id` 재방문 `region` 필드 |
| `Store name` | 이 주문과 연결된 상거래 저장소의 이름입니다. 가입으로 계산됨 `sales_order`.`store_id` to `store`.`store_id` 재방문 `name` 필드 |

## 일반 지표

| **지표 이름** | **설명** | **건설** |
|---|---|---|
| `Avg order value` | 매출이 로 정의된 주문당 평균 매출액 `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | 모든 고객과 주문에 대해 고객의 (n-1) 주문과 n번째 주문 사이의 평균 시간입니다 | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | 모든 세금 및 할인이 적용되기 전에 GMV가 소계로 정의된 모든 주문에 대한 총 상품 값의 합계 | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | 모든 고객과 주문에 대해 고객의 (n-1) 주문과 n번째 주문 사이의 중간값 시간입니다 | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | 총 주문 수 | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | 모든 주문에 대한 수익 합계. 여기서 수익은 모든 세금, 할인, 운송 등이 적용된 후 고객이 지불한 최종 가격으로 정의됩니다 | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | 모든 주문에 대한 출하 금액의 합계 | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | 모든 주문에 적용되는 세금의 합계 | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | 주어진 보고 시간 간격으로 주문을 배치하는 고유 고객 수입니다. 예를 들어 보고서 간격이 주별 경우, 지정된 주에 하나 이상의 주문을 배치하는 각 고객은 해당 주에 수행한 주문 수에 관계없이 정확히 한 번 계산됩니다 | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` 경로 결합

`customer_entity`

* 가입 대상 `customer_entity` 주문을 한 고객과 연관된 새 고객 레벨 열을 생성할 수 있는 테이블입니다.
   * 경로: `sales_order.customer_id` (다) => `customer_entity.entity_id` (1)

`customer_group`

* 가입 대상 `customer_group` 주문을 수행한 고객의 고객 그룹 이름을 반환하는 새 열을 만들 수 있는 표입니다.
   * 경로: `sales_order.customer_group_id` (다) => `customer_group.customer_group_id` (1)

`sales_order_address`

* 가입 대상 `sales_order_address` 테이블과 함께 청구 및 운송 위치를 반환하는 새 열을 생성할 수 있습니다. 청구 또는 배송 세부 정보가 필요한지 여부에 따라 두 개의 연결 경로가 가능합니다.
   * 경로:
      * 배송: `sales_order.shipping_address_id`(다) => `sales_order_address.entity_id` (1)
      * 청구: `sales_order.billing_address_id`(다) => `sales_order_address.entity_id` (1)

`store`

* 가입 대상 `store` 테이블과 연결된 상거래 저장소와 관련된 세부 정보를 반환하는 새 열을 만들 수 있습니다.
   * 경로: `sales_order.store_id` (다) => `store.store_id` (1)
