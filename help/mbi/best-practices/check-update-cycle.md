---
title: 갱신 주기 상태 확인
description: 업데이트 주기 상태를 확인하는 방법을 알아봅니다.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# 주기 진행 업데이트

에 로그인할 때 [!DNL MBI] 대시보드 를 사용하면 마지막 업데이트 주기의 상태를 확인하는 여러 가지 방법이 있습니다. 모든 것은 [사용자 권한](../administrator/user-management/user-management.md) 당신은 가지고 있습니다.

## 업데이트 주기 상태를 확인해야 하는 이유는 무엇입니까?

상태 업데이트 주기를 확인하는 것은 [!DNL MBI] 계정이 필요합니다. 만약 [기대치를 충족하지 못하는 결과](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)예: 의 일별 판매 [!DNL MBI] eCommerce 플랫폼 또는 사용자 [[!DNL Google] 전자 상거래 매출](https://support.magento.com/hc/en-us/articles/360016505232) 마지막 데이터 포인트를 확인하여 업데이트가 완료되면 문제가 해결되는지 확인할 수 있습니다.

## [!UICONTROL Read-Only] 및 [!UICONTROL Standard]** 사용자

`Read-only` 사용자는 대시보드에 로그인하고 페이지 오른쪽 상단의 아이콘을 마우스로 가리키면 데이터가 얼마나 최근에 업데이트되었는지 볼 수 있습니다. 마지막 데이터 포인트를 가져온 시기를 표시합니다.

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] 사용자

`Admin` 사용자는 대시보드에 로그인하고 계정 통합에 대한 간단한 상태 아이콘과 함께 위의 마지막 데이터 포인트를 볼 수 있습니다.

자세한 내용은 관리자가 **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

이 페이지에는 현재 업데이트 상태 및 마지막으로 완료된 업데이트 시간이 표시됩니다.

업데이트가 현재 진행 중인 경우 업데이트가 완료되면 이메일 알림을 요청하는 링크가 표시됩니다.

업데이트가 진행 중이 아니면 업데이트를 시작하도록 강제하는 링크가 표시됩니다.

>[!NOTE]
>
>일시 중단 시간이 있는 경우(원하지 않는 시간) [!DNL MBI] (데이터 업데이트)를 설정하면 업데이트를 강제 수행하면 해당 일시 중단 시간의 제한 사항을 고려하지 않는 업데이트 주기가 시작됩니다.
