---
title: ' [!DNL Commerce Intelligence] 계정 분류 해제'
description: ' [!DNL Commerce Intelligence] 계정을 정리하는 방법을 알아봅니다.'
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
role: Admin, User
feature: Accounts
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# [!DNL Adobe Commerce Intelligence] 계정 정리

[!DNL Commerce Intelligence]에서 6개월이나 6년 동안 활동했는지에 관계없이 정돈된 계정을 유지하는 것은 조직이 플랫폼을 최대한 활용하는 데 무엇보다 중요합니다. 시간이 지남에 따라 더 이상 필요하지 않은 사용자, 대시보드, 보고서, 지표 및 열이 있는 것이 당연합니다. 일회용으로 보고서를 만들어 놓고 잊어버렸거나 회사에서 나간 사용자가 계정을 비활성화한 적이 없을 수 있습니다.

[ 계정의 ](../best-practices/naming-elements.md)모든 요소에 대해 표준화되고 명확한 이름 지정[!DNL Commerce Intelligence])을 사용하면 아래 계정 감사 단계를 통해 사용자의 불필요한 분석과 혼란을 줄일 수 있습니다. 한 가지 추가 이점에는 [잠재적으로 더 빠른 업데이트 주기](../best-practices/reduce-update-cycle-time.md)가 포함됩니다.

## 1단계: 비활성 사용자 식별

계정을 정리하는 첫 번째 단계는 회사를 떠났거나 현재 역할에서 [!DNL Commerce Intelligence]을(를) 더 이상 사용하지 않는 사람과 같이 비활성 사용자의 계정을 비활성화하는 것입니다.

이렇게 하려면 오른쪽 상단의 탐색 모음에서 회사 이름을 클릭한 다음 **[!UICONTROL Manage Users]**&#x200B;을(를) 선택합니다. 그런 다음 비활성화할 사용자를 선택하고 **[!UICONTROL Deactivate User]**&#x200B;을(를) 클릭합니다.

>[!NOTE]
>
>이 작업을 수행하려면 [관리자 권한](../administrator/user-management/user-management.md)이 필요합니다.

>[!WARNING]
>
>사용자를 비활성화하면 해당 사용자가 만든 차트, 대시보드 및 기타 자산이 제거됩니다. 이러한 자산을 유지하려면 사용자를 비활성화하기 전에 [!DNL Commerce Intelligence] [지원](../guide-overview.md#Submitting-a-Support-Ticket) 팀에 문의하세요. 지원을 통해 이러한 에셋을 다른 사용자에게 전송할 수 있습니다.

### 사용자 다시 활성화

사용자를 다시 활성화하려면 비활성화된 이메일 주소와 동일한 계정을 다시 만들어 사용자를 다시 초대하고, 로그인 시 사용자의 액세스 및 소유한 데이터가 복원됩니다.

## 2단계: 사용하지 않는 대시보드 및 보고서 삭제

계정 감사의 다음 단계는 사용하지 않는 대시보드 및 보고서를 삭제하는 것입니다.

>[!NOTE]
>
>이 작업을 수행하려면 `Admin` 또는 `Standard` [사용자 권한](../administrator/user-management/user-management.md)이 필요합니다.

`Admin` 또는 `Standard` 액세스 권한이 있는 모든 사용자는 보고서와 대시보드를 만들 수 있습니다. 이러한 이유로 이러한 권한이 있는 모든 사용자는 아래 단계에 따라 사용하지 않는 보고서를 식별하고 제거해야 합니다.

### 대시보드 및 보고서 검토

삭제하기 전에 보고서와 대시보드를 검토하여 사용 중인 항목을 평가해야 합니다. 아래 설명된 **[!UICONTROL find unused reports]** 기능을 사용할 수 있지만 초기 검토를 통해 정리 작업의 생산성을 높일 수 있습니다.

### 대시보드 및 보고서 삭제

대시보드 및 보고서에 액세스한 후 계정 정리를 시작할 수 있습니다.

**대시보드에서 보고서를 제거하려면**

1. 대시보드에서 제거할 보고서를 찾습니다.
1. 보고서의 오른쪽 상단 모서리에서 **[!UICONTROL Options]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL Remove From Dashboard]**&#x200B;을(를) 클릭합니다.

**전체 대시보드를 삭제하려면**

1. **[!UICONTROL Manage Data]**&#x200B;을(를) 선택한 다음 **[!UICONTROL Dashboards**]을(를) 선택합니다.
1. 삭제할 대시보드에서 를 클릭합니다.
1. **[!UICONTROL Delete Dashboard]**&#x200B;을(를) 클릭합니다.

**[!UICONTROL Dashboard Options]**&#x200B;을(를) 선택한 다음 대시보드 자체에서 **[!UICONTROL Delete]**&#x200B;을(를) 선택할 수도 있습니다.

