---
title: 예상 상거래 데이터
description: Commerce 사용자가 MBI에 가져오는 기본 데이터 표를 알아봅니다
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# 예상 상거래 데이터

그러고 나면 [상거래 스토어에 연결됨](../../../data-analyst/importing-data/integrations/magento.md)Data Warehouse 관리자를 사용하여 분석을 위해 상거래 데이터베이스에서 관련 데이터 필드를 쉽게 추적할 수 있습니다.

이 문서에서는 Commerce 사용자가 가져오는 기본 데이터 테이블을 살펴봅니다 [!DNL MBI].

| **테이블 이름** | **설명** |
|-----|-----|
| `Customers` | 다음 `customer\_entity` 및 관련 표에서는 각 *등록 고객* 데이터베이스에 이메일 주소 및 등록 날짜와 같이 표시됩니다. 이 정보를 사용하여 고객 수준 속성 및 집단에 의해 세그먼트화할 수 있습니다. |
| `Orders` | 다음 `sales\_flat\_order` 테이블 레코드 는 `created\_at` 순서와 `base\_grand\_total` 수입을 합산하는 필드입니다. 이러한 필드는 주문 수준 지표의 기반이 됩니다. 주문이 *등록 고객*, `customer\_id` 필드가  `customer\_entity` 고객 구매 행동에 대한 분석을 허용하는 표. |
| `Order items` | 다음 `sales\_flat\_order\_item` 테이블은 주문에 속하는 각 품목을 기록합니다. 여기에는 다음이 포함됩니다 `price` 및 `qty\_ordered` 필드 및 `order\_id` 에 연결되는 필드 `sales\_flat\_order` 테이블. 이 표는 다음과 같은 지표의 기반입니다 `Item sold`, 및에 의해 세그먼트화할 수 있습니다. `product` 및 `product type`. |
| `Products` | 다음 `catalog\_product\_entity` 표는 카테고리, 크기 및 색상과 같은 제품 수준 속성에 대한 정보를 저장합니다. |
| `Categories` | 제품이 하나 또는 여러 항목에 속합니다 `product categories`, 상거래 빌드가 설정되는 방식에 따라 다릅니다. 다음 `catalog\_category\_entity` 표는 이러한 카테고리의 계층(예: Apprel > Top > T-Shirts)을 저장하고 `catalog\_category\_product` 표는 제품과 해당 카테고리 간의 연결을 기록합니다. |

{style=&quot;table-layout:auto&quot;}

## 관련

* [연결 중 [!DNL Adobe Commerce]](../integrations/magento.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
