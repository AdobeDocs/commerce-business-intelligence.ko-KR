---
title: 예상 대차 데이터
description: Spree에서 사용자의 [!DNL MBI] 계정이 필요합니다.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 예상됨 [!DNL Spree] 데이터

그러고 나면 [연결 [!DNL Spree] 스토어](../../../data-analyst/importing-data/integrations/spree.md)를 사용하여 다음을 수행할 수 있습니다. [Data Warehouse 관리자](../../data-warehouse-mgr/tour-dwm.md) 에서 관련 데이터 필드를 쉽게 추적할 수 있습니다. [!DNL Spree] 분석 플랫폼.

이 문서에서는 가져올 수 있는 기본 데이터 테이블을 살펴봅니다 [!DNL Spree] 내 [!DNL MBI] 계정, 링크 포함 [추가 설명서](https://guides.spreecommerce.org/developer/addresses.html#address) 정보 [!DNL Spree] 데이터.

| **테이블 이름** | **설명** |
|-----|-----|
| `Users` | 다음 `users` 표에는 개인의 이메일, 이름 및 등록 날짜를 포함하여 등록된 고객에 대한 계정 세부 사항이 포함되어 있습니다. 이를 통해 다양한 고객 세그먼트와 구매 행동을 분석할 수 있습니다. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | 다음 `orders` 표는 모든 주문 수준 지표의 기초 역할을 합니다. 여기에 기록된 내용은 고객의 모든 구매 내역 [!DNL Spree] 저장, 포함 `completed\_at` (주문 타임스탬프), `user\_id` (주문을 한 등록된 사용자의 id). 등록된 사용자가 순서를 지정한 경우 `user\_id` 에 다시 연결됩니다. `users` 사용자 구매 행동에 대한 분석을 허용하는 표. |
| `Line items` | 다음 `line\_items` 표는 다음 중 하나의 하위입니다 `orders` 테이블 또는 `subscriptions`. 주문 또는 구독의 라인 항목 세부 사항을 기록합니다. 여러 제품이 있는 주문의 경우, 각 제품은 다음을 포함하여 이 표에 고유한 데이터 행이 있습니다. `product\_id` 이렇게 하면 `Products` 테이블. |
| `Products` | 다음 `products` 테이블은 Spree 카탈로그의 판매 가능 품목에 대한 모든 제품 상세내역을 기록합니다. 이렇게 하면 제품 속성별로 라인 항목 수준 지표를 세그먼트화할 수 있습니다. |
| `Subscriptions` | 만약 [!DNL Spree] 구독 확장, `subscriptions` 테이블에는 각 개별 구독 정보가 포함됩니다. `created\_at` (시작 날짜), `cancelled\_at` (구독이 취소된 날짜) 및 `interval` 구독 취소. |

{style=&quot;table-layout:auto&quot;}

## 관련:

* [연결 중 [!DNL Spree]](../integrations/spree.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
