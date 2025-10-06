---
title: 매핑 테이블을 사용하여 데이터 표준화
description: 매핑 테이블을 사용하여 작업하는 방법을 알아봅니다.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# 매핑 테이블을 사용하여 데이터 표준화

`Report Builder`에서 `Revenue by State` 보고서를 작성하는 중이라고 가정해 보십시오. 보고서에 `billing state` 그룹화를 추가하려고 할 때까지 모든 것이 잘 진행되고 있습니다. 다음 내용이 표시됩니다.

![이름이 일치하지 않는 지저분한 상태 세그먼트를 표시하는 차트](../../assets/Messy_State_Segments.png)

## 어떻게 이런 일이 일어날 수 있죠?

안타깝게도, 표준화의 부족은 보고서를 작성할 때 때때로 지저분한 데이터와 골칫거리로 이어질 수 있습니다. 이 예에는 고객이 청구 상태 정보를 입력할 수 있는 드롭다운 메뉴 또는 표준화된 방법이 없을 수 있습니다. 이렇게 하면 동일한 상태에 대해 다양한 값(`pa`, `PA`, `penna`, `pennsylvania` 및 `Pennsylvania`)이 나타나며, 이로 인해 `Report Builder`에 이상한 결과가 발생합니다.

데이터를 정리하거나 필요한 열을 데이터베이스에 직접 삽입하는 데 도움이 되는 기술 리소스가 있을 수 있습니다. 그렇지 않으면 다른 해결 방법이 있습니다. **매핑 테이블**. 매핑 테이블을 사용하면 데이터를 단일 출력에 매핑하여 지저분한 데이터를 빠르고 쉽게 정리하고 표준화할 수 있습니다.

>[!NOTE]
>
>Adobe 지원 팀의 도움이 없으면 통합 테이블에 대한 매핑 테이블을 만들 수 없습니다.

## 만들려면 어떻게 해야 합니까? {#how}

**데이터 서식 새로 고침:**

* 스프레드시트에 머리글 행이 있는지 확인합니다.
* 쉼표를 사용하지 마십시오! 이 경우 파일을 업로드할 때 문제가 발생합니다.
* 날짜에는 표준 날짜 형식 `(YYYY-MM-DD HH:MM:SS)`을(를) 사용하십시오.
* 백분율을 소수 자릿수로 입력해야 합니다.
* 선행 또는 후행 0이 제대로 유지되는지 확인합니다.

시작하기 전에 Adobe에서는 [원시 테이블 데이터를 내보내기](../../tutorials/export-raw-data.md)할 것을 권장합니다. 원시 데이터를 먼저 확인하면 정리해야 하는 데이터에 대해 가능한 모든 조합을 탐색할 수 있으므로 매핑 테이블이 모든 항목을 포함하도록 할 수 있습니다.

매핑 테이블을 만들려면 [파일 업로드를 위한 서식 지정 규칙](../../data-analyst/importing-data/connecting-data/using-file-uploader.md)을 따르는 2열 스프레드시트를 만들어야 합니다.

첫 번째 열에서 **각 행에 있는 하나의 값만**&#x200B;을 사용하여 데이터베이스에 저장된 값을 입력합니다. 예를 들어 `pa`과(와) `PA`은(는) 같은 줄에 있을 수 없습니다. 각 입력에 고유한 행이 있어야 합니다. 예제는 아래를 참조하십시오.

두 번째 열에 **이(가) 있어야 하는 값**&#x200B;을(를) 입력하십시오. 청구 상태 예를 계속 진행하여 `pa`, `PA`, `Pennsylvania` 및 `pennsylvania`을(를) 간단히 `PA`하려면 각 입력 값에 대해 이 열에 `PA`을(를) 입력합니다.

![원래 값과 표준화된 값을 보여 주는 예제 매핑 테이블](../../assets/Mapping_table_examples.jpg)

## [!DNL Commerce Intelligence]에서 사용하려면 어떻게 해야 합니까? {#use}

매핑 테이블을 만들었으면 [파일을 &#x200B;](../../data-analyst/importing-data/connecting-data/using-file-uploader.md)에 업로드[!DNL Commerce Intelligence]하고 [조인된 열을 만들기](../../data-analyst/data-warehouse-mgr/calc-column-types.md)하여 새 필드를 원하는 테이블로 이동해야 합니다. 파일이 Data Warehouse에 동기화된 후 이 작업을 수행할 수 있습니다.

이 예제에서는 조인된 열을 사용하여 `mapping_state` 테이블(`state_input`)에서 만든 열을 `customer_address` 테이블로 이동합니다. 이렇게 하면 보고서의 `state_input` 열 대신 `state` 열을 기준으로 그룹화할 수 있습니다.

`joined` 열을 만들려면 Data Warehouse 관리자에서 필드를 재배치할 테이블로 이동합니다. 이 예제에서는 `customer_address` 테이블이 됩니다.

1. **[!UICONTROL Create a Column]**&#x200B;을(를) 클릭합니다.
1. `Joined Column` 드롭다운에서 `Definition`을(를) 선택합니다.
1. 열에 데이터베이스의 `state` 열과 구별되는 이름을 지정하십시오. Report Builder에서 세그먼트화할 때 사용할 열을 알 수 있도록 열 이름을 `billing state (mapped)`로 지정합니다.
1. 테이블을 연결하는 데 필요한 경로가 없으므로 경로를 생성해야 합니다. **[!UICONTROL Create new path]** 드롭다운에서 `Select a table and column`을(를) 클릭합니다.

   테이블 관계가 무엇인지 또는 기본 키와 외래 키를 제대로 정의하는 방법을 잘 모를 경우 [자습서](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)에서 도움말을 확인하십시오.

   * `Many`측에서 필드를 재배치할 테이블을 선택합니다(다시 말해 `customer_address`임). 이 예제에서는 `Foreign Key` 열 또는 `state` 열을 선택합니다.
   * `One`측에서 `mapping` 테이블 및 `Primary key` 열을 선택합니다. 이 경우 `state_input` 테이블에서 `mapping_state` 열을 선택합니다.
   * 다음은 경로의 모양입니다.

     ![상태 매핑 계산 경로를 표시하는 Data Warehouse 관리자](../../assets/State_Mapping_Path.png)

1. 완료되면 **[!UICONTROL Save]**&#x200B;을(를) 클릭하여 경로를 만듭니다.
1. 저장 후 경로가 바로 채워지지 않을 수 있습니다. 이 경우 `Path` 상자를 클릭하고 만든 경로를 선택하십시오.
1. 열을 만들려면 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

## 이제 어떻게 해야 합니까? {#wrapup}

업데이트 주기가 완료되면 새로 결합된 열을 사용하여 데이터베이스의 지저분한 열 대신 데이터를 적절하게 세그먼트화할 수 있습니다. 이제 그룹화 옵션을 살펴보십시오. 더 이상 스트레스를 주지 않습니다.

![표준화 후 클린 상태 세그먼트를 표시하는 차트](../../assets/Clean_State_Segments.png)

매핑 테이블은 Data Warehouse에서 잠재적으로 지저분한 데이터를 정리할 때 언제든지 유용합니다. 그러나 매핑 테이블은 [복제 [!DNL Google Analytics channels] in [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md)와 같은 멋진 다른 사용 사례에도 사용할 수 있습니다.

### 관련 항목

* [테이블 관계 이해 및 평가](../data-warehouse-mgr/table-relationships.md)
* [계산된 열에 대한 경로 생성/삭제](../data-warehouse-mgr/create-paths-calc-columns.md)
