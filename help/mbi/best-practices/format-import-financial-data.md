---
title: 재무 데이터 서식 지정 및 가져오기
description: 재무 데이터의 형식을 지정하고 가져오는 방법을 알아봅니다.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 재무 데이터 형식 지정 및 가져오기

이 항목에서는 [!DNL Adobe Commerce Intelligence]에서 분석할 재무 데이터를 가져오는 가장 좋은 방법에 대해 설명합니다.

2차원의 교차 탭 데이터 테이블은 종종 재무 데이터에 사용되는 형식입니다. 열과 행 모두에서 레이블로 분류된 값을 사용하는 경우 이러한 유형의 레이아웃은 사람의 눈과 스프레드시트 도구로 쉽게 볼 수 있지만 데이터베이스에 익숙하지 않습니다.

![](../../mbi/assets/crosstab.png)

[!DNL Commerce Intelligence]에서 이 데이터를 가져오고 분석하려면 테이블을 1차원 목록으로 병합해야 합니다. 병합되면 각 데이터 값은 모두 단일 행에 있는 여러 레이블로 분류됩니다. 여기서 각 행은 고유하거나, 고유 식별자를 갖게 됩니다(예: 기본 키 열).

![](../../mbi/assets/flattened.png)

## 가져오기용 Excel 파일 서식 지정

[!DNL Excel] 피벗 테이블을 사용하여 2차원 테이블을 병합하려면 다음을 수행합니다.

1. 2차원 데이터 테이블이 있는 파일을 엽니다.
1. 피벗 테이블 마법사를 엽니다. [!DNL Windows]에서 바로 가기는 `Alt-D`입니다. [!DNL Mac OS]에서 `Command-Option-P`을(를) 입력하십시오.
1. **[!UICONTROL Multiple consolidated ranges]**&#x200B;을(를) 선택하고 **[!UICONTROL Next]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL I will create the page fields]**&#x200B;을(를) 선택하고 **[!UICONTROL Next]**&#x200B;을(를) 클릭합니다.
1. 레이블을 포함하여 2차원 테이블의 전체 데이터 세트를 선택합니다. 원하는 페이지 필드 수에 대해 `0`이(가) 선택되어 있는지 확인하고 **[!UICONTROL Next]**&#x200B;을(를) 클릭합니다.
1. 새 시트에 피벗 테이블을 만들고 **[!UICONTROL Finish]**&#x200B;을(를) 클릭합니다.
1. 필드 목록에서 열 및 행 필드의 선택을 취소합니다.
1. 결과 숫자 값을 두 번 클릭하여 병합된 소스 데이터를 새 시트에 표시합니다.
   ![](../../mbi/assets/pivot-table-double-click.png)
1. `CSV` 파일로 저장합니다.

## 요약

데이터 테이블이 목록 형식으로 변환되어 원래 정보가 모두 보존되므로 분석을 위해 [가져온 위치 [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md)로 가져올 수 있습니다.
