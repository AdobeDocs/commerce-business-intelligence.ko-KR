---
title: Adobe Commerce 사용자 및 권한 관리
description: Commerce Intelligence 사용자를 관리하는 방법을 알아봅니다.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# 사용자 권한 관리

[!DNL Adobe Commerce Intelligence]은(는) 조직 전체에서 신뢰할 수 있는 단일 소스입니다. 각 사용자에게는 [다른 사용자와 공유](../../data-user/dashboards/share-dashboard-with-users.md)할 수 있는 자체 대시보드 세트가 있습니다.

## 사용자 권한 수준

[!DNL Commerce Intelligence]에는 계정을 만들 때 선택된 세 가지 일반 권한 수준이 사용자에게 적용됩니다.

* `Admin`
* `Standard`
* `Read-Only`

이러한 권한을 통해 사용자는 특정 작업을 수행하거나 [!DNL Commerce Intelligence]의 특정 부분에 액세스할 수 있습니다. 다음은 [!DNL Commerce Intelligence]에서 각 권한 수준이 수행할 수 있는 작업의 표입니다.

|   | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **사용자 만들기/관리** | ✔ |   |   |
| **전자 메일 요약 만들기** | ✔ | ✔ |   |
| **대시보드 만들기/편집/공유** | ✔ | ✔ |   |
| **대시보드 보기** | ✔ | ✔ | ✔ |
| **시각적 보고서 만들기/편집/삭제** | ✔ | ✔* |   |
| **SQL 보고서 만들기/편집/삭제** | ✔ |  |   |
| **대시보드 복제** | ✔ |   |   |
| **통합 추가/관리** | ✔ |   |   |
| **Data Warehouse 관리자에 액세스** | ✔ |   |   |
| **테이블 및 열 동기화/동기화 해제** | ✔ |   |   |
| **지표 만들기/편집** | ✔ |   |   |
| **필터 집합 만들기/편집** | ✔ |   |   |
| **계산된 열 만들기/편집** | ✔ |   |   |
| **종속 보고서 목록 만들기** | ✔ |   |   |
| **시스템 요약 액세스** | ✔ |   |   |
| **표준 시간대 설정에 액세스** | ✔ |   |   |
| **청구 액세스** | ✔ | ✔** |   |
| **지원팀에 문의** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_특정 지표에 대한&#x200B;**[!UICONTROL Standard]**&#x200B;사용자의 [액세스](../../administrator/user-management/restrict-metric-access.md)을 제한할 수 있습니다._
>
>**[!UICONTROL Standard] _사용자는 추가 권한 설정으로 청구에 액세스할 수 있습니다._
>
>**[!UICONTROL Read-Only]** 사용자는 공유된 대시보드만 _보기_&#x200B;할 수 있으며 [!DNL Commerce Intelligence]에서 만들거나 편집할 수 없으며 새 대시보드를 검색하여 계정에 추가할 수도 없습니다. Adobe은 귀하 또는 귀하의 팀의 다른 구성원이 유지 관리하는 **[!UICONTROL Read-Only]**&#x200B;명의 사용자와 특정 대시보드 세트를 공유할 것을 권장합니다. 대시보드 세트를 복제하지 마십시오.

## 추가 권한: 청구 및 기술 {#billingtech}

일반 권한 수준 외에 `Billing`과(와) `Technical`, 두 개의 다른 사용자 지정도 있습니다. 이러한 지정은 일반 권한 수준에서 사용해야 합니다.

### 청구

`Billing`명의 사용자가 청구 페이지에 액세스할 수 있으며 결제 정보를 변경할 수 있습니다. 또한 청구 관련 질문이 있는 경우 Adobe으로 문의할 수도 있습니다.

`Admin`명의 사용자는 기본적으로 `Billing` 탭에 액세스할 수 있지만 `Standard`명의 사용자는 프로필에서 `Billing` 확인란을 선택한 경우에도 액세스할 수 있습니다.

![청구](../../assets/billing.png)<!--{: width="550" height="363"}-->

### 기술

`Technical`명의 사용자에게 해당 사용자에 대한 권한이 없습니다. 이 설정은 조직 내 기술 담당자를 표시합니다. 이러한 사용자는 기술 관련 질문이 있는 경우 Adobe으로 문의할 수 있습니다.

`Admin`명의 사용자가 **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]**&#x200B;을(를) 클릭하고 프롬프트에 따라 새 사용자를 계정에 추가할 수 있습니다. 사용자가 [!DNL Commerce Intelligence]에서 만들어지면 초대하는 행운의 사용자에게 계정 설정 프로세스를 완료하는 방법에 대한 전자 메일 지침이 전송됩니다.

`Admins`은(는) 언제든지 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**&#x200B;을(를) 클릭하여 계정의 모든 사용자를 볼 수 있습니다. 이 페이지에는 사용자의 권한과 액세스 가능한 지표 및 대시보드가 표시됩니다.
