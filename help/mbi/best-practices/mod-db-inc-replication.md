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

다음 `Modified At` 가장 이상적인 복제 방법인 메서드는 `datetime` 새 데이터 및/또는 업데이트된 데이터를 감지하는 열입니다. 다음 사항을 기억하십시오. `datetime` 이 메서드를 사용하는 테이블의 열은 인덱싱되어야 하며 언제든지 null 값을 포함할 수 없습니다.

테이블에 이 없는 경우 `datetime` 열, 인덱스를 추가할 수 있습니다. `modified at` 열. Null 값은 다음에서 사용할 수 없습니다. `modified at` 열. 열이 모든 행에 대해 채워져 있는지 확인합니다.

을(를) 확인하려면 `Modified At` 메서드는 의도한 대로 작동하므로 테이블에서 행을 삭제할 수 없습니다. 대신 를 추가하여 행을 부적합으로 표시해야 합니다 `deleted` 열을 테이블에 추가합니다. 이 열은 `1` 행이 유효하지 않고 `0` 그렇지 않으면. 그런 다음 지표 및 보고서를 작성할 때 이 열을 사용하여 잘못된 행을 필터링할 수 있습니다.

## 단일 자동 증분 기본 키에 대한 수정 사항

다음과 같은 경우 `Modified At` 메서드를 활성화할 수 없는 경우 단일 자동 증분 기본 키가 다음 최적 옵션입니다. 이 방법을 사용하여 Data Warehouse에서 현재 최고값보다 높은 기본 키 값을 검색하여 표에서 새 데이터를 검색합니다.

이 방법을 사용하는 테이블은 기본 키를 자동으로 증가시키는 정수가 있는 단일 열이라는 점을 기억하십시오. 데이터베이스에서 이 메서드를 사용하려면 다음을 수정하십시오.

* 기본 키가 복합 키 또는 정수가 아닌 경우 기본 키를 자동 증분 정수로 변경합니다
* 기본 키가 단일 정수 열이지만 비순차적으로 키를 할당할 수 있는 경우 기본 키를 자동 증분으로 변경합니다

## 요약

테이블을 약간 수정하면 보다 빠르고 효율적인 증분 복제 방법을 활용할 수 있습니다. 그러나 이것이 불가능할 경우 다음 작업을 수행할 수 있습니다. [업데이트 시간 단축](../best-practices/reduce-update-cycle-time.md) 및 [데이터베이스 최적화](../best-practices/opt-db-analysis.md).
