---
title: 지표 액세스 제한
description: 지표 액세스 및 제한 사항으로 작업하는 방법을 알아봅니다.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 지표 사용자 관리

사용자 권한 수준을 설정하는 것 외에도 사용자별로 지표에 대한 액세스를 제한할 수 있습니다. 예를 들어, 회계 부서에서 매출 관련 지표에 액세스할 수 있지만 사용자 확보 지표는 액세스할 수 없도록 하려면 해당 지표에 대한 액세스를 제한할 수 있습니다.

이와 같은 경우 Adobe은 해당 사용자의 계정을 로 설정할 것을 권장합니다 **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** 지표, 계산된 열, 통합 또는 사용자를 만들거나 변경할 필요가 없지만 Data Warehouse의 데이터에 액세스해야 하는 사용자에게 권한을 제공해야 합니다. 데이터에 대한 액세스를 완전히 제한하려면 **[!UICONTROL Read Only]** 대신 권한을 부여합니다.

권한 수준을 설정한 후 지표 를 선택할 수 있습니다. **[!UICONTROL Standard]** 사용자는 다음을 수행하여 액세스할 수 있습니다.

1. 다음으로 이동 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. 원하는 사용자 계정을 선택합니다.
1. 다음 **[!UICONTROL Metrics]** 탭에는 사용 가능한 지표 목록이 표시됩니다. 사용자에게 액세스 권한을 부여할 지표를 확인하고 사용자에게 액세스 권한이 없어야 하는 지표의 선택을 해제합니다.
1. [!DNL Adobe Commerce Intelligence] 변경 사항을 자동으로 저장합니다. 변경이 성공하면, [!DNL Commerce Intelligence] 디스플레이 **[!UICONTROL Saved!]** 을 클릭합니다.

>[!NOTE]
>
>이 있는 모든 사용자 **[!UICONTROL Standard]** 권한은 모든 지표 외에 데이터 내보내기를 통해 Data Warehouse의 모든 데이터에 액세스할 수 있습니다. [!DNL Google Analytics].

지표를 편집하고 지표에 대한 액세스를 제한할 수도 있습니다. **[!UICONTROL Standard]** 에서 사용자 선택 **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** 섹션.

>[!NOTE]
>
>지표를 복제하는 경우 [!DNL Commerce Intelligence] 는 원래 지표에 설정된 사용자 권한을 복사합니다.
