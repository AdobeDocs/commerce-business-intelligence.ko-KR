---
title: 데이터 검사 구성
description: 변경할 수 있는 값으로 데이터 열을 구성하는 방법을 알아봅니다.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# 데이터 검사 구성

데이터베이스 테이블에는 변경할 수 있는 값이 있는 데이터 열이 있을 수 있습니다. 예를 들어 `orders`) 테이블 위에 `status`. 처음에 데이터베이스에 주문을 쓰는 경우 상태 열에는 값이 포함될 수 있습니다 _보류 중_. 그러면 이 순서가 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) 이 `pending` 값.

주문 상태는 변경될 수 있지만 항상 `pending` 상태. 결국 `complete` 또는 `cancelled`. Data Warehouse이 이 변경 사항을 동기화하려면 열에 새 값이 있는지 다시 확인해야 합니다.

이 기능이 [복제 방법](../data-warehouse-mgr/cfg-replication-methods.md) 우리가 얘기했어? 재확인 처리는 선택한 복제 방법에 따라 달라집니다. 다음 `Modified\_At` 재검사를 구성할 필요가 없으므로 복제 방법은 값 변경 처리를 위해 가장 적합한 방법입니다. 다음 `Auto-Incrementing Primary Key` 및 `Primary Key Batch Monitoring` 메서드를 사용하려면 구성을 다시 확인해야 합니다.

이러한 방법 중 하나를 사용할 때 변경할 수 있는 열에 재확인을 위해 플래그를 지정해야 합니다. 다음 세 가지 방법으로 데이터를 수집할 수 있습니다.

* 업데이트의 일부로 실행되는 감사 프로세스는 다시 검사할 열에 플래그를 지정합니다.

   >[!NOTE]
   >
   >auditor는 샘플링 프로세스를 사용하므로 변경 열이 즉시 잡히지 않을 수 있습니다.

* Data Warehouse 관리자에서 열 옆에 있는 확인란을 선택하고 을 클릭하여 직접 설정할 수 있습니다 **[!UICONTROL Set Recheck Frequency]**&#x200B;및 변경을 확인해야 하는 시기에 적절한 시간 간격을 선택합니다.
* 의 구성원 [!DNL MBI] Data Warehouse 팀이 Data Warehouse에서 다시 체크 인할 열을 수동으로 표시할 수 있습니다. 변경할 수 있는 열이 있는 경우 팀에 문의하여 재검사가 설정되도록 요청하십시오. 요청과 함께 열 목록을 빈도와 함께 포함하십시오.

## 빈도 다시 확인 {#frequency}

**알고 있었어?**
재확인 설정 `primary key` 열은 변경된 값에 대해 열을 확인하지 않습니다. 테이블이 삭제된 행에 대해 확인되고 모든 삭제 내용이 Data Warehouse에서 삭제됩니다.

열에 재확인을 위해 플래그가 지정되면 재확인 빈도를 설정할 수도 있습니다. 특정 열이 덜 자주 변경되는 경우 덜 자주 재검사할 수 있습니다 [업데이트 주기 최적화](../../best-practices/reduce-update-cycle-time.md).

빈도 옵션은 다음과 같습니다.

* `always` - 업데이트 때마다 다시 확인
* `daily` - 재확인은 선언된 시간대에 대해 자정 이후에 업데이트되는 첫 번째 작업입니다
* `weekly` - 재점검은 예약된 시간대의 금요일 오후 9시 이후에 수행됩니다.
* `monthly` - 재점검은 금요일 오후 9시 이후에 선언된 시간대에 대해 4주마다 업데이트됨
* `once` - 다음 업데이트에서만 발생합니다(일회성 새로 고침).

업데이트 시간은 동기화해야 하는 데이터 수와 상관관계가 있으므로 `daily`, `weekly`, 또는 `monthly` 모든 업데이트 대신 다시 확인합니다.

## 재확인 빈도 관리 {#manage}

테이블 이름을 클릭한 다음 개별 열을 확인하여 Data Warehouse에서 주파수를 관리할 수 있습니다. 동기화 상태 및 재확인 빈도(예: **변경 사항?** 열)은 테이블의 각 열에 대해 표시됩니다.

재확인 빈도를 변경하려면 변경할 열 옆의 확인란을 클릭한 다음 **[!UICONTROL Set Recheck Frequency]** 드롭다운을 클릭하고 원하는 빈도를 설정합니다.

![](../../assets/dwm-recheck.png)

가끔 `Paused` 에서 `Changes?` 열. 이 값은 테이블의 [복제 방법](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 가 로 설정되어 있습니다. `Paused`.

이러한 열을 검토하여 업데이트를 최적화하고 변경 가능한 열이 다시 확인되도록 하는 것이 좋습니다. 데이터가 변경되는 빈도를 고려하여 열에 대한 재확인 빈도가 불필요하게 높은 경우 업데이트를 최적화하기 위해 빈도를 줄이는 것이 좋습니다.

문의 사항이 있거나 현재 복제 방법 또는 재검사에 대해 문의하시기 바랍니다.

**관련:**

* [업데이트 시간 단축](../../best-practices/reduce-update-cycle-time.md)
* [분석을 위한 데이터베이스 최적화](../../best-practices/opt-db-analysis.md)
