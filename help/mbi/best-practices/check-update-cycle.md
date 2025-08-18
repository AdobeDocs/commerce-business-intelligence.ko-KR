---
title: 업데이트 주기 상태 확인
description: 업데이트 주기 상태를 확인하는 방법을 알아봅니다.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# 업데이트 주기 진행률

[!DNL Adobe Commerce Intelligence] 대시보드에 로그인하면 마지막 업데이트 주기 상태를 확인하는 여러 가지 방법이 있습니다. 사용자가 보유한 [사용자 권한](../administrator/user-management/user-management.md)의 유형에 따라 다릅니다.

## 업데이트 주기 상태를 확인해야 하는 이유는 무엇입니까?

상태 업데이트 주기를 확인하는 것은 [!DNL Commerce Intelligence] 계정의 데이터를 감사할 때 유용합니다. [예상과 일치하지 않는 결과](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)가 표시되는 경우(예: [!DNL Commerce Intelligence]의 일일 매출이 전자 상거래 플랫폼 또는 [[!DNL Google] 전자 상거래 매출에 표시되는 내용과 일치하지 않음](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=ko)) 업데이트가 완료되면 마지막 데이터 포인트를 확인하여 문제가 해결되었는지 확인할 수 있습니다.

## [!UICONTROL Read-Only] 및 [!UICONTROL Standard] 사용자

`Read-only`명의 사용자가 대시보드에 로그인한 후 페이지 오른쪽 상단의 아이콘으로 마우스를 가져가면 데이터가 얼마나 최근에 업데이트되었는지 확인할 수 있습니다. 마지막 데이터 포인트를 가져온 시간을 보여 줍니다.

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin]명의 사용자

`Admin`명의 사용자가 대시보드에 로그인하면 계정 통합에 대한 간단한 상태 아이콘과 함께 위의 마지막 데이터 포인트를 볼 수 있습니다.

자세한 내용을 보려면 관리자가 **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**&#x200B;을(를) 클릭할 수 있습니다.

![](../../mbi/assets/detail-manage-data-integrations.png)

이 페이지에는 현재 업데이트 상태와 마지막으로 완료된 업데이트 시간이 표시됩니다.

업데이트가 진행 중인 경우 업데이트가 완료되면 이메일 알림을 요청하는 링크가 표시됩니다.

업데이트가 진행 중이 아닌 경우 업데이트를 강제로 시작하는 링크가 표시됩니다.

>[!NOTE]
>
>일시 중단 시간([!DNL Commerce Intelligence]에서 데이터를 업데이트하지 않으려는 시간)이 설정된 경우 강제로 업데이트를 수행하면 해당 일시 중단 시간의 제한을 고려하지 않는 업데이트 주기가 시작됩니다.
