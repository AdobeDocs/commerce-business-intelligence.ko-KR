---
title: Google Analytics 차트 만들기
description: Google Analytics 데이터로 차트를 만드는 방법에 대해 알아봅니다.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 만들기 [!DNL Google Analytics] 차트

(정규 표현식 구문 도움말 사용)

다음을 연결한 후 [[!DNL Google Analytics] account](../../data-analyst/importing-data/integrations/google-analytics.md)에서 차트를 생성할 수 있습니다. [!DNL Google Analytics] 데이터.

## 만들기 [!DNL Google Analytics] 차트

1. 클릭 **[!UICONTROL Add Chart** > **Create New Chart]**.

1. 에서 지표 선택 시 `Chart Builder`를 클릭하고 목록의 맨 아래로 스크롤하여 [!DNL Google Analytics] 프로필. 두 번째 지표 드롭다운이 표시됩니다. 여기에서 분석할 지표를 선택할 수 있습니다.

1. 지표를 선택한 후 다음을 선택하여 다른 차트처럼 이 차트를 진행할 수 있습니다. `time period`, `interval`, 및 데이터 `perspectives` 보고 싶으신 거군요

1. 여기서 한 가지 주요한 차이점은 `√` 필터에는 정규 표현식을 사용합니다. 정규 표현식(regex for short)은 검색 패턴을 설명하는 특수 텍스트 문자열입니다. 다음에서 정규 표현식 구문의 예를 참조하십시오. [[!DNL Google] analytics 정규 표현식에 대한 안내서](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>\ 문자를 사용하여 이스케이프해야 하는 특수 문자는 아래 메타문자뿐입니다.

|  |  |  |  |  |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
