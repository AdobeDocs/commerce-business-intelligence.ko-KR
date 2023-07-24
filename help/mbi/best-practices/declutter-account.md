---
title: 내 콘텐츠 제거 [!DNL Commerce Intelligence] 계정
description: 다음을 정리하는 방법 알아보기 [!DNL Commerce Intelligence] 계정입니다.
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# 정리 [!DNL Adobe Commerce Intelligence] 계정

다음을 수행했는지 여부 [!DNL Commerce Intelligence] 6개월 또는 6년 동안 깔끔한 계정을 유지하는 것은 조직이 플랫폼을 최대한 활용하는 데 가장 중요합니다. 시간이 지남에 따라 더 이상 필요하지 않은 사용자, 대시보드, 보고서, 지표 및 열이 있는 것이 당연합니다. 일회용으로 보고서를 만들어 놓고 잊어버렸거나 회사에서 나간 사용자가 계정을 비활성화한 적이 없을 수 있습니다.

포함 [모든 요소에 대해 표준화되고 명확한 이름 지정](../best-practices/naming-elements.md)의 ) [!DNL Commerce Intelligence] 계정, 아래 계정 감사 단계는 사용자의 어수선하고 불필요한 분석을 줄이는 데 도움이 됩니다. 한 가지 추가 이점은 다음과 같습니다 [잠재적으로 더 빠른 업데이트 주기](../best-practices/reduce-update-cycle-time.md).

## 1단계: 비활성 사용자 식별

계정을 정리하는 첫 번째 단계는 회사를 떠났거나 더 이상 사용하지 않는 사람과 같은 비활성 사용자의 계정을 비활성화하는 것입니다 [!DNL Commerce Intelligence] 현재 역할로 전환됩니다.

이렇게 하려면 오른쪽 상단의 탐색 모음에서 회사 이름을 클릭한 다음 을 선택합니다. **[!UICONTROL Manage Users]**. 그런 다음 비활성화할 사용자를 선택하고 **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>필요 사항 [관리자 권한](../administrator/user-management/user-management.md) 이렇게 하려면.

