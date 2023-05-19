---
title: SQL과 Data Warehouse 관리자의 차이점
description: SQL과 Data Warehouse 관리자의 차이점에 대해 알아봅니다.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 차이점 [!DNL SQL] 및 [!DNL Data Warehouse Manager]

에서 만들어진 열 사이에는 두 가지 주요 차이점이 있습니다. [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) 및 를 사용하여 생성된 [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). 하나는 업데이트 주기에 대한 종속이고 다른 하나는 열을 계정에 저장하는 방법입니다.

## 의 열 [!DNL SQL Report Builder]

열은 업데이트 주기에 종속되지 않으므로 열을 반복하기 전에 하나가 완료될 때까지 더 이상 기다릴 필요가 없습니다. 실수를 한 경우 수정하기 위해 몇 번의 키 입력만 수행하면 됩니다. 다시 작업하기 전에 두 번의 업데이트가 완료되기를 더 이상 기다릴 필요가 없습니다.

>[!IMPORTANT]
>
>을 사용하여 만드는 열 [!DNL SQL] 편집기가 Data Warehouse에 저장되지 않았습니다. 항상 열이 포함된 쿼리에 액세스할 수 있지만 둘 이상의 보고서에서 열을 사용하려면 각 보고서에 대한 쿼리에 열을 다시 만들어야 합니다. 즉, 다음을 사용하여 생성된 열이 [!DNL SQL] 기존 버전에서는 편집기를 사용할 수 없습니다. [!DNL Report Builder].

## Data Warehouse 관리자의 열

열은 업데이트 주기에 따라 달라지므로 전체 주기를 완료해야 편집할 수 있습니다. 이러한 열은 Data Warehouse 관리자에 저장되며 기존 열에 사용할 수 있습니다 [!DNL Report Builder] 또는 [!DNL SQL Report Builder].
