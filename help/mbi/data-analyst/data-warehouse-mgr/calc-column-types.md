---
title: 계산된 열 유형
description: 열을 만들어 분석을 위한 데이터를 증가시키고 최적화하는 방법을 알아봅니다.
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---

# 계산된 열 유형

* [동일한 테이블 계산](#sametable)
* [일대다 계산](#onetomany)
* [계산과 계산](#manytoone)
* [편리한 참조 맵](#map)
* [고급 계산된 열](#advanced)

내 [Data Warehouse 관리자](../data-warehouse-mgr/tour-dwm.md)를 사용하면 열을 만들어 분석을 위한 데이터를 늘리고 최적화할 수 있습니다. [이 기능](../data-warehouse-mgr/creating-calculated-columns.md) Data Warehouse 관리자에서 테이블을 선택하고 **[!UICONTROL Create New Column]**.

이 문서에서는 Data Warehouse 관리자를 사용하여 만들 수 있는 열 유형과 해당 열의 보기 및 설명, [참조 맵](#map) 열을 만드는 데 필요한 모든 입력 중에서 선택합니다. 다음 세 가지 방법으로 계산된 열을 만들 수 있습니다.

* [동일한 테이블 계산된 열](#sametable)
* [일대다 계산된 열](#onetomany)
* [일대일 계산된 열](#manytoone)

## 동일한 테이블 계산된 열 {#sametable}

이러한 열은 같은 테이블의 입력 열을 사용하여 작성됩니다.

### 연령 {#age}

연령 계산된 열은 현재 시간과 일부 입력 시간 사이의 시간(초)을 반환합니다.

아래 예에서는 을 만들었습니다 `Seconds since customer's most recent order` 에서 `customers` 테이블. 이를 활용하여 내에서 구매하지 않은(종종 대량 구매라고도 함) 고객의 사용자 목록을 만들 수 있습니다 `X days`.

![](../../assets/age.gif)

### 통화 변환기

통화 변환기 계산 열은 열의 기본 통화를 원하는 새 통화로 변환합니다.

아래 예에서는 을 만들었습니다 `base\_grand\_total In AED`, 변환 `base\_grand\_total` 기본 통화에서 AED로 `sales\_flat\_order` 테이블. 이 열은 로컬 통화로 보고하려는 여러 통화가 있는 저장소에서 잘 작동합니다.

상거래 클라이언트의 경우, `base\_currency\_code` 필드는 일반적으로 기본 통화를 저장합니다. 다음 `Spot Time` 필드는 지표에 사용된 날짜와 일치해야 합니다.

![](../../assets/currency_converter.png)

## 일대다 계산된 열 {#onetomany}

`One-to-Many` 열 [두 테이블 사이의 경로 사용](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). 이 경로는 항상 속성이 있는 하나의 테이블과 해당 속성이 &quot;재배치됨&quot;으로 전달되는 많은 테이블을 의미합니다. 경로는 `foreign key--primary key` 관계.

### 조인된 열 {#joined}

연결된 열은 하나의 테이블에서 속성을 재배치합니다 *to* 많은 테이블요 1/many의 클래식 예는 고객(하나)과 주문(많이)입니다.

아래 예에서는 `Customer's group\_id` 차원이 `orders` 테이블.

![](../../assets/joined_column.gif)

## 일대일 계산된 열 {#manytoone}

이러한 열은 일대다 열이 수행하는 것과 동일한 경로를 사용하지만, 데이터를 반대 방향으로 가리킵니다. 열은 많은 면이 아니라 경로의 한 쪽에 만들어집니다. 이 관계 때문에 열의 값은 집계가 되어야 합니다. 즉, 많은 쪽의 데이터 포인트에서 수행되는 수학 연산입니다. 이에 대한 사용 사례는 많으며, 몇 가지 사용 사례가 아래에 나와 있습니다.

### 카운트 {#count}

이 유형의 계산된 열은 많은 테이블의 값 수를 반환합니다 *on* 한 테이블.

아래 예에서는 차원입니다 `Customer's lifetime number of canceled orders` 이(가) 생성되면 `customers` 테이블(필터 사용) `orders.status`).

![](../../assets/many_to_one.gif){: width=&quot;699&quot; height=&quot;351&quot;}

### 합계 {#sum}

합계 계산된 열은 `many` 테이블 위에

다음과 같은 고객 수준 차원을 만드는 데 사용할 수 있습니다 `Customer's lifetime revenue`.

### 최소 또는 최대 {#minmax}

최소 또는 최대 계산된 열은 여러 면에 있는 가장 작은 레코드 또는 가장 큰 레코드를 반환합니다.

다음과 같은 고객 수준 차원을 만드는 데 사용할 수 있습니다 `Customer's first order date`.

### 존재함 {#exists}

exists calculated 열은 여러 면에 레코드가 있는지 여부를 결정하는 이진 테스트입니다. 즉, 새 열은 `1` 각 테이블에 하나 이상의 행이 연결되면 `0` 연결할 수 없는 경우

이러한 유형의 차원은 예를 들어 고객이 특정 제품을 구매한 경우 결정됩니다. 다음 사이 조인 사용 `customers` 테이블 및 `orders` 테이블, 특정 제품에 대한 필터, 차원 `Customer has purchased Product X?` 작성할 수 있습니다.

## 편리한 참조 맵 {#map}

계산된 열을 만들 때 모든 입력을 기억하는 데 약간 문제가 있다면 다음 참조 맵을 빌드할 때 바로 보관해 보십시오.

![](../../assets/merged_reference_map.png)

## 고급 계산된 열 {#advanced}

비즈니스에 대한 질문을 분석하고 답하기 위해, 원하는 정확한 열을 작성할 수 없는 상황이 발생할 수 있습니다. 이런 경우, 우리는 당신을 커버했습니다!

신속한 전환을 위해, 확인을 권장합니다. [고급 계산 열 유형](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) 지원 팀에서 작성할 수 있는 열 종류를 알아보기 위한 안내서입니다. 이 문서에서, 열을 만드는 데 필요한 정보도 다룹니다. 요청을 포함하여 포함하십시오.

## 관련 설명서

* [계산된 열 만들기](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [계산된 열에 대한 경로 만들기/삭제](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [테이블 관계 이해 및 평가](../../data-analyst/data-warehouse-mgr/table-relationships.md)
