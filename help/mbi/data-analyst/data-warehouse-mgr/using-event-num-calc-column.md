---
title: 이벤트 번호 계산 열
description: 이벤트 번호 계산 열의 목적과 용도에 대해 알아봅니다.
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 3%

---

# 이벤트 번호 계산 열

이 항목에서는 의 목적과 용도를 간략하게 설명합니다. `Event Number` 계산된 열에서 사용할 수 있음 **[!DNL Manage Data > Data Warehouse]** 페이지를 가리키도록 업데이트하는 중입니다. 아래는 그것이 하는 일에 대한 설명이며, 그 다음은 예시, 그리고 그것을 만드는 역학이다.

**설명**

다음 `Event Number` 열 유형은 특정 이벤트에 대해 이벤트가 발생한 시퀀스를 식별합니다 **이벤트 소유자**, 다음과 같음 `customer` 또는 `user`. SQL에 익숙한 경우 이 열 유형은 `RANK` 함수. 데이터에 있는 처음 이벤트, 반복 이벤트 또는 n번째 이벤트 간의 동작 차이를 관찰하는 데 사용할 수 있습니다.

동률인 경우 이 열에는 동일한 항목이 포함됩니다 **rank** 을 누릅니다. 예를 들어, 숫자가 5,8,10,10,12인 경우 순위는 1,2,3,3,5가 됩니다.

이 열의 가장 일반적인 사용 사례는 최초 구매자와 반복 구매자를 분석하는 것입니다. (지표나 보고서에) 필터를 추가하여 구매자를 처음 식별할 때 `Customer's order number` = 1. `Customer's order number` 은(는) 유형의 열입니다. `Event Number`.

**예**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

위의 예에서 열은 `Owner's event number` 은(는) `Event Number` 열. 소유자의 이벤트에 대해 이벤트가 발생한 순서대로 순위를 매깁니다( 를 기반으로 함). `timestamp` 열).

예를 들어, 다음과 같은 모든 행을 고려하십시오. `owner_id = A`. 테이블의 첫 번째 행은 이 소유자의 가장 빠른 타임스탬프이고 그 다음이 테이블의 세 번째 행, 그 다음이 테이블의 네 번째 행입니다.

**역학**

다음은 을(를) 만드는 방법에 대한 몇 가지 지침입니다 `Event Number` 열:

1. 다음 위치로 이동 **[!UICONTROL Manage Data > Data Warehouse]** 페이지를 가리키도록 업데이트하는 중입니다.

1. 이 열을 생성할 테이블로 이동합니다.

1. 클릭 **[!UICONTROL Create a Column]** 및 선택 `EVENT_NUMBER (…)` 열 유형: `Same Table` 섹션.

1. 첫 번째 드롭다운 `Event Owner` 등급을 결정할 엔티티를 지정합니다. 다음의 경우에 `Customer's order number`, 고객 식별자(예: ) `customer_id` 또는 `customer_email` 이(가) 다음이 될 수 있습니다. `Event Owner`.

1. 두 번째 드롭다운 `Event Rank` 행의 등급을 결정하는 시퀀스를 적용하는 열을 지정합니다. 다음의 경우에 `Customer's order number`, `created_at` 타임스탬프는 다음과 같습니다. `Event Rank`.

1. 아래 `Options` 드롭다운에서 필터를 추가하여 고려되지 않은 행을 제외할 수 있습니다. 제외된 행에는 `NULL` 이 열의 값입니다.

1. 열에 이름을 입력하고 클릭 **[!UICONTROL Save]**.

1. 열을 사용할 수 있습니다. _즉시._
