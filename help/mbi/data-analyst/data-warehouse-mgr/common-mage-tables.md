---
title: 일반 상거래 테이블
description: 다음과 같은 몇 가지 일반적인 표에 대해 알아봅니다. [!DNL MBI] 고객이 활용합니다.
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# 일반 상거래 테이블

먼저 상거래 인스턴스를 [[!DNL MBI]](../importing-data/integrations/magento.md), [!DNL MBI] 일부 상거래 테이블(일반적으로 4-6개 테이블)에서 데이터를 자동으로 복제하여 초기 대시보드 및 보고서 세트를 구성합니다. 이 경우 시작점이 좋긴 하지만 대부분의 스토어 인스턴스는 수백 개 또는 수백 개의 추가 테이블을 생성하므로 비즈니스 성능에 대한 중요한 통찰력을 제공할 수 있습니다.

아래는 다음과 같은 몇 가지 일반적인 테이블 목록입니다 [!DNL MBI] 고객이 활용합니다. 다음에 [상거래 인스턴스를 MBI에 연결](../../data-analyst/importing-data/integrations/magento.md)를 사용하여 다음을 수행할 수 있습니다. [Data Warehouse 관리자](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 관련 데이터 필드를 추적하기 위해

| 테이블 이름 | 설명 |
|---|---|
| `catalog_category_entity` | 의 각 행 `catalog_category_entity` 표에서는 특정 카테고리를 설명합니다. 관련 `catalog_category_entity_varchar` 테이블 및 `catalog_category_product` 매핑 테이블에서 각 제품에 대한 범주 정보를 얻을 수 있습니다. |
| `catalog_category_product` | 의 각 행 `catalog_category_product` 테이블에는 제품과 카테고리의 조합이 나열됩니다. 따라서 특정 제품이 다른 카테고리와 함께 이 표에 여러 번 존재할 수 있으며, 특정 카테고리가 다른 제품과 연관된 이 테이블에 여러 번 존재할 수 있습니다. 이 테이블은 `catalog_category_entity` 테이블(카테고리 레벨 세부 정보를 보유함) 및 `catalog_product_entity` 테이블(제품 수준 세부 정보가 들어 있음). |
| `catalog_product_entity` | 의 각 행 `catalog_product_entity` 표는 특정 제품을 나타냅니다. 여기에는 해당 제품이 상거래 계정 및 해당 SKU에서 생성된 시기가 포함됩니다. |
| `customer_entity` | 의 각 행 [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) 표는 웹 사이트에서 등록된 사용자를 나타냅니다. 등록 날짜 및 이메일 주소와 같은 기본 고객 수준 세부 사항이 이 표에 생깁니다. |
| `quote` | 의 각 행 [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) 표는 해당 장바구니가 결국 주문으로 변환되었는지 여부, 체크아웃 프로세스에서 생성된 장바구니를 나타냅니다. 이 테이블의 잠재적 크기로 인해 60일 이상 오래된 전환되지 않은 장바구니가 있는 경우와 같이 특정 기준이 충족되는 경우 레코드를 주기적으로 삭제하는 것이 좋습니다. |
| `quote_item` | 의 각 행 [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 표는 장바구니가 결국 주문으로 변환되었는지 여부에 따라 장바구니에 추가된 항목을 나타냅니다. 이 테이블의 잠재적 크기로 인해 60일 이상 오래된 전환되지 않은 장바구니가 있는 경우와 같이 특정 기준이 충족되는 경우 레코드를 주기적으로 삭제하는 것이 좋습니다. |
| `sales_order` | 의 각 행 [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) 표는 사이트에 배치된 순서를 나타냅니다. 이 표에는 주문 일자, 주문 주문을 한 고객, 주문 총액, 할인 및 쿠폰 코드 사용과 같은 주문 수준 정보가 포함되어 있습니다. |
| `sales_order_address` | 각 행은 `sales_order_address` 테이블에는 특정 주문에 대한 배송 및 청구 정보가 포함되어 있습니다. 설정 `sales_order` 표, `billing_address_id` 그리고 `shipping_address_id` 특정 주문의 경우 특정 행( `entity_id`)을 클릭하여 제품에서 사용할 수 있습니다. `sales_order_address` 테이블. |
| `sales_order_item` | 의 각 행 [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 테이블은 특정 주문에서 특정 품목을 식별합니다. 각 행에는 제품, 구매 수량 및 해당 품목이 연관된 주문과 같은 상세내역이 포함됩니다. |

{style=&quot;table-layout:auto&quot;}

## 관련 설명서

[[!DNL Magento] 엔티티 관계 다이어그램](../data-warehouse-mgr/entity-rel-diag.md)
