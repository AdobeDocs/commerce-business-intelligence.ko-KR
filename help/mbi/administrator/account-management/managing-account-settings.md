---
title: 계정 설정 관리
description: Data Warehouse에 대한 계정 설정을 사용자 지정하는 방법을 알아봅니다.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 계정 설정 사용자 지정

>[!NOTE]
>
>[관리자 권한이 필요합니다.](../../administrator/user-management/user-management.md)

[!DNL Commerce Intelligence] 계정에서 Data Warehouse에 대한 계정 설정을 사용자 지정할 수 있습니다. 화면 오른쪽 상단에서 조직 이름을 선택한 다음 드롭다운에서 **[!UICONTROL Account Settings]**&#x200B;을(를) 선택하여 액세스할 수 있습니다.

* **[!UICONTROL Client Name:]** 이 설정은 모든 대시보드의 오른쪽 상단 모서리와 계정 전체의 다른 위치에 표시됩니다. **[!UICONTROL "Vandelay Industries Co., Ltd]**&#x200B;을(를) **[!UICONTROL "Vandelay]**(으)로 변경하려는 경우 이 작업을 수행합니다.

* **[!UICONTROL Currency:]** 계정의 모든 통화 값에 대한 *기본 통화*&#x200B;입니다. 소수점 또는 통화 값이 Data Warehouse에 동기화될 때마다 이 설정은 보고서 내에서 해당 값 앞에 배치된 기호를 결정합니다.

* **[!UICONTROL Blackout Hours:]** 이 설정은 하루 중 선택한 시간 동안 Data Warehouse이 연결된 데이터베이스에 액세스하지 않도록 합니다. 모든 시간은 0시 및 동부 표준시(EST)로 표시됩니다. 예를 들어 오전 9시부터 오후 1시(EST) 사이에 프로덕션 데이터베이스에 액세스하지 않으려면 **9, 10, 11, 12** 자릿수 배열을 입력해야 합니다.

* **[!UICONTROL Forced update hours:]** 이 설정을 사용하면 지정한 *시간 동안* 계정에서 Data Warehouse 업데이트가 자동으로 시작됩니다. 일시 중단 시간과 마찬가지로 ET에도 있습니다. 예를 들어 Data Warehouse 업데이트가 **자정** 및 **정오** EST에 자동으로 시작되도록 하려면 다음 숫자 배열을 입력해야 합니다. **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** 이 옵션은 보고서 중 하나의 데이터를 새로 고치기 전에 *전자 메일 요약을 보내도록 예약되어 있는 상황을 관리합니다*. **아니요**&#x200B;를 선택하면 계정이 예약된 시간에 이메일 전송을 건너뜁니다. 대신 데이터가 업데이트되면 계정이 해당 데이터를 보냅니다. **[!UICONTROL Yes]**&#x200B;을(를) 선택하면 귀하의 계정에서 이메일을 보내고, 데이터가 오래되었음을 설명하는 메시지를 포함하며, 데이터가 업데이트되면 다른 이메일을 보냅니다.

* **[!UICONTROL Enable data updates:]** 이 옵션을 사용하면 계정에서 데이터 업데이트가 실행됩니다. 설정을 **[!UICONTROL No]**(으)로 변경하면 계정에서 데이터 동기화 및 열 계산이 중지됩니다.

>[!NOTE]
>
>변경한 후 **[!UICONTROL Save Customizations]**&#x200B;을(를) 선택하십시오.
