---
title: 예상 Commerce 데이터
description: Commerce 사용자가 Commerce Intelligence으로 가져오는 기본 데이터 표 살펴보기
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# [!DNL Adobe Commerce]개의 데이터가 필요합니다.

[에 [!DNL Adobe Commerce] 스토어](../../../data-analyst/importing-data/integrations/magento.md)를 연결한 후 Data Warehouse Manager를 사용하여 분석을 위해 Commerce 데이터베이스에서 관련 데이터 필드를 쉽게 추적할 수 있습니다.

이 항목에서는 Commerce 사용자가 [!DNL Commerce Intelligence]&#x200B;(으)로 가져오는 기본 데이터 표에 대해 살펴봅니다.

| **테이블 이름** | **설명** |
|-----|-----|
| `Customers` | `customer\_entity` 및 관련 표에서는 데이터베이스에 있는 각 *등록 고객*&#x200B;과 관련된 정보(이메일 주소 및 등록 날짜 등)를 설명합니다. 이 정보를 사용하여 고객 수준 속성 및 집단에 따른 세그먼트화를 시작할 수 있습니다. |
| `Orders` | `sales\_flat\_order` 테이블은 주문된 `created\_at` 타임스탬프 및 매출을 합산하는 `base\_grand\_total` 필드를 포함하여 모든 주문을 기록합니다. 이러한 필드는 주문 수준 지표의 기본입니다. *등록된 고객*&#x200B;이 주문한 경우 `customer\_id` 필드가 `customer\_entity` 테이블로 다시 연결되어 고객 구매 행동을 분석할 수 있습니다. |
| `Order items` | `sales\_flat\_order\_item` 테이블은 주문에 속하는 각 항목을 기록합니다. 여기에는 `price` 및 `qty\_ordered` 필드와 `order\_id` 테이블에 연결된 `sales\_flat\_order` 필드가 포함됩니다. 이 테이블은 `Item sold`과(와) 같은 지표의 기초이며 `product` 및 `product type`별로 세그먼트화할 수 있습니다. |
| `Products` | `catalog\_product\_entity` 표에는 범주, 크기 및 색상과 같은 제품 수준 특성에 대한 정보가 저장됩니다. |
| `Categories` | Commerce 빌드 설정 방법에 따라 제품이 하나 이상의 다른 `product categories`에 속합니다. `catalog\_category\_entity` 테이블은 이러한 범주의 계층 구조(예: Apparel > Tops > T-Shirts)를 저장하고 `catalog\_category\_product` 테이블은 제품과 해당 범주 간의 연결을 기록합니다. |

{style="table-layout:auto"}

## 관련 항목

* [&#x200B; [!DNL Adobe Commerce] 연결 중](../integrations/magento.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ko)
