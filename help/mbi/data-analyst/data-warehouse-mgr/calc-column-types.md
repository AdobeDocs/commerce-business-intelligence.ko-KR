---
title: 계산된 열 유형
description: 열을 만들어 분석을 위해 데이터를 보강하고 최적화하는 방법을 알아봅니다.
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 0%

---

# 계산된 열 유형

* [동일한 테이블 계산](#sametable)
* [일대다 계산](#onetomany)
* [다대일 계산](#manytoone)
* [핸디 참조 맵](#map)
* [고급 계산 열](#advanced)

다음 범위 내 [Data Warehouse 관리자](../data-warehouse-mgr/tour-dwm.md)열을 만들어 분석을 위해 데이터를 보강하고 최적화할 수 있습니다. [이 기능](../data-warehouse-mgr/creating-calculated-columns.md) Data Warehouse 관리자에서 테이블을 선택하고 을 클릭하여 액세스할 수 있습니다. **[!UICONTROL Create New Column]**.

이 항목에서는 Data Warehouse 관리자로 생성할 수 있는 열 유형에 대해 설명합니다. 또한 설명, 해당 열의 시각적 둘러보기 및 [참조 맵](#map) 열을 만드는 데 필요한 모든 입력 중. 다음 세 가지 방법으로 계산된 열을 만들 수 있습니다.

1. [동일한 테이블 계산 열](#sametable)
1. [일대다 계산된 열](#onetomany)
1. [다대일 계산 열](#manytoone)

## 동일한 테이블 계산 열 {#sametable}

이러한 열은 동일한 테이블의 입력 열을 사용하여 작성됩니다.

### 나이 {#age}

나이 계산 열은 현재 시간과 일부 입력 시간 사이의 초 수를 반환합니다.

아래 예제는 `Seconds since customer's most recent order` 다음에서 `customers` 테이블. 내에서 구매(때로는 이탈이라고도 함)하지 않은 고객의 사용자 목록을 구성하는 데 사용할 수 있습니다 `X days`.

![](../../assets/age.gif)

### 통화 변환기

통화 변환기 계산된 열은 열의 기본 통화를 원하는 새 통화로 변환합니다.

아래 예제는 `base\_grand\_total In AED`, 변환 `base\_grand\_total` 에서 AED로의 기본 통화입니다. `sales\_flat\_order` 테이블. 이 열은 현지 통화로 보고하려는 여러 통화가 있는 스토어에 적합합니다.

상거래 클라이언트의 경우 `base\_currency\_code` 필드는 일반적으로 기본 통화를 저장합니다. 다음 `Spot Time` 필드는 지표에 사용된 날짜와 일치해야 합니다.

![](../../assets/currency_converter.png)

## 일대다 계산된 열 {#onetomany}

`One-to-Many` 열 [두 표 사이에 경로 사용](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). 이 경로는 항상 속성이 있는 하나의 테이블과 해당 속성이 &quot;재배치&quot;되는 많은 테이블을 의미합니다. 경로는 다음과 같이 설명할 수 있습니다. `foreign key--primary key` 관계.

### 조인된 열 {#joined}

조인된 열은 한 테이블에서 속성을 재배치합니다 *끝* 여러 테이블. 일중/다의 고전적인 예는 고객(일중) 및 주문(다수)입니다.

아래 예에서는 `Customer's group\_id` 차원은 아래에 연결됩니다. `orders` 테이블.

![](../../assets/joined_column.gif)

## 다대일 계산 열 {#manytoone}

이러한 열은 일대다 열과 동일한 경로를 사용하지만 데이터를 반대 방향으로 지정합니다. 열은 패스의 한 쪽에 만들어집니다(많은 쪽이 아니라). 이러한 관계 때문에 열의 값은 집계, 즉 다변도의 데이터 포인트에서 수행되는 수학적 연산이 되어야 합니다. 이에 대한 많은 사용 사례가 있으며 몇 가지 예가 아래에 나와 있습니다.

### 카운트 {#count}

이 유형의 계산된 열은 많은 테이블에 있는 값의 개수를 반환합니다. *대상* 한 테이블이요

아래 예에서 차원은 `Customer's lifetime number of canceled orders` 이(가) 다음에 생성됨: `customers` 표(필터 포함) `orders.status`).

![](../../assets/many_to_one.gif){: width=&quot;699&quot; height=&quot;351&quot;}

### 합계 {#sum}

Sum calculated 열은 `many` 테이블 위에 놓입니다.

다음과 같은 고객 수준 차원을 만드는 데 사용할 수 있습니다. `Customer's lifetime revenue`.

### 최소 또는 최대 {#minmax}

최소 또는 최대 계산 열은 다방면에 존재하는 가장 작거나 가장 큰 레코드를 반환합니다.

다음과 같은 고객 수준 차원을 만드는 데 사용할 수 있습니다. `Customer's first order date`.

### 존재함 {#exists}

계산된 열은 다변에서 레코드의 존재를 결정하는 이진 테스트입니다. 즉, 새 열은 `1` 경로가 각 테이블의 하나 이상의 행을 연결하는 경우 `0` 연결할 수 없는 경우.

이 유형의 차원은 예를 들어 고객이 특정 제품을 구매한 적이 있는지 여부를 결정할 수 있습니다. 간 조인 사용 `customers` 테이블 및 `orders` 표, 특정 제품에 대한 필터, 차원 `Customer has purchased Product X?` 빌드할 수 있습니다.

## 핸디 참조 맵 {#map}

계산된 열을 생성할 때 모든 입력을 기억하는 데 문제가 있는 경우, 작성 시 이 참조 맵을 근처에 보관하십시오.

![](../../assets/merged_reference_map.png)

## 고급 계산 열 {#advanced}

비즈니스에 대한 질문을 분석하고 답변하는 퀘스트에서 원하는 정확한 열을 작성할 수 없는 상황이 발생할 수 있습니다.

빠른 전환을 위해 Adobe은 [고급 계산 열 유형](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) Adobe 지원 팀이 빌드할 수 있는 열 종류를 안내하는 안내서입니다. 이 항목에서는 열을 만드는 데 필요한 정보(요청에 포함)도 다룹니다.

## 관련 설명서

* [계산된 열 만들기](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [계산된 열에 대한 경로 생성/삭제](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [테이블 관계 이해 및 평가](../../data-analyst/data-warehouse-mgr/table-relationships.md)
