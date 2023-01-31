---
title: 매핑 테이블을 사용하여 데이터 표준화
description: 매핑 테이블을 사용하여 작업하는 방법을 알아봅니다.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# 매핑 테이블을 사용하여 데이터 표준화

그림 설명: 당신은 `Report Builder`, 구축 `Revenue by State` 보고서 세트에 대해 설명합니다. 당신은 영역에 있습니다. 모든 것이 순조롭게 진행되고 있다 `billing state` 보고서를 그룹화하면 다음과 같은 내용이 표시됩니다.

![](../../assets/Messy_State_Segments.png)

## 어떻게 이런 일이 일어날 수 있죠?

안타깝게도, 표준화의 부족은 때때로 보고서를 작성할 때 지저분한 데이터와 두통을 초래할 수 있습니다. 이 예제에서는 고객이 청구 상태 정보를 입력하는 드롭다운 메뉴 또는 표준화된 방법이 없을 수 있습니다. 이로 인해 다양한 값이 생성됩니다. `pa`, `PA`, `penna`, `pennsylvania`, 및 `Pennsylvania` - 이는 확실히 어떤 이상한 결과를 가져올 동일한 주에- `Report Builder`.

데이터를 정리하거나 데이터베이스에 직접 필요한 열을 삽입할 수 있는 기술 리소스가 있을 수 있지만 그렇지 않은 경우 다른 해결 방법이 있습니다. **매핑 테이블**. 매핑 테이블을 사용하면 데이터를 하나의 출력에 매핑하여 복잡한 데이터를 빠르고 쉽게 정리하고 표준화할 수 있습니다.

>[!NOTE]
>
>지원 팀의 도움 없이는 통합 테이블에 대한 매핑 테이블을 만들 수 없습니다. 자세한 내용은 Adobe에 문의하십시오.

## 어떻게 만드나요? {#how}

**데이터 서식 재교육:**

* 스프레드시트에 머리글 행이 있는지 확인합니다.
* 쉼표를 사용하지 마십시오! 이 경우 파일을 업로드할 때 문제가 발생합니다.
* 표준 날짜 형식 사용 `(YYYY-MM-DD HH:MM:SS)` 추가 날짜:
* 백분율을 소수로 입력해야 합니다.
* 선행 또는 후행 0이 올바르게 유지되는지 확인하십시오.

살펴보기 전에 [원시 테이블 데이터 내보내기](../../tutorials/export-raw-data.md). 원시 데이터를 먼저 보면 정리해야 하는 데이터에 대해 가능한 모든 조합을 탐색할 수 있으므로 매핑 테이블에서 모든 것을 포함하도록 할 수 있습니다.

매핑 테이블을 만들려면 다음에 오는 두 개의 열 스프레드시트를 생성해야 합니다 [파일 업로드를 위한 규칙 서식](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

첫 번째 열에서 데이터베이스에 저장된 값을 **각 행에 하나의 값만 사용할 수 있습니다.**. 예, `pa` 및 `PA` 같은 줄에 있을 수 없습니다. 각 입력에는 고유한 행이 있어야 합니다. 예를 보려면 아래를 참조하십시오.

두 번째 열에서 다음 값 입력 **다음과 같습니다.**. 필요한 경우 청구 상태 예 계속 `pa`, `PA`, `Pennsylvania`, 및 `pennsylvania` 그냥 `PA`을 입력하면 `PA` 이 열에서 각 입력 값에 대해 지정합니다.

![](../../assets/Mapping_table_examples.jpg)

## 에서 무엇을 해야 합니까 [!DNL MBI] 사용하려고? {#use}

매핑 테이블 만들기를 마쳤으면 다음을 수행해야 합니다 [파일 업로드](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 변환 [!DNL MBI] 및 [연결된 열 만들기](../../data-analyst/data-warehouse-mgr/calc-column-types.md) 새 필드를 원하는 테이블로 재배치합니다. 파일이 데이터 웨어하우스에 동기화된 후에 이 작업을 수행할 수 있습니다.

이 예제에서는 만든 열을 `mapping_state` 테이블 (`state_input`) `customer_address` 연결된 열을 사용하는 표 이렇게 하면 우리는 깨끗하게 그룹화할 수 있다 `state_input` 열 대신 `state` 열.

을(를) 만들려면 `joined` 열에서 Data Warehouse 관리자에서 해당 필드가 재배치될 테이블로 이동합니다. 이 예제에서는 `customer_address` 테이블.

1. 클릭 **[!UICONTROL Create a Column]**.
1. 선택 `Joined Column` 에서 `Definition` 드롭다운.
1. 열과 다른 이름을 지정합니다. `state` 열에 있는 항목이 없습니다. 같이 가겠습니다 `billing state (mapped)` report builder에서 세그먼트화할 때 사용할 열을 알 수 있습니다.
1. 테이블을 연결하는 데 필요한 경로가 존재하지 않으므로 새 경로를 만들어야 합니다. 클릭 **[!UICONTROL Create new path]**  에서 `Select a table and column` 드롭다운.

   테이블 관계가 무엇인지 또는 기본 키와 외래 키를 올바르게 정의하는 방법을 모를 경우 체크 아웃하십시오 [adobe 튜토리얼](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) 도움이 필요하십니까?

   * 설정 `Many` 그런 다음 필드를 (다시) (으)로 재배치하려는 테이블을 선택합니다 `customer_address`) 및 `Foreign Key` 열 또는 `state` 열이 포함되어 있습니다.
   * 설정 `One` side를 선택하고 `mapping` 테이블 및 `Primary key` 열. 이 경우 `state_input` 열 `mapping_state` 테이블.
   * 다음은 Dell의 경로 모습입니다.

      ![](../../assets/State_Mapping_Path.png)

1. 완료되면 를 클릭합니다 **[!UICONTROL Save]** 경로 생성
1. 저장 후 경로가 즉시 채워지지 않을 수 있습니다. 이렇게 되면 `Path` 상자를 열고 방금 만든 경로를 선택합니다.
1. 클릭 **[!UICONTROL Save]** 열을 만들려면

바로 그거야!

## 이제 어떻게 하죠? {#wrapup}

업데이트 주기가 완료되면 새로 연결된 열을 사용하여 데이터베이스에서 지저분한 열 대신 데이터를 적절하게 세그먼트화할 수 있습니다. 지금 우리의 그룹화 옵션들을 살펴보십시오 - 더 이상 스트레스 사태가 없도록.

![](../../assets/Clean_State_Segments.png)

매핑 테이블은 데이터 웨어하우스에서 일부 지저분한 데이터를 정리할 때 언제든지 편리하게 사용할 수 있습니다. 그러나 매핑 테이블은 다음과 같은 일부 다른 멋진 사용 사례에 사용할 수도 있습니다 [MBI에서 Google Analytics 채널 복제](../data-warehouse-mgr/rep-google-analytics-channels.md).

### 관련

* [테이블 관계 이해 및 평가](../data-warehouse-mgr/table-relationships.md)
* [계산된 열에 대한 경로 만들기/삭제](../data-warehouse-mgr/create-paths-calc-columns.md)
