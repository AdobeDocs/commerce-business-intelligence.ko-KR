---
title: 파일 업로더 사용
description: 모든 데이터를 단일 Data Warehouse에 넣는 방법을 알아봅니다.
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 0%

---

# 파일 업로더 사용

>[!NOTE]
>
>[관리자 권한](../../../administrator/user-management/user-management.md)이 필요합니다.

[!DNL Adobe Commerce Intelligence]은(는) 시각화 기능 때문만이 아니라 모든 데이터를 단일 Data Warehouse에 넣을 수 있는 기능을 제공하므로 강력한 기능입니다. 데이터베이스 및 통합 외부에 있는 데이터도 Data Warehouse 관리자의 [파일 업로드] 도구를 사용하여 [!DNL Commerce Intelligence](으)로 가져올 수 있습니다.

광고 캠페인을 예로 사용하십시오. 온라인 및 오프라인 캠페인을 모두 실행하는 경우 온라인 통합의 데이터만 분석하는 경우에는 전체 상황을 파악할 수 없습니다. 오프라인 캠페인 데이터가 포함된 스프레드시트를 업로드하면 두 데이터 세트를 모두 분석하고 캠페인 성과를 보다 강력하게 이해할 수 있습니다.

## 제한 사항 및 요구 사항 {#require}

1. **파일 업로드에 대해 지원되는 형식은 `CSV` 또는`comma separated values`**&#x200B;뿐입니다. Excel에서 작업하는 경우 다른 이름으로 저장 기능을 사용하여 파일을 `.csv` 형식으로 저장할 수 있습니다.
1. **`CSV`개 파일은`UTF-8 encoding`**&#x200B;을(를) 사용해야 합니다. 대부분의 경우, 이것은 문제가 아닙니다. 파일을 업로드하는 동안 이 오류가 발생하면 [이 지원 문서를 참조하십시오](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html).
1. **파일은 100MB**&#x200B;보다 클 수 없습니다. 파일이 이보다 큰 경우 테이블을 청크로 분리하여 개별 파일로 저장합니다. 초기 파일이 로드된 후 데이터를 추가할 수 있습니다.
1. **모든 테이블에`primary key`**&#x200B;이(가) 있어야 합니다. 테이블에 `primary key` 또는 테이블의 각 행에 대한 고유 식별자로 사용할 수 있는 열이 하나 이상 있어야 합니다. `primary key`(으)로 지정된 모든 열은 *절대*&#x200B;이(가) 될 수 있습니다. `primary key`은(는) 각 행에 숫자를 제공하는 열을 추가하는 것만큼 간단하거나 고유한 값의 열을 만들기 위해 연결된 두 개의 열일 수 있습니다(예: `campaign name` 및 `date`).

   열(또는 열)이 고유한 것으로 지정되었지만 중복되는 행이 있는 경우 중복 행을 가져오지 않습니다.

## 업로드할 데이터 서식 지정 {#formatting}

데이터를 [!DNL Commerce Intelligence]에 업로드하려면 먼저 이 섹션의 지침에 따라 형식이 지정되었는지 확인하십시오.

### 머리글 행 {#header}

열 레이블을 지정하고 올바르게 가져오려면 스프레드시트의 첫 행이 각 열의 데이터를 설명하는 헤더인지 확인합니다.

열 이름은 고유해야 하며 문자, 숫자, 공백 및 `$ % # /` 기호만 포함해야 합니다. 열 이름에 쉼표가 포함되어 있으면 파일을 업로드할 때 두 개의 열로 분할됩니다. Adobe 또한 업데이트 속도를 최적화하려면 파일에 85개 이하의 열이 있는 것이 좋습니다.

### 쉼표가 있는 데이터 {#commas}

파일은 `CSV` 형식이어야 하므로 쉼표를 사용하면 데이터 업로드에 문제가 발생할 수 있습니다. `CSV` 파일은 쉼표를 사용하여 새 값을 나타내므로 `Campaigns`, `August`과(와) 같은 이름의 열은 하나가 아닌 두 개의 열(`Campaigns` 및 `August`)로 읽혀 모든 데이터를 한 행으로 이동합니다. Adobe은 가능한 한 쉼표를 사용하지 않는 것을 권장합니다. 업데이트가 완료되면 `Data Preview`을(를) 사용하여 데이터가 올바르게 표시되는지 확인할 수 있습니다.

