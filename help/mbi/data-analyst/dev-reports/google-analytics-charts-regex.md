---
title: Google Analytics 차트 만들기
description: Google Analytics 데이터에서 차트를 만드는 방법을 알아봅니다.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# 만들기 [!DNL Google Analytics] 차트

(regex 구문 도움말 사용)

연결 후 [[!DNL Google Analytics] account](../../data-analyst/importing-data/integrations/google-analytics.md)를 사용하여 차트를 만들 수 있습니다 [!DNL Google Analytics] 데이터.

## 만들기 [!DNL Google Analytics] 차트

1. 클릭 **[!UICONTROL Add Chart** > **Create New Chart]**.

1. 에서 지표를 선택할 때 `Chart Builder`를 목록의 맨 아래로 스크롤하여 [!DNL Google Analytics] 프로필. 두 번째 지표 드롭다운이 표시됩니다. 여기에서 분석할 지표를 선택할 수 있습니다.

1. 지표를 선택한 후 을(를) 선택하여 다른 차트처럼 이 차트를 계속 진행할 수 있습니다. `time period`, `interval`, 및 데이터 `perspectives` 보고 싶은 거

1. 여기서 가장 큰 차이점은 `√` 필터에 정규 표현식을 사용합니다. 정규 표현식(약어의 regex)은 검색 패턴을 설명하는 특수 텍스트 문자열입니다. 에서 regex 구문의 예를 참조하십시오. [[!DNL Google] analytics 정규 표현식에 대한 안내서](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>\ 문자를 사용하여 이스케이프해야 하는 유일한 특수 문자는 아래 메타문자입니다.

|  |  |  |  |  |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style=&quot;table-layout:auto&quot;}
