---
title: 순차적 비교 계산 열
description: 순차적 비교 계산 열의 목적과 용도에 대해 알아봅니다.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 2433a614e9858684842804a0ae29fb67f0d41ead
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# 순차적 비교 계산 열

이 항목에서는 `Sequential Comparison` 페이지에서 사용할 수 있는 **[!DNL Manage Data > Data Warehouse]** 계산 열의 목적과 용도에 대해 간략하게 설명합니다. 아래는 그것이 하는 일에 대한 설명이며, 그 뒤에 예제와 그것을 만드는 역학이 이어진다.

**설명**

`Sequential Comparison` 열 형식: 연속 이벤트 간의 차이점을 찾습니다. `Sequential Comparison` 열의 가장 일반적인 형식은 `Seconds since previous order` 열입니다. 이 열에는 세 가지 입력이 필요합니다.

1. `Event Owner`: 이 입력은 행이 그룹화된 엔터티를 결정합니다. 예를 들어, `Seconds since previous order` 열에서 이벤트 소유자는 고객입니다. 동일한 고객의 이전 주문 이후 시간(초)을 찾으려고 하기 때문입니다.
1. `Event Date`: 이 입력은 이벤트 시퀀스를 적용합니다. `Seconds since previous order`의 경우 순서의 타임스탬프가 포함된 열은 `Event Date`이어야 합니다. 이 입력은 항상 타임스탬프입니다.
1. `Value to Compare`: 이 입력은 비교할 실제 값입니다. 현재 행 값에서 이전 행 값을 뺍니다. 따라서 고객의 연속 주문 간의 시간 차이를 찾는 열을 `Seconds since previous order`이라고 합니다. 이 입력은 타임스탬프일 필요가 없습니다. 타임스탬프가 아닌 예는 고객의 연속적인 주문 간 주문 값의 차이를 찾는 것입니다.

**예**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | NULL |
| **`2`** | B | 2015-01-01 00:30:00 | NULL |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015년 1월 2일 13일:00:0 | 126000 |
| **`5`** | B | 2015년 1월 3일 13일:00:0 | 217800 |

위의 예에서 `Seconds since owner's previous event`은(는) `Sequential Comparison` 계산 열입니다. `owner_id = A`의 경우 먼저 `timestamp` 열을 기반으로 시퀀스를 식별한 다음 현재 이벤트의 타임스탬프에서 이전 이벤트의 `timestamp`을(를) 뺍니다. 테이블의 세 번째 행인 `owner_id A`에 대한 두 번째 행에서 `Seconds since owner's previous event` 값은 &#39;2015-01-01 02:00&#39;과(와) &#39;2015-01-01 00:00:0&#39; 사이의 초 수입니다. 이 차이는 2시간 = 7,200초와 같습니다.

이 계산된 열 형식의 경우 소유자의 첫 번째 이벤트에 해당하는 행에 `NULL` 값이 있습니다.

**기계**

**이벤트 번호** 열을 만들려면:

1. **[!DNL Manage Data > Data Warehouse]** 페이지로 이동합니다.

1. 이 열을 생성할 테이블로 이동합니다.

1. 오른쪽 상단의 **[!UICONTROL Create New Column]**&#x200B;을(를) 클릭합니다.

1. `Same Table`을(를) `Definition Type`(으)로 선택합니다. 비교하려는 열이 같은 테이블에 없는 경우 위치를 다시 지정해야 할 수 있습니다.)

1. `SEQUENTIAL_COMPARISON`을(를) `Column Definition Equation`(으)로 선택합니다.

1. 위에서 설명한 대로 입력을 선택합니다.
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. 행이 고려되지 않도록 제외하기 위해 필터를 추가할 수도 있습니다. 제외된 행에 이 열에 대한 `NULL` 값이 있습니다.

1. 페이지 맨 위에 열 이름을 입력하고 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

1. 열은 *즉시*&#x200B;을 사용할 수 있습니다.

![초](../../assets/SEC_new.png)
