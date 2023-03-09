---
title: Data Warehouse 보기 만들기 및 사용
description: 기존 테이블을 수정하여 새 웨어하우스된 테이블을 만들거나 SQL을 사용하여 여러 테이블을 함께 연결하거나 통합하는 방법에 대해 알아봅니다.
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1064'
ht-degree: 9%

---

# Data Warehouse 보기 작업

이 문서에서는 의 목적 및 용도에 대해 간략하게 설명합니다. `Data Warehouse Views` 다음으로 이동하여 액세스 가능 **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. 다음은 기능 및 보기를 만드는 방법에 대한 설명과 사용 방법에 대한 예입니다 `Data Warehouse Views` 통합하기 [!DNL Facebook] 및 [!DNL AdWords] 데이터를 사용합니다.

## 일반 목적

다음 `Data Warehouse Views` 기능은 기존 테이블을 수정하여 새 웨어하우스된 테이블을 생성하거나 SQL을 사용하여 여러 테이블을 결합 또는 통합하는 방법입니다. 한 번 `Data Warehouse View` 업데이트 주기에서 만들고 처리하면 Data Warehouse에서 `Data Warehouse Views` 드롭다운, 아래 표시:

![](../../assets/Data_Warehouse.png)

여기에서 새 보기는 다른 테이블과 마찬가지로 작동하므로 새로 계산된 열을 생성하거나 지표 및 보고서를 작성할 수 있습니다.

`Data Warehouse Views` 는 모든 보고를 하나의 새 테이블에 작성할 수 있도록 유사하지만 서로 다른 여러 테이블을 통합하는 데 주로 사용됩니다. 몇 가지 일반적인 예로는 이전 데이터베이스와 라이브 데이터베이스의 테이블을 통합하여 기록 데이터와 현재 데이터를 결합하거나 Facebook 및 AdWords와 같은 여러 광고 소스를 하나로 결합하는 작업이 있습니다 `Consolidated ad spend` 테이블.

SQL에 익숙하다면 이러한 통합 예는 모두 `UNION` 함수를 사용할 수 있지만 새 보기를 작성할 때 모든 PostgreSQL 구문과 함수를 사용할 수 있습니다.

## Data Warehouse 보기 만들기 및 관리

신규 `Data Warehouse Views` 로 이동하여 기존 보기를 만들고 삭제할 수 있습니다. **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**, 아래와 같이 표시됩니다.

![](../../assets/Data_Warehouse_Views.png)

여기에서 아래 샘플 지침에 따라 보기를 만들 수 있습니다.

1. 기존 보기를 관찰하는 경우 **[!UICONTROL New Data Warehouse View]** 을 눌러 빈 쿼리 창을 엽니다. 빈 쿼리 창이 이미 열려 있는 경우 다음 단계로 진행합니다.
1. 을(를) 입력하여 보기의 이름을 지정합니다. `View Name` 필드. 여기에 제공된 이름은 Data Warehouse에서 보기의 표시 이름을 결정합니다. `View names` 소문자, 숫자 및 밑줄(_)로 제한됩니다. 다른 문자는 사용할 수 없습니다.
1. 제목이 있는 창에 쿼리를 입력합니다. `Select Query`표준 PostgreSQL 구문을 사용합니다.
   >[!NOTE]
   >
   >쿼리에서 특정 열 이름을 참조해야 합니다. 사용 `*`모든 열을 선택하는 문자는 허용되지 않습니다.

1. 완료되면 다음을 클릭하십시오. **[!UICONTROL Save]** 보기를 저장합니다. 보기에 일시적으로 `Pending` 상태가 다음 전체 업데이트 주기에 의해 처리될 때까지 상태를 나타내며, 이 시점에서 상태가 다음으로 변경됩니다. `Active`. 업데이트로 처리되면 보기를 보고서에서 사용할 수 있습니다.

저장 후 기본 쿼리가 을(를) 생성하는 데 사용되었다는 점을 참고하십시오. `Data Warehouse View` 편집할 수 없습니다. 의 구조를 조정해야 하는 경우 `Data Warehouse View`, 보기를 만들고 계산된 열, 지표 또는 보고서를 원래 보기에서 새 보기로 수동으로 마이그레이션해야 합니다. 마이그레이션이 완료되면 원본 보기를 안전하게 삭제할 수 있습니다. 이유 `Data Warehouse Views` 는 편집할 수 없습니다. Adobe은 다음을 사용하여 쿼리 출력을 테스트할 것을 권장합니다. `SQL Report Builder` 쿼리를 Data Warehouse 보기로 저장하기 전에

## 예: [!DNL Facebook] 및 [!DNL Google AdWords] 데이터

