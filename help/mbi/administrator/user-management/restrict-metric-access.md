---
title: 지표 액세스 제한
description: 지표 액세스 및 제한 사항으로 작업하는 방법을 알아봅니다.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 지표 사용자 관리

사용자 권한 수준을 설정할 수 있을 뿐만 아니라 사용자별로 지표에 대한 액세스를 제한할 수도 있습니다. 예를 들어, 회계 부서가 매출 관련 지표에 액세스하지만 사용자 확보 지표는 액세스하도록 하려는 경우 해당 지표에 대한 액세스를 제한할 수 있습니다.

이러한 경우 사용자의 계정을 **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** 지표, 계산된 열, 통합 또는 사용자를 만들거나 변경할 필요가 없지만 Data Warehouse의 데이터에 액세스할 필요가 있는 사용자에게 권한을 부여해야 합니다. 데이터에 대한 액세스를 완전히 제한하려면 **[!UICONTROL Read Only]** 대신 사용 권한을 부여합니다.

권한 수준을 설정한 후에는 지표를 **[!UICONTROL Standard]** 사용자는 다음을 수행하여 액세스할 수 있습니다.

1. 이동 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. 원하는 사용자 계정을 선택합니다.
1. 다음 **[!UICONTROL Metrics]** 탭에는 사용 가능한 지표 목록이 표시됩니다. 사용자가 액세스할 지표를 확인합니다. 사용자가 액세스할 수 없도록 하려면 이 옵션을 선택 취소합니다.
1. [!DNL MBI] 변경 내용을 자동으로 저장합니다. 변경이 성공하면 [!DNL MBI] 디스플레이 **[!UICONTROL Saved!]** 를 클릭합니다.

>[!NOTE]
>
>다음을 사용하는 모든 사용자 **[!UICONTROL Standard]** 권한은 데이터 내보내기를 통해 데이터 웨어하우스의 모든 데이터에 액세스할 수 있으며 [!DNL Google Analytics].

지표를 편집하여 지표에 대한 액세스를 제한할 수도 있습니다. **[!UICONTROL Standard]** 에서 사용자 선택 **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** 섹션을 참조하십시오.

>[!NOTE]
>
>지표를 복제하는 경우, [!DNL MBI] 원래 지표에 설정된 사용자 권한을 복사합니다.