![대시보드 톱니바퀴 메뉴에서 옵션 삭제](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>대시보드를 삭제해도 대시보드 내의 보고서는 삭제되지 않으므로 보고서를 삭제하려면 한 단계를 더 수행해야 합니다.

**사용하지 않는 보고서를 삭제하려면**

1. **[!UICONTROL Manage Data]**&#x200B;을(를) 선택한 다음 **[!UICONTROL Reports]**&#x200B;을(를) 선택합니다.
1. 지표 목록 아래에 있는 **사용하지 않는 보고서만 표시** 상자를 선택합니다. 이렇게 하면 대시보드 또는 이메일 요약에 사용되지 않는 보고서 목록이 만들어집니다.
1. 삭제할 보고서를 선택합니다. 보고서 목록 위에 있는 확인란을 클릭하여 모두 선택할 수 있습니다.
1. **[!UICONTROL Delete Selected]**&#x200B;을(를) 클릭합니다.

다음은 사용되지 않은 보고서 삭제 프로세스에 대해 설명합니다.

![대시보드에 없는 보고서를 표시하는 사용되지 않은 보고서 목록](../../mbi/assets/unused_reports.png)

## 3단계: 사용하지 않는 지표 삭제

사용자 목록, 대시보드 및 보고서를 정리한 후 지표 목록을 감사하는 단계로 이동할 수 있습니다. 이렇게 하면 새 지표가 다른 정의로 만들어졌거나 사용 중이 아닌 오래된 지표일 수 있는 모든 것을 식별할 수 있습니다.

1. 지표에 대한 종속 보고서 목록을 생성하려면 **[!DNL Manage Data]**(으)로 이동한 다음 **[!UICONTROL Metrics]** 클릭을 선택하십시오.
1. 지표 옆에 있는 **[!UICONTROL Edit]**&#x200B;을(를) 클릭합니다.
1. 페이지 맨 아래에 **[!UICONTROL Dependent Charts]** 섹션이 표시됩니다. 링크를 클릭하여 이 지표에 대한 종속 보고서 목록을 생성합니다.
1. 시스템이 검사를 완료한 후 [!DNL Commerce Intelligence]은(는) 이 지표를 사용하는 대시보드, 보고서 및 사용자 목록을 표시합니다.

![선택한 열을 사용하는 보고서를 표시하는 보고서 종속성 대화 상자](../../mbi/assets/report_dependecies.png)

지표가 더 이상 필요하지 않은 경우 **[!UICONTROL Metrics]**&#x200B;을(를) 클릭하여 **[!UICONTROL Back to Metric List]** 페이지로 돌아가 삭제할 지표를 찾습니다. **[!UICONTROL Delete]**&#x200B;을(를) 클릭합니다.

## 4단계: 동기화된 열 평가

마지막 단계는 Data Warehouse에서 현재 동기화 중인 열을 평가하는 것입니다. 열 동기화를 해제하면 계정이 더 이상 사용되지 않을 뿐만 아니라 업데이트 시간도 줄어들 수 있습니다.

계속 진행하려면 [!DNL Commerce Intelligence] [지원](../guide-overview.md#Submitting-a-Support-Ticket)에 문의하세요. 지원 팀은 SQL 보고서를 제외하고 사용자의 대시보드에서 사용되지 않고 전자 메일 요약에 사용되지 않는 모든 열을 포함하는 보고서를 만들 수 있습니다. 그런 다음 Data Warehouse Manager를 통해 이 보고서를 동기화하지 않을 열을 선택하는 안내서로 사용할 수 있습니다.

>[!NOTE]
>
>나중에 언제든지 이러한 열을 다시 동기화할 수 있습니다. 열의 동기화를 해제하면 Data Warehouse에서 모든 데이터가 제거됩니다. 업데이트 주기 동안 이 열에 새 값이나 업데이트된 값이 선택되어 있지 않다는 의미일 뿐입니다.

**열 동기화를 해제하려면**

1. **[!DNL Manage Data]**(으)로 이동한 다음 **[!UICONTROL Data Warehouse]**(으)로 이동합니다.
1. **[!UICONTROL Synced Tables]** 목록에서 열이 포함된 테이블로 이동합니다.
1. 동기화를 해제할 하나 이상의 열 옆에 있는 하나 이상의 상자를 선택합니다.

   >[!NOTE]
   >
   >전체 테이블을 삭제하지 않으면 기본 키 열의 동기화를 해제할 수 없습니다.

1. 하나 이상의 열을 동기화하지 않으려면 **[!UICONTROL Remove]**&#x200B;을(를) 클릭하십시오.

전체 프로세스를 살펴보겠습니다.

![Data Warehouse 관리자에서 열 옵션 삭제](../../mbi/assets/drop_column.png)

## 요약

이제 [!DNL Commerce Intelligence] 계정을 더 깔끔하게 정리하여 사용자와 팀을 쉽게 탐색할 수 있습니다.
