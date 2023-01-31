---
title: 순차적 비교 계산된 열
description: 순차적 비교 계산 열의 목적과 사용에 대해 알아봅니다.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# 순차적 비교 계산된 열

이 항목에서는 의 목적과 사용에 대해 간략하게 설명합니다 `Sequential Comparison` 계산된 열은에서 사용할 수 있습니다. **[!DNL Manage Data > Data Warehouse]** 페이지. 아래는 그것이 무엇을 하는지, 그 다음에 예를 들고, 그것을 만드는 역학에 대한 설명입니다.

**설명**

다음 `Sequential Comparison` 열 유형: 연속된 이벤트 간의 차이를 찾습니다. 가장 일반적인 `Sequential Comparison` 열은 `Seconds since previous order` 열. 이 열에 필요한 세 개의 입력이 있습니다.

1. `Event Owner`: 이 입력은 행이 그룹화되는 엔터티를 결정합니다. 예를 들어, `Seconds since previous order` 열에서 동일한 고객의 이전 순서 이후 시간(초)을 찾으려면 이벤트 소유자가 고객입니다.
1. `Event Date`: 이 입력은 이벤트 시퀀스를 적용합니다. 의 경우 `Seconds since previous order`를 설정하는 경우 순서의 타임스탬프가 포함된 열은 `Event Date`. 이 입력은 항상 타임스탬프입니다.
1. `Value to Compare`: 이 입력은 비교할 실제 값입니다. 현재 행의 값에서 이전 행의 값을 빼기 위해 따라서 고객의 연속 주문 간의 시간 차이를 찾는 열이 호출됩니다 `Seconds since previous order`. 이 입력은 타임스탬프가 될 필요가 없습니다. 타임스탬프가 아닌 예는 고객의 연속된 주문 간의 순서 값 차이를 찾는 것입니다.

**예**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | NULL |
| **`2`** | B | 2015-01-01 00:30:00 | NULL |
| **`3`** | A | 2015-01-01 02:00:00 | 7200년 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

위의 예에서 `Seconds since owner's previous event` 은 `Sequential Comparison` 계산된 열입니다. 대상 `owner_id = A`를 지정하는 경우, 먼저 `timestamp` 열을 누른 다음 이전 이벤트의 `timestamp` 현재 이벤트의 타임스탬프에서 확인하십시오. 표의 세 번째 행 - 의 두 번째 행 `owner_id A` - 값 `Seconds since owner's previous event` 는 &#39;2015-01-01 02:00&#39;과 &#39;2015-01-01 00&#39; 사이의 초 수입니다:00:00&#39;. 이 차이는 2시간 = 7200초입니다.

이 계산된 열 유형의 경우 소유자의 첫 번째 이벤트에 해당하는 행에는 `NULL` 값.

**역학**

을(를) 만들려면 **이벤트 번호** 열:

1. 로 이동합니다 **[!DNL Manage Data** > **Data Warehouse]** 페이지.
1. 이 열을 만들 테이블로 이동합니다.
1. 클릭 **[!UICONTROL Create New Column]** 화면 오른쪽 상단에 있습니다.
1. 선택 `Same Table` 로서의 `Definition Type` 비교하려는 열이 동일한 테이블에 없는 경우 다시 배치해야 할 수 있습니다.
1. 선택 `SEQUENTIAL_COMPARISON` 로서의 `Column Definition Equation`.
1. 위에서 설명한 대로 입력을 선택합니다.
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`
1. 행을 고려하지 않도록 제외하기 위해 필터를 추가할 수도 있습니다. 제외된 행에는 이 열에 대한 NULL 값이 있습니다.
1. 페이지 상단에 있는 열 이름을 입력하고 클릭 **[!UICONTROL Save]**.
1. 열을 사용할 수 있습니다 *즉시*.

![SEC](../../assets/SEC_new.png)
