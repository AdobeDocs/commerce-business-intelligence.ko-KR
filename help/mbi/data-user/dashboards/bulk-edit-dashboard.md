---
title: 대시보드에서 차트 벌크 편집
description: 에서 벌크 편집 기능을 사용하는 방법을 알아봅니다. [!DNL MBI].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# 대시보드에서 차트 벌크 편집

벌크 편집 기능을 사용하면 대시보드에서 차트 이름과 날짜를 쉽게 변경할 수 있습니다. 예를 들어, 특정 대시보드의 모든 차트를 단일 저장소를 참조하고 분기보다 월별로 보고하도록 할 수 있습니다. 모든 것을 수동으로 변경하는 대신 `bulk-editing` 기능이 작업을 수행합니다. 이 문서에서 사용 방법을 알아봅니다.

* [다음 ](#findreplace)

* [다음 ](#prepend)

* [다음 ](#dates)

이것은, 이것을 고려하라 - *이러한 변경 사항은 영구적이어야 합니까?* 그렇지 않은 경우 대시보드를 복제한 다음 새 대시보드에서 날짜를 변경하는 것이 좋습니다. 이렇게 하면 필요한 변경 작업을 수행하는 동안 원래 대시보드를 유지할 수 있습니다.

>[!NOTE]
>
>많은 보고서를 변경하는 경우 업데이트 프로세스에 시간이 좀 걸릴 수 있습니다.

## 사용 `Find/Replace` {#findreplace}

1. 톱니바퀴(![](../../assets/gear-icon.png)) 아이콘을 클릭한 다음 대시보드 이름 옆에 있는 를 클릭합니다. [!UICONTROL Bulk Edit Reports] 창을 엽니다.

1. 클릭 **[!UICONTROL Chart Title Find and Replace]** 팝업 창에서 클릭합니다.

1. 에서 `Chart Title Find` 필드에서 찾을 단어나 문자를 입력합니다.

1. 에서 `Replace With` 필드에 포함할 단어나 문자를 입력합니다 `Find` 필드.

1. 클릭 **[!UICONTROL Update Reports]**.

예:

![일괄 편집](../../assets/bulk_edit.gif)

## 사전 보류 중 `Chart Names` {#prepend}

1. 톱니바퀴(![](../../assets/gear-icon.png)) 아이콘을 클릭한 다음 대시보드 이름 옆에 있는 를 클릭합니다. [!UICONTROL Bulk Edit Reports] 창을 엽니다.

1. 클릭 **[!UICONTROL Prepend Report Names]** 팝업 창에서 클릭합니다.

1. 차트 앞에 추가할 단어나 문자를 입력합니다.

1. 클릭 **[!UICONTROL Update Reports]**.

예:

![프리펜드](../../assets/prepend.gif)

## 변경 `Dates` {#dates}

1. 톱니바퀴(![](../../assets/gear-icon.png)) 아이콘을 클릭한 다음 대시보드 이름 옆에 있는 를 선택합니다 `!UICONTROL Bulk Edit Reports` 창을 엽니다.

1. 클릭 **[!UICONTROL Change Dates]** 팝업 창에서 클릭합니다.

1. 새 항목 설정 `Start/End Date` 및 `Time Interval`. 이러한 필드를 그대로 둘 수도 있습니다.

1. 클릭 **[!UICONTROL Update Reports]**.

예:

![날짜 변경](../../assets/dates.gif)
