---
title: 대시보드
description: 대시보드를 만들고 사용하는 방법을 알아봅니다.
exl-id: a872344b-ac66-41eb-a471-5a69f8802527
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# 대시보드

[!DNL MBI] 대시보드는 저장소의 성능 및 판매 활동을 한눈에 파악할 수 있도록 해줍니다. 개별 대시보드는 다른 사용자와 공유되고 논리 그룹으로 구성할 수 있습니다. 다른 사용자에 대해 다른 수준의 권한을 설정할 수도 있습니다.

새 보고서를 만들고, 대시보드에 추가하고, 데이터를 Excel로 내보내는 것은 쉽습니다. 차트 및 보고서의 크기를 조정하고 대시보드에서 위치를 지정할 수 있습니다.

![대시보드](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 대시보드 만들기 {#createdash}

대시보드는 기본적으로 Report Builder에서 생성한 분석을 위한 테마 버킷입니다. 다음은 팀이 조직 전체에서 하나의 정확한 소스를 공동 관리하고 유지할 수 있도록 유도하는 방법입니다.

*관리자 또는 표준 사용자인 경우*&#x200B;을 클릭하고 `Dashboard Options` 드롭다운 및 선택 `Create New dashboard`.

사용자가 만드는 대시보드의 모습은 전적으로 사용자에 따라 다릅니다. 요구 사항과 워크플로우에 맞게 대시보드에서 요소를 구성하고 크기를 조정할 수 있습니다.

![대시보드 요소 크기 조정](../../assets/arrange_resize_dashboard_element.gif)

### 새 대시보드 만들기

1. 메뉴에서 **[!UICONTROL Dashboards]**.

1. 대시보드 헤더의 왼쪽 위 모서리에 기본 대시보드의 이름이 나타납니다. 아래쪽 화살표(![](../../assets/magento-bi-btn-down.png)) 사용 가능한 옵션을 표시합니다.

   ![대시보드 만들기](../../assets/magento-bi-dashboard-create.png)

1. 클릭 **[!UICONTROL Create Dashboard]**. 그런 다음 다음을 수행합니다.

   * 을(를) 입력합니다. `Name` 참조하십시오.

   * 새 `Group` 대시보드에 그룹 이름을 입력합니다.

      예를 들어 상거래 설치에 여러 저장소 보기가 있는 경우 각 저장소 보기에 대한 그룹을 만들 수 있습니다.

   * 클릭 **[!UICONTROL Create]**.

   ![대시보드 이름](../../assets/magento-bi-dashboard-create-name.png)

   * 새 대시보드의 이름이 왼쪽 위 모서리에 나타납니다. 아래쪽 화살표(![](../../assets/magento-bi-btn-down.png)) 옵션을 표시합니다. 그룹을 생성한 경우, 목록에 있는 그룹 아래에 새 대시보드가 나타납니다.


### 보고서 추가

1. 보고서를 추가하려면 다음 중 하나를 수행합니다.

   * 을(를) 클릭합니다. **[!UICONTROL Add a report]** 페이지에서 메시지를 표시합니다.

   * 대시보드 헤더에서 **[!UICONTROL Add Report]**.

      ![보고서 추가](../../assets/magento-bi-dashboard-create-add-report.png)

1. 클릭 **[!UICONTROL Create Report]** 다음을 표시합니다. **[!UICONTROL Report Builder Options]**.

   ![Report Builder 옵션](../../assets/magento-bi-report-builder.png)

## 대시보드에서 항목 정렬

* 차트나 보고서의 크기를 조정하려면 오른쪽 아래 모서리를 새 크기로 드래그합니다.

* 차트나 보고서를 이동하려면 커서가 십자 모양으로 변경될 때까지 제목 또는 헤더 위로 마우스를 가져갑니다. 그런 다음 해당 위치를 드래그합니다.

## 대시보드 관리 {#managedash}

in **[!DNL Manage Data** > **Dashboards]**, 보유한 대시보드에 대한 사용자 권한을 관리하고, 더 이상 필요하지 않은 대시보드를 삭제하고, 기본 대시보드를 설정할 수 있습니다.

### 대시보드 공유 {#sharingdash}

실제 확장 [!DNL MBI] 조직 전체에서 중요한 인사이트를 제공하고 다른 팀 구성원과 함께 만든 대시보드를 공유하는 것이 좋습니다. *자신이 소유한 대시보드를 공유할 수 있습니다* 다음을 클릭하여 `Share Dashboard` 옵션 을 클릭합니다.

대시보드를 공유할 때 조직 전체에 대한 권한을 지정하거나 개별 기준으로 할 수 있습니다. 즉, 보고서를 보고 편집할 수 있는 사람을 결정할 수 있습니다.

>[!NOTE]
>
>`Read-Only` 사용자는 자신과 직접 공유되는 대시보드에만 액세스할 수 있습니다. 사용자는 자체적으로 대시보드를 검색하고 추가할 수 없습니다. 잊지 말고 계속하세요!

### 공유 대시보드 액세스 {#accessshared}

*관리자 또는 표준 사용자인 경우* 공유 대시보드를 계정에 추가하려면 을(를) 클릭하여 추가할 수 있습니다 **[!UICONTROL Dashboard Options]** 을 클릭한 다음 **[!UICONTROL Find]** 아래에 표시됩니다.

![대시보드 찾기](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### 대시보드 설정 관리

1. 메뉴에서 **[!DNL Manage Data** > **Dashboards]**.

1. 해당되는 경우 신규 `Dashboard Name`.

1. 대시보드를 특정 페이지에 지정하려면 `Dashboard Group`그룹 목록에서 을(를) 선택합니다.

   **`Permissions`**

   모든 사용자에게 동일한 수준의 대시보드에 대한 액세스 권한을 제공하려면 다음을 수행하십시오.

   1. 아래 **`Shared with`**&#x200B;다음 옵션 중 하나를 선택합니다.

      * `View`
      * `Edit`
      * `None`
   1. 확인 메시지가 표시되면 을 클릭합니다 **[!UICONTROL OK]** 각 사용자의 권한 수준을 업데이트하려면

   1. 개인의 권한 수준을 변경하려면 목록에서 사용자를 찾아서 권한 수준을 변경합니다. 변경 사항이 자동으로 저장됩니다.

   **`Default`**

   1. 이 대시보드를 [!DNL MBI] 계정, **[!UICONTROL Make Default]**.

   **`Remove`**

   1. 대시보드를 제거하려면 **[!UICONTROL Delete Dashboard]**.
