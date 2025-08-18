---
title: Google Analytics 차트 만들기
description: Google Analytics 데이터에서 차트를 만드는 방법을 알아봅니다.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# [!DNL Google Analytics] 차트 만들기

(정규 표현식 구문 도움말 사용)

[[!DNL Google Analytics] 계정](../../data-analyst/importing-data/integrations/google-analytics.md)을 연결한 후 [!DNL Google Analytics] 데이터로 차트를 만들 수 있습니다.

## [!DNL Google Analytics] 차트 만들기

1. **[!UICONTROL Add Chart** > **Create New Chart]**&#x200B;을(를) 클릭합니다.

1. `Chart Builder`에서 지표를 선택할 때 목록의 아래쪽으로 스크롤하여 [!DNL Google Analytics] 프로필이 포함된 섹션을 찾습니다. 두 번째 지표 드롭다운이 표시됩니다. 여기에서 분석할 지표를 선택할 수 있습니다.

1. 지표를 선택한 후 보려는 `time period`, `interval` 및 데이터 `perspectives`을(를) 선택하여 이 차트를 다른 차트처럼 진행할 수 있습니다.

1. 여기에서 한 가지 주요 차이점은 `√`이(가) 필터에 대해 정규 표현식을 사용한다는 것입니다. 정규 표현식(regex for short)은 검색 패턴을 설명하는 특수 텍스트 문자열입니다. Analytics 정규 표현식에 대한 [[!DNL Google] 안내서](https://support.google.com/analytics/answer/1034324?hl=en)에서 정규 표현식 구문의 예를 참조하십시오.

>[!NOTE]
>
>\ 문자를 사용하여 이스케이프해야 하는 특수 문자는 아래 메타문자뿐입니다.

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
