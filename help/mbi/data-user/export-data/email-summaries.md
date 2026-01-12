---
title: 자동화된 이메일 요약 만들기
description: 자동화된 이메일 요약을 만드는 방법을 알아봅니다.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: a65ededb203b7551fdfcb31cff130ef85b01fbe3
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# 자동화된 이메일 요약 만들기

이메일 요약은 주요 관련자와 비즈니스의 상태 및 트렌드를 공유하는 데 사용할 수 있는 강력한 커뮤니케이션 도구입니다. 전자 메일 요약을 사용하여 다음과 같은 작업을 수행할 수 있습니다.

* 보고서를 포함하는 이메일 그래픽 요약
* 이메일 요약 작성자가 이메일을 수신하지 못하도록 포함 또는 제외
* 이메일 전송 시간 예약
* 기존의 예약된 이메일 요약 편집, 삭제 및 일시 중지

## 새 이메일 요약 만들기

1. 사이드바에서 **[!DNL Manage Data]**&#x200B;을(를) 클릭한 다음 **[!UICONTROL Email Summary]**&#x200B;을(를) 클릭합니다.

   전자 메일 요약을 처음 만드는 경우 이 페이지에는 저장된 요약이 표시되지 않습니다.

1. 오른쪽 상단 모서리에서 **[!UICONTROL Create New Email Summary]**&#x200B;을(를) 클릭합니다.

1. 요약의 이름을 입력합니다.

   요약에 포함된 내용을 전달하는 이름을 선택합니다. 예: `AOV Comparison`.

1. `Choose Content` 섹션에서 요약에 포함할 보고서를 선택합니다.

   컨텐츠를 추가하는 두 가지 옵션이 있습니다.

   * **개별 보고서 선택** - 대시보드에서 특정 보고서를 선택합니다.
   * **전체 대시보드 선택** - 대시보드의 모든 보고서를 대시보드 레이아웃에 표시할 때 포함합니다.

   소유한 보고서를 최대 10개까지 선택할 수 있습니다. 보고서를 선택한 후 나타나는 아이콘을 사용하여 해당 보고서를 테이블이나 차트로 전송할지 선택합니다. 보고서를 숫자로 저장한 경우 숫자로만 보낼 수 있습니다. 오래된 데이터가 포함된 보고서가 포함된 전자 메일 요약을 보내는 방법에 대한 자세한 내용은 [계정 설정 관리](../../administrator/account-management/managing-account-settings.md)를 참조하십시오.

   전체 대시보드를 추가하는 경우 다음과 같은 형식 및 삭제 옵션이 있습니다.

   * 보고서의 서식을 차트 또는 표로 변경
   * 이메일에 포함되지 않은 보고서 삭제
   * 테이블 형식 보고서에 대한 CSV 파일을 포함하도록 선택합니다. 이렇게 하면 수신자가 받은 편지함에서 직접 원시 및 내보내기 가능한 데이터에 액세스할 수 있습니다.

   >[!NOTE]
   >
   >`Cohort` 보고서는 새 아키텍처를 사용하는 경우에만 사용할 수 있습니다.

   >[!NOTE]
   >
   >큰 CSV 첨부 파일은 이메일당 총 25MB까지 지원됩니다.

1. (선택 사항) 전자 메일을 받으려면 `Send Email To Me`을(를) 선택합니다.

1. 전자 메일에 다른 사용자를 포함하려면 `Add Email Recipients` 필드에 쉼표, 공백, 탭 또는 세미콜론으로 구분하여 전자 메일 주소를 입력하십시오.

## 일정 이메일 요약

`Set when to send the Email Summary` 필드에서 전자 메일 요약을 보낼 시기를 지정할 수 있습니다. 옵션은 다음과 같습니다.

* `Manual`
* `Once`
* `Repeating`

### 나중에 보낼 전자 메일 요약을 저장하십시오.

1. `Manual` 필드에서 `Set when to send the Email Summary`을(를) 선택합니다.

1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

   이렇게 하면 전자 메일 요약 목록에 요약이 저장됩니다.

1. 요약을 보낼 준비가 되면 톱니바퀴 아이콘을 클릭하고 `Send Now`을(를) 선택합니다.

### 이메일 요약을 한 번 보내기

1. `Once` 필드에서 `Set when to send the Email Summary`을(를) 선택합니다.

1. `Select Start Date` 일정에서 시작 날짜를 지정하십시오.

1. `Select time to send` 필드에 전자 메일을 보낼 시간을 지정합니다.

### 반복 일정 만들기

1. `Repeating` 필드에서 `Set when to send the Email Summary`을(를) 선택합니다.

1. `Set Frequency` 필드에서 `Daily`, `Weekly` 또는 `Monthly`을(를) 선택합니다.

1. `Select Start Date` 일정에서 시작 날짜를 지정하십시오.

1. `Select time to send` 필드에 전자 메일을 보낼 시간을 지정합니다.

1. (선택 사항) 종료 날짜를 지정하려면 `End Date`을(를) 선택하고 달력에서 종료 날짜를 선택합니다.

## 기존 이메일 요약 수정

전자 메일 요약을 만들고 저장하면 `Email Summaries` 페이지에 저장된 모든 요약 목록이 표시됩니다. 자세한 내용을 보려면 각 행에서 (`+`)을(를) 확장할 수 있습니다. 이 보기의 열은 다음과 같습니다.

* `Email Name` - 전자 메일 요약 이름
* `Content` - 보고서 이름과 같은 요약 내 콘텐츠 유형
* `Scheduled` - 전자 메일 요약을 보낸 빈도, 날짜 및 시간
* `Recipients` - 전자 메일 요약 수신자
* `Created Date` - 전자 메일 요약을 만든 날짜
* `Status` - `Paused` 또는 `Active`

>[!NOTE]
>
>오래된 데이터가 포함된 보고서가 포함된 전자 메일 요약을 보내는 방법에 대한 자세한 내용은 [계정 설정 관리](../../administrator/account-management/managing-account-settings.md)를 참조하십시오.

각 행의 오른쪽에 있는 톱니바퀴 아이콘을 클릭하여 다음을 수행합니다.

* `Send Now` - 지정된 모든 받는 사람에게 전자 메일 요약을 즉시 보냅니다.
* `Edit` - 전자 메일 요약 세부 정보 수정
* `Pause/Active` - 전자 메일 요약 게재 일시 중지 또는 활성화
* `Delete` - 전자 메일 요약 삭제
