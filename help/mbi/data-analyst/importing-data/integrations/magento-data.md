---
title: 예상 상거래 데이터
description: Commerce 사용자가 Commerce Intelligence로 가져오는 기본 데이터 표 살펴보기
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 예상 [!DNL Adobe Commerce] 데이터

다음 작업을 수행한 후 [을(를) 연결했습니다. [!DNL Adobe Commerce] 스토어](../../../data-analyst/importing-data/integrations/magento.md), Data Warehouse 관리자를 사용하여 분석을 위해 상거래 데이터베이스에서 관련 데이터 필드를 쉽게 추적할 수 있습니다.

이 항목에서는 Commerce 사용자가 가져오는 기본 데이터 테이블에 대해 살펴봅니다 [!DNL Commerce Intelligence].

| **테이블 이름** | **설명** |
|-----|-----|
| `Customers` | 다음 `customer\_entity` 및 관련 표에서는 각 항목과 연관된 정보를 설명합니다. *등록된 고객* 이메일 주소 및 등록 날짜와 같은 데이터베이스. 이 정보를 사용하여 고객 수준 속성 및 집단에 따른 세그먼트화를 시작할 수 있습니다. |
| `Orders` | 다음 `sales\_flat\_order` 테이블은 다음을 포함한 모든 주문을 기록합니다. `created\_at` 주문이 배치된 타임스탬프 및 `base\_grand\_total` 매출을 합산하는 필드입니다. 이러한 필드는 주문 수준 지표의 기본입니다. 주문을한 경우 *등록된 고객*, `customer\_id` 필드 링크가 다시 다음으로 연결됨  `customer\_entity` 고객 구매 행동에 대한 분석을 허용하는 표. |
| `Order items` | 다음 `sales\_flat\_order\_item` 테이블은 주문에 속하는 각 항목을 기록합니다. 여기에는 다음이 포함됩니다. `price` 및 `qty\_ordered` 필드 및 `order\_id` 에 연결하는 필드 `sales\_flat\_order` 테이블. 이 표는 다음과 같은 지표의 기초입니다. `Item sold`, 세그먼트화할 수 있는 기준 `product` 및 `product type`. |
| `Products` | 다음 `catalog\_product\_entity` 표에는 카테고리, 크기 및 색상과 같은 제품 수준 특성에 대한 정보가 저장되어 있습니다. |
| `Categories` | 제품이 하나 이상의 다른 제품에 속합니다. `product categories`, 상거래 빌드를 설정하는 방법에 따라 다릅니다. 다음 `catalog\_category\_entity` 테이블은 이러한 카테고리의 계층(예: 의류 > 탑 > 티셔츠)을 저장하고 `catalog\_category\_product` 표는 제품과 해당 범주 간의 연결을 기록합니다. |

{style="table-layout:auto"}

## 관련 항목

* [연결 중 [!DNL Adobe Commerce]](../integrations/magento.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
