---
title: 재무 데이터 형식 지정 및 가져오기
description: 재무 데이터의 형식을 지정하고 가져오는 방법을 알아봅니다.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# 재무 데이터 형식 지정 및 가져오기

이 항목에서는 분석을 위해 재무 데이터를 가져오는 가장 좋은 방법을 설명합니다. [!DNL MBI].

2차원 교차 탭 데이터 테이블은 재무 데이터에 사용되는 형식입니다. 열과 행 모두에서 레이블로 값을 분류하면 이러한 유형의 레이아웃은 사람의 눈과 스프레드시트 도구를 사용하여 쉽게 볼 수 있지만 데이터베이스에는 적합하지 않습니다.

![](../../mbi/assets/crosstab.png)

에서 이 데이터를 가져오고 분석하려면 [!DNL MBI]를 채울 때는 표를 1차원 목록으로 병합해야 합니다. 병합되면 각 데이터 값은 단일 행에 있는 여러 레이블로 분류됩니다. 이 레이블은 각각 고유하거나 기본 키 열과 같이 고유한 식별자가 있습니다.

![](../../mbi/assets/flattened.png)

## 가져올 Excel 파일 형식 지정

Excel 피벗 테이블을 사용하여 2차원 테이블을 병합하려면 다음을 수행하십시오.

1. 2차원 데이터 테이블로 파일을 엽니다.
1. 피벗 테이블 마법사를 엽니다. Windows에서는 바로 가기가 `Alt-D`. Mac OSX에서 `Command-Option-P`.
1. 선택 **[!UICONTROL Multiple consolidated ranges]** 을(를) 클릭합니다. **[!UICONTROL Next]**.
1. 선택 **[!UICONTROL I will create the page fields]** 을(를) 클릭합니다. **[!UICONTROL Next]**.
1. 레이블을 포함하여 2차원 테이블에서 전체 데이터 세트를 선택합니다. 확인 `0` 원하는 페이지 필드 수에 대해 을 선택하고 을(를) 클릭합니다. **[!UICONTROL Next]**.
1. 새 시트에 피벗 테이블을 만들고 **[!UICONTROL Finish]**.
1. 필드 목록에서 열 및 행 필드를 선택 취소합니다.
1. 결과 숫자 값을 두 번 클릭하여 새 시트에 플랫 소스 데이터를 표시합니다.
   ![](../../mbi/assets/pivot-table-double-click.png)
1. 다른 이름으로 저장 `CSV` 파일.

바로 그거야! 데이터 테이블이 모든 원본 정보를 보존하여 목록 형식으로 변환되었으므로 이제 [가져오기 대상 [!DNL MBI]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) 참조하십시오.