이 문서의 앞부분에 언급된 예 중 하나를 자세히 살펴보십시오. 통합 [!DNL Facebook] 및 [!DNL AdWords] 데이터를 새로운 통합 광고 테이블에 지출 가장 일반적으로는 아래 샘플 데이터 세트가 있는 두 테이블의 통합이 포함됩니다.

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | eee | 60 | 2017-05-05 00:00:00 | 2000 | 10.2 |
| 2 | ggg | 40 | 2017-05-23 00:00:00 | 900 | 4.6 |
| 3 | aaa | 22 | 2017-06-12 00:00:00 | 400 | 2.5 |
| 4 | eee | 350 | 2017-06-30 00:00:00 | 14500 | 35 |
| 5 | fff | 280 | 2017-07-10 00:00:00 | 10200 | 28.5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aaa | 25 | 2017-05-01 00:00:00 | 1200 | 5 |
| 2 | ddd | 12 | 2017-05-15 00:00:00 | 800 | 2.5 |
| 3 | aaa | 40 | 2017-05-22 00:00:00 | 2000 | 7 |
| 4 | aaa | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | ccc | 5 | 2017-07-06 00:00:00 | 300 | 1.2 |

두 항목을 모두 포함하는 단일 광고 지출 테이블을 만들려면 [!DNL Facebook] 및 [!DNL AdWords] 캠페인을 사용하려면 SQL 쿼리를 작성하고 `UNION ALL` 함수. A `UNION ALL` 문은 각 쿼리의 결과를 단일 출력에 추가하면서 서로 다른 여러 SQL 쿼리를 결합하는 데 가장 많이 사용됩니다.

에는 몇 가지 요구 사항이 있습니다. `UNION` PostgreSQL에 요약된 언급할 가치가 있는 명령문 [설명서](https://www.postgresql.org/docs/8.3/queries-union.html):

* 모든 쿼리는 동일한 수의 열을 반환해야 합니다.
* 해당 열에는 동일한 데이터 유형이 있어야 합니다.

실행 시 `UNION` 또는 `UNION ALL` 명령문, 최종 출력의 열 이름은 첫 번째 쿼리의 열 이름을 반영합니다.

일반적으로 [!DNL Facebook] 및 [!DNL Google AdWords] 에 데이터 사용 `Data Warehouse View` 다음과 유사한 쿼리가 있는 7개의 열이 있는 테이블을 만들어야 합니다.

```sql
    SELECT
        "_id" as id,
        'AdWords' as ad_source,
        "date",
        "campaign",
        "adCost" as spend,
        "impressions",
        "adClicks" as clicks
    FROM campaigns67890
    UNION
    SELECT
        "_id" as id,
        'Facebook' as ad_source,
        "date_start" as date,
        "campaign_name" as campaign,
        "spend",
        "impressions",
        "clicks"
    FROM facebook_ads_insights_12345
```

위에 대한 몇 가지 중요한 사항:

* 명확성을 위해 모든 쿼리에서 이름이 일치하도록 모든 열에 별칭을 지정합니다. 그러나 이는 요구 사항이 아닙니다. SELECT 쿼리에서 열이 호출되는 순서는 줄이 어떻게 정렬되는지 나타냅니다.
* 라는 새 열 `ad_source` 을(를) 보다 쉽게 필터링할 수 있도록 만들었습니다. [!DNL AdWords] 또는 [!DNL Facebook] 데이터. 이 쿼리는 두 테이블의 모든 데이터를 결합합니다. 과 같은 열을 만들지 않는 경우 `ad_source`, 특정 소스에서 지출을 식별하는 쉬운 방법이 없습니다.

위의 쿼리를 다음으로 저장 `Data Warehouse View` 두 옵션을 모두 사용하여 테이블을 만듭니다. [!DNL Facebook] 및 [!DNL AdWords] 다음과 유사한 지출:

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00:00:00 | aaa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00:00:00 | eee | 10.2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | ddd | 2.5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | ggg | 4.6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | aaa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | aaa | 2.5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | aaa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | eee | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | ccc | 1.2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | fff | 28.5 | 10200 | 280 |

이제 각 광고 소스에 대해 별도의 마케팅 지표 세트를 만드는 대신, 위의 표를 사용하여 단일 지표 세트만 만들어 모든 광고를 캡처할 수 있습니다.

**추가 도움말을 찾고 계십니까?**

SQL 작성 및 생성 `Data Warehouse Views` 이 기술 지원에는 포함되어 있지 않습니다. 그러나 서비스 팀은 보기 만들기에 대한 지원을 제공합니다. 특정 분석을 위해 새 데이터베이스를 사용하여 기존 데이터베이스를 마이그레이션하고 단일 Data Warehouse 보기를 만드는 모든 작업에 대해 지원 팀이 도움을 줄 수 있습니다.

일반적으로 새 항목 만들기 `Data Warehouse View` 2~3개의 유사 구조 테이블을 통합하려면 5시간의 서비스 시간이 필요하며, 이는 약 1,250달러의 작업 비용으로 해석됩니다. 그러나 필요한 예상 투자를 늘릴 수 있는 몇 가지 일반적인 요소는 다음과 같습니다.

* 세 개 이상의 테이블을 단일 뷰로 통합
* 두 개 이상의 Data Warehouse 보기 생성
* 복잡한 조인 논리 또는 필터링 조건
* 데이터 구조가 다른 두 개 이상의 테이블 통합
