---
title: 다른 사용자와 대시보드 공유
description: 다른 사용자와 대시보드를 공유하는 방법을 알아봅니다.
exl-id: 6279b049-d1b2-4d40-b30b-ee8772e990f4
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/19tCk4327YLMnSrgQ0xHBinwiK2XHd7QU6l5rO-B6-k
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 269
ht-degree: 0%

---

# 다른 사용자와 대시보드 공유

대시보드 공유는 팀이 계속 진행할 수 있도록 하고 공동 토론을 유도할 수 있는 좋은 방법입니다. 중앙 대시보드를 만들고 공유하면 제어를 유지하면서 팀에 필요한 정보를 제공할 수 있습니다. [[!DNL Adobe] 권장](../../best-practices/share-dashboard-best-practice.md){: target="_blank"}은(는) 우연한 변경을 최소화하기 위해 선택한 몇 개에 `Edit` 권한을 부여할 것을 권장합니다.

>[!NOTE]
>
>공유 중인 대시보드에 특정 사용자가 액세스할 수 없는 지표로 만들어진 보고서가 포함되어 있으면 보고서에 `Error Loading Data` 메시지가 표시됩니다. 데이터를 특정 사용자에게 표시하려면 [관리자 사용자](../../administrator/user-management/user-management.md)가 해당 보고서에 사용된 모든 지표에 대한 액세스 권한을 부여해야 합니다.

## 대시보드 공유

1. 화면 상단의 **[!UICONTROL Share Dashboard]**&#x200B;을(를) 클릭합니다.

   [!DNL Commerce Intelligence] 계정의 모든 사용자 목록이 표시됩니다.

1. 대시보드를 공유할 사용자를 선택하려면 이름 왼쪽에 있는 상자를 선택합니다.

   모든 사용자를 선택/선택 해제하려면 **[!UICONTROL Select]**&#x200B;을(를) 클릭하고 각각 `Everyone` 또는 `None`을(를) 선택합니다.

1. 권한은 사용자별로 또는 일괄적으로 설정할 수 있습니다.

   *개별 사용 권한을 설정하려면* 사용자 이름 오른쪽에 있는 **[!UICONTROL None]**&#x200B;을(를) 클릭하십시오. 이 드롭다운에서 사용자가 보유해야 하는 권한 유형을 선택합니다.

   *사용 권한을 일괄적으로 설정하려면* **[!UICONTROL Set Permissions]**&#x200B;을(를) 클릭하십시오. 이 드롭다운에서 선택한 사용자에게 부여할 권한 유형을 선택합니다.

   >[!NOTE]
   >
   >이 기능을 사용하여 이전에 설정한 권한을 업데이트할 수도 있습니다. 예를 들어, 다른 사용자와의 대시보드 공유를 중지하려면 해당 권한을 `None`(으)로 설정하십시오.

1. 대시보드를 공유하려면 **[!UICONTROL Save Changes]**&#x200B;을(를) 클릭합니다. 선택한 사용자는 대시보드를 볼 수 있도록 초대하는 이메일을 받게 됩니다.

예:

![대시보드 공유](../../assets/Share_Dashboards.gif)
