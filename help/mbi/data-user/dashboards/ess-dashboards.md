---
title: 대시보드
description: 대시보드를 만들고 작업하는 방법을 알아봅니다.
exl-id: a872344b-ac66-41eb-a471-5a69f8802527
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# 대시보드

[!DNL Adobe Commerce Intelligence] 대시보드를 통해 스토어의 성능과 영업 활동을 한 눈에 볼 수 있습니다. 개별 대시보드를 다른 사용자와 공유하고 논리 그룹으로 구성할 수 있습니다. 다른 사용자에 대해 서로 다른 수준의 권한을 설정할 수도 있습니다.

보고서를 만들고 대시보드에 추가한 다음 데이터를 Excel로 내보내기가 쉽습니다. 차트와 보고서의 크기를 조정하고 대시보드의 위치로 드래그할 수 있습니다.

![대시보드](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 대시보드 만들기 {#createdash}

대시보드는 Report Builder에서 만드는 분석에 대해 공유할 수 있는 테마 버킷입니다. 이렇게 하면 팀이 조직 전체에 걸쳐 단일 소스로 공동 작업하고 유지하도록 권장할 수 있습니다.

*관리자 또는 표준 사용자인 경우*&#x200B;를 클릭하고 대시보드를 만들 수 있습니다. `Dashboard Options` 드롭다운 및 선택 `Create New dashboard`.

사용자가 만드는 대시보드의 모습은 전적으로 사용자의 책임입니다. 필요에 따라 원하는 대로 대시보드에서 요소를 정렬하고 크기를 조정할 수 있습니다.

![대시보드 요소 크기 조정](../../assets/arrange_resize_dashboard_element.gif)

### 대시보드 만들기

1. 메뉴에서 **[!UICONTROL Dashboards]**.

1. 기본 대시보드 이름은 대시보드 헤더의 왼쪽 위 모서리에 나타납니다. 아래쪽 화살표(![](../../assets/magento-bi-btn-down.png)사용 가능한 옵션을 표시합니다.

   ![대시보드 만들기](../../assets/magento-bi-dashboard-create.png)

1. 클릭 **[!UICONTROL Create Dashboard]**. 그런 다음 다음을 수행합니다.

   * 입력 `Name` 대시보드에 사용됩니다.

   * 을(를) 만들려면 `Group` 대시보드에 대해 그룹 이름을 입력합니다.

      예를 들어 Commerce 설치에 여러 스토어 보기가 있는 경우 각 스토어 보기에 대한 그룹을 만들 수 있습니다.

   * 클릭 **[!UICONTROL Create]**.

   ![대시보드 이름](../../assets/magento-bi-dashboard-create-name.png)

   * 새 대시보드의 이름이 왼쪽 위 모서리에 나타납니다. 아래쪽 화살표(![](../../assets/magento-bi-btn-down.png))을 클릭하여 옵션을 표시합니다. 그룹을 만든 경우 새 대시보드가 목록의 그룹 아래에 나타납니다.


### 보고서 추가

1. 보고서를 추가하려면 다음 중 하나를 수행하십시오.

   * 다음을 클릭합니다. **[!UICONTROL Add a report]** 를 페이지의 프롬프트에 표시합니다.

   * 대시보드 헤더에서 을 클릭합니다. **[!UICONTROL Add Report]**.

      ![보고서 추가](../../assets/magento-bi-dashboard-create-add-report.png)

1. 클릭 **[!UICONTROL Create Report]** 표시 방법 **[!UICONTROL Report Builder Options]**.

   ![Report Builder 옵션](../../assets/magento-bi-report-builder.png)

## 대시보드에서 항목 정렬

* 차트 또는 보고서의 크기를 조정하려면 오른쪽 아래 모서리를 새 크기로 끕니다.

* 차트나 보고서를 이동하려면 커서가 십자형으로 변경될 때까지 제목이나 머리글 위로 마우스를 가져갑니다. 그런 다음 위치로 드래그합니다.

## 대시보드 관리 {#managedash}

위치 **[!DNL Manage Data** > **Dashboards]**, 소유한 대시보드에 대한 사용자 권한을 관리하고, 더 이상 필요하지 않은 대시보드를 삭제하고, 기본 대시보드를 설정할 수 있습니다.

### 대시보드 공유 {#sharingdash}

정확하게 크기 조정 [!DNL Commerce Intelligence] 조직 전체에서 중요한 통찰력을 제공하고, Adobe은 사용자가 만든 대시보드를 다른 팀 구성원과 공유할 수 있도록 권장합니다. *소유한 대시보드를 공유할 수 있습니다.* 을(를) 클릭하여 `Share Dashboard` 페이지 맨 위에 있는 옵션입니다.

대시보드를 공유할 때 조직 전체 또는 개별적으로 권한을 할당할 수 있습니다. 즉, 보고서를 보고 편집할 수 있는 사용자를 결정할 수 있습니다.

>[!NOTE]
>
>`Read-Only` 사용자는 직접 공유되는 대시보드에만 액세스할 수 있으며, 대시보드를 직접 검색하고 추가할 수는 없습니다. 그들을 순환에 유지하는 것을 잊지 마세요!

### 공유 대시보드 액세스 {#accessshared}

*관리자 또는 표준 사용자인 경우* 공유 대시보드를 계정에 추가하려면 다음을 클릭합니다. **[!UICONTROL Dashboard Options]** 을 클릭한 다음 **[!UICONTROL Find]** 드롭다운에서 을 클릭합니다.

![대시보드 찾기](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### 대시보드 설정 관리

1. 메뉴에서 **[!DNL Manage Data** > **Dashboards]**.

1. 해당하는 경우 새 이름을 입력합니다. `Dashboard Name`.

1. 대시보드를 특정 대상에 지정하려면 `Dashboard Group`그룹 목록에서 을 선택합니다.

   **`Permissions`**

   모든 사용자에게 대시보드에 대한 동일한 액세스 수준을 부여하려면 다음을 수행하십시오.

   1. 아래 **`Shared with`**, 다음 옵션 중 하나를 선택합니다.

      * `View`
      * `Edit`
      * `None`
   1. 확인을 묻는 메시지가 나타나면 **[!UICONTROL OK]** 을 클릭하여 각 사용자의 권한 수준을 업데이트합니다.

   1. 개인의 권한 수준을 변경하려면 목록에서 사용자를 찾아 권한 수준을 변경합니다. 변경 사항이 자동으로 저장됩니다.

   **`Default`**

   1. 이 대시보드를 의 기본값으로 설정하려면 [!DNL Commerce Intelligence] 계정, 클릭 **[!UICONTROL Make Default]**.

   **`Remove`**

   1. 대시보드를 제거하려면 **[!UICONTROL Delete Dashboard]**.
