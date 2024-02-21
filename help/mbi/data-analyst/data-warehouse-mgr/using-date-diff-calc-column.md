---
title: 날짜 차이 계산 열 사용
description: 날짜 차이 계산 열의 목적과 용도에 대해 알아봅니다.
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 2433a614e9858684842804a0ae29fb67f0d41ead
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 날짜 차이 계산 열

이 항목에서는 의 목적과 용도를 간략하게 설명합니다. `Date Difference` 계산된 열에서 사용할 수 있음 **[!DNL Manage Data > Data Warehouse]** 페이지를 가리키도록 업데이트하는 중입니다. 아래는 그것이 하는 일에 대한 설명이며, 그 다음은 예시, 그리고 그것을 만드는 역학이다.

**설명**

다음 `Date Difference` 열 유형은 이벤트 타임스탬프를 기반으로 단일 레코드에 속하는 두 이벤트 간의 시간을 계산합니다. 이 열에서 계산된 원시 값은 초 단위이지만 보고서에 표시하기 위해 분, 시간, 일 등으로 자동 변환됩니다. 그러나 필터/그룹으로 사용되는 경우 값(초)을 사용할 수 있습니다.

A `date difference` 계산된 열은 고객 등록과 첫 번째 주문 사이의 평균 시간과 같이, 두 이벤트 사이의 평균 또는 중간 시간을 계산하는 지표를 만드는 데 사용할 수 있습니다.

**예**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}


위의 예에서 `Date Difference` 열은 `Seconds between timestamp_2 and timestamp_1` 열. 계산을 수행합니다 `timestamp_2 minus timestamp_1`.

**역학**

다음 단계에서는 을(를) 만드는 방법을 설명합니다 `Date Difference` 열.

1. 다음 위치로 이동 **[!DNL Manage Data > Data Warehouse]** 페이지를 가리키도록 업데이트하는 중입니다.
1. 이 열을 생성할 테이블로 이동합니다.
1. 클릭 **[!UICONTROL Create a Column]** 열을 다음과 같이 구성합니다.
   * 선택 `Column Definition Type` > `Same Table`
   * 선택 `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * 선택 `Ending DATETIME` 열 > 종료 날짜/시간 필드를 선택합니다. 이 필드는 일반적으로 나중에 발생하는 이벤트입니다.
   * 선택 `Starting DATETIME` 열** > 시작 날짜/시간 필드를 선택합니다. 이 필드는 일반적으로 이전에 발생하는 이벤트입니다.

1. 열에 이름을 입력하고 클릭 **[!UICONTROL Save]**.
1. 열을 사용할 수 있습니다. *즉시*.

예를 들어 다음 예제는 `Seconds between order date and customer's creation date`:

![](../../assets/date_diff.png)
