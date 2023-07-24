---
title: 계산된 열의 경로 만들기 또는 삭제
description: 열을 만드는 테이블이 정보를 가져오는 테이블과 어떻게 관련이 있는지 설명하는 경로를 정의하는 방법을 알아봅니다.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# 계산된 열의 경로 만들기 또는 삭제

## 계산된 열 새로 고침

날짜 [계산된 열 만들기](../data-warehouse-mgr/creating-calculated-columns.md) Data Warehouse에서 열을 만드는 테이블이 정보를 가져오는 테이블과 어떻게 관련이 있는지 설명하는 경로를 정의하라는 메시지가 표시됩니다. 경로를 성공적으로 만들려면 다음 두 가지를 알아야 합니다.

1. 데이터베이스의 테이블이 서로 관련되는 방식
1. 이 관계를 정의하는 기본 및 외래 키

이 정보를 알고 있으면 이 항목의 지침에 따라 경로를 쉽게 만들 수 있습니다. 귀사의 기술 전문가에게 문의하거나 [전문 서비스 팀](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## 테이블 관계 및 주요 유형에 대한 새로 고침 {#refresher}

### 테이블 관계 {#relationships}

이 개념은 다음에서 다룹니다. [테이블 관계 이해 및 평가 문서](../../data-analyst/data-warehouse-mgr/table-relationships.md)하지만 요약하면 아무도 해치지 않잖아, 그렇지?

다음 세 가지 방법 중 하나로 표를 서로 연결할 수 있습니다.

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | 사람과 운전면허증 번호 간의 관계. 운전면허증은 1인만 가질 수 있고 운전면허증번호는 1인에게만 속한다. |
| **`one-to-many`** | 주문과 품목 간의 관계 - 주문에는 많은 품목이 포함될 수 있지만 품목은 단일 주문에 속합니다. 이 경우 주문 테이블은 한 쪽이고 항목 테이블은 여러 쪽입니다. |
| **`many-to-many`** | 제품과 카테고리 간의 관계: 제품은 많은 카테고리에 속할 수 있으며, 카테고리는 많은 제품을 포함할 수 있습니다. |

{style="table-layout:auto"}

두 테이블 간의 관계를 이해하면 이 함수를 사용하여 한 테이블에서 다른 테이블로 정보를 가져오기 위해 만들어야 하는 경로를 결정할 수 있습니다. 이 다음 단계에서는 테이블 관계를 용이하게 하는 기본 및 외래 키를 알아야 합니다.

### 기본 및 외래 키 {#keys}

A `Primary Key` 는 테이블 내에서 고유한 값을 생성하는 변경되지 않는 열 또는 열 집합입니다. 예를 들어 고객이 웹 사이트에서 주문하면 새 행이 `orders` 새 항목이 있는 장바구니의 표 `order_id`. 이 `order_id` 고객과 비즈니스 모두 해당 특정 주문의 진행 상황을 추적할 수 있습니다. 주문 ID는 고유하므로 일반적으로 다음과 같습니다. `Primary Key` / `orders` 테이블.

A `Foreign Key` 는 테이블 내에 만들어지고 `Primary Key` 다른 테이블의 열입니다. 외래 키는 분석가가 레코드를 쉽게 조회하고 함께 연결할 수 있도록 표 사이에 참조를 생성합니다. 각 고객의 주문에 대해 알고 싶다고 가정해 보겠습니다. 다음 `customer id` 열 (`Primary Key` / `customers` table) 및 `order_id` 열 (`Foreign Key` 다음에서 `customers` 표, 참조 `Primary Key` / `orders` 표 참조)를 통해 이 정보를 연결하고 분석할 수 있습니다. 경로를 만들 때 두 가지를 모두 정의하라는 메시지가 표시됩니다. `Primary Key` 및 `Foreign Key`.

## 경로 만들기 {#createpath}

Data Warehouse에서 열을 만들 때 한 테이블에서 다른 테이블로 정보를 가져오는 경로를 정의해야 합니다. 테이블 사이에 경로가 존재하기 때문에 경로가 미리 채워지는 경우가 있지만 그렇지 않으면 경로를 만들어야 합니다.

다음 사이의 관계 사용 **고객** 및 **주문 수** 어떻게 하는지 보여주기 위해서죠. 분류:

* 관계는 다음과 같습니다 `one-to-many` - 한 고객은 여러 개의 주문을 가질 수 있지만 한 주문에는 한 고객만 포함될 수 있습니다. 이는 관계의 방향 또는 계산된 열을 만들어야 하는 위치를 알려줍니다. 이 경우 의 정보를 의미합니다. `orders` 테이블을 `customers` 테이블.
* 다음 `primary key` 을(를) 사용하고자 하는 경우 `customers.customerid`또는 `customer ID` 열의 `customers` 테이블.
* 다음 `foreign key` 을(를) 사용하고자 하는 경우 `orders.customerid`또는 `customer ID` 열의 `orders` 테이블.

이제 경로를 만들 수 있습니다.

1. 클릭 **[!UICONTROL Data > Data Warehouse]**.
1. 테이블 목록에서 열을 만들 테이블을 클릭합니다. 이 예에서는 다음과 같습니다 `customers` 테이블.
1. 테이블 스키마가 표시됩니다. 클릭 **[!UICONTROL Create New Column]**.
1. 열에 이름을 지정하십시오(예: ). `Customer's orders`.
1. 열에 대한 정의를 선택합니다. 다음을 확인하십시오. [계산된 열 안내서](../data-warehouse-mgr/creating-calculated-columns.md) 편리한 치트 시트요.
1. 다음에서 [!UICONTROL Select table and column] 드롭다운에서 **[!UICONTROL Create new path]** 옵션을 선택합니다.

   ![계산된 열의 경로 만들기 모달](../../assets/Creating_Paths_modal.png)

1. 드롭다운을 사용하여 각 테이블에 대한 기본 키와 외래 키를 선택합니다.

   다음에서 `Many` 측면을 선택하고 `orders.customerid` - 고객이 많은 주문을 할 수 있다는 점을 기억하십시오.

   다음에서 `One` 측면을 선택하고 `customers.customerid` - 주문에는 고객이 한 명만 있을 수 있습니다.

1. 클릭 **[!UICONTROL Save]** 을 클릭하여 경로를 저장하고 열 만들기를 완료합니다.

### 경로 생성의 제한 사항 {#limits}

* **[!DNL Commerce Intelligence]기본/외래 키 관계를 추측할 수 없음**. 계정에 잘못된 데이터를 도입하지 않으려는 경우 경로를 수동으로 만들어야 합니다.

* **현재, 경로는 두 개의 서로 다른 테이블 사이에만 지정할 수 있습니다**. 다시 만들려는 논리에 두 개 이상의 테이블이 포함됩니까? 그런 다음 (1) 열을 먼저 중간 테이블에 연결한 다음 &quot;최종 대상&quot; 테이블에 연결하거나 (2) [전문 서비스 팀](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 목표에 대한 최상의 접근 방법을 찾을 수 있습니다.

* **열은 한 번에 하나의 경로에 대한 외래 키 참조만 될 수 있습니다.**. 예를 들어 다음과 같습니다. `order_items.order_id` 포인트 대상 `orders.id`, 그런 다음 `order_items.order_id` 다른 항목을 가리킬 수 없습니다.

* **`Many-to-many`경로는 기술적으로 생성될 수 있지만 어느 한쪽이 진실도 아니기 때문에 종종 잘못된 데이터를 생성합니다 `one-to-many` 외래 키**. 이러한 경로에 가장 적합한 접근 방법은 항상 원하는 특정 분석에 따라 다릅니다. 최상의 솔루션을 확인하려면 RJ 분석팀에 문의하십시오.

위의 제한 사항 중 하나 이상으로 인해 계산된 열을 만들 수 없는 경우 지원 센터에 현재 사용 중인 열에 대한 설명을 문의하십시오

## 계산된 열 경로 삭제 {#delete}

Data Warehouse에서 잘못된 경로를 생성했습니까? 아니면 봄맞이 대청소를 좀 하고 있어서 정리하고 싶은 거 아니야? 계정에서 경로를 삭제해야 하는 경우 [Adobe 지원 분석가에게 티켓 보내기](../../guide-overview.md#Submitting-a-Support-Ticket). **경로의 이름을 포함해야 합니다.**

## 요약 {#wrapup}

이제 Data Warehouse에서 계산된 열에 대한 경로를 쉽게 만들 수 있습니다. 특정 경로에 대해 여전히 확실하지 않은 경우 언제든지 을(를) 클릭할 수 있습니다 **[!UICONTROL Support]** (으)로 [!DNL Commerce Intelligence] 도움을 받을 계정.

## 관련 항목

* [테이블 관계 이해 및 평가](../data-warehouse-mgr/table-relationships.md)
* [계산된 열에 대한 경로 만들기](../data-warehouse-mgr/create-paths-calc-columns.md)
* [계산된 열 유형](../data-warehouse-mgr/calc-column-types.md) 을(를) 만드는 중입니다.
