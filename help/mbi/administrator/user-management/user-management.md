---
title: Adobe Commerce 사용자 및 권한 관리
description: Commerce Intelligence 사용자를 관리하는 방법을 알아봅니다.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 사용자 권한 관리

[!DNL Adobe Commerce Intelligence] 는 조직 전체에서 신뢰할 수 있는 단일 소스입니다. 각 사용자에게는 다음과 같은 작업을 수행할 수 있는 자체 대시보드 세트가 있습니다 [다른 사용자와 공유](../../data-user/dashboards/share-dashboard-with-users.md).

## 사용자 권한 수준

위치 [!DNL Commerce Intelligence]에는 계정을 만들 때 선택되는 세 가지 일반 권한 수준이 사용자에게 적용됩니다.

* `Admin`
* `Standard`
* `Read-Only`

이러한 권한을 통해 사용자는 특정 작업을 수행하거나 특정 [!DNL Commerce Intelligence]. 다음은 각 권한 수준에서 수행할 수 있는 작업입니다 [!DNL Commerce Intelligence]:

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
| **시스템 요약 액세스** | ✔ |  |  |
| **시간대 설정에 액세스** | ✔ |  |  |
| **청구 액세스** | ✔ | ✔** |  |
| **지원 문의** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_다음을 제한할 수 있습니다.**[!UICONTROL Standard]**사용자 [특정 지표에 대한 액세스](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _사용자는 추가 권한 설정으로 청구에 액세스할 수 있습니다._
>
>**[!UICONTROL Read-Only]** 사용자는 만 할 수 있습니다. _보기_ 공유된 대시보드: 의 항목을 만들거나 편집할 수 없습니다. [!DNL Commerce Intelligence]또한 새 대시보드를 검색하고 계정에 추가할 수 없습니다. Adobe은 특정 대시보드 세트를 와 공유할 것을 권장합니다 **[!UICONTROL Read-Only]** 귀하 또는 귀하의 팀의 다른 멤버가 유지 관리하는 사용자. 대시보드 세트를 복제하지 마십시오.

## 추가 권한: 청구 및 기술 {#billingtech}

일반 권한 수준 외에 두 가지 다른 사용자 지정도 있습니다. `Billing` 및 `Technical`. 이러한 지정은 일반 권한 수준에서 사용해야 합니다.

### 청구

`Billing` 사용자는 청구 페이지에 액세스할 수 있으며 결제 정보를 변경할 수 있습니다. 또한 청구 관련 질문이 있는 경우 Adobe으로 문의할 수도 있습니다.

`Admin` 사용자는에 대한 액세스 권한이 있습니다. `Billing` 기본적으로 탭이지만 `Standard` 사용자에게 다음이 있는 경우 액세스 권한을 부여할 수도 있습니다. `Billing` 프로필에서 선택한 확인란입니다.

![과금](../../assets/billing.png)<!--{: width="550" height="363"}-->

### 기술

`Technical` 사용자에게 이에 대한 권한이 없습니다. 이 설정은 조직 내의 기술 담당자를 표시합니다. 이러한 사용자는 기술 관련 질문이 있는 경우 Adobe으로 문의할 수 있습니다.

`Admin` 을 클릭하여 새 사용자를 자신의 계정에 추가할 수 있습니다. **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** 프롬프트에 따라 을 클릭합니다. 사용자가에 생성된 후 [!DNL Commerce Intelligence]을(를) 초대하는 행운의 사용자에게 계정 설정 프로세스를 완료하는 방법에 대한 이메일 지침이 전송됩니다.

언제든지, `Admins` 을 클릭하여 계정의 모든 사용자를 볼 수 있습니다. **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. 이 페이지에는 사용자의 권한과 액세스 가능한 지표 및 대시보드가 표시됩니다.
