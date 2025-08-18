---
title: 일반 Commerce 표
description: ' [!DNL Commerce Intelligence] 고객이 사용하는 보다 일반적인 테이블에 대해 알아봅니다.'
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# 일반 Commerce 표

[!DNL Adobe Commerce] 인스턴스를 [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md)에 처음 연결하면 [!DNL Commerce Intelligence]에서 일부 상거래 테이블(일반적으로 4~6개 테이블)의 데이터를 자동으로 복제하여 초기 대시보드 및 보고서 세트를 구성합니다. 시작점은 훌륭하지만 대부분의 스토어 인스턴스는 수백 개의 추가 테이블을 생성하지 않더라도 수십 개의 테이블을 생성하여 비즈니스의 성능에 중요한 insight을 제공할 수 있습니다.

다음은 [!DNL Commerce Intelligence] 고객이 사용하는 일반적인 테이블 중 일부 목록입니다. [Commerce 인스턴스를 Commerce Intelligence에 연결](../../data-analyst/importing-data/integrations/magento.md)한 후 [Data Warehouse 관리자](../../data-analyst/data-warehouse-mgr/tour-dwm.md)를 사용하여 관련 데이터 필드를 추적할 수 있습니다.

| 테이블 이름 | 설명 |
|---|---|
| `catalog_category_entity` | `catalog_category_entity` 테이블의 각 행은 특정 범주를 설명합니다. 연결된 `catalog_category_entity_varchar` 테이블 및 `catalog_category_product` 매핑 테이블을 사용하면 각 제품에 대한 범주 정보를 얻을 수 있습니다. |
| `catalog_category_product` | `catalog_category_product` 테이블의 각 행에는 제품과 범주의 조합이 나열됩니다. 따라서 주어진 제품은 다른 범주를 가진 이 테이블에 여러 번 존재할 수 있으며 주어진 범주는 다른 제품과 연관된 이 테이블에 여러 번 존재할 수 있습니다. 이 테이블은 범주 수준 세부 정보를 포함하는 `catalog_category_entity` 테이블과 제품 수준 세부 정보를 포함하는 `catalog_product_entity` 테이블을 인덱싱합니다. |
| `catalog_product_entity` | `catalog_product_entity` 테이블의 각 행은 특정 제품을 나타냅니다. 여기에는 해당 제품이 Commerce 계정 및 해당 SKU에서 만들어진 시기가 포함됩니다. |
| `customer_entity` | [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) 테이블의 각 행은 웹 사이트에 등록된 사용자를 나타냅니다. 등록 날짜 및 이메일 주소와 같은 기본 고객 수준 세부 정보가 이 표에 있습니다. |
| `quote` | [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) 테이블의 각 행은 체크아웃 프로세스에서 만들어진 장바구니를 나타냅니다(해당 장바구니가 결국 주문으로 변환되었는지 여부). 이 테이블의 잠재적 크기 때문에 Adobe에서는 60일 이상 된 전환되지 않은 장바구니가 있는 경우와 같이 특정 기준이 충족되는 경우 레코드를 주기적으로 삭제할 것을 권장합니다. |
| `quote_item` | [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 테이블의 각 행은 장바구니가 주문으로 변환되었는지 여부에 관계없이 장바구니에 추가된 항목을 나타냅니다. 이 테이블의 잠재적 크기 때문에 Adobe에서는 60일 이상 된 전환되지 않은 장바구니가 있는 경우와 같이 특정 기준이 충족되는 경우 레코드를 주기적으로 삭제할 것을 권장합니다. |
| `sales_order` | [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) 테이블의 각 행은 사이트에 배치된 순서를 나타냅니다. 이 표에는 주문 날짜, 주문한 고객, 주문 총액, 할인 및 쿠폰 코드 사용량 등의 주문 수준 정보가 포함되어 있습니다. |
| `sales_order_address` | `sales_order_address` 테이블의 각 행에는 특정 주문에 대한 배송 및 청구 정보가 포함되어 있습니다. `sales_order` 테이블에서 지정된 순서에 대한 `billing_address_id` 및 `shipping_address_id`이(가) `entity_id` 테이블의 특정 행(`sales_order_address`)을 참조합니다. |
| `sales_order_item` | [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 테이블의 각 행은 특정 순서에서 특정 항목을 식별합니다. 각 행에는 제품, 구매 수량, 주어진 품목과 연관된 주문 등의 세부 사항이 포함됩니다. |

{style="table-layout:auto"}

## 관련 설명서

[엔티티 관계 다이어그램](../data-warehouse-mgr/entity-rel-diag.md)
