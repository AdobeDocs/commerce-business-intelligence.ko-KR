---
title: 예상 스트라이프 데이터
description: Stripe에서 Commerce Intelligence로 가져올 수 있는 기본 데이터 테이블을 살펴봅니다.
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# 예상 [!DNL Stripe] 데이터

다음 이후 [다음을 연결했습니다. [!DNL Stripe] account](../integrations/stripe.md), 다음을 사용할 수 있습니다. [Data Warehouse 관리자](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 분석을 위해 관련 데이터 필드를 쉽게 추적할 수 있습니다.

이 항목에서는 가져올 수 있는 기본 데이터 테이블을 살펴봅니다 [!DNL Stripe] 대상 [!DNL Commerce Intelligence]. 설치가 완료되면 Data Warehouse에 다음 테이블이 만들어집니다. 각 테이블의 속성에 대해 자세히 알아보려면 테이블 이름 열의 링크를 클릭합니다.

| **테이블 이름** | **설명** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | 고객 객체를 사용하면 반복 비용을 수행하고 동일한 고객과 연관된 여러 비용을 추적할 수 있습니다. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | 이 표에는 금액, 통화, 상태, 고객 ID 등 신용 카드 및 직불 카드에 부과되는 요금에 대한 정보가 포함되어 있습니다. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | 이 테이블에는 고객에게 적용할 퍼센트 또는 금액 할인 정보가 포함되어 있습니다. 쿠폰은 송장에만 적용되며 일회성 요금에는 적용되지 않습니다. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | 이 테이블에는 부채 금액, 가입, 송장 항목, 자동 기산 조정 등을 포함한 송장에 대한 정보가 포함되어 있습니다. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | 이 표에는 사이트의 다양한 제품 및 기능 수준에 대한 가격 정보가 포함되어 있습니다. 예를 들어 기본 기능에 대해 10달러/월 플랜과 프리미엄 기능에 대해 20달러/월 플랜이 있을 수 있습니다. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | 이 표에는 고객이 속한 구독 플랜에 대한 세부 정보가 포함되어 있습니다. 속성에는 고객 ID, 상태, 취소/종료 날짜, 세금 백분율, 체험판 정보 등이 포함됩니다. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | 이벤트는 계정에서 발생한 흥미로운 사항에 대해 알려줍니다. [관심 있는 이벤트 발생 시](https://stripe.com/docs/api/events/types)에 새 이벤트 개체가 만들어집니다. 예를 들어, 전하가 성공하면 `charge.succeeded` 이벤트가 생성되거나, 송장을 지급할 수 없는 경우 `invoice.payment\_failed` 이벤트가 생성됩니다. |

{style="table-layout:auto"}

>[!NOTE]
>
>많은 API 요청으로 인해 여러 이벤트가 생성될 수 있습니다. 예를 들어 고객에 대한 가입을 생성하는 경우 두 가지를 모두 받습니다. `customer.subscription.created` 이벤트 및 a  `charge.succeeded` 이벤트.

## 관련 항목:

* [연결 중 [!DNL Stripe]](../integrations/stripe.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
