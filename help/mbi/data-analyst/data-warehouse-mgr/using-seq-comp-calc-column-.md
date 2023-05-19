---
title: 순차적 비교 계산 열
description: 순차적 비교 계산 열의 목적과 용도에 대해 알아봅니다.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 2%

---

# 순차적 비교 계산 열

이 항목에서는 의 목적과 용도를 간략하게 설명합니다. `Sequential Comparison` 계산된 열에서 사용할 수 있음 **[!DNL Manage Data > Data Warehouse]** 페이지를 가리키도록 업데이트하는 중입니다. 아래는 그것이 하는 일에 대한 설명이며, 그 뒤에 예제와 그것을 만드는 역학이 이어진다.

**설명**

다음 `Sequential Comparison` 열 유형: 연속 이벤트 간의 차이를 찾습니다. 의 가장 일반적인 유형 `Sequential Comparison` 열은 `Seconds since previous order` 열. 이 열에는 세 가지 입력이 필요합니다.

1. `Event Owner`: 이 입력은 그룹화된 행을 위한 엔티티를 결정합니다. 예를 들어, `Seconds since previous order` 열에서 이벤트 소유자는 고객입니다. 동일한 고객의 이전 주문 이후 시간(초)을 찾으려고 하기 때문입니다.
1. `Event Date`: 이 입력은 이벤트 시퀀스를 적용합니다. 의 경우에는 `Seconds since previous order`: 순서의 타임스탬프가 포함된 열은 `Event Date`. 이 입력은 항상 타임스탬프입니다.
1. `Value to Compare`: 이 입력은 비교할 실제 값입니다. 현재 행 값에서 이전 행 값을 뺍니다. 따라서 고객의 연속적인 주문 간의 시간 차이를 찾는 열을 호출합니다 `Seconds since previous order`. 이 입력은 타임스탬프일 필요가 없습니다. 타임스탬프가 아닌 예는 고객의 연속적인 주문 간 주문 값의 차이를 찾는 것입니다.

**예**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | NULL |
| **`2`** | B | 2015-01-01 00:30:00 | NULL |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

위의 예에서, `Seconds since owner's previous event` 은(는) `Sequential Comparison` 계산 열입니다. 의 경우 `owner_id = A`를 설정하는 경우 먼저 `timestamp` 열을 선택한 다음 이전 이벤트의 `timestamp` (현재 이벤트의 타임스탬프 기준). 테이블의 세 번째 행에서 - 다음에 대한 두 번째 행 `owner_id A` - 값 `Seconds since owner's previous event` 은 &#39;2015-01-01 02:00&#39;과 &#39;2015-01-01 00 사이의 초 수입니다.:00:00&#39;. 이 차이는 2시간 = 7,200초와 같습니다.

이 계산된 열 유형의 경우 소유자의 첫 번째 이벤트에 해당하는 행에는 `NULL` 값.

**역학**

을(를) 만들려면 **이벤트 번호** 열:

1. 다음 위치로 이동 **[!DNL Manage Data > Data Warehouse]** 페이지를 가리키도록 업데이트하는 중입니다.

1. 이 열을 생성할 테이블로 이동합니다.

1. 클릭 **[!UICONTROL Create New Column]** 오른쪽 상단 모서리입니다.

1. 선택 `Same Table` (으)로 `Definition Type` 비교하려는 열이 동일한 테이블에 없는 경우 열을 재배치해야 할 수 있습니다.

1. 선택 `SEQUENTIAL_COMPARISON` (으)로 `Column Definition Equation`.

1. 위에서 설명한 대로 입력을 선택합니다.
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. 행이 고려되지 않도록 제외하기 위해 필터를 추가할 수도 있습니다. 제외된 행에는 `NULL` 이 열의 값입니다.

1. 페이지 상단에 열 이름을 입력하고 를 클릭합니다. **[!UICONTROL Save]**.

1. 열을 사용할 수 있습니다. *즉시*.

![초](../../assets/SEC_new.png)
