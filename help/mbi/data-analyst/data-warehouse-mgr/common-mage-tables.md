---
title: 일반 상거래 테이블
description: 다음과 같은 몇 가지 일반적인 표에 대해 알아봅니다. [!DNL Commerce Intelligence] 고객은 를 사용합니다.
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 일반 상거래 테이블

을(를) 처음 연결할 때 [!DNL Adobe Commerce] 인스턴스 대상 [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md), [!DNL Commerce Intelligence] 는 일부 상거래 테이블(일반적으로 4~6개 테이블)의 데이터를 자동으로 복제하여 초기 대시보드 및 보고서 세트를 구성합니다. 시작점은 훌륭하지만 대부분의 스토어 인스턴스는 수백 개의 추가 테이블을 생성하지 않더라도 수십 개의 테이블을 생성하여 비즈니스 성능에 대한 중요한 통찰력을 제공할 수 있습니다.

다음은 다음과 같은 몇 가지 일반적인 표의 목록입니다. [!DNL Commerce Intelligence] 고객은 를 사용합니다. 이후 [상거래 인스턴스를 Commerce Intelligence에 연결](../../data-analyst/importing-data/integrations/magento.md), 다음을 사용할 수 있습니다. [Data Warehouse 관리자](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 관련 데이터 필드를 추적할 수 있습니다.

| 테이블 이름 | 설명 |
|---|---|
| `catalog_category_entity` | 의 각 행 `catalog_category_entity` 이 표에서는 특정 범주를 설명합니다. 관련 항목 포함 `catalog_category_entity_varchar` 테이블 및 `catalog_category_product` 매핑 테이블을 사용하면 각 제품에 대한 범주 정보를 얻을 수 있습니다. |
| `catalog_category_product` | 의 각 행 `catalog_category_product` 표에는 제품과 범주의 조합이 나와 있습니다. 따라서 주어진 제품은 다른 범주를 가진 이 테이블에 여러 번 존재할 수 있으며 주어진 범주는 다른 제품과 연관된 이 테이블에 여러 번 존재할 수 있습니다. 이 표에서는 를 색인화합니다. `catalog_category_entity` 테이블(카테고리 수준 세부 정보를 보유함) 및 `catalog_product_entity` 테이블(제품 수준 세부 정보가 들어 있음) |
| `catalog_product_entity` | 의 각 행 `catalog_product_entity` 표는 특정 제품을 나타냅니다. 여기에는 해당 제품이 상거래 계정 및 해당 SKU에서 만들어진 시기가 포함됩니다. |
| `customer_entity` | 의 각 행 [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) 표는 웹 사이트에 등록된 사용자를 나타냅니다. 등록 날짜 및 이메일 주소와 같은 기본 고객 수준 세부 정보가 이 표에 있습니다. |
| `quote` | 의 각 행 [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) 테이블은 체크아웃 프로세스에서 생성된 장바구니를 나타냅니다(해당 장바구니가 결국 주문으로 변환되었는지 여부). Adobe 이 테이블의 잠재적 크기 때문에 60일 이상 된 전환되지 않은 장바구니가 있는 경우와 같이 특정 기준이 충족되는 경우 레코드를 정기적으로 삭제하는 것이 좋습니다. |
| `quote_item` | 의 각 행 [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 테이블은 장바구니에 추가된 항목을 나타내며, 장바구니가 결국 주문으로 변환되었는지 여부를 나타냅니다. Adobe 이 테이블의 잠재적 크기 때문에 60일 이상 된 전환되지 않은 장바구니가 있는 경우와 같이 특정 기준이 충족되는 경우 레코드를 정기적으로 삭제하는 것이 좋습니다. |
| `sales_order` | 의 각 행 [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) 표는 사이트에 배치된 주문을 나타냅니다. 이 표에는 주문 날짜, 주문한 고객, 주문 총액, 할인 및 쿠폰 코드 사용량 등의 주문 수준 정보가 포함되어 있습니다. |
| `sales_order_address` | 의 각 행 `sales_order_address` 테이블에는 특정 주문에 대한 배송 및 청구 정보가 포함되어 있습니다. 다음에서 `sales_order` 테이블, `billing_address_id` 및 `shipping_address_id` 주어진 주문에 대해 특정 행( 식별자로 식별됨)을 참조하십시오. `entity_id`)에 있는 `sales_order_address` 테이블. |
| `sales_order_item` | 의 각 행 [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 테이블은 특정 주문에서 특정 품목을 식별합니다. 각 행에는 제품, 구매 수량, 주어진 품목과 연관된 주문 등의 세부 사항이 포함됩니다. |

{style="table-layout:auto"}

## 관련 설명서

[엔티티 관계 다이어그램](../data-warehouse-mgr/entity-rel-diag.md)
