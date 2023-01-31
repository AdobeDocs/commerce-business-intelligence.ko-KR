---
title: 사용자 및 권한 관리
description: 관리 방법 알아보기 [!DNL MBI] 사용자 참조.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# 사용자 권한 관리

MBI는 조직 전체에서 단일 진실 소스여야 합니다. 각 사용자는 가능한 고유한 대시보드 세트를 가질 수 있습니다 [다른 사용자와 공유](../../data-user/dashboards/share-dashboard-with-users.md).

## 사용자 권한 수준

in [!DNL MBI]에는 계정을 만들 때 선택된 사용자에게 적용되는 세 가지 일반 권한 수준이 있습니다.

* `Admin`
* `Standard`
* `Read-Only`

이러한 권한을 통해 사용자는 특정 작업을 수행하거나 [!DNL MBI]. 다음은 각 권한 수준에서 MBI에서 수행할 수 있는 작업의 표입니다.

|  | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **사용자 만들기/관리** | ✔ |  |  |
| **이메일 요약 만들기** | ✔ | ✔ |  |
| **대시보드 만들기/편집/공유** | ✔ | ✔ |  |
| **대시보드 보기** | ✔ | ✔ | ✔ |
| **시각적 보고서 만들기/편집/삭제** | ✔ | ✔* |  |
| **SQL 보고서 만들기/편집/삭제** | ✔ |  |  |
| **대시보드 복제** | ✔ |  |  |
| **통합 추가/관리** | ✔ |  |  |
| **Data Warehouse 관리자 액세스** | ✔ |  |  |
| **테이블 및 열 동기화/동기화 해제** | ✔ |  |  |
| **지표 만들기/편집** | ✔ |  |  |
| **필터 세트 만들기/편집** | ✔ |  |  |
| **계산된 열 만들기/편집** | ✔ |  |  |
| **종속 보고서 목록 만들기** | ✔ |  |  |
| **액세스 시스템 요약** | ✔ |  |  |
| **시간대 설정 액세스** | ✔ |  |  |
| **액세스 청구** | ✔ | ✔** |  |
| **지원 문의** | ✔ | ✔ | ✔ |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>_을(를) 제한할 수 있습니다&#x200B;**[!UICONTROL Standard]**사용자 [특정 지표에 대한 액세스](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _사용자는 추가 권한 설정으로 과금에 액세스할 수 있습니다._
>
>**[!UICONTROL Read-Only]** 사용자는 _보기_ 공유된 대시보드 에서는 아무 것도 만들거나 편집할 수 없습니다 [!DNL MBI]를 검색하고 새 대시보드를 계정에 추가할 수 없습니다. 특정 대시보드 세트를 **[!UICONTROL Read-Only]** 사용자 또는 팀의 다른 구성원이 유지 관리하는 사용자. 대시보드 세트를 복제하지 마십시오.

## 추가 권한: 청구 및 기술 {#billingtech}

일반 권한 수준 외에 두 개의 다른 사용자 지정도 있습니다. `Billing` 및 `Technical`. 이러한 지정은 일반 권한 수준과 함께 사용됩니다.

### 과금

`Billing` 사용자는 청구 페이지에 액세스할 수 있으며 결제 정보를 변경할 수 있습니다. 또한 청구 관련 문의 사항은 Adobe 팀이 문의할 수도 있습니다.

`Admin` 사용자는 기본적으로 청구 탭에 액세스할 수 있지만 표준 사용자는 `Billing` 프로필에서 선택한 확인란.

![과금](../../assets/billing.png)<!--{: width="550" height="363"}-->

### 기술

`Technical` 사용자에게만 해당하는 권한이 없습니다. 이 설정은 조직 내의 기술 연락처를 표시합니다. 기술 관련 문의 사항은 Adobe 팀이 연락할 수 있습니다.

`Admin` 사용자는 **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** 화면의 지시를 따릅니다. 사용자가 만들어지면에서 [!DNL MBI]을 지정하는 운 좋은 사람은 계정 설정 프로세스를 완료하는 방법에 대한 이메일 지침을 받게 됩니다.

언제든지 `Admins` 을 클릭하여 계정의 모든 사용자를 볼 수 있습니다 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. 이 페이지에는 사용자의 권한과 액세스 권한이 있는 지표 및 대시보드가 표시됩니다.
