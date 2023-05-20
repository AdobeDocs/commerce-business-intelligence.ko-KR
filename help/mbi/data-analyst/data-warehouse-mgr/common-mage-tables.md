---
title: 일반적인 상거래 Tables
description: 고객이 사용 하는  [!DNL Commerce Intelligence]  몇 가지 일반적인 표에 대해 알아봅니다.
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 일반적인 상거래 Tables

에 [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md) [!DNL Commerce Intelligence] 인스턴스를 처음 연결 [!DNL Adobe Commerce] 하면 일부 상거래 테이블 (일반적으로 4-6 표)의 데이터를 자동으로 복제 하 여 대시보드 및 보고서의 초기 세트를 구성 합니다. 이 기능은 좋은 시작 지점을 제공 하지만 대부분의 스토어 인스턴스는 비즈니스 성과에 중요 인사이트를 제공할 수 있는 수백 개 이상의 추가 테이블을 생성 하지 않습니다.

다음은 고객이 사용 하는 [!DNL Commerce Intelligence] 몇 가지 일반적인 표 목록입니다. [상거래 인스턴스를 상거래 인텔리전스 ](../../data-analyst/importing-data/integrations/magento.md) 에 연결한 후 데이터 웨어하우스 관리자 ](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 를 사용 [ 하 여 관련 데이터 필드를 추적할 수 있습니다.

| 테이블 이름 | 설명 |
|---|---|
| `catalog_category_entity` | 표의 각 행 `catalog_category_entity` 은 특정 카테고리를 설명 합니다. 연결 `catalog_category_entity_varchar` 된 테이블 및 `catalog_category_product` 매핑 테이블을 사용 하 여 각 제품에 대 한 카테고리 정보를 얻을 수 있습니다. |
| `catalog_category_product` | 표의 각 행 `catalog_category_product` 에는 제품과 카테고리의 조합이 표시 됩니다. 따라서 해당 제품은이 테이블에서 서로 다른 카테고리를 사용 하 여 여러 번 존재할 수 있으며, 특정 카테고리는 여러 제품에 연결 된 여러 번이 테이블에 존재할 수 있습니다. 이 표는 `catalog_category_entity` 테이블 (카테고리 수준 세부 사항을 포함)과 `catalog_product_entity` 테이블 (제품 수준 세부 사항을 포함)을 인덱싱합니다. |
| `catalog_product_entity` | 테이블의 `catalog_product_entity` 각 행은 특정 제품을 나타냅니다. 여기에는 해당 제품이 Commerce 계정 및 SKU에서 작성 된 시간을 포함 합니다. |
| `customer_entity` | 표의 각 행 [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) 은 웹 사이트에서 등록 된 사용자를 나타냅니다. 이 테이블에서 등록 날짜 및 이메일 주소를 좋아요 기본 고객 수준 세부 사항을 참조 하십시오. |
| `quote` | 테이블의 [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) 각 행은 장바구니 최종적으로 주문으로 변환 되었는지 여부에 관계 없이 체크아웃 프로세스에서 작성 된 장바구니를 나타냅니다. 이 테이블의 잠재적 크기 때문에 60 일 보다 오래 된 변환 되지 않은 장바구니를 충족 하는 경우 처럼 특정 기준이 충족 되는 경우 주기적으로 레코드를 삭제 하는 것이 좋습니다 Adobe Systems. |
| `quote_item` | 테이블의 [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 각 행은 장바구니 최종적으로 주문으로 변환 되었는지 여부에 관계 없이 장바구니에 추가 된 항목을 나타냅니다. 이 테이블의 잠재적 크기 때문에 60 일 보다 오래 된 변환 되지 않은 장바구니를 충족 하는 경우 처럼 특정 기준이 충족 되는 경우 주기적으로 레코드를 삭제 하는 것이 좋습니다 Adobe Systems. |
| `sales_order` | 테이블의 [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) 각 행은 사이트에 배치 된 순서를 나타냅니다. 이 테이블에는 주문 날짜, 주문 된 고객, 주문 총액, 할인율 및 쿠폰 코드 사용과 같은 주문 수준 정보가 포함 되어 있습니다. |
| `sales_order_address` | 테이블의 `sales_order_address` 각 행에는 특정 주문에 대 한 배송 및 과금 정보가 포함 되어 있습니다. `sales_order`테이블 `billing_address_id` 에서 주어진 주문의 및은 `shipping_address_id` 테이블에서 `sales_order_address` 식별 `entity_id` 된 특정 행을 가리킵니다. |
| `sales_order_item` | 테이블의 [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 각 행은 특정 순서에서 특정 항목을 식별 합니다. 각 행에는 제품, 구매한 수량, 주어진 항목이 연결 된 순서 등의 세부 사항이 포함 됩니다. |

{style="table-layout:auto"}

## 관련 설명서

[엔티티 관계 다이어그램](../data-warehouse-mgr/entity-rel-diag.md)
