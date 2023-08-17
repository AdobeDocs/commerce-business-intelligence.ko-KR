---
title: 원시 데이터 내보내기
description: 에서 레코드를 내보내는 방법 알아보기 [!DNL Commerce Intelligence] Data Warehouse을 통해 대시보드를 구동하는 항목을 자세히 살펴볼 수 있습니다.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# 원시 데이터 내보내기

원시 데이터 내보내기를 사용하면 Data Warehouse에서 레코드를 내보내 대시보드를 구동하는 항목을 자세히 살펴볼 수 있습니다. 또한 원시 데이터 내보내기가 도움이 될 수 있습니다 [정확한 데이터 불일치](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

원시 데이터 내보내기는 관련 지표의 정규화 취소 및 사전 합계를 통해 생성된 추가 열 및 차원에 대한 액세스를 제공합니다. 예를 들어, `User's first order date` 는 의 각 사용자에 대해 내보낼 수 있는 차원입니다 [!DNL Commerce Intelligence]를 설정하는 경우, 데이터베이스에서 사용하지 못할 수도 있습니다.

이 튜토리얼에서는 다음 내용을 다룹니다.

* [내보낼 데이터 선택](#select)
* [내보내기 다운로드(](#download)
* [내역 내보내기 액세스](#historical)

## 1단계: 내보낼 데이터 선택 {#select}

에서 원시 데이터를 내보낼 수 있는 방법에는 두 가지가 있습니다 [!DNL Commerce Intelligence]:

1. 차트 수준에서
1. 테이블 수준에서

### 의 테이블 수준에서 내보내기 [!UICONTROL Manage Data] 탭

에서 테이블을 내보내려면 [!UICONTROL Manage Data] 탭, 다음이 필요합니다. [관리자](../administrator/user-management/user-management.md) 사용 권한.

1. 클릭 **[!UICONTROL Manage Data** > **&#x200B;데이터 내보내기&#x200B;**> **원시 데이터 내보내기]**.
1. 다음 항목이 표시됨: `Export List` 최근에 생성된 데이터 내보내기(있는 경우) 클릭 **[!UICONTROL Add Export]** 내보내기를 만들려면.
1. 다음 `New Raw Data Export` 대화 상자가 표시됩니다. 여기에서 열 및 필터를 선택하거나 선택 취소하여 내보내기를 사용자 지정할 수 있습니다.

   * `Table` - `Table` 필드는 데이터를 내보낼 테이블을 선택합니다. 기본적으로 탐색한 테이블이 표시됩니다.
   * `Export Name` - 이 필드에 내보내기의 이름을 입력합니다. For example: `Philadelphia - Daily Revenue`.
   * `Available Columns` - 이 필드에는 익스포트에 포함할 수 있는 데이터베이스의 열(차원)이 나열됩니다. 열을 추가하려면 해당 이름을 클릭합니다.
   * `Selected Columns` - 이 필드에는 현재 내보내기에 포함된 열(차원)이 나열됩니다. 열을 제거하려면 열 이름을 클릭합니다.
   * `Filter` - 이 섹션에는 내보내기에 현재 적용된 필터가 나열됩니다. 이러한 필터는 변경할 수 있습니다. 특정 데이터 세트를 내보내기 위해 새 필터를 추가할 수도 있습니다.
   * 완료되면 다음을 클릭하십시오. **[!UICONTROL Export Data]**.

### 대시보드에서 차트 수준에서 내보내기

1. 차트의 오른쪽 위 모서리에 있는 톱니바퀴 아이콘을 클릭합니다.

1. 선택 `Raw Export` 드롭다운에서 다음을 표시합니다. `Raw Export` 대화 상자.

1. 내보내기를 사용자 지정하려면 `table`, `columns`, 및 `filters` 포함 또는 제외할 수 있습니다. 이 모듈의 필드에 대한 자세한 내용은 이전 섹션을 참조하십시오.

   >[!NOTE]
   >
   >에 표시되는 테이블 `Table` 필드는 기본적으로 차트를 구동하는 테이블입니다.

1. 완료되면 다음을 클릭하십시오. **[!UICONTROL Export Data]**.

차트 수준에서 전체 프로세스를 살펴봅니다.

![](../assets/Chart-level_export.gif)

## 2단계: 내보내기 다운로드 {#download}

내보내기에서 선택을 완료한 후 바로 처리가 시작됩니다. `Raw Data Export` 대화 상자. 일부 내보내기의 크기가 클 수 있으므로 1,000만 행으로 제한되고 실행하는 데 시간이 다소 걸릴 수 있습니다.

내보내기가 준비되었는지 확인하려면 **[!UICONTROL Raw Data Exports]** 을 클릭합니다. 클릭 **[!UICONTROL Download]** 압축 파일을 다운로드하려면 `.csv` 내보내기의 파일입니다.

![](../assets/Downloading_export.gif)

## 3단계: 내역 내보내기 액세스 {#historical}

이전 내보내기를 보려면 **[!UICONTROL Raw Data Export]** 화면의 오른쪽 상단에 있습니다. 보류 중인 보고서와 완료된 보고서는 최대 7일 동안 액세스할 수 있습니다.
