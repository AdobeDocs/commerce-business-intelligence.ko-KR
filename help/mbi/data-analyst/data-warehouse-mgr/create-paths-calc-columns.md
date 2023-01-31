---
title: 계산된 열에 대한 경로 만들기 또는 삭제
description: 열을 만드는 테이블이 정보를 가져오는 테이블과 어떻게 관련되는지를 설명하는 경로를 정의하는 방법을 알아봅니다.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# 계산된 열에 대한 경로 만들기 또는 삭제

## 계산된 열 리프레셔

When [계산된 열 만들기](../data-warehouse-mgr/creating-calculated-columns.md) Data Warehouse에서 열을 만드는 테이블이 정보를 가져오는 테이블과 어떻게 관련되는지를 설명하는 경로를 정의하라는 메시지가 표시됩니다. 경로를 성공적으로 만들려면 다음 두 가지 사항을 알고 있어야 합니다.

1. 데이터베이스의 테이블이 서로 어떻게 관련되는지
1. 이 관계를 정의하는 기본 및 외래 키

이 정보를 알고 있으면 이 문서의 지침에 따라 경로를 쉽게 만들 수 있습니다. 확실하지 않은 경우 이러한 개념에 대한 개요를 제공했지만, 조직의 기술 전문가에게 문의하거나 지원 팀에 문의할 수 있습니다.

## 테이블 관계 및 키 유형의 새로 고침 {#refresher}

### 테이블 관계 {#relationships}

우리는 이 개념을 우리 회사의 [테이블 관계 이해 및 평가 문서](../../data-analyst/data-warehouse-mgr/table-relationships.md)하지만 간단한 요약이 사람을 다치게 하지 않죠?

표는 다음 세 가지 방법 중 하나로 서로 관련될 수 있습니다.

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | 사람과 운전면허증 번호 사이의 관계. 한 사람만이 하나의 운전면허번호를 가질 수 있고, 운전면허번호는 한 사람에게만 속합니다. |
| **`one-to-many`** | 주문과 품목 간의 관계 - 주문에 많은 품목이 포함될 수 있지만, 품목은 단일 주문에 속합니다. 이 경우 주문 테이블은 한 측면이고 품목 테이블은 여러 측면입니다. |
| **`many-to-many`** | 제품과 카테고리 간의 관계: 제품은 여러 카테고리에 속할 수 있으며 카테고리에는 여러 제품이 포함될 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

두 테이블 간의 관계를 이해하면 한 테이블에서 다른 테이블로 정보를 가져오기 위해 만들 경로를 결정하는 데 사용할 수 있습니다. 이 다음 단계에서는 테이블 관계를 용이하게 하는 기본 키와 외래 키를 파악해야 합니다.

### 기본 및 외래 키 {#keys}

A `Primary Key` 는 테이블 내에서 고유한 값을 생성하는 변경되지 않는 열 또는 열 세트입니다. 예를 들어 고객이 웹 사이트에서 주문을 하면 새 행이 `orders` 장바구니에 있는 표(새 항목 포함) `order_id`. 이 `order_id` 고객과 비즈니스 모두 특정 주문의 진행 상황을 추적할 수 있습니다. 주문 id는 고유하므로 일반적으로 다음과 같습니다 `Primary Key` / `orders` 테이블.

A `Foreign Key` 는 `Primary Key` 다른 테이블의 열 외래 키는 테이블 간에 참조를 만들어 분석가가 레코드를 쉽게 조회하고 연결할 수 있도록 합니다. 각 고객의 주문을 알고 싶다고 가정합니다. 다음 `customer id` 열 (`Primary Key` 의 `customers` 표)와 `order_id` 열 (`Foreign Key` 에서 `customers` 표, 참조 `Primary Key` 의 `orders` 표)를 사용하면 이 정보를 연결하고 분석할 수 있습니다. 경로를 만들 때 두 경로를 모두 정의하라는 메시지가 표시됩니다 `Primary Key` 및 `Foreign Key`.

## 경로 만들기 {#createpath}

데이터 웨어하우스에서 열을 만들 때 한 테이블의 정보를 다른 테이블로 가져오는 경로를 정의해야 합니다. 테이블 사이에 경로가 이미 있으므로 경로가 미리 채워지는 경우가 있지만 그렇지 않은 경우 경로를 만들어야 합니다.

Adobe는 **고객** 및 **주문** 어떻게 진행되었는지 보여드리겠습니다. 분류:

