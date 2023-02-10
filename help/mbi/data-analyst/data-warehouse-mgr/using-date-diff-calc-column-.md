---
title: 날짜 차이 계산된 열 사용
description: 날짜 차이 계산 열의 목적과 용도를 알아봅니다.
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 2%

---

# 날짜 차이 계산된 열

이 항목에서는 의 목적과 사용에 대해 간략하게 설명합니다 `Date Difference` 계산된 열은에서 사용할 수 있습니다. **[!DNL Manage Data > Data Warehouse]** 페이지. 아래는 그것이 무엇을 하는지, 그 다음에 예를 들고, 그것을 만드는 역학에 대한 설명입니다.

**설명**

다음 `Date Difference` 열 유형: 이벤트 타임스탬프를 기반으로 하여 단일 레코드에 속하는 두 이벤트 사이의 시간을 찾습니다. 이 열에서 계산된 원시 값은 초 단위이지만, 보고서에 표시하기 위해 분, 시간, 일 등으로 자동 변환됩니다. 그러나 을으로 필터/그룹으로 사용하는 경우 이 값을 초 단위로 사용할 수 있습니다.

A `date difference` 계산된 열을 사용하여 고객 등록과 첫 번째 주문 간의 평균 시간과 같이 두 이벤트 간의 평균 또는 중간값을 계산하는 지표를 만들 수 있습니다.

**예**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style=&quot;table-layout:auto&quot;}


위의 예에서 `Date Difference` 열은 `Seconds between timestamp_2 and timestamp_1` 열. 계산을 수행합니다 `timestamp_2 minus timestamp_1`.

**역학**

다음 절차에서는 `Date Difference` 열.

1. 로 이동합니다 **[!DNL Manage Data > Data Warehouse]** 페이지.
1. 이 열을 만들 테이블로 이동합니다.
1. 클릭 **[!UICONTROL Create a Column]** 열을 다음과 같이 구성합니다.
   * 선택 `Column Definition Type` > `Same Table`
   * 선택 `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * 선택 `Ending DATETIME` column > end datetime 필드를 선택합니다. 이 필드는 일반적으로 나중에 발생하는 이벤트입니다
   * 선택 `Starting DATETIME` column** > start datetime 필드를 선택합니다. 이 필드는 일반적으로 이전에 발생한 이벤트입니다

1. 열에 이름을 입력하고 클릭 **[!UICONTROL Save]**.
1. 열을 사용할 수 있습니다 *즉시*.

예를 들어, 다음 예제가 `Seconds between order date and customer's creation date`:

![](../../assets/date_diff.png)
