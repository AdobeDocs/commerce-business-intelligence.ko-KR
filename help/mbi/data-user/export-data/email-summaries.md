---
title: 자동화된 이메일 요약 만들기
description: 자동화된 이메일 요약을 만드는 방법을 알아봅니다.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 자동화된 이메일 요약 만들기

이메일 요약은 주요 이해 관계자와 비즈니스의 현재 상태 및 트렌드를 공유하는 데 사용할 수 있는 강력한 커뮤니케이션 도구입니다. 이메일 요약을 사용하면 다음 작업을 수행할 수 있습니다.

* 보고서를 포함하는 이메일 그래픽 요약
* 이메일 요약 작성자가 이메일을 받지 못하도록 포함하거나 제외합니다
* 이메일 전송 시점을 예약합니다.
* 예약된 기존 이메일 요약 편집, 삭제 및 일시 중지

## 새 이메일 요약 만들기

1. 클릭 **[!DNL Manage Data]** 그런 다음 **[!UICONTROL Email Summary]** 을 클릭합니다.

   이메일 요약을 처음 만드는 경우 이 페이지에 저장된 요약이 표시되지 않습니다.

1. 클릭 **[!UICONTROL Create New Email Summary]** 오른쪽 상단 모서리에서

1. 요약의 이름을 입력합니다.

   요약에 포함된 내용을 전달하는 이름을 선택합니다. 예, `AOV Comparison`.

1. 에서 `Choose Content` 섹션에서 요약에 포함할 보고서를 선택합니다.

   소유하는 보고서를 최대 10개까지 선택할 수 있습니다. 보고서를 선택한 후 나타나는 아이콘을 사용하여 해당 보고서를 테이블이나 차트로 보내려면 선택합니다. 보고서를 숫자로 저장한 경우 숫자로 전송할 수만 있습니다. 오래된 데이터가 있는 보고서가 포함된 이메일 요약 전송에 대한 자세한 내용은 [계정 설정 관리](../../administrator/account-management/managing-account-settings.md).

   >[!NOTE]
   >
   >`Cohort` 보고서는 새 아키텍처를 사용하는 경우에만 사용할 수 있습니다.

1. (선택 사항) 선택 `Send Email To Me` 이메일을 수신하려면

1. 이메일에 다른 사용자를 포함하려면 전자 메일 주소를 `Add Email Recipients` 필드는 쉼표, 공백, 탭 또는 세미콜론으로 구분됩니다.

## 예약 이메일 요약

에서 `Set when to send the Email Summary` 필드에서는 전자 메일 요약을 보낼 시기를 지정할 수 있습니다. 옵션은 다음과 같습니다.

* `Manual`
* `Once`
* `Repeating`

### 나중에 전송할 이메일 요약 저장

1. 선택 `Manual` 에서 `Set when to send the Email Summary` 필드.

1. 클릭 **[!UICONTROL Save]**.

   이렇게 하면 요약이 이메일 요약 목록에 저장됩니다.

1. 요약을 보낼 준비가 되면 톱니바퀴 아이콘을 클릭하고 을 선택합니다 `Send Now`.

### 전자 메일 요약 한 번 보내기

1. 선택 `Once` 에서 `Set when to send the Email Summary` 필드.

1. 에서 시작 날짜를 지정합니다. `Select Start Date` 달력.

1. 에서 이메일을 보낼 시간을 지정합니다 `Select time to send` 필드.

### 반복 일정 만들기

1. 선택 `Repeating` 에서 `Set when to send the Email Summary` 필드.

1. 에서 `Set Frequency` 필드, 선택 `Daily`, `Weekly`, 또는 `Monthly`.

1. 에서 시작 날짜를 지정합니다. `Select Start Date` 달력.

1. 에서 이메일을 보낼 시간을 지정합니다 `Select time to send` 필드.

1. (선택 사항) 종료 날짜를 지정하려면 `End Date` 달력에서 종료 날짜를 선택합니다.

## 기존 전자 메일 요약 수정

이메일 요약을 작성하고 저장하면 `Email Summaries` 페이지에 저장된 모든 요약 목록이 표시됩니다. 확장(`+`)를 참조하십시오. 이 보기의 열은 다음과 같습니다.

* `Email Name` - 이메일 요약 이름
* `Content` - 보고서 이름과 같이 요약 내에 있는 컨텐츠의 유형입니다. 오래된 데이터가 있는 보고서가 포함된 이메일 요약 전송에 대한 자세한 내용은 [계정 설정 관리](../../administrator/account-management/managing-account-settings.md).
* `Scheduled` - 이메일 요약 전송 빈도, 날짜 및 시간
* `Recipients` - 이메일 요약 수신자
* `Created Date` - 이메일 요약을 만든 날짜
* `Status` - `Paused` 또는 `Active`

각 행 오른쪽에 있는 톱니바퀴 아이콘을 클릭하여 다음을 수행합니다.

* `Send Now` - 지정한 모든 수신자에게 즉시 전자 메일 요약을 보냅니다.
* `Edit` - 이메일 요약 세부 사항을 수정할 수 있습니다
* `Pause/Active` - 이메일 요약이 전달되지 않도록 일시 중지하거나 구성 방법에 따라 요약을 활성화할 수 있습니다
* `Delete` - 이메일 요약을 삭제합니다