* 관계는 `one-to-many` - 고객은 많은 주문을 받을 수 있지만 주문에는 하나의 고객만 있을 수 있습니다. 이는 관계의 방향 또는 계산된 열을 만들 위치를 알려줍니다. 이 경우 는 `orders` 테이블을 `customers` 테이블.
* 다음 `primary key` 우리는 `customers.customerid`또는 `customer ID` 열 `customers` 테이블.
* 다음 `foreign key` 우리는 `orders.customerid`또는 `customer ID` 열 `orders` 테이블.

이제, 우리는 실제로 그 길을 만드는 과정을 안내합니다.

1. 클릭 **[!UICONTROL Data > Data Warehouse]**.
1. 테이블 목록에서 열을 만들 테이블을 클릭합니다. 이 예제에서는 `customers` 테이블.
1. 테이블 스키마가 표시됩니다. 클릭 **[!UICONTROL Create New Column]**.
1. 열에 이름을 지정합니다(예: ). `Customer's orders`.
1. 열에 대한 정의를 선택합니다. 다음을 확인하십시오 [계산된 열 안내서](../data-warehouse-mgr/creating-calculated-columns.md) 유용한 치트 시트를 위해.
1. 에서 [!UICONTROL Select table and column] 드롭다운에서 **[!UICONTROL Create new path]** 선택 사항입니다.

   ![계산된 열 모달에 대한 경로 만들기](../../assets/Creating_Paths_modal.png)

1. 드롭다운을 사용하여 각 테이블의 기본 키와 외래 키를 선택합니다.

   설정 `Many` 우리는 선택한다 `orders.customerid` - 기억하십시오. 고객은 많은 주문을 받을 수 있습니다.

   설정 `One` 우리는 선택한다 `customers.customerid` - 주문에는 고객이 하나만 있을 수 있습니다.

1. 클릭 **[!UICONTROL Save]** 경로를 저장하고 열 만들기를 완료합니다.

### 경로 작성 제한 사항 {#limits}

* **[!DNL MBI]1차/2차 키 관계를 추정할 수 없음**. 계정에 잘못된 데이터를 도입하지 않으려는 경우 경로를 수동으로 만들어야 합니다.
* **현재 경로는 두 개의 서로 다른 테이블 사이에만 지정할 수 있습니다**. 다시 만들려는 논리에 두 개 이상의 테이블이 포함됩니까? 그런 다음 (1) 먼저 열을 중간 테이블에 연결한 다음 &quot;최종 대상&quot; 표에 연결하거나 (2) 목표에 대한 가장 좋은 접근 방식을 찾기 위해 팀에 문의하는 것이 적절할 수 있습니다.
* **한 번에 하나의 PATH에 대한 외래 키 참조만 열 수 있습니다**. 예를 들어 `order_items.order_id` 점 `orders.id`, 그런 다음 `order_items.order_id` 다른 항목을 가리키도록 지정할 수 없습니다.
* **`Many-to-many`경로는 기술적으로 작성할 수 있지만, 어느 쪽도 참이기 때문에 종종 잘못된 데이터를 생성합니다 `one-to-many` 외래 키**. 이러한 경로에 액세스하는 가장 좋은 방법은 항상 원하는 특정 분석에 따라 다릅니다. 최상의 솔루션을 검색하려면 RJ 분석가 팀에 문의하십시오.

위의 제한 사항 중 하나 이상으로 인해 계산된 열을 만들 수 없는 경우 지원 센터에 현재 사용 중인 열에 대한 설명을 문의하십시오

## 계산된 열 경로 삭제 {#delete}

Data Warehouse에서 잘못된 경로를 생성했습니까? 아니면 봄맞이 청소를 하고 청소하고 싶으세요? 계정에서 경로를 삭제해야 할 경우 다음을 수행할 수 있습니다 [우리의 지원 분석가에게 표를 보내다](../../guide-overview.md). **경로 이름을 반드시 포함하십시오!**

## 포장 {#wrapup}

이제 Data Warehouse에서 계산된 열에 대한 경로를 만드는 것이 편해야 합니다. 특정 경로에 대해 아직 확실하지 않은 경우 **[!UICONTROL Support]** 다음 위치에서 [!DNL MBI] 지원을 받을 계정입니다.

## 관련

* [테이블 관계 이해 및 평가](../data-warehouse-mgr/table-relationships.md)
* [계산된 열에 대한 경로 만들기](../data-warehouse-mgr/create-paths-calc-columns.md)
* [계산된 열 유형](../data-warehouse-mgr/calc-column-types.md) 만들기 시도 중입니다.
