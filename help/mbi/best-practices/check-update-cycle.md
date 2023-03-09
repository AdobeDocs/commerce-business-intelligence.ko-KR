---
title: 업데이트 주기 상태 확인
description: 업데이트 주기 상태를 확인하는 방법을 알아봅니다.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# 업데이트 주기 진행률

에 로그인할 때 [!DNL MBI] 대시보드에는 마지막 업데이트 주기의 상태를 확인하는 몇 가지 방법이 있습니다. 모두 다음에 대한 유형에 따라 다릅니다. [사용자 권한](../administrator/user-management/user-management.md) 가지고 계시죠.

## 업데이트 주기 상태를 확인해야 하는 이유는 무엇입니까?

상태 업데이트 주기를 확인하는 것은 의 데이터를 감사할 때 유용합니다. [!DNL MBI] 계정입니다. 다음이 보이면 [기대에 미치지 못하는 결과](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md), (예: 일별 판매) [!DNL MBI] 은(는) 전자 상거래 플랫폼 또는 의 보기와 일치하지 않습니다. [[!DNL Google] 전자 상거래 매출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=en) 업데이트가 완료되면 마지막 데이터 포인트에서 문제가 해결되었는지 확인할 수 있습니다.

## [!UICONTROL Read-Only] 및 [!UICONTROL Standard]** 사용자

`Read-only` 사용자는 대시보드에 로그인한 다음 페이지 오른쪽 상단의 아이콘 위로 마우스를 가져가면 데이터가 얼마나 최근에 업데이트되었는지 확인할 수 있습니다. 마지막 데이터 포인트를 가져온 시간을 보여 줍니다.

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] 사용자

`Admin` 사용자는 대시보드에 로그인하고 계정 통합에 대한 간단한 상태 아이콘과 함께 위의 마지막 데이터 포인트를 볼 수 있습니다.

자세한 내용을 보려면 관리자 사용자는 **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

이 페이지에는 현재 업데이트 상태와 마지막으로 완료된 업데이트 시간이 표시됩니다.

업데이트가 진행 중인 경우 업데이트가 완료되면 이메일 알림을 요청하는 링크가 표시됩니다.

업데이트가 진행 중이 아닌 경우 업데이트를 강제로 시작하는 링크가 표시됩니다.

>[!NOTE]
>
>일시 중단 시간(원하지 않는 시간)이 있는 경우 [!DNL MBI] 데이터 업데이트) 설정을 강제로 업데이트하면 해당 일시 중단 시간의 제한을 준수하지 않는 업데이트 주기가 시작됩니다.
