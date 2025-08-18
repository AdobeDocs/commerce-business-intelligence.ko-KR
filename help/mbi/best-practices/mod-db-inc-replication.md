---
title: 증분 복제를 지원하도록 데이터베이스 수정
description: 증분 복제를 지원하도록 데이터베이스를 수정하는 방법에 대해 알아봅니다.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# 증분 복제 지원

현재 테이블에서 증분 복제를 허용하지 않는 경우 가능한 솔루션에 대한 다음 권장 사항을 참조하십시오.

## 수정된 위치에 대한 수정 사항

가장 이상적인 복제 방법인 `Modified At` 메서드는 `datetime` 열을 사용하여 새 데이터 및/또는 업데이트된 데이터를 검색합니다. 이 메서드를 사용하는 테이블의 `datetime` 열은 인덱싱되어야 하며 언제든지 null 값을 포함할 수 없습니다.

테이블에 `datetime` 열이 없는 경우 인덱스 `modified at` 열을 추가할 수 있습니다. `modified at` 열에는 Null 값을 사용할 수 없습니다. 열이 모든 행에 대해 채워져 있는지 확인합니다.

`Modified At` 메서드가 의도한 대로 작동하도록 하려면 테이블에서 행을 삭제할 수 없습니다. 대신 테이블에 `deleted` 열을 추가하여 행을 유효하지 않은 것으로 표시해야 합니다. 이 열은 행이 잘못된 경우 `1`을(를) 반환하고 그렇지 않은 경우 `0`을(를) 반환합니다. 그런 다음 지표 및 보고서를 작성할 때 이 열을 사용하여 잘못된 행을 필터링할 수 있습니다.

## 단일 자동 증분 기본 키에 대한 수정 사항

`Modified At` 메서드를 사용하도록 설정할 수 없는 경우에는 단일 자동 증분 기본 키가 그 다음으로 좋은 옵션입니다. 새 데이터는 Data Warehouse에서 현재 가장 높은 값보다 높은 기본 키 값을 검색하여 이 방법을 사용하여 테이블에서 검색됩니다.

이 방법을 사용하는 테이블은 기본 키를 자동으로 증가시키는 정수가 있는 단일 열이라는 점을 기억하십시오. 데이터베이스에서 이 메서드를 사용하려면 다음을 수정하십시오.

* 기본 키가 복합 키 또는 정수가 아닌 경우 기본 키를 자동 증분 정수로 변경합니다
* 기본 키가 단일 정수 열이지만 비순차적으로 키를 할당할 수 있는 경우 기본 키를 자동 증분으로 변경합니다

## 요약

테이블을 약간 수정하면 보다 빠르고 효율적인 증분 복제 방법을 활용할 수 있습니다. 그러나 가능하지 않은 경우 [업데이트 시간을 줄이고](../best-practices/reduce-update-cycle-time.md) [데이터베이스를 최적화하고](../best-practices/opt-db-analysis.md)하는 다른 단계를 취할 수 있습니다.
