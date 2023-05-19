---
title: sales_order 테이블
description: sales_order 테이블을 사용하여 작업하는 방법을 알아봅니다.
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# `sales_order` 표

다음 `sales_order` 표 (`sales_flat_order` 에서 M1)은 각 주문이 캡처되는 위치입니다. 일반적으로, Commerce에 주문을 별도의 행으로 분할하는 사용자 지정 구현이 있지만 각 행은 하나의 고유한 순서를 나타냅니다.

이 표에는 해당 주문이 게스트 체크아웃을 통해 처리되었는지 여부에 관계없이 모든 고객 주문이 포함됩니다. 스토어에서 게스트 체크아웃을 수락하면 이에 대한 자세한 정보를 찾을 수 있습니다 [사용 사례](../data-warehouse-mgr/guest-orders.md).

## 공통 열

| **열 이름** | **설명** |
|---|---|
| `base_currency_code` | 캡처된 모든 값에 대한 통화 `base_*` 필드 (즉, `base_grand_total`, `base_subtotal`등). 이는 일반적으로 상거래 저장소의 기본 통화를 반영합니다 |
| `base_discount_amount` | 주문에 적용된 할인 값 |
| `base_grand_total` | 세금, 배송, 할인이 모두 적용된 후 고객이 주문에 대해 지불하는 최종 가격. 정확한 계산은 사용자 정의가 가능하지만 일반적으로 `base_grand_total` 다음과 같이 계산됩니다. `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | 주문에 포함된 모든 품목의 총 상품 가치. 세금, 배송, 할인 등은 포함되지 않습니다 |
| `base_shipping_amount` | 주문에 적용된 배송 값 |
| `base_tax_amount` | 주문에 적용된 세금 값 |
| `billing_address_id` | `Foreign key` 과(와) 연계됨 `sales_order_address` 테이블. 가입 대상 `sales_order_address.entity_id` 주문과 연관된 청구 주소 상세내역을 확인하려면 |
| `coupon_code` | 주문에 적용된 쿠폰. 적용된 쿠폰이 없는 경우 이 필드는 다음과 같습니다. `NULL` |
| `created_at` | UTC로 로컬에 저장된 주문의 생성 타임스탬프. 의 구성에 따라 [!DNL Commerce Intelligence], 이 타임스탬프는에서 보고 시간대로 변환될 수 있습니다. [!DNL Commerce Intelligence] 데이터베이스 시간대와 다릅니다. |
| `customer_email` | 주문 고객의 이메일 주소. 이 값은 게스트 체크아웃을 통해 처리된 주문을 포함하여 모든 상황에서 채워집니다 |
| `customer_group_id` | 와(과) 연결된 외래 키 `customer_group` 테이블. 가입 대상 `customer_group.customer_group_id` 주문과 연계된 고객 그룹 확인 |
| `customer_id` | `Foreign key` 과(와) 연계됨 `customer_entity` 테이블(고객이 등록된 경우). 가입 대상 `customer_entity.entity_id` 주문과 연관된 고객 속성을 확인합니다. 주문이 게스트 체크아웃을 통해 이루어진 경우 이 필드는 다음과 같습니다. `NULL` |
| `entity_id` (PK) | 테이블에 대한 고유 식별자로, Commerce 인스턴스 내의 다른 테이블에 대한 조인에 일반적으로 사용됩니다. |
| `increment_id` | 주문에 대한 고유 식별자로, 일반적으로 (으)로 지칭됨 `order_id` Adobe Commerce 내. 다음 `increment_id` 는 다음과 같은 외부 소스 조인에 가장 많이 사용됩니다. [!DNL Google Ecommerce] |
| `shipping_address_id` | 와(과) 연결된 외래 키 `sales_order_address` 테이블. 가입 대상 `sales_order_address.entity_id` 주문과 연계된 배송 주소 세부 정보를 확인하려면 |
| `status` | 주문 상태. 상거래 인스턴스에 구현된 &#39;완료&#39;, &#39;처리&#39;, &#39;취소됨&#39;, &#39;환불됨&#39; 및 모든 사용자 지정 상태와 같은 값을 반환할 수 있습니다. 주문이 처리되면 변경될 수 있습니다. |
| `store_id` | `Foreign key` 과(와) 연계됨 `store` 테이블. 가입 대상 `store`.`store_id` 주문과 연결된 상거래 스토어 보기를 확인하려면 |

{style="table-layout:auto"}

## 공통 계산된 열

| **열 이름** | **설명** |
|---|---|
| `Billing address city` | 주문에 대한 청구 도시입니다. 조인으로 계산됨 `sales_order`.`billing_address_id` 끝 `sales_order_address`.`entity_id` 및 반환 `city` 필드 |
| `Billing address country` | 주문에 대한 청구 국가 코드. 조인으로 계산됨 `sales_order`.`billing_address_id` 끝 `sales_order_address`.`entity_id` 및 반환 `country_id` |
| `Billing address region` | 주문에 대한 청구 지역(대개는 주 또는 시/도)입니다. 조인으로 계산됨 `sales_order`.`billing_address_id` 끝 `sales_order_address`.`entity_id` 및 반환 `region` 필드 |
| `Customer's first order date` | 해당 고객이 주문한 첫 번째 주문의 타임스탬프. 고객의 &quot;인수 날짜&quot;로 간주되는 경우가 많습니다. 최소값을 반환하여 계산됨 `sales_order`.`created_at` 각 고유 고객에 대한 값 |
| `Customer's first order's billing region` | 주문을 한 고객에 대한 고객 확보 청구 지역. 를 반환하여 계산됨 `Billing address region` 고객의 첫 번째 주문과 연계됨 |
| `Customer's first order's coupon_code` | 해당 주문을 한 고객에 대한 고객 확보 쿠폰 코드. 를 반환하여 계산됨 `coupon_code` 고객의 첫 번째 주문과 연계됨 |
| `Customer's group code` | 이 주문을 한 고객의 그룹 이름. 조인으로 계산됨 `sales_order`.`customer_group_id` 끝 `customer_group`.`customer_group_id` 및 반환 `customer_group_code` 필드 |
| `Customer's lifetime number of coupons` | 이 고객이 수행한 모든 주문에 적용된 총 쿠폰 수량입니다. 다음 위치에 있는 주문 수를 계산하여 계산 `coupon_code` 은(는) 아님 `NULL` 각 고유 고객용 |
| `Customer's lifetime number of orders` | 이 고객이 수행한 총 주문 수. 의 행 수를 계산하여 계산됩니다. `sales_order` 각 고유 고객에 대한 테이블 |
| `Customer's lifetime revenue` | 이 고객이 수행한 모든 주문에 대한 총 매출액 합계. 다음을 합산하여 계산됨 `base_grand_total` 각 고유 고객의 모든 주문에 대한 필드 |
| `Customer's order number` | 해당 고객 주문에 대한 순차적 주문 등급. 고객이 수행한 모든 주문을 식별하고 를 기준으로 오름차순으로 정렬하여 계산됩니다. `created_at` 타임스탬프 및 각 주문에 증가하는 정수 값 할당. 예를 들어 고객의 첫 번째 주문은 `Customer's order number` 중 1에 해당하는 고객의 두 번째 주문은 `Customer's order number` 2개 등 |
| `Customer's order number (previous-current)` | 고객의 이전 주문 등급과 이 주문 등급이 연결된 후 `-` 문자. 를 연결하여 계산됨(&quot;`Customer's order number` - 1&quot;)(&quot; 포함)`-`&quot; 뒤에 &quot;`Customer's order number`&quot;. 예를 들어, 고객의 두 번째 구매와 연관된 주문의 경우 이 열은 다음 값을 반환합니다. `1-2`. 두 주문 이벤트 사이의 시간을 나타낼 때 가장 많이 사용됩니다(즉, &quot;주문 사이의 시간&quot; 차트). |
| `Is customer's last order?` | 해당 주문이 고객의 마지막 주문에 해당하는지 아니면 가장 최근 주문에 해당하는지 여부를 결정합니다. 다음을 비교하여 계산됨 `Customer's order number` 값: `Customer's lifetime number of orders`. 이 두 필드가 지정된 순서에 대해 같으면 이 열이 반환됩니다 `Yes`; 그렇지 않으면 `No` |
| `Number of items in order` | 주문에 포함된 항목의 총 수량입니다. 조인으로 계산됨 `sales_order`.`entity_id` 끝 `sales_order_item`.`order_id` 및 합계 `sales_order_item`.`qty_ordered` 필드 |
| `Seconds between customer's first order date and this order` | 이 주문과 고객의 첫 번째 주문 사이의 경과 시간입니다. 빼서 계산됨 `Customer's first order date` 다음에서 `created_at` 각 주문에 대해 초 단위의 정수로 반환됨 |
| `Seconds since previous order` | 이 주문과 고객의 직전 주문 사이의 경과 시간. 다음을 빼서 계산됨 `created_at` 의 이전 주문에 대한 `created_at` (이 주문의 경우, 초 단위의 정수)로 반환됩니다. 예를 들어, 고객의 세 번째 주문에 해당하는 주문 레코드의 경우 이 열은 고객의 두 번째 주문과 세 번째 주문 사이의 시간(초)을 반환합니다. 고객의 첫 번째 주문에 대해 이 필드는 를 반환합니다 `NULL` |
| `Shipping address city` | 주문에 대한 배송 도시입니다. 조인으로 계산됨 `sales_order`.`shipping_address_id` 끝 `sales_order_address`.`entity_id` 및 반환 `city` 필드 |
| `Shipping address country` | 주문에 대한 배송 국가 코드. 조인으로 계산됨 `sales_order`.`Shipping_address_id` 끝 `sales_order_address`.`entity_id` 및 반환 `country_id` |
| `Shipping address region` | 주문에 대한 배송 지역(대부분의 경우 주 또는 시). 조인으로 계산됨 `sales_order`.`shipping_address_id` 끝 `sales_order_address`.`entity_id` 및 반환 `region` 필드 |
| `Store name` | 이 주문과 연계된 상거래 스토어의 이름. 조인으로 계산됨 `sales_order`.`store_id` 끝 `store`.`store_id` 및 반환 `name` 필드 |

