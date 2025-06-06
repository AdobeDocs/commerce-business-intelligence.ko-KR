---
title: 보고서 사용
description: 보고서 데이터를 사용하는 방법을 알아봅니다.
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# 보고서 사용

[!DNL Adobe Commerce Intelligence]의 보고서를 사용하여 지난해와 비교하여 이번 달 매출을 확인하고 싶은지 또는 최신 [!DNL Google AdWords] 캠페인에 대한 획득 비용을 알고 싶은지 등 비즈니스 질문에 답변해 보십시오.

질문에서 대답으로 이어지는 그 길은 정확히 어떤 모습일까요?

이 프로세스를 시각화하는 데 도움이 되도록 해당 경로가 아래에 매핑됩니다. 이 항목에서는 분석 질문에 접근하는 방법과 필요한 데이터를 가져오는 데 필요한 백엔드 로지스틱스에 대해 설명합니다.

## 질문으로 시작

고객 만족도 향상부터 공급비 절감에 이르기까지 비즈니스를 개선하기 위해 끊임없이 질문을 던지고 있다는 것을 알고 있습니다. 질문을 해석하여 의사 결정을 유도하는 데 도움이 되는 분석에 집중합니다.

이 예에서는 다음 질문에 답하려고 한다고 가정합니다.

* 신규 등록자는 얼마나 빠르게 전환합니까?

## 측정 식별

질문에 답하는 데 도움이 될 수 있는 분석 및 측정 목록을 식별할 때입니다. 이 예에서는 다음 지표에 중점을 둡니다.

* 사용당 등록에서 첫 번째 구매 날짜까지의 평균 시간.

이렇게 하면 등록 날짜와 사용자의 첫 번째 구매 날짜 사이에 경과된 평균 시간이 표시되고 전환 단계의 이 마지막 단계에서 사용자가 어떻게 행동하는지에 대한 아이디어가 제공됩니다.

## 데이터 찾기

무엇을 측정할지 이해하는 것은 우리에게 그곳의 한 부분만을 가져다 준다. 사용자당 등록에서 첫 번째 구매 날짜까지의 평균 시간을 평가하려면 측정이 구성하는 모든 데이터 포인트를 식별해야 합니다.

측정값을 핵심 구성 요소로 분류합니다. 등록한 사람의 수, 구매한 사람의 수 및 이 두 이벤트 사이에 경과된 시간을 알고 있어야 합니다.

상위 수준에서 데이터베이스에서 이 데이터를 찾을 위치를 알아야 합니다. 구체적으로 다음과 같습니다.

* 누군가가 등록할 때마다 데이터 행을 기록하는 테이블
* 누군가 구매할 때마다 데이터 행을 기록하는 테이블
* `purchase` 테이블을 `customer` 테이블에 연결하거나 참조하는 데 사용할 수 있는 열입니다. 이렇게 하면 누가 구매했는지 알 수 있습니다.

보다 세분화된 수준에서 이 분석에 사용되는 정확한 데이터 필드를 식별해야 합니다.

* 고객의 등록 날짜가 포함된 데이터 테이블 및 열: 예: `user.created\_at`
* 구매 날짜가 포함된 데이터 테이블 및 열: 예: `order.created\_at`

## 분석을 위한 데이터 열 만들기

위에 요약된 기본 데이터 열 외에도 다음을 포함하여 이 분석을 활성화하려면 계산된 데이터 필드 세트가 필요합니다.

* 특정 사용자의 `MIN(order.created_at`을(를) 반환하는 `Customer's first purchase date`

그런 다음 를 만드는 데 사용됩니다.

* `Time between a customer's registration date and first purchase date`: 등록과 첫 번째 구매 날짜 사이에 경과된 특정 사용자의 시간을 반환합니다. 이것이 나중에 지표의 기본입니다.

이 두 필드는 사용자 수준(예: `user` 테이블)에서 만들어야 합니다. 이를 통해 사용자에 의해 평균 분석을 정규화할 수 있습니다(즉, 이 평균 계산의 분모가 사용자 수임).

[!DNL Commerce Intelligence]개의 단계가 있는 곳입니다. [!DNL Commerce Intelligence] Data Warehouse을 사용하여 위의 열을 만들 수 있습니다. Adobe 분석가 팀에 문의하여 새 열을 만들 특정 정의를 제공하십시오. [열 편집기](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)를 사용할 수도 있습니다.