>[!WARNING]
>
>사용자를 비활성화하면 해당 사용자가 만든 차트, 대시보드 및 기타 자산이 제거됩니다. 이러한 에셋을 유지하려면 [!DNL Commerce Intelligence] [지원](../guide-overview.md#Submitting-a-Support-Ticket) 팀을 만든 후 사용자를 비활성화하십시오. 지원을 통해 이러한 에셋을 다른 사용자에게 전송할 수 있습니다.

### 사용자 다시 활성화

사용자를 다시 활성화하려면 비활성화된 이메일 주소와 동일한 계정을 다시 만들어 사용자를 다시 초대하고, 로그인 시 사용자의 액세스 및 소유한 데이터가 복원됩니다.

## 2단계: 사용하지 않는 대시보드 및 보고서 삭제

계정 감사의 다음 단계는 사용하지 않는 대시보드 및 보고서를 삭제하는 것입니다.

>[!NOTE]
>
>필요 사항 `Admin` 또는 `Standard` [사용자 권한](../administrator/user-management/user-management.md) 이렇게 하려면.

이 있는 모든 사용자 `Admin` 또는 `Standard` 액세스 권한은 보고서와 대시보드를 만들 수 있습니다. 이러한 이유로 이러한 권한이 있는 모든 사용자는 아래 단계에 따라 사용하지 않는 보고서를 식별하고 제거해야 합니다.

### 대시보드 및 보고서 검토

삭제하기 전에 보고서와 대시보드를 검토하여 사용 중인 항목을 평가해야 합니다. 사용할 수 있는 동안 **[!UICONTROL find unused reports]** 아래에 설명된 기능을 사용하면 초기 검토를 통해 정리 작업의 생산성을 높일 수 있습니다.

### 대시보드 및 보고서 삭제

대시보드 및 보고서에 액세스한 후 계정 정리를 시작할 수 있습니다.

**대시보드에서 보고서 제거하기**

1. 대시보드에서 제거할 보고서를 찾습니다.
1. 선택 **[!UICONTROL Options]** 을 클릭합니다.
1. 클릭 **[!UICONTROL Remove From Dashboard]**.

**전체 대시보드 삭제하기**

1. 선택 **[!UICONTROL Manage Data]**, 그런 다음 **[!UICONTROL Dashboards**].
1. 삭제할 대시보드에서 를 클릭합니다.
1. 클릭 **[!UICONTROL Delete Dashboard]**.

다음을 선택할 수도 있습니다. **[!UICONTROL Dashboard Options]**, 그런 다음 **[!UICONTROL Delete]** 대시보드 자체에서.

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>대시보드를 삭제해도 대시보드 내의 보고서는 삭제되지 않으므로 보고서를 삭제하려면 한 단계를 더 수행해야 합니다.

**사용하지 않는 보고서를 삭제하려면**

1. 선택 **[!UICONTROL Manage Data]**, 그런 다음 **[!UICONTROL Reports]**.
1. 다음 확인: **사용하지 않은 보고서만 표시** 지표 목록 아래에 있는 상자입니다. 이렇게 하면 대시보드 또는 이메일 요약에 사용되지 않는 보고서 목록이 만들어집니다.
1. 삭제할 보고서를 선택합니다. 보고서 목록 위에 있는 확인란을 클릭하여 모두 선택할 수 있습니다.
1. 클릭 **[!UICONTROL Delete Selected]**.

다음은 사용되지 않은 보고서 삭제 프로세스에 대해 설명합니다.

![](../../mbi/assets/unused_reports.png)

## 3단계: 사용하지 않는 지표 삭제

사용자 목록, 대시보드 및 보고서를 정리한 후 지표 목록을 감사하는 단계로 이동할 수 있습니다. 이렇게 하면 새 지표가 다른 정의로 만들어졌거나 사용 중이 아닌 오래된 지표일 수 있는 모든 것을 식별할 수 있습니다.

1. 지표에 대한 종속 보고서 목록을 생성하려면 로 이동합니다. **[!DNL Manage Data]**&#x200B;을 선택한 다음 클릭 을 선택합니다. **[!UICONTROL Metrics]**.
1. 클릭 **[!UICONTROL Edit]** 를 클릭합니다.
1. 페이지 하단에 라는 섹션이 표시됩니다. **[!UICONTROL Dependent Charts]**. 링크를 클릭하여 이 지표에 대한 종속 보고서 목록을 생성합니다.
1. 시스템이 검사를 완료한 후, [!DNL Commerce Intelligence] 이 지표를 사용하는 대시보드, 보고서 및 사용자 목록을 표시합니다.

![](../../mbi/assets/report_dependecies.png)

지표가 더 이상 필요하지 않은 경우 로 다시 이동합니다. **[!UICONTROL Metrics]** 클릭하여 페이지 만들기 **[!UICONTROL Back to Metric List]** 삭제할 지표를 찾습니다. 클릭 **[!UICONTROL Delete]**.

## 4단계: 동기화된 열 평가

마지막 단계는 Data Warehouse에서 현재 동기화 중인 열을 평가하는 것입니다. 열 동기화를 해제하면 계정이 더 이상 사용되지 않을 뿐만 아니라 업데이트 시간도 줄어들 수 있습니다.

이 작업을 진행하려면 다음으로 연락하십시오. [!DNL Commerce Intelligence] [지원](../guide-overview.md#Submitting-a-Support-Ticket). 지원 팀은 SQL 보고서를 제외하고 사용자의 대시보드에서 사용되지 않고 전자 메일 요약에 사용되지 않는 모든 열을 포함하는 보고서를 만들 수 있습니다. 그런 다음 Data Warehouse 관리자를 통해 이 보고서를 동기화 해제할 열을 선택하는 안내서로 사용할 수 있습니다.

>[!NOTE]
>
>나중에 언제든지 이러한 열을 다시 동기화할 수 있습니다. 열의 동기화를 해제하면 Data Warehouse에서 모든 데이터가 제거됩니다. 업데이트 주기 동안 이 열에 새 값이나 업데이트된 값이 선택되어 있지 않다는 의미일 뿐입니다.

**열(또는 열) 동기화 해제**

1. 다음으로 이동 **[!DNL Manage Data]**, 그런 다음 **[!UICONTROL Data Warehouse]**.
1. 다음에서 **[!UICONTROL Synced Tables]** 열을 포함하는 테이블로 이동합니다.
1. 동기화를 해제할 하나 이상의 열 옆에 있는 하나 이상의 상자를 선택합니다.
   >[!NOTE]
   >
   >전체 테이블을 삭제하지 않으면 기본 키 열의 동기화를 해제할 수 없습니다.

1. 클릭 **[!UICONTROL Remove]** 하나 이상의 열의 동기화를 해제합니다.

전체 프로세스를 살펴보겠습니다.

![](../../mbi/assets/drop_column.png)

## 요약

사용자 [!DNL Commerce Intelligence] 이제 계정을 더 깔끔하게 정리하고 팀과 함께 탐색할 수 있습니다.
