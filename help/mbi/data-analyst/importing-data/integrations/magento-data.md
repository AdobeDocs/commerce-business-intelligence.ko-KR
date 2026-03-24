---
title: 예상 Commerce 데이터
description: Commerce 사용자가 Commerce Intelligence으로 가져오는 기본 데이터 표 살펴보기
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/D-GNfk1-kMscgF1xBKM5xG7wRV4IkIDh9wEBCMGb630
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 239
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
