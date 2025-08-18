---
title: 이벤트 번호 계산 열
description: 이벤트 번호 계산 열의 목적과 용도에 대해 알아봅니다.
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# 이벤트 번호 계산 열

이 항목에서는 `Event Number` 페이지에서 사용할 수 있는 **[!DNL Manage Data > Data Warehouse]** 계산 열의 목적과 용도에 대해 간략하게 설명합니다. 아래는 그것이 하는 일에 대한 설명이며, 그 다음은 예시, 그리고 그것을 만드는 역학이다.

**설명**

`Event Number` 열 형식은 **또는**&#x200B;과(와) 같은 특정 `customer`이벤트 소유자`user`에 대해 이벤트가 발생한 시퀀스를 식별합니다. SQL에 익숙한 경우 이 열 형식은 `RANK` 함수와 동일합니다. 데이터에 있는 처음 이벤트, 반복 이벤트 또는 n번째 이벤트 간의 동작 차이를 관찰하는 데 사용할 수 있습니다.

동률인 경우 이 열에는 연결된 이벤트에 대해 동일한 **순위**&#x200B;가 포함되어 있으며 후속 숫자를 건너뜁니다. 예를 들어, 숫자가 5,8,10,10,12인 경우 순위는 1,2,3,3,5가 됩니다.

이 열의 가장 일반적인 사용 사례는 최초 구매자와 반복 구매자를 분석하는 것입니다. `Customer's order number` = 1에 (지표 또는 보고서에) 필터를 추가하여 구매자를 처음 식별합니다. `Customer's order number`은(는) `Event Number` 형식의 열입니다.

**예**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| ** 1 | A | 2015-01-01 00:00:00 | 1 |
| ** 2 | B | 2015-01-01 00:30:00 | 1 |
| ** 3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015년 1월 2일 13일:00:0 | 3 |
| ** 5 | B | 2015년 1월 3일 13일:00:0 | 2 |

위의 예에서 `Owner's event number` 열은 `Event Number` 열입니다. `timestamp` 열을 기준으로 발생한 순서대로 소유자의 이벤트에 등급을 매깁니다.

예를 들어 `owner_id = A`인 모든 행을 고려하십시오. 테이블의 첫 번째 행은 이 소유자의 가장 빠른 타임스탬프이고 그 다음이 테이블의 세 번째 행, 그 다음이 테이블의 네 번째 행입니다.

**기계**

다음은 `Event Number` 열 만들기에 대한 지침입니다.

1. **[!UICONTROL Manage Data > Data Warehouse]** 페이지로 이동합니다.

1. 이 열을 생성할 테이블로 이동합니다.

1. **[!UICONTROL Create a Column]**&#x200B;을(를) 클릭하고 `EVENT_NUMBER (…)` 섹션 아래에서 `Same Table` 열 형식을 선택합니다.

1. 첫 번째 드롭다운 `Event Owner`은(는) 등급을 결정할 엔터티를 지정합니다. `Customer's order number`의 경우 `customer_id` 또는 `customer_email`과(와) 같은 고객 식별자는 `Event Owner`입니다.

1. 두 번째 드롭다운 `Event Rank`은(는) 행의 등급을 결정하는 시퀀스를 적용하는 열을 지정합니다. `Customer's order number`인 경우 `created_at` 타임스탬프는 `Event Rank`입니다.

1. `Options` 드롭다운에서 행을 고려하지 않도록 제외하는 필터를 추가할 수 있습니다. 제외된 행에 이 열에 대한 `NULL` 값이 있습니다.

1. 열에 이름을 입력하고 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

1. 열은 _즉시 사용할 수 있습니다._
