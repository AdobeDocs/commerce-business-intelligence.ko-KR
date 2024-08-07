---
title: 대시보드 그룹 사용
description: 대시보드를 더 잘 구성할 수 있도록 하는 방법을 알아봅니다.
exl-id: e48b7345-62d0-4898-997e-3c3c02040ad3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 대시보드 그룹 사용

대시보드 그룹을 사용하면 대시보드를 더 잘 구성할 수 있습니다. 가장 일반적인 사용 사례는 유사한 대시보드를 동일한 &quot;그룹&quot;에 그룹화하는 것입니다. 예를 들어 마케팅과 관련된 모든 대시보드를 대시보드 그룹 &quot;마케팅&quot; 아래에 그룹화할 수 있습니다.

대시보드 선택 드롭다운에서 대시보드 그룹은 알파벳 순서로 표시되며, &quot;그룹 없음&quot; 아래의 모든 대시보드는 마지막으로 표시됩니다. 동일한 그룹 아래의 대시보드는 각 그룹 내에서 사전순으로 함께 표시됩니다.

## 대시보드 그룹 공유

대시보드 그룹은 사용자 간에 직접 공유할 수 없습니다. 대시보드가 사용자와 공유되면 대시보드 그룹이 없는 경우 해당 사용자에 대해 해당 대시보드 그룹이 자동으로 생성됩니다. 대시보드 그룹이 있으면 대시보드가 목록에 추가됩니다.

소유자가 대시보드의 그룹을 변경하면 대시보드가 공유된 모든 사용자에 대해 변경 사항이 자동으로 반영됩니다. 사용자가 소유하지 않은 대시보드에 대한 대시보드 그룹을 변경할 수 없습니다.

## 대시보드 그룹 만들기

다음 두 가지 방법 중 하나로 대시보드 그룹을 만들 수 있습니다.

1. 대시보드를 만들 때:

   ![대시보드 그룹 만들기](../../assets/create-dashboard-groups-new-dashboard.png)

1. 기존 대시보드의 그룹을 변경할 때 `Manage Data > Dashboards` 페이지에서 다음 작업을 수행합니다.

   1. 그룹을 생성할 대시보드를 클릭합니다.

   1. `Dashboard Group (optional)` 아래에 현재 대시보드 그룹이 나타납니다.

   1. 그룹을 만들려면 새 그룹의 이름을 입력한 다음 상자 바깥쪽을 클릭합니다.

      ![대시보드 그룹 만들기](../../assets/create-dashboard-groups-existing-dashboard.png)

## 기존 그룹에 기존 대시보드 추가

1. `Manage Data > Dashboards` 페이지에서 그룹을 변경할 대시보드를 선택하십시오.

1. `Dashboard Group (optional)` 아래의 텍스트는 대시보드의 현재 대시보드 그룹을 표시합니다.

1. 대시보드의 그룹을 변경하려면 목록에서 다른 그룹을 선택하십시오(이 경우 `PS`, `Campaigns`).

   ![그룹 대시보드 변경](../../assets/add-existing-dashboard-existing-group.png)

## 대시보드 그룹 삭제

대시보드 그룹 아래에 대시보드가 없으면 자동으로 삭제됩니다.
