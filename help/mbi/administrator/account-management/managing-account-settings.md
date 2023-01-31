---
title: 계정 설정 관리
description: Data Warehouse에 대한 많은 계정 설정을 사용자 지정하는 방법을 알아봅니다.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# 계정 설정 사용자 지정

>[!NOTE]
>
>필요한 경우 [관리자 권한.](../../administrator/user-management/user-management.md)

사용자 [!DNL MBI] account에서는 data warehouse에 대한 여러 계정 설정을 사용자 지정할 수 있습니다. 화면의 오른쪽 상단 모서리에서 조직 이름을 선택한 다음 선택하여 액세스할 수 있습니다 **[!UICONTROL Account Settings]** 드롭다운

* **[!UICONTROL Client Name:]** 이 설정은 모든 대시보드 및 계정 전체의 다른 위치에 있는 오른쪽 모서리에 나타납니다. 변경하려는 경우 **[!UICONTROL "Vandelay Industries Co., Ltd]** 변환 후: **[!UICONTROL "Vandelay]**&#x200B;여기서 수행해야 합니다.

* **[!UICONTROL Currency:]** 이것은 *기본 통화* 의 모든 통화 값을 사용할 수 있습니다. 소수점 또는 통화 값이 데이터 웨어하우스에 동기화될 때마다 이 설정은 보고서 내에서 해당 값 앞에 배치된 기호를 결정합니다.

* **[!UICONTROL Blackout Hours:]** 이 설정은 선택한 시간 동안 데이터 웨어하우스에서 연결된 데이터베이스에 액세스하지 못하도록 합니다. 모든 시간은 0시간 및 동부 표준시(EST)로 표시됩니다. 예를 들어, 오전 9:00과 오후 1:00의 EST 시간 사이에 프로덕션 데이터베이스에 액세스하지 않으려면 다음 자릿수 배열을 입력해야 합니다. **9,10,11,12**.

* **[!UICONTROL Forced update hours:]** 이 설정은 데이터 웨어하우스 업데이트가 계정에서 자동으로 시작됩니다 *시간* 지정한 경우 정전 시간과 마찬가지로, 이것들은 또한 ET에 있습니다. 예를 들어 데이터 웨어하우스 업데이트를 다음에서 자동으로 시작하려는 경우 **자정** 및 **정오** EST, 다음 자릿수를 입력해야 합니다. **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** 이 옵션은 전자 메일 요약을 전송하도록 예약된 상황에서 수행할 작업을 시스템에 알려줍니다 *보고서 중 하나에서 데이터 전에* 는 현재까지의 새로운 기능을 제공합니다. 만약 **아니요**&#x200B;을 지정하면 계정이 예약된 시간에 이메일 전송을 건너뛰고 대신 데이터가 업데이트되면 전송합니다. 만약 **[!UICONTROL Yes]**, 계정이 이메일을 전송하고 데이터가 부실함을 설명하는 메시지를 포함하며, 데이터가 업데이트되면 다른 이메일이 전송됩니다.

* **[!UICONTROL Enable data updates:]** 이 옵션을 사용하면 계정에서 데이터 업데이트가 실행됩니다. 설정을 **[!UICONTROL No]**, 데이터 동기화 및 열 계산은 계정에서 완전히 중지됩니다.

>[!NOTE]
>
>반드시 선택합니다 **[!UICONTROL Save Customizations]** 변경한 후
