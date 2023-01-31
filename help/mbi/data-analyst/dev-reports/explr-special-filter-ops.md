---
title: 특수 필터 연산자
description: 보고서를 만들거나 지표를 만들 때 필터에 사용되는 몇 가지 특수 연산자에 대해 알아봅니다.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# 필터 옵션

이 문서에서 몇 가지 특별한 사항을 살펴보겠습니다 `operators` 에서 사용 `filters` when [보고서 만들기](../../tutorials/using-visual-report-builder.md){: target=&quot;_blank&quot;} 또는 [지표 만들기](../../data-user/reports/ess-manage-data-metrics.md){: target=&quot;_blank&quot;}.

## `Filter Operators`

* `LIKE` 패턴 일치용. 와일드카드 문자 %(문자 수가 다른 와일드카드) 또는 _( 와일드카드 단일 문자의 경우)와 함께 사용해야 합니다.  예를 들어 제한 사항 `LIKE \_ake%` 에 대해 true를 반환합니다. `Jake Stein`, `Jake Smith`, 또는 `Fake Smith`.  에 대해 false를 반환합니다 `Drake Smith`.

* `NOT LIKE` 는 위의 패턴 일치와 유사하지만 일치하지 않는 패턴을 확인합니다.

* `IS` 열이 `NULL`또는 비어 있습니다.

* `IS NOT` 는 와(과) 유사합니다 `IS` 연산자이지만 NULL이 아닌 열이 있는지 확인합니다.

* `IN` 쉼표로 구분된 목록에서 값이 있는지 확인합니다. (예: &quot;색상&quot; `IN` red,orange&quot;는 색상에 해당합니다 `equal to` 빨간색 또는 색상 `equal to` 주황색).

* `NOT IN` 와 유사함 `IN` 위에 있지만 값이 없는지 확인합니다.
