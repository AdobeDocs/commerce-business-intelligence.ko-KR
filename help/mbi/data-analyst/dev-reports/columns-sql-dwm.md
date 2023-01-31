---
title: SQL과 Data Warehouse 관리자 간의 차이점
description: SQL과 Data Warehouse 관리자 간의 차이점을 알아봅니다.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# SQL과 Data Warehouse 관리자 간의 차이점

에서 만들어진 열에는 두 가지 주요 차이가 있습니다 [SQL Report Builder](../dev-reports/sql-rpt-bldr.md) 그리고 [Data Warehouse 관리자](../data-warehouse-mgr/creating-calculated-columns.md): 하나는 업데이트 주기에 대한 종속이고 다른 하나는 계정에 열이 저장되는 방식입니다.

## 의 열 `SQL Report Builder`

열은 업데이트 주기에 종속되지 않으므로 열을 반복하기 전에 열이 완료될 때까지 더 이상 기다릴 필요가 없습니다. 실수를 하면 몇 번의 키 입력만으로 이를 수정할 수 있습니다. 두 개의 업데이트가 중지될 때까지 더 이상 기다릴 필요가 없습니다.

>[!IMPORTANT]
>
>SQL 편집기를 사용하여 만든 열은 Data Warehouse에 저장되지 않습니다. 열은 항상 포함하는 쿼리에 액세스할 수 있지만 둘 이상의 보고서에서 열을 사용하려면 각 보고서에 대한 쿼리에서 다시 만들어야 합니다. 즉, SQL 편집기를 사용하여 만든 열은 기존의 `Report Builder`.

## Data Warehouse 관리자의 열

열은 업데이트 주기에 따라 달라지므로 전체 주기를 완료해야 열을 편집할 수 있습니다. 이러한 열은 Data Warehouse 관리자에 저장되며, 다음과 같이 기존 `Report Builder` 또는 `SQL Report Builder`.
