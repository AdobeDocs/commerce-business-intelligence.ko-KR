---
title: 이벤트 번호 계산된 열
description: 이벤트 번호 계산 열의 목적과 용도를 알아봅니다.
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 이벤트 번호 계산된 열

이 항목에서는 의 목적과 사용에 대해 간략하게 설명합니다 `Event Number` 계산된 열은에서 사용할 수 있습니다. **[!DNL Manage Data > Data Warehouse]** 페이지. 아래는 그것이 무엇을 하는지, 그 다음에 예를 들고, 그것을 만드는 역학에 대한 설명입니다.

**설명**

다음 `Event Number` 열 유형: 특정 이벤트에 대해 이벤트가 발생한 시퀀스를 식별합니다 **이벤트 소유자**, 비슷함 `customer` 또는 `user`. SQL에 익숙하다면 이 열 유형은 `RANK` 함수 위에 있어야 합니다. 처음 이벤트, 반복 이벤트 또는 데이터에 있는 n번째 이벤트 간의 동작 차이를 관찰하는 데 사용할 수 있습니다.

항목의 경우 이 열에는 다음이 포함됩니다 **등급** 연결된 이벤트에 대해 및에서 후속 숫자를 건너뜁니다. 예를 들어, 숫자 5,8,10,10,12의 순위를 매긴 경우, 그 순위는 1,2,3,3,5입니다.

이 열의 가장 일반적인 사용 사례는 처음 구매자와 반복 구매자를 분석하는 것입니다. 처음 구매자는 다음에 필터(지표 또는 보고서)를 추가하여 식별됩니다. `Customer's order number` = 1. `Customer's order number` 는 유형의 열입니다 `Event Number`.

**예**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2개 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2개 |

위의 예에서 열은 `Owner's event number` is `Event Number` 열. 이벤트 순서에 따라 소유자의 이벤트에 대한 등급을 지정합니다(기준 `timestamp` 열)에 포함될 수도 있습니다.

예를 들어, `owner_id = A`. 테이블의 첫 번째 행은 이 소유자에 대한 첫 번째 타임스탬프이며, 그 뒤에는 테이블의 세 번째 행이 있고 그 뒤에는 테이블의 네 번째 행이 옵니다.

**역학**

다음은 만들기 작업에 대한 몇 가지 지침입니다 `Event Number` 열:

1. 로 이동합니다 **[!UICONTROL Manage Data > Data Warehouse]** 페이지.
1. 이 열을 만들 테이블로 이동합니다.
1. 클릭 **[!UICONTROL Create a Column]** 그리고 `EVENT_NUMBER (…)` 열 유형: 아래에 `Same Table` 섹션을 참조하십시오.
1. 첫 번째 드롭다운 `Event Owner` 등급을 결정할 엔터티를 지정합니다. 의 경우 `Customer's order number`, 와 같은 고객 식별자 `customer_id` 또는 `customer_email` 이 경우 `Event Owner`.
1. 두 번째 드롭다운 `Event Rank` 행의 순위를 결정하는 시퀀스를 적용하는 열을 지정합니다. 의 경우 `Customer's order number`, `created_at` 타임스탬프는 `Event Rank`.
1. 아래에 `Options` 드롭다운에서 필터를 추가하여 행이 고려되지 않도록 제외할 수 있습니다. 제외된 행에는 `NULL` 이 열에 대한 값입니다.
1. 열에 이름을 입력하고 클릭 **[!UICONTROL Save]**.
1. 열을 사용할 수 있습니다 _즉시 작동합니다._
