---
title: 스트라이프 데이터가 필요합니다.
description: 스트라이프에서 로 가져올 수 있는 기본 데이터 테이블을 탐색합니다 [!DNL MBI].
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 예상됨 [!DNL Stripe] 데이터

후 [연결 [!DNL Stripe] account](../integrations/stripe.md)를 사용하여 다음을 수행할 수 있습니다. [Data Warehouse 관리자](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 분석을 위한 관련 데이터 필드를 쉽게 추적할 수 있습니다.

이 문서에서는 가져올 수 있는 기본 데이터 테이블을 살펴봅니다 [!DNL Stripe] 변환 [!DNL MBI]. 설정이 완료되면 데이터 웨어하우스에서 다음 테이블이 만들어집니다. 각 테이블의 속성에 대해 자세히 알려면 테이블 이름 열의 링크를 누릅니다.

| **테이블 이름** | **설명** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/api/curl#customer_object) | 고객 객체를 사용하면 반복 비용을 수행하고 동일한 고객과 연관된 여러 비용을 추적할 수 있습니다. |
| [`Charges`](https://stripe.com/docs/api/curl#charge_object) | 이 표에는 금액, 통화, 상태, 고객 ID 등을 비롯하여 신용 카드 및 직불 카드에 대한 정보가 포함되어 있습니다. |
| [`Coupons`](https://stripe.com/docs/api/curl#coupon_object) | 이 표에는 고객에게 적용할 수 있는 퍼센트 또는 금액 할인 정보가 포함되어 있습니다. 쿠폰은 송장에만 적용됩니다. 그들은 일회성 요금에는 적용되지 않는다. |
| [`Invoices`](https://stripe.com/docs/api/curl#invoice_object) | 이 테이블에는 부채 금액, 가입, 송장 항목, 자동 기산 조정 등을 포함한 송장에 대한 정보가 들어 있습니다. |
| [`Plans`](https://stripe.com/docs/api/curl#plan_object) | 이 표에는 사이트의 다양한 제품 및 기능 수준에 대한 가격 정보가 포함되어 있습니다. 예를 들어, 기본 기능에 대해 월별 $10와 프리미엄 기능에 대한 $20/월별 플랜이 있을 수 있습니다. |
| [`Subscriptions`](https://stripe.com/docs/api/curl#subscription_object) | 이 표에는 고객이 속한 구독 계획의 세부 사항이 포함되어 있습니다. 속성은 고객 ID, 상태, 취소/종료 날짜, 세금 백분율, 평가판 정보 등을 포함합니다. |
| [`Events`](https://stripe.com/docs/api/curl#event_object) | 사건들은 한 계좌에서 방금 일어났던 흥미로운 일에 대해 당신에게 알려줍니다. [흥미로운 사건이 발생할 때](https://stripe.com/docs/api/curl#event_types)를 입력하면 새 이벤트 개체가 만들어집니다. 예를 들어 비용이 성공하면 `charge.succeeded` 이벤트가 생성됨; 또는 송장을 지급할 수 없는 경우 `invoice.payment\_failed` 이벤트가 생성됩니다. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>많은 API 요청으로 인해 여러 이벤트가 생성될 수 있습니다. 예를 들어, 고객에 대한 새 가입을 구성하면 두 가지 모두 받게 됩니다 `customer.subscription.created` 이벤트 및  `charge.succeeded` 이벤트.

## 관련:

* [연결 중 [!DNL Stripe]](../integrations/stripe.md)
* [통합 재인증](https://support.magento.com/hc/en-us/articles/360016733151)
