---
title: 데이터 검사 구성
description: 변경 가능한 값으로 데이터 열을 구성하는 방법에 대해 알아봅니다.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# 데이터 검사 구성

데이터베이스 테이블에는 변경 가능한 값이 있는 데이터 열이 있을 수 있습니다. 예를 들어, `orders`) 테이블에 라는 열이 있을 수 있습니다. `status`. 주문이 데이터베이스에 처음 기록되면 상태 열에 값이 포함될 수 있습니다 _보류 중_. 주문은에서 복제됩니다. [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) 함께 `pending` 값.

하지만 주문 상태는 변경될 수 있습니다. 항상 `pending` 상태. 결국에는 다음과 같이 될 수 있습니다. `complete` 또는 `cancelled`. Data Warehouse이 이 변경 사항을 동기화하도록 하려면 열에 새 값을 다시 선택해야 합니다.

이것이 과 어떻게 일치합니까? [복제 메서드](../data-warehouse-mgr/cfg-replication-methods.md) 그게 논의됐나요? 재검사 처리는 선택한 복제 방법에 따라 달라집니다. 다음 `Modified\_At` 재검사를 구성하지 않아도 되므로 복제 방법은 변경 값을 처리하는 데 가장 적합합니다. 다음 `Auto-Incrementing Primary Key` 및 `Primary Key Batch Monitoring` 메서드를 사용하려면 구성을 다시 확인해야 합니다.

이러한 방법 중 하나를 사용하는 경우 변경 가능한 열에 다시 확인하도록 플래그를 지정해야 합니다. 세 가지 방법으로 이 작업을 수행할 수 있습니다.

* 다시 검사할 업데이트 플래그 열의 일부로 실행되는 감사 프로세스입니다.

   >[!NOTE]
   >
   >Auditor는 샘플링 프로세스에 의존하며 변화하는 열을 즉시 포착하지 못할 수 있습니다.

* Data Warehouse 관리자에서 열 옆에 있는 확인란을 선택하고 **[!UICONTROL Set Recheck Frequency]**&#x200B;을 클릭하고 변경 사항을 확인해야 할 적절한 시간 간격을 선택합니다.
* 의 멤버 [!DNL MBI] Data Warehouse 팀은 Data Warehouse에서 다시 확인할 열을 수동으로 표시할 수 있습니다. 변경할 수 있는 열이 있는 경우 팀에 문의하여 재검사를 요청하십시오. 요청에 빈도와 함께 열 목록을 포함하십시오.

## 빈도 다시 확인 {#frequency}

**알고 있었어?**
에서 재확인 설정 `primary key` 열은 변경된 값에 대해 열을 확인하지 않습니다. 테이블에서 삭제된 행이 확인되고 삭제된 행은 Data Warehouse에서 삭제됩니다.

열에 다시 확인 표시가 있으면 다시 확인하는 빈도를 설정할 수도 있습니다. 특정 열이 자주 변경되지 않는 경우 재검사를 덜 자주 선택하면 됩니다 [업데이트 주기 최적화](../../best-practices/reduce-update-cycle-time.md).

빈도 옵션은 다음과 같습니다.

* `always` - 모든 업데이트 중에 다시 확인
* `daily` - 재확인은 선언된 시간대에 대해 자정 이후 첫 번째 업데이트로 수행됩니다.
* `weekly` - 재확인은 매주 9시(금요일) 기준으로 선언된 시간대에 대해 업데이트됩니다.
* `monthly` - 재확인 4주마다 금요일 오후 9시 이후에 선언된 시간대에 대해 업데이트됩니다.
* `once` - 다음 업데이트(일회성 새로 고침)에서만 발생합니다.

업데이트 시간은 동기화할 데이터의 양과 상관 관계가 있으므로 Adobe은 를 선택하는 것을 권장합니다. `daily`, `weekly`, 또는 `monthly` 모든 업데이트 대신 다시 확인합니다.

## 재확인 빈도 관리 {#manage}

테이블 이름을 클릭한 다음 개별 열을 선택하여 Data Warehouse에서 빈도를 다시 확인할 수 있습니다. 동기화 상태 및 재확인 빈도( **변경 내용?** 열)은 테이블의 각 열에 대해 표시됩니다.

재확인 빈도를 변경하려면 변경할 열 옆에 있는 확인란을 클릭합니다. 그런 다음 **[!UICONTROL Set Recheck Frequency]** 드롭다운을 클릭하고 원하는 빈도를 설정합니다.

![](../../assets/dwm-recheck.png)

가끔 볼 수 있습니다 `Paused` 다음에서 `Changes?` 열. 이 값은 테이블이 [복제 방법](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 이(가) (으)로 설정됨 `Paused`.

Adobe은 이러한 열을 검토하여 업데이트를 최적화하고 변경 가능한 열을 다시 확인하는 것이 좋습니다. Adobe 데이터가 변경되는 빈도를 고려할 때 열에 대한 재확인 빈도가 높은 경우 업데이트를 최적화하기 위해 열을 줄이는 것이 좋습니다.

질문이 있거나 현재 복제 방법 또는 재검사에 대해 문의하려면 당사에 문의하십시오.

**관련 항목:**

* [업데이트 시간 단축](../../best-practices/reduce-update-cycle-time.md)
* [분석을 위해 데이터베이스 최적화](../../best-practices/opt-db-analysis.md)
