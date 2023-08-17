---
title: 복제 방법 구성
description: 표를 구성하는 방법과 표 데이터가 작동하는 방식을 통해 표에 가장 적합한 복제 방법을 선택할 수 있습니다.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 0%

---

# 복제 방법 구성

`Replication` 방법 및 [재확인](../data-warehouse-mgr/cfg-data-rechecks.md) 데이터베이스 테이블에서 새 데이터 또는 업데이트된 데이터를 식별하는 데 사용됩니다. 이러한 매개 변수를 올바르게 설정하는 것은 데이터의 정확성과 최적화된 업데이트 시간을 모두 보장하는 데 중요합니다. 이 항목에서는 복제 방법을 중점적으로 다룹니다.

에서 새 테이블이 동기화되는 경우 [Data Warehouse 관리자](../data-warehouse-mgr/tour-dwm.md)즉, 테이블에 대해 복제 방법이 자동으로 선택됩니다. 다양한 복제 방법, 표의 구성 방법 및 표 데이터의 작동 방식을 이해하면 표에 가장 적합한 복제 방법을 선택할 수 있습니다.

## 복제 방법이란 무엇입니까?

`Replication` 메서드는 세 개의 그룹으로 나뉩니다. `Incremental`, `Full Table`, 및 `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) 는 다음을 의미합니다. [!DNL Commerce Intelligence] 모든 복제 시도 시 신규 또는 업데이트된 데이터만 복제합니다. Adobe 이러한 메서드는 지연을 크게 줄이므로 가능하면 이를 사용하는 것이 좋습니다.

[**[!UICONTROL Full Table Replication]**](#fulltable) 는 다음을 의미합니다. [!DNL Commerce Intelligence] 모든 복제 시도 시 표의 전체 내용을 복제합니다. 복제되는 데이터의 양이 너무 많기 때문에 이러한 메서드는 지연 및 업데이트 시간을 늘릴 수 있습니다. Adobe 테이블에 타임스탬프가 지정된 열이나 날짜/시간 열이 포함되어 있는 경우 증분 메서드를 대신 사용하는 것이 좋습니다.

**[!UICONTROL Paused]** 테이블에 대한 복제가 중지 또는 일시 중지되었음을 나타냅니다. [!DNL Commerce Intelligence] 는 업데이트 주기 동안 새 데이터나 업데이트된 데이터를 확인하지 않습니다. 즉, 이 항목을 복제 방법으로 가진 테이블에서 데이터가 복제되지 않습니다.

## 증분 복제 방법 {#incremental}

### 수정된 날짜 (가장 이상적인)

다음 `Modified At` 복제 방법에서는 복제할 데이터를 찾기 위해 날짜/시간 열(행이 만들어지면 채워지고 데이터가 변경될 때 업데이트됨)을 사용합니다. 이 메서드는 다음 기준을 충족하는 테이블을 사용하도록 설계되었습니다.

* 다음 포함: `datetime` 행이 만들어질 때 처음에 채워지고 행이 수정될 때마다 업데이트되는 열
* 다음 `datetime` 열이 null이 아닙니다.
* 행은 테이블에서 삭제되지 않습니다

이러한 기준 외에도 Adobe은 **색인화** 다음 `datetime` 다음에 사용된 열 `Modified At` 복제를 통해 복제 속도를 최적화할 수 있습니다.

업데이트가 실행되면 값이 인 행을 검색하여 새 데이터나 변경된 데이터를 식별합니다 `datetime` 가장 최근 업데이트 후에 발생한 열입니다. 새 행이 검색되면 Data Warehouse에 복제됩니다. 에 행이 있는 경우 [Data Warehouse 관리자](../data-warehouse-mgr/tour-dwm.md): 현재 데이터베이스 값으로 덮어쓰여집니다.

예를 들어 테이블에는 라는 열이 있을 수 있습니다. `modified\_at` 데이터가 마지막으로 변경된 시간을 나타냅니다. 가장 최근 업데이트가 화요일 12시에 실행된 경우 업데이트는 `modified\_at` 화요일 정오보다 큰 값. 화요일 정오 이후에 생성되거나 수정된 모든 검색된 행은 Data Warehouse에 복제됩니다.

**알고 있었어?**
데이터베이스가 현재 다음을 지원할 수 없는 경우에도 `Incremental` 복제 방법, 다음을 수행할 수 있습니다. [데이터베이스 변경](../../best-practices/mod-db-inc-replication.md) 을(를) 사용할 수 있도록 하는 것입니다. `Modified At` 또는 `Single Auto Incrementing PK`.

`Modified At` 는 가장 이상적인 복제 방법일 뿐만 아니라 가장 빠른 복제 방법입니다. 이 방법은 대규모 데이터 세트에서 눈에 띄는 속도 증가를 생성할 뿐만 아니라 재확인 옵션을 구성할 필요가 없습니다. 다른 방법은 작은 데이터 하위 집합이 변경된 경우에도 변경 사항을 식별하기 위해 전체 테이블을 반복해야 합니다. `Modified At` 작은 부분집합만 반복합니다.

### 단일 자동 증분 기본 키

`Auto Incrementing` 는 행에 기본 키를 순차적으로 할당하는 동작입니다. 테이블이 `Auto Incrementing` 그리고 테이블에서 가장 높은 기본 키는 1,000이고, 그 다음 기본 값은 1,001 이상입니다. 를 사용하지 않는 테이블 `Auto Incrementing` 비헤이비어는 기본 키 값을 1,000 미만으로 할당하거나 훨씬 큰 숫자로 이동할 수 있지만, 일반적으로 사용되지는 않습니다.

이 메서드는 다음 기준을 충족하는 테이블에서 새 데이터를 복제하도록 설계되었습니다.

* `single-column primary key`; 및
* `primary key` 데이터 유형: `integer`; 및
* `auto incrementing` 기본 키 값.

테이블이 을 사용하는 경우 `Single Auto Incrementing Primary Key` 복제에서는 Data Warehouse의 현재 최고 값보다 높은 기본 키 값을 검색하여 새 데이터를 검색합니다. 예를 들어 Data Warehouse에서 가장 높은 기본 키 값이 500인 경우 다음 업데이트가 실행되면 기본 키 값이 501 이상인 행을 검색합니다.

### 날짜 추가

다음 `Add Date` 메서드는 다음과 유사하게 작동합니다. `Single Auto Incrementing Primary Key` 메서드를 사용합니다. 이 메서드는 테이블의 기본 키에 정수를 사용하는 대신 `timestamped` 새 행을 확인하는 열입니다.

테이블에서 를 사용하는 경우 `Add Date` 복제에서는 Data Warehouse에 동기화된 최신 날짜보다 타임스탬프가 지정된 값을 검색하여 새 데이터를 검색합니다. 예를 들어 업데이트가 2015/20/12 09에 마지막으로 실행된 경우:00:00: 타임스탬프가 이보다 큰 행은 새 데이터로 표시되고 복제됩니다.

>[!NOTE]
>
>와(과) 달리 `Modified At` 메서드, `Add Date` 기존 행에서 업데이트된 정보를 확인하지 않습니다. 새 행만 기다립니다.

## 전체 테이블 복제 방법 {#fulltable}

### 전체 테이블

`Full table` 복제는 새 행이 발견될 때마다 전체 테이블을 새로 고칩니다. 새 행이 있다고 가정할 때 모든 업데이트 중에 모든 데이터를 다시 처리해야 하므로 이 방법은 가장 효율성이 낮은 복제 방법입니다.

새 행은 동기화 프로세스가 시작될 때 데이터베이스를 쿼리하고 행 수를 계산하여 감지됩니다. 로컬 데이터베이스에 보다 많은 행이 포함된 경우 [!DNL Commerce Intelligence]그런 다음 테이블이 새로 고쳐집니다. 행 수가 동일한 경우 또는 [!DNL Commerce Intelligence] 다음 포함 *기타* 로컬 데이터베이스보다 행이 많으면 테이블을 건너뜁니다.

이는 다음과 같은 중요한 사항을 발생시킵니다. **`Full Table`다음 경우에는 복제가 호환되지 않습니다.**

* 후속 업데이트 주기 사이에 로컬 데이터베이스 테이블에서 생성된 행보다 더 많은 행이 삭제되거나
* 열 값은 변경되지만 추가 행은 만들어지지 않습니다

위의 시나리오 중 하나에서 `Full Table` 복제는 변경 사항을 감지하지 못하며 데이터가 부실 상태가 됩니다. 이 복제 방법의 비효율성과 위에서 언급한 요구 사항으로 인해, `Full Table` 복제는 최후의 수단으로만 권장됩니다.

### 기본 키 일괄 처리

테이블에서 를 사용하는 경우 `Primary Key Batch` (PK 배치), 기본 키 값의 범위 내 행 또는 배치 수를 계산하여 새 데이터를 검색합니다. 일반적으로 이 값이 정수와 함께 사용된다고 생각하지만 시스템이 상수 범위를 정의할 수 있는 방식으로 텍스트 값도 정렬할 수 있습니다.

예를 들어 업데이트가 실행되고 1~100개의 키 범위에 대한 행 수를 실행한다고 가정해 보겠습니다. 이 업데이트에서 시스템은 37개의 행을 찾아 기록합니다. 다음 업데이트에서는 1-100 범위에서 행 카운트가 다시 수행되며 41개의 행을 찾습니다. 마지막 업데이트와 비교하여 행 수에 차이가 있으므로 시스템이 해당 범위(또는 배치)를 더 자세히 검사합니다.

이 방법은 다음 기준을 충족하는 테이블에서 데이터를 복제하기 위한 것입니다.

* 정수가 아닌 단일 열 또는
* 복합 키(기본 키로 구성된 여러 열) - 복합 기본 키에 사용되는 열은 null 값을 가질 수 없습니다. 또는
* 단일 열, 정수 및 기본 키 값 비자동 증분

배치를 검사하고 변경 사항을 찾기 위해 발생해야 하는 처리량으로 인해 이 방법은 매우 느리므로 이상적인 방법이 아닙니다. Adobe은 다른 복제 방법을 지원하도록 필요한 사항을 수정할 수 없는 한 이 방법을 사용하지 않는 것이 좋습니다. 이 메서드를 사용해야 하는 경우 업데이트 시간이 늘어날 것으로 예상됩니다.

## 복제 방법 설정 중

복제 방법은 테이블에 따라 설정됩니다. 테이블에 대한 복제 방법을 설정하려면 [`Admin`](../../administrator/user-management/user-management.md) Data Warehouse 관리자에 액세스할 수 있는 권한.

1. Data Warehouse 관리자에서 테이블을 선택합니다. `Synced Tables` 테이블의 스키마를 표시할 목록입니다.
1. 현재 복제 방법은 표 이름 아래에 나열되어 있습니다. 변경하려면 링크를 클릭합니다.
1. 표시되는 팝업에서 다음 중 하나 옆에 있는 라디오 단추를 클릭합니다. `Incremental` 또는 `Full Table` 복제 - 복제 유형을 선택합니다.
1. 그런 다음 **[!UICONTROL Replication Method]** 드롭다운을 클릭하여 방법을 선택합니다. 예를 들어, `Paused` 또는 `Modified At`.

   >[!NOTE]
   >
   >**일부 증분 메서드를 사용하려면 를 설정해야 합니다.`Replication Key`**. [!DNL Commerce Intelligence] 은 이 키를 사용하여 다음 업데이트 주기가 시작되는 위치를 결정합니다.
   >
   >예를 들어 `modified at` 을 위한 메서드 `orders` 테이블, 다음을 설정해야 합니다. `date column` 를 복제 키로 사용합니다. 복제 키에 대한 몇 가지 옵션이 있을 수 있지만 `created at`또는 주문이 생성된 시간입니다. 마지막 업데이트 주기가 2015년 12월 1일에 중지된 경우 00:10:00, 다음 사이클은 `created at` 이 날짜 이후입니다.

1. 완료되면 다음을 클릭하십시오. **[!UICONTROL Save]**.

전체 프로세스를 살펴봅니다.

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## 요약

이 표를 정리하면 다양한 복제 방법을 비교합니다. Data Warehouse 테이블에 대한 방법을 선택할 때 매우 편리합니다.

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | 빠름 | 느림 | 아니요 | 아니요 | 아니요 | 예 |
| `Primary Key Batch Monitoring` | 느림 | 느림 | 예 | 예 | 예 | 예 |
| `Modified At` | 빠름 | 빠름 | 예 | 예 | 예 | 아니요 |

{style="table-layout:auto"}

## 관련 설명서

* [데이터 재확인 이해](../data-warehouse-mgr/cfg-data-rechecks.md)
* [지원할 데이터베이스 수정 ](../../best-practices/mod-db-inc-replication.md)
* [분석을 위해 데이터베이스 최적화](../../best-practices/opt-db-analysis.md)
* [업데이트 시간 단축](../../best-practices/reduce-update-cycle-time.md)
