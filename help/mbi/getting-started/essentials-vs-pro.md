---
title: MBI Essentials와 Pro 비교
description: MBI Essentials와 MBI Pro이 어떻게 다른지 알아봅니다.
exl-id: 624a6285-8497-43d9-a56d-8ae503e0e2dd
source-git-commit: dcd02693b3ca060ecdc47cbee189428ce157dd58
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 4%

---

# [!DNL MBI Essentials] vs [!DNL MBI Pro]

>[!NOTE]
>
>이 설명서에 대한 보관 문서입니다 [!DNL MBI].

다음 표에서는 Essentials 및 Pro에 포함된 내용을 설명합니다.

|  | **`MBI Essentials`** | **`MBI Pro`** |
|-----|-----|-----|
| `Pre-Defined Reports` | 최대 100개 | 사용자 지정 |
| `Pre-Defined Dashboards` | 5-6 | 사용자 지정 |
| `New Custom Report Creation` | 예 | 예 |
| `Commerce Tables` | 4-6 | 제한 없음 |
| `Log-ins/User Accounts` | 10 | 20 |
| `User Permissions` | 예 | 예 |
| `Data Warehouse Manager` | 사용할 수 없음 | 사용 가능 |
| `Email Reports` | 예 | 예 |
| `Cohort Report Builder` | 예 | 예 |
| `Google Analytics Live Integration` | 예 | 제한 없음 |
| `3rd Party Integrations` | 사용할 수 없음 | 사용 가능 |
| `Full API Access` | 아니요 | 예 |
| `Access to CS, AM, or Analysts` | 아니요 | 예 |
| `Professional Services` | 사용 가능 | 사용 가능 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>테이블 수는 게스트 체크아웃에 따라 다릅니다.

**포함된 테이블**

* `sales\_order`
* `sales\_order\_item`
* `sales\_order\_address`
* `customer\_entity`
* `customer\_group`
* `store`

## 필수 항목에 포함된 열

의 항목 _기울임체_ 계산 필드입니다.

* `sales_order` 표
   * `entity_id`
   * `base_grand_total`
   * `customer_id`
   * `status`
   * `customer_email`
   * `store_id`
   * `base_currency_code`
   * `billing_address_id`
   * `shipping_address_id`
   * `base_shipping_amount`
   * `base_tax_amount`
   * `coupon_code`
   * `created_at`
   * `updated_at`
   * `base_subtotal`
   * `customer_group_id`
   * `base_discount_amount`
   * `base_discount_invoiced`
   * `increment_id`
   * `Customer's order number`
   * `Customer's first order date`
   * `Customer's lifetime number of orders`
   * `Is customer's last order?`
   * `Billing address region`
   * `Shipping address country`
   * `Customer's lifetime revenue`
   * `Seconds between customer's first order date and this order`
   * `Seconds since previous order`
   * `Store name`
   * `Customer's lifetime number of coupons`
   * `Customer's order number (previous-current)`
   * `Shipping address region`
   * `Number of items in order`
   * `Billing address city`
   * `Shipping address city`
   * `Customer's group code`
   * `Customer's first order's billing region`
   * `Customer's first order's coupon_code`
   * `Customer's creation date`
   * `Billing address country`

* `sales_order_item` 표
   * `item_id`
   * `qty_ordered`
   * `base_price`
   * `name`
   * `order_id`
   * `sku`
   * `product_type`
   * `product_id`
   * `created_at`
   * `updated_at`
   * `parent_item_id`
   * `store_id`
   * `base_discount_amount`
   * `base_discount_invoiced`
   * `Order's coupon_code`
   * `Order item total value (quantity * price)`
   * `Order's increment_id`
   * `Customer's email`
   * `Customer's lifetime number of orders`
   * `Store name`
   * `Customer's order number`
   * `Order's status`
   * `Customer's lifetime revenue`

* `sales_order_address` 표
   * `entity_id`
   * `city`
   * `region`
   * `country_id`

* `customer_entity` 표
   * `entity_id`
   * `email`
   * `group_id`
   * `created_at`
   * `updated_at`
   * `store_id`
   * `Customer's lifetime revenue`
   * `Customer's lifetime number of coupons`
   * `Customer's first order date`
   * `Customer's lifetime number of orders`
   * `Seconds since customer's first order date`
   * `Customer's first 30 day revenue`
   * `Customer's first order's billing region`
   * `Customer's first order's coupon_code`
   * `Customer's group code`
   * `Store name`

* `customer_group` 표
   * `customer_group_id`
   * `customer_group_code`

* `store` 표
   * `store_id`
   * `name`

