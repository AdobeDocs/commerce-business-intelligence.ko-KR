---
title: 대시보드에서 차트 벌크 편집
description: ' [!DNL Commerce Intelligence]에서 대량 편집 기능을 사용하는 방법에 대해 알아봅니다.'
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# 대시보드에서 차트 벌크 편집

벌크 편집 기능을 사용하면 대시보드에서 차트 이름과 날짜를 쉽게 변경할 수 있습니다. 예를 들어 특정 대시보드의 모든 차트가 단일 저장소를 참조하고 분기별이 아닌 월별 기준으로 보고하도록 할 수 있습니다. 모든 항목을 수동으로 변경하는 대신 `bulk-editing` 기능을 사용할 수 있도록 하십시오. 이 항목에서는 다음을 사용하는 방법을 배웁니다.

* [&#x200B; [!DNL Find/Replace] 기능](#findreplace)

* [&#x200B; [!DNL Prepend Name] 기능](#prepend)

* [&#x200B; [!DNL Change Dates] 기능](#dates)

*이 변경 내용을 영구적으로 적용해야 하는지 확인하십시오.* 그렇지 않으면 대시보드를 복제한 다음 새 대시보드에서 날짜를 변경하는 것이 좋습니다. 이를 통해 필요한 변경 사항을 유지하면서 원래 대시보드를 유지할 수 있습니다.

>[!NOTE]
>
>많은 보고서를 변경하는 경우 업데이트 프로세스에 약간의 시간이 걸릴 수 있습니다.

## [!DNL Find/Replace] 사용 중 {#findreplace}

1. 대시보드 이름 옆에 있는 톱니바퀴 아이콘(![톱니바퀴 아이콘](../../assets/gear-icon.png))을 클릭한 다음 [!UICONTROL Bulk Edit Reports] 창을 클릭합니다.

1. 팝업에서 **[!UICONTROL Chart Title Find and Replace]**&#x200B;을(를) 클릭합니다.

1. `Chart Title Find` 필드에 찾을 단어 또는 문자를 입력합니다.

1. `Replace With` 필드에 `Find` 필드의 내용을 대체할 단어 또는 문자를 입력합니다.

1. **[!UICONTROL Update Reports]**&#x200B;을(를) 클릭합니다.

예:

![일괄 편집](../../assets/bulk_edit.gif)

## `Chart Names` 앞에 추가 {#prepend}

1. 대시보드 이름 옆에 있는 톱니바퀴 아이콘(![톱니바퀴 아이콘](../../assets/gear-icon.png))을 클릭한 다음 [!UICONTROL Bulk Edit Reports] 창을 클릭합니다.

1. 팝업에서 **[!UICONTROL Prepend Report Names]**&#x200B;을(를) 클릭합니다.

1. 차트 앞에 추가할 단어 또는 문자를 입력합니다.

1. **[!UICONTROL Update Reports]**&#x200B;을(를) 클릭합니다.

예:

![prepend](../../assets/prepend.gif)

## `Dates` 변경 중 {#dates}

1. 대시보드 이름 옆에 있는 톱니바퀴 아이콘(![톱니바퀴 아이콘](../../assets/gear-icon.png))을 클릭한 다음 [!UICONTROL Bulk Edit Reports] 창을 선택합니다.

1. 팝업 창에서 **[!UICONTROL Change Dates]**&#x200B;을(를) 클릭합니다.

1. 새 `Start/End Date` 및 `Time Interval`을(를) 설정합니다. 이러한 필드는 변경하지 않고 그대로 둘 수도 있습니다.

1. **[!UICONTROL Update Reports]**&#x200B;을(를) 클릭합니다.

예:

![날짜 변경](../../assets/dates.gif)
