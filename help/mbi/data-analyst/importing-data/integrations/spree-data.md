---
title: 예상 Spre 데이터
description: Spree에서 로 가져올 수 있는 기본 데이터 표를 살펴봅니다. [!DNL Commerce Intelligence] 계정입니다.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 예상 [!DNL Spree] 데이터

다음 작업을 수행한 후 [을(를) 연결했습니다. [!DNL Spree] 스토어](../../../data-analyst/importing-data/integrations/spree.md), 다음을 사용할 수 있습니다. [Data Warehouse 관리자](../../data-warehouse-mgr/tour-dwm.md) 에서 관련 데이터 필드를 쉽게 추적하려면 [!DNL Spree] 분석을 위한 플랫폼.

이 항목에서는 가져올 수 있는 기본 데이터 테이블을 살펴봅니다 [!DNL Spree] 에 [!DNL Commerce Intelligence] 계정, 링크 포함 [추가 설명서](https://guides.spreecommerce.org/developer/addresses.html#address) 정보 [!DNL Spree] 데이터.

| **테이블 이름** | **설명** |
|-----|-----|
| `Users` | 다음 `users` 테이블에는 개인의 이메일, 이름 및 등록 날짜를 포함하여 등록된 고객의 계정 세부 정보가 포함됩니다. 이를 통해 다양한 고객 세그먼트 및 해당 구매 행동을 분석할 수 있습니다. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | 다음 `orders` 표는 모든 주문 수준 지표의 기초 역할을 합니다. 여기에 기록되어 있는 것은 고객님의 구매에 대한 모든 주문 세부 사항입니다 [!DNL Spree] store, 포함 `completed\_at` (순서의 타임스탬프), `user\_id` (주문한 등록된 사용자의 id) 등록된 사용자가 주문한 경우 `user\_id` 로 돌아가는 링크 `users` 사용자 구매 행동에 대한 분석을 허용하는 표. |
| `Line items` | 다음 `line\_items` 테이블은 다음 중 하나의 하위 항목입니다. `orders` 표 또는 `subscriptions`. 주문 또는 구독의 라인 항목 세부 사항을 기록합니다. 여러 제품이 있는 주문의 경우 각 제품에는 `product\_id` 을(를) 통해 `Products` 테이블. |
| `Products` | 다음 `products` 테이블은 Spree 카탈로그의 판매 가능 품목에 대한 모든 제품 상세내역을 기록합니다. 제품 속성별로 라인 항목 수준 지표를 세그먼트화할 수 있습니다. |
| `Subscriptions` | 다음 항목이 있는 경우: [!DNL Spree] 구독 확장, `subscriptions` 표에는 다음을 포함한 각 개별 가입의 정보가 들어 있습니다. `created\_at` (시작 날짜), `cancelled\_at` (구독이 취소된 날짜) 및 `interval` 구독. |

{style="table-layout:auto"}

## 관련 항목:

* [연결 중 [!DNL Spree]](../integrations/spree.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
