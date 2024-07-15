---
title: 특수 필터 연산자
description: 보고서를 만들거나 지표를 만들 때 필터에 사용되는 몇 가지 특수 연산자에 대해 알아봅니다.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# 필터 옵션

이 항목에서는 [보고서 만들기](../../tutorials/using-visual-report-builder.md){: target=&quot;_blank&quot;} 또는 [지표 만들기](../../data-user/reports/ess-manage-data-metrics.md){: target=&quot;_blank&quot;} 시 `filters`에서 사용되는 몇 가지 특수 `operators`을 살펴봅니다.

## `Filter Operators`

* 패턴 일치를 위한 `LIKE`. 와일드카드 문자 %(문자의 수가 다양한 와일드카드의 경우) 또는 _(와일드카드 단일 문자의 경우)와 함께 사용해야 합니다.  예를 들어 `LIKE \_ake%` 제한은 `Jake Stein`, `Jake Smith` 또는 `Fake Smith`에 대해 true를 반환합니다.  `Drake Smith`에 대해 false를 반환합니다.

* `NOT LIKE`은(는) 위의 패턴 일치와 비슷하지만 일치하지 않는 패턴을 확인합니다.

* `IS`은(는) 열이 `NULL`인지 또는 비어 있는지 확인합니다.

* `IS NOT`은(는) 위의 `IS` 연산자와 비슷하지만 NULL이 아닌 열을 확인합니다.

* `IN`은(는) 쉼표로 구분된 목록에 값이 있는지 확인합니다. 예를 들어 &quot;색상 `IN` red,orange&quot;는 색상 `equal to` red 또는 색상 `equal to` orange와 동일합니다.

* `NOT IN`은(는) 위의 `IN`과(와) 유사하지만 값이 없는지 확인합니다.