## 일반 지표

| **지표 이름** | **설명** | **구성** |
|---|---|---|
| `Avg order value` | 매출이 다음으로 정의되는 주문당 평균 수익 `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | 모든 고객 및 주문에 대한 고객의 (n-1) 주문과 n번째 주문 간의 평균 시간 | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | 모든 세금 및 할인이 적용되기 전에 GMV가 소계로 정의되는 모든 주문에 대한 총 상품 가치의 합계 | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | 모든 고객 및 주문에 대한 고객의 (n-1) 주문과 n번째 주문 간의 평균 시간 | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | 주문된 총 주문 수 | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | 모든 세금, 할인, 운송 등이 적용된 후 매출이 고객이 최종 지불한 가격으로 정의되는 모든 주문에 대한 매출의 합계 | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | 모든 주문에 대한 배송 금액의 합계 | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | 모든 주문에 적용된 세금의 합계 | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | 지정된 보고 시간 간격으로 주문을 한 고유 고객의 수입니다. 예를 들어 보고서의 간격이 주별이면 주어진 주에 하나 이상의 주문을 한 각 고객은 그 주에 수행한 주문 수에 관계없이 정확히 1회로 계산됩니다 | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` 패스 연결

`customer_entity`

* 가입 대상 `customer_entity` 테이블 - 주문한 고객과 연관된 새 고객 수준 열을 생성합니다.
   * 경로: `sales_order.customer_id` (다) => `customer_entity.entity_id` (1)

`customer_group`

* 가입 대상 `customer_group` 테이블 - 주문을 한 고객의 고객 그룹명을 반환하는 열을 생성합니다.
   * 경로: `sales_order.customer_group_id` (다) => `customer_group.customer_group_id` (1)

`sales_order_address`

* 가입 대상 `sales_order_address` 주문과 연관된 청구 및 운송 위치를 반환하는 열을 만드는 테이블입니다. 청구 또는 배송 세부 사항 필요 여부에 따라 두 가지 조인 경로가 가능합니다.
   * 경로:
      * 배송: `sales_order.shipping_address_id`(다) => `sales_order_address.entity_id` (1)
      * 청구: `sales_order.billing_address_id`(다) => `sales_order_address.entity_id` (1)

`store`

* 가입 대상 `store` 주문과 연결된 상거래 저장소 관련 세부 정보를 반환하는 열을 만드는 테이블입니다.
   * 경로: `sales_order.store_id` (다) => `store.store_id` (1)