### 날짜

날짜가 포함된 모든 데이터 집합은 [표준 날짜 형식](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` 또는 `MM/DD/YYYY`을(를) 사용해야 합니다.

### 특수 문자

일부 특수 문자는 허용되지 않습니다. 예를 들어 파이프 기호 `& # 1 2 4`은(는) 열을 만드는 것으로 해석되며 파일을 업로드할 때 오류가 발생합니다.

### 십진수

통화 값에는 데이터 형식 `Decimal Number`이(가) 선택되어 있어야 하며 이러한 열은 Data Warehouse에서 소수점 이하 두 자리로 자동으로 반올림됩니다. 소수점 이하 자릿수를 반올림하거나 이보다 높은 정밀도를 유지하려면 `Non-Currency Decimal Number` 데이터 형식을 선택해야 합니다.

### 백분율

백분율을 소수 자릿수로 입력해야 합니다. For example:

| **오른쪽:** | **잘못됨:** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style="table-layout:auto"}

### 선행 및/또는 후행 0이 있는 값 {#zeroes}

ZIP 코드 및 ID와 같은 파일의 일부 값은 0으로 시작되거나 끝날 수 있습니다. 0이 제대로 유지되고 업로드되도록 하려면 서식 유형(예: [숫자에서 텍스트로](https://support.microsoft.com/en-us/office/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4?ui=en-us&amp;rs=en-us&amp;ad=us))을 변경하거나 숫자 서식을 적용할 수 있습니다.

숫자 서식을 변경하는 방법의 예로 `US ZIP codes`을(를) 사용하십시오. [!DNL Excel]에서 `ZIP codes`과(와) [숫자 형식을 변경](https://support.microsoft.com/en-us/office/display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d?ui=en-us&amp;rs=en-us&amp;ad=us)하여 `ZIP code`을(를) 포함하는 열을 강조 표시합니다. 사용자 지정 숫자 형식을 선택할 수도 있고 `Type` 창에서 `00000`을(를) 입력합니다. 일부 코드는 `00000` 형식으로 지정되고 다른 코드는 `00000-0000`인 경우 이 메서드가 문제를 일으킬 수 있습니다.

`Type`은(는) ID와 같은 다른 데이터 형식](https://support.microsoft.com/en-us/office/keeping-leading-zeros-and-large-numbers-1bf7b935-36e1-4985-842f-5dfa51f85fe7?correlationid=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-us&amp;rs=en-us&amp;ad=us)을(를) 수용하도록 형식이 다르게 [될 수 있습니다. 예를 들어 `ID`이(가) 9자리 길이이면 `Type`은(는) `000000000` 또는 `000-000-000`일 수 있습니다. `123456`이(가) `000-123-456`(으)로 변경됩니다.

[!DNL Google Docs] 및 [!DNL Apple Numbers] 리소스의 경우 이 페이지 하단에 있는 [관련](#related) 목록을 참조하십시오.

## 데이터 업로드 중 {#uploading}

스프레드시트의 형식이 올바르고 [!DNL Commerce Intelligence]에 적합하므로 Data Warehouse에 추가하십시오.

1. 시작하려면 **[!UICONTROL Data** > **File Uploads]**(으)로 이동합니다.

1. **[!UICONTROL Upload to New Table]** 탭을 클릭합니다.

1. **[!UICONTROL Choose File]**&#x200B;을(를) 클릭하고 파일을 선택합니다. 업로드를 시작하려면 **[!UICONTROL Open]**&#x200B;을(를) 클릭하십시오.

   업로드가 완료되면 파일에 있는 [!DNL Commerce Intelligence] 열 목록이 표시됩니다.

1. 열 이름과 데이터 유형이 올바른지 확인합니다. 특히 날짜 열이 숫자가 아닌 날짜로 읽히는지 확인합니다.

   >[!NOTE]
   >
   >`datatype`은(는) 중요하므로 이 단계를 건너뛰지 마십시오!

1. 키 아이콘 아래에 있는 확인란을 사용하여 테이블의 `primary key`을(를) 구성하는 열을 선택합니다.

1. 테이블 이름을 지정합니다.

1. **[!UICONTROL Save Table]**&#x200B;을(를) 클릭합니다.

*성공!테이블을 저장한 후 화면 맨 위에* 메시지가 나타납니다.

시각화가 필요한 경우 전체 프로세스를 살펴보십시오.

![](../../../assets/fileupload.gif)

업로드된 테이블은 Data Warehouse 관리자에서 테이블 목록(모든 테이블 및 동기화된 테이블 옵션 모두)의 **파일 업로드** 섹션 아래에 표시됩니다.

![](../../../assets/upload-tables.png)

## 기존 테이블에 데이터 업데이트 또는 추가 {#appending}

이미 업로드한 파일에 추가할 새로운 데이터가 있습니까? 문제 없음 - [!DNL Commerce Intelligence]에서 데이터를 쉽게 업데이트하고 추가할 수 있습니다.

1. 시작하려면 **[!UICONTROL Manage Data** > **File Uploads]**(으)로 이동합니다.

1. 기존 테이블에 대한 **[!UICONTROL Edit/Upload `.csv`]** 탭을 클릭합니다.

1. 드롭다운에서 업데이트하거나 추가할 테이블의 이름을 클릭합니다.

1. 드롭다운을 사용하여 중복 행을 처리하는 옵션을 선택합니다.

   | 옵션 | 설명 |
   |---|---|
   | `Overwrite old row with new row` | 기존 테이블과 새 파일 모두에서 행에 동일한 기본 키가 있는 경우 기존 데이터를 새 데이터로 덮어씁니다. 시간이 지남에 따라 값이 변경되는 열(예: 상태 열)에 사용하는 방법입니다. 기존 데이터를 덮어쓰고 새 데이터로 업데이트합니다. 기존 표에 기본 키가 없는 행은 새 행으로 추가됩니다. |
   | `Retain old row; discard new row` | 이렇게 하면 기존 테이블과 새 파일 모두에서 행에 동일한 기본 키가 있는 경우 새 데이터가 무시됩니다. |
   | `Purge all existing rows first and ignore duplicate keys within the file` | 이렇게 하면 기존 데이터가 삭제되고 파일의 새 데이터로 바뀝니다. 기존 표에 데이터가 필요하지 않은 경우에만 이 옵션을 사용하십시오. |

1. **[!UICONTROL Choose File]**&#x200B;을(를) 클릭하고 파일을 선택합니다.

1. 업로드를 시작하려면 **[!UICONTROL Open]**&#x200B;을(를) 클릭하십시오.

   업로드가 완료되면 [!DNL Commerce Intelligence]이(가) 파일의 데이터 구조를 확인합니다. *성공!테이블을 저장한 후 화면 맨 위에* 메시지가 나타납니다.

## 데이터 가용성 {#availability}

파일 업로드의 데이터는 계산된 열과 마찬가지로 다음 업데이트 주기가 완료된 후에 사용할 수 있습니다. 파일을 업로드하는 동안 업데이트가 진행 중이었다면 다음 업데이트 이후에나 데이터를 사용할 수 있습니다. 업데이트 주기가 완료되면 Data Warehouse의 `Data Preview` 탭으로 이동하여 파일이 올바르게 업로드되고 데이터가 예상대로 표시되는지 확인할 수 있습니다.

## 요약 {#wrapup}

이 항목에서는 데이터 가져오기를 사용하는 기본 사항만 다루지만 보다 고급 작업을 수행할 수도 있습니다. 금융, 전자 상거래, 광고 지출 및 기타 유형의 데이터 형식 지정 및 가져오기에 대한 지침은 관련 문서를 확인하십시오.

또한 파일 업로드는 데이터를 [!DNL Commerce Intelligence](으)로 가져오는 유일한 방법이 아닙니다. [데이터 가져오기 API](https://developer.adobe.com/commerce/services/reporting/import-api/) 함수를 사용하면 임의의 데이터를 [!DNL Commerce Intelligence] Data Warehouse에 푸시할 수 있습니다.

## 관련 항목 {#related}

* [재무 데이터 서식 지정 및 가져오기](../../../best-practices/format-import-financial-data.md)
* [오프라인/기타 광고 지출 데이터 가져오기](../connecting-data/import-offline-ad-data.md)
* [[!DNL Google ECommerce]개의 데이터가 필요합니다.](../integrations/google-ecommerce-data.md)

## 타사 리소스

* [숫자 데이터 서식 가이드](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] 데이터 서식 가이드](https://support.google.com/docs/answer/56470?hl=en)