프로덕션 서버에 불필요한 부담을 주기 때문에 이러한 계산된 데이터 필드를 데이터베이스에 직접 생성하지 않는 것이 좋습니다.

## 지표 만들기

분석에 필요한 데이터 필드가 있으므로 관련 지표를 찾거나 만들어 분석을 구성할 수 있습니다.

여기에서 다음 계산을 수행합니다.


_[등록 및 구매한 총 고객 수]_ / `Time between a customer's registration date and first purchase date`&rbrack;의 합계&lbrack;

고객의 등록 날짜에 따라 시간 경과나 추세를 통해 이 계산을 표시하려고 합니다. [!DNL Commerce Intelligence]에서 [이 지표를 만들기](../../data-user/reports/ess-manage-data-metrics.md)하는 방법은 다음과 같습니다.

1. **[!UICONTROL Data]**(으)로 이동하여 `Metrics` 탭을 선택합니다.
1. **[!UICONTROL Add New Metric]**&#x200B;을(를) 클릭하고 `user` 테이블(위에서 차원을 만든 위치)을 선택합니다.
1. 드롭다운에서 `Customer's registration date` 열로 정렬된 `user` 테이블의 `Time between a customer's registration date and first purchase date` 열에 있는 `Average`을(를) 선택합니다.
1. 관련 필터 또는 필터 세트를 추가합니다.

이제 이 지표가 준비되었습니다.

## 보고서 만들기

새 지표가 설정되면 이 지표를 사용하여 등록 날짜별 등록과 첫 번째 구매 날짜 사이의 평균 시간을 보고할 수 있습니다.

대시보드로 이동하여 위에서 만든 지표를 사용하여 [보고서를 만들기](../../data-user/reports/ess-manage-data-metrics.md)하면 됩니다.

### `Visual Report Builder` {#visualrb}

[데이터를 시각화하는 가장 쉬운 방법은 `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md)입니다. SQL에 익숙하지 않거나 보고서를 빠르게 만들려는 경우 시각적 Report Builder이 가장 좋습니다. 몇 번의 클릭만으로 지표를 추가하고, 데이터를 세그먼트화하고, 조직 전체에 걸쳐 보고서를 만들 수 있습니다. 이 옵션은 기술 전문 지식이 필요하지 않으므로 초보자 및 전문가 모두에게 적합합니다.

|  |  |
|--- |--- |
| **다음 작업에 적합합니다...** | **다음 용도로는 적합하지 않습니다...** |
| - 모든 수준의 분석/기술 경험<br>- 보고서를 빠르게 만들기<br>- 다른 사용자와 공유할 분석 만들기 | - SQL 관련 함수가 필요한 분석<br>- 새 열 테스트 - 계산된 열은 초기 데이터 채우기의 업데이트 주기에 따라 달라지지만 SQL을 사용하여 생성된 열은 그렇지 않습니다. |

{style="table-layout:auto"}

### 보고서 설명 및 이미지

#### 보고서에 설명 추가

Adobe 팀의 다른 멤버와 공유되는 보고서를 만들 때는 다른 사용자가 분석을 더 잘 이해할 수 있도록 설명을 추가하는 것이 좋습니다.

1. 보고서 맨 위에 있는 **[!UICONTROL i]**&#x200B;을(를) 클릭합니다.
1. 단어 상자에 설명을 입력합니다.
1. **[!UICONTROL Save Description]**&#x200B;을(를) 클릭합니다.

아래를 참조하십시오.

![차트 설명](../../assets/Chart_Description.gif)

#### 보고서를 이미지로 내보내기

프레젠테이션이나 문서에 보고서를 포함해야 합니까? 모든 보고서의 오른쪽 위 모서리에 있는 `Report Options` 메뉴를 사용하여 모든 보고서를 이미지(PNG, PDF 또는 SVG 형식)로 저장할 수 있습니다.

1. 보고서의 오른쪽 위 모서리에 있는 톱니바퀴 아이콘을 클릭합니다.
1. 드롭다운에서 `Enlarge`을(를) 선택합니다.
1. 보고서가 확대되면 보고서의 오른쪽 상단 모서리에서 **[!UICONTROL Download]**&#x200B;을(를) 클릭합니다.
1. 드롭다운에서 선호하는 이미지 형식을 선택합니다. 다운로드가 즉시 시작됩니다.

아래를 참조하십시오.

![](../../assets/exp-rep-as-image.gif)
