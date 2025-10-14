---
title: 예상 Spre 데이터
description: Spree에서  [!DNL Commerce Intelligence]  계정으로 가져올 수 있는 기본 데이터 테이블을 살펴봅니다.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# [!DNL Spree]개의 데이터가 필요합니다.

[에 [!DNL Spree] 스토어](../../../data-analyst/importing-data/integrations/spree.md)를 연결한 후 [Data Warehouse 관리자](../../data-warehouse-mgr/tour-dwm.md)를 사용하여 분석을 위해 [!DNL Spree] 플랫폼에서 관련 데이터 필드를 쉽게 추적할 수 있습니다.

이 항목에서는 [!DNL Spree] 데이터에 대한 [!DNL Commerce Intelligence]추가 설명서[에 대한 링크를 포함하여 &#x200B;](https://guides.spreecommerce.org/developer/addresses.html#address)에서 [!DNL Spree] 계정으로 가져올 수 있는 기본 데이터 테이블을 살펴봅니다.

| **테이블 이름** | **설명** |
|-----|-----|
| `Users` | `users` 테이블에는 개인의 이메일, 이름, 등록 날짜 등 등록된 고객의 계정 세부 정보가 포함되어 있습니다. 이를 통해 다양한 고객 세그먼트 및 해당 구매 행동을 분석할 수 있습니다. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | `orders` 테이블은 모든 주문 수준 지표의 기초 역할을 합니다. 여기에 기록된 내용은 [!DNL Spree]&#x200B;(주문 타임스탬프), `completed\_at`(주문한 등록된 사용자 ID)을 포함하여 `user\_id` 스토어에서 구매한 모든 주문 세부 정보입니다. 등록된 사용자가 주문한 경우 `user\_id`이(가) `users` 테이블로 다시 연결되어 사용자의 구매 행동을 분석할 수 있습니다. |
| `Line items` | `line\_items` 테이블은 `orders` 테이블 또는 `subscriptions`의 하위 테이블입니다. 주문 또는 구독의 라인 항목 세부 사항을 기록합니다. 여러 제품이 있는 주문의 경우 각 제품에는 `product\_id` 테이블에 연결할 수 있는 `Products`을(를) 포함하여 이 테이블에 고유한 데이터 행이 있습니다. |
| `Products` | `products` 테이블은 Spree 카탈로그의 판매 가능 항목에 대한 모든 제품 세부 정보를 기록합니다. 제품 속성별로 라인 항목 수준 지표를 세그먼트화할 수 있습니다. |
| `Subscriptions` | [!DNL Spree] 구독 확장명이 있는 경우 `subscriptions` 테이블에는 `created\_at`(시작 날짜), `cancelled\_at`(구독이 취소된 날짜) 및 `interval`을(를) 포함한 각 개별 구독의 정보가 저장됩니다. |

{style="table-layout:auto"}

## 관련 항목:

* [&#x200B; [!DNL Spree] 연결 중](../integrations/spree.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ko)
