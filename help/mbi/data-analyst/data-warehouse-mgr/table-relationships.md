---
title: 테이블 관계 이해 및 평가
description: 한 테이블에서 다른 테이블의 엔티티에 속할 수 있는 발생 횟수를 이해하는 방법에 대해 알아봅니다.
exl-id: e7256f46-879a-41da-9919-b700f2691013
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---

# 테이블 관계 이해 및 평가

주어진 두 테이블 간의 관계를 평가할 때 한 테이블에서 다른 테이블의 엔티티에 속할 수 있는 발생 횟수 또는 그 반대의 발생 횟수를 이해해야 합니다. 예를 들어 `users` 테이블과 `orders` 테이블을 사용합니다. 이 경우 주어진 **사용자**&#x200B;가 수행한 **주문**&#x200B;의 수와 **주문**&#x200B;에 속하는 가능한 **사용자**&#x200B;의 수를 알고 싶습니다.

[계산된 열](../data-warehouse-mgr/creating-calculated-columns.md) 및 [차원](../data-warehouse-mgr/manage-data-dimensions-metrics.md)의 정확도에 영향을 주므로 데이터 무결성을 유지하려면 관계를 이해하는 것이 중요합니다. 자세한 내용은 [관계 유형](#types) 및 [Data Warehouse의 테이블을 평가하는 방법](#eval)을 참조하세요.

## 관계 유형 {#types}

두 테이블 사이에 있을 수 있는 관계에는 세 가지 유형이 있습니다.

1. [&#39;일대일&#39;](#onetoone)
1. [일대다](#onetomany)
1. [다대다](#manytomany)

### `One-to-One` {#onetoone}

`one-to-one` 관계에서 테이블 `B`의 레코드는 테이블 `A`의 한 레코드에만 속합니다. `A` 테이블의 레코드는 `B` 테이블의 한 레코드에만 속합니다.

예를 들어, 사람과 운전면허번호 간의 관계에서 사람은 운전면허번호를 하나만 가질 수 있고 운전면허번호는 사람에게만 속한다.

![](../../assets/one-to-one.png)

### `One-to-Many` {#onetomany}

`one-to-many` 관계에서 테이블 `A`의 레코드가 테이블 `B`의 여러 레코드에 속할 수 있습니다. `orders`과(와) `items` 사이의 관계를 생각해 보십시오. 주문에는 여러 항목이 포함될 수 있지만 한 항목은 단일 주문에 속합니다. 이 경우 `orders` 테이블은 한 쪽이고 `items` 테이블은 여러 쪽입니다.

![](../../assets/one-to-many_001.png)

### `Many-to-Many` {#manytomany}

`many-to-many` 관계에서 테이블 `B`의 레코드가 테이블 `A`의 여러 레코드에 속할 수 있습니다. 또는 그 반대로 테이블 `A`의 레코드는 테이블 `B`의 여러 레코드에 속할 수 있습니다.

**제품**&#x200B;과(와) **카테고리** 간의 관계에 대해 생각해 보십시오. 제품은 여러 카테고리에 속할 수 있으며 카테고리는 많은 제품을 포함할 수 있습니다.

![](../../assets/many-to-many.png)

## 테이블 평가 {#eval}

표 사이에 존재하는 관계 유형이 주어지면 Data Warehouse에서 표를 평가하는 방법을 배울 수 있습니다. 이러한 관계는 다중 테이블 계산 열이 정의되는 방식을 형성하므로 테이블 관계를 식별하는 방법과 해당 테이블이 속하는 측면(`one` 또는 `many`)을 이해하는 것이 중요합니다.

Data Warehouse 내에 있는 주어진 테이블 쌍의 관계를 평가하는 데 사용할 수 있는 방법에는 두 가지가 있습니다. 첫 번째 방법에서는 테이블의 엔터티가 서로 상호 작용하는 방식을 고려하는 [개념 프레임워크](#concept)를 사용합니다. 두 번째 메서드는 [테이블의 스키마](#schema)를 사용합니다.

### 개념 프레임워크 사용 {#concept}

이 방법에서는 개념 프레임워크를 사용하여 두 테이블의 엔티티가 상호 작용하는 방법을 설명합니다. 이 틀은 관계를 고려할 때 무엇이 가능한지 평가한다는 것을 이해하는 것이 중요하다.

예를 들어, 사용자와 주문에 대해 생각할 때 관계에서 가능한 모든 것을 고려합니다. 등록된 사용자는 라이프타임 내에 주문을 하지 않거나 한 개의 주문만 또는 여러 개의 주문을 할 수 있습니다. 비즈니스를 시작하고 주문이 없는 경우 주어진 사용자가 생애에 많은 주문을 할 수 있습니다. 이를 위해 테이블이 만들어져 있다.

이 메서드를 사용하려면 다음을 수행하십시오.

1. 각 테이블에 설명되어 있는 엔티티를 식별합니다. **힌트: 일반적으로 명사**&#x200B;입니다. 예를 들어 `user` 및 `orders` 테이블은 사용자 및 주문을 명시적으로 설명하고 있습니다.

1. 이러한 엔티티가 상호 작용하는 방법을 설명하는 하나 이상의 동사를 식별합니다. 예를 들어 사용자를 주문과 비교할 때 사용자는 &quot;주문&quot;을 합니다. 다른 방향으로 이동하면, 주문이 사용자에게 &quot;속함&quot;입니다.

이 유형의 프레임워크는 Data Warehouse에 있는 모든 테이블 쌍에 적용할 수 있습니다. 이를 통해 관계의 유형과 어느 테이블이 한 면이고 어느 테이블이 여러 면인지 쉽게 식별할 수 있습니다.

두 테이블의 상호 작용 방식을 설명하는 용어를 식별한 후에는 첫 번째 엔티티의 특정 인스턴스가 두 번째 엔티티와 어떤 관계를 갖는지 고려하여 상호 작용을 양방향으로 프레임화합니다. 다음은 각 관계의 몇 가지 예입니다.

### `One-to-One`

주어진 한 사람이 단 하나의 운전면허증 번호만을 가질 수 있다. 주어진 운전면허증 번호 하나는 오직 한 사람의 것이다.

각 테이블이 한쪽인 `one-to-one` 관계입니다.

![](../../assets/one-to-one3.png)

### `One-to-Many`

주어진 한 주문에는 여러 항목이 포함될 수 있습니다. 주어진 항목 하나는 오더 하나에 속합니다.

Orders 테이블은 한쪽이고 Items 테이블은 여러 쪽인 `one-to-many` 관계입니다.

![](../../assets/one-to-many3.png)

### `Many-to-Many`

주어진 한 가지 제품이 아마도 많은 범주에 속할 수 있다. 하나의 주어진 카테고리에 많은 제품이 포함될 수 있습니다.

각 테이블이 여러 쪽인 `many-to-many` 관계입니다.

![](../../assets/many-to-many3.png)

### 테이블의 스키마 사용 {#schema}

두 번째 메서드는 테이블 스키마를 사용합니다. 스키마는 [`Primary`](https://en.wikipedia.org/wiki/Unique_key) 및 [`Foreign`](https://en.wikipedia.org/wiki/Foreign_key) 키인 열을 정의합니다. 이러한 키를 사용하여 테이블을 서로 연결하고 관계 유형을 결정할 수 있습니다.

두 테이블을 함께 연결하는 열을 식별하면 열 유형을 사용하여 테이블 관계를 평가합니다. 다음은 몇 가지 예입니다.

### `One-to-one`

두 테이블의 `primary key`을(를) 사용하여 테이블을 연결하는 경우 각 테이블에서 동일한 고유 엔터티가 설명되고 관계는 `one-to-one`입니다.

예를 들어, `users` 테이블은 대부분의 사용자 특성(예: 이름)을 캡처할 수 있지만, 보조 `user_source` 테이블은 사용자 등록 소스를 캡처할 수 있습니다. 각 테이블에서 행은 한 명의 사용자를 나타냅니다.

![](../../assets/one-to-one1.png)

### `One-to-many`

>[!NOTE]
>
>손님 주문도 받으시나요? 게스트 주문이 테이블 관계에 미치는 영향에 대해 알아보려면 [게스트 주문](../data-warehouse-mgr/guest-orders.md)을 참조하세요.

`primary key`을(를) 가리키는 `Foreign key`을(를) 사용하여 테이블을 연결할 때 이 설정에서는 `one-to-many` 관계를 설명합니다. 한쪽은 `primary key`을(를) 포함하는 테이블이고 다른 쪽은 `foreign key`을(를) 포함하는 테이블입니다.

![](../../assets/one-to-many1.png)

### `Many-to-many`

다음 중 하나가 true이면 관계는 `many-to-many`입니다.

* `Non-primary key`개의 열을 사용하여 두 테이블을 연결하고 있습니다.
  ![](../../assets/many-to-many1.png)
* 복합 `primary key`의 일부를 사용하여 두 테이블을 연결합니다.

![](../../assets/many-to-mnay2.png)

## 다음 단계

테이블 관계를 올바르게 평가하는 것은 데이터를 정확하게 모델링하는 데 중요합니다. 표 간의 관계를 이해했으므로 [Data Warehouse 관리자로 수행할 수 있는 작업](../data-warehouse-mgr/tour-dwm.md)을 참조하세요.
