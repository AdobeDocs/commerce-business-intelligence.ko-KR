---
title: 자동화된 이메일 요약 만들기
description: 자동화된 이메일 요약을 만드는 방법을 알아봅니다.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 자동화된 이메일 요약 만들기

이메일 요약은 주요 관련자와 비즈니스의 상태 및 트렌드를 공유하는 데 사용할 수 있는 강력한 커뮤니케이션 도구입니다. 전자 메일 요약을 사용하여 다음과 같은 작업을 수행할 수 있습니다.

* 보고서를 포함하는 이메일 그래픽 요약
* 이메일 요약 작성자가 이메일을 수신하지 못하도록 포함 또는 제외
* 이메일 전송 시간 예약
* 기존의 예약된 이메일 요약 편집, 삭제 및 일시 중지

## 새 이메일 요약 만들기

1. 클릭 **[!DNL Manage Data]** 그러면 **[!UICONTROL Email Summary]** 를 클릭합니다.

   전자 메일 요약을 처음 만드는 경우 이 페이지에는 저장된 요약이 표시되지 않습니다.

1. 클릭 **[!UICONTROL Create New Email Summary]** 오른쪽 상단 모서리입니다.

1. 요약의 이름을 입력합니다.

   요약에 포함된 내용을 전달하는 이름을 선택합니다. For example, `AOV Comparison`.

1. 다음에서 `Choose Content` 섹션에서 요약에 포함할 보고서를 선택합니다.

   소유한 보고서를 최대 10개까지 선택할 수 있습니다. 보고서를 선택한 후 나타나는 아이콘을 사용하여 해당 보고서를 테이블이나 차트로 전송할지 선택합니다. 보고서를 숫자로 저장한 경우 숫자로만 보낼 수 있습니다. 오래된 데이터가 있는 보고서가 포함된 이메일 요약을 보내는 방법에 대한 자세한 내용은 [계정 설정 관리](../../administrator/account-management/managing-account-settings.md).

   >[!NOTE]
   >
   >`Cohort` 보고서는 새 아키텍처를 사용하는 경우에만 사용할 수 있습니다.

1. (선택 사항) 선택 `Send Email To Me` 이메일을 받고 싶은 경우.

1. 이메일에 다른 사용자를 포함시키려면 `Add Email Recipients` 쉼표, 공백, 탭 또는 세미콜론으로 구분된 필드.

## 일정 이메일 요약

다음에서 `Set when to send the Email Summary` 필드에서 이메일 요약을 보낼 시기를 지정할 수 있습니다. 옵션은 다음과 같습니다.

* `Manual`
* `Once`
* `Repeating`

### 나중에 보낼 전자 메일 요약 저장

1. 선택 `Manual` 다음에서 `Set when to send the Email Summary` 필드.

1. 클릭 **[!UICONTROL Save]**.

   이렇게 하면 전자 메일 요약 목록에 요약이 저장됩니다.

1. 요약을 보낼 준비가 되면 톱니바퀴 아이콘을 클릭하고 을 선택합니다 `Send Now`.

### 이메일 요약을 한 번 보내기

1. 선택 `Once` 다음에서 `Set when to send the Email Summary` 필드.

1. 에서 시작 날짜를 지정합니다. `Select Start Date` 달력.

1. 이메일을 보낼 시간 지정 `Select time to send` 필드.

### 반복 일정 만들기

1. 선택 `Repeating` 다음에서 `Set when to send the Email Summary` 필드.

1. 다음에서 `Set Frequency` 필드, 선택 `Daily`, `Weekly`, 또는 `Monthly`.

1. 에서 시작 날짜를 지정합니다. `Select Start Date` 달력.

1. 이메일을 보낼 시간 지정 `Select time to send` 필드.

1. (선택 사항) 종료 날짜를 지정하려면 `End Date` 달력에서 종료 날짜를 선택합니다.

## 기존 이메일 요약 수정

이메일 요약을 만들고 저장한 후 `Email Summaries` 저장된 요약 목록이 페이지에 표시됩니다. 를 확장할 수 있습니다(`+`) 각 행을 참조하십시오. 이 보기의 열은 다음과 같습니다.

* `Email Name` - 이메일 요약 이름
* `Content` - 보고서 이름과 같은 요약 내 콘텐츠 유형. 오래된 데이터가 있는 보고서가 포함된 이메일 요약을 보내는 방법에 대한 자세한 내용은 [계정 설정 관리](../../administrator/account-management/managing-account-settings.md).
* `Scheduled` - 이메일 요약이 전송되는 빈도, 날짜 및 시간
* `Recipients` - 이메일 요약 수신자
* `Created Date` - 이메일 요약이 생성된 날짜
* `Status` - `Paused` 또는 `Active`

각 행의 오른쪽에 있는 톱니바퀴 아이콘을 클릭하여 다음을 수행합니다.

* `Send Now` - 지정된 모든 수신자에게 이메일 요약을 즉시 전송합니다.
* `Edit` - 이메일 요약의 세부 사항을 수정할 수 있습니다.
* `Pause/Active` - 이메일 요약 전달을 일시 중지하거나 구성 방법에 따라 요약을 활성화할 수 있습니다.
* `Delete` - 이메일 요약을 삭제합니다.
