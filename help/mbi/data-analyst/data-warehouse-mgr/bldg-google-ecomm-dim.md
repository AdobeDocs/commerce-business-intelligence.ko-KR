---
title: 빌드[!DNL Google ECommerce] 차원
description: 전자 상거래 데이터를 주문 및 고객 데이터와 연결하는 차원을 빌드하는 방법을 알아봅니다.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# [!DNL Google ECommerce] 차원 작성

>[!NOTE]
>
>[관리자 권한](../../administrator/user-management/user-management.md)이 필요합니다.

[계정 연결[!DNL Google ECommerce]](../../data-analyst/importing-data/integrations/google-ecommerce.md)을(를) 완료했으므로 [!DNL Commerce Intelligence]의 해당 데이터를 어떻게 할 수 있습니까? 이 항목에서는 전자 상거래 데이터를 주문 및 고객 데이터와 연결하는 차원을 빌드하는 방법을 설명합니다.

다루는 차원을 통해 [마케팅 채널 및 캠페인에 대한 중요한 질문에 답변하는 분석을 빌드할 수 있습니다](../../data-analyst/analysis/most-value-source-channel.md). 각 소스에서 발생하는 매출의 비율은 얼마입니까? [!DNL Facebook] 획득 고객의 라이프타임 값은 [!DNL Google]의 고객과 어떻게 비교됩니까?

## 사전 요구 사항 및 개요

이 항목에서 차원을 만들려면 [!DNL Google ECommerce] 테이블, `orders` 테이블 및 `customers` 테이블이 필요합니다. 차원을 빌드하려면 먼저 해당 테이블을 [Data Warehouse에 동기화](../../data-analyst/data-warehouse-mgr/tour-dwm.md)해야 합니다. 동기화된 테이블은 `Synced Tables`의 `Data Warehouse Manager` 섹션에 표시됩니다.

다음은 새로 고침이 필요한 경우 테이블과 열을 동기화하는 방법을 간략하게 살펴보겠습니다.

![](../../assets/Syncing_New_Columns.gif)

`orders` 테이블에서 [!DNL Google eCommerce] 테이블로의 조인을 만든 후 아래 목록에서 처음 세 개의 차원을 만듭니다. 그런 다음 이러한 차원을 사용하여 `customers` 표에 세 개의 사용자/고객 차원을 만듭니다. 이 열을 `orders` 테이블에 조인합니다.

다음 차원에 대해 설명합니다.

* **주문 테이블**

* 주문의 [!DNL Google Analytics] 소스
* 주문의 [!DNL Google Analytics] 보통
* [!DNL Google Analytics]A 캠페인 주문
* 고객의 첫 번째 주문 [!DNL Google Analytics] 소스
* 고객의 첫 번째 주문은 보통 [!DNL Google Analytics]개입니다.
* 고객의 첫 번째 주문 [!DNL Google Analytics] 캠페인

* **고객 테이블**

* 고객의 첫 번째 주문 [!DNL Google Analytics] 소스
* 고객의 첫 번째 주문은 보통 [!DNL Google Analytics]개입니다.
* 고객의 첫 번째 주문 [!DNL Google Analytics] 캠페인

## 차원 빌드

차원을 만들려면 [ > ](../data-warehouse-mgr/tour-dwm.md)을(를) 클릭하여 **[!UICONTROL Data]** Data Warehouse 관리자&#x200B;**[!UICONTROL Data Warehouse]**&#x200B;를 엽니다.

### 주문 테이블, 1라운드

이 예제에서는 **Order의 [!DNL Google Analytics] Source** 차원을 빌드합니다.

1. Data Warehouse의 테이블 목록에서 주문 정보가 포함된 테이블(이 경우 `orders`)을 클릭합니다.
1. **[!UICONTROL Create a Column]**&#x200B;을(를) 클릭합니다.
1. 열 이름을 지정합니다.
1. `Joined Column`정의 드롭다운[에서 ](../data-warehouse-mgr/calc-column-types.md)을(를) 선택합니다. 이 예제는 [일대일 관계](../data-warehouse-mgr/table-relationships.md)에서 작동하며 `eCommerce.transactionID` 열을 `orders` 테이블의 정확히 하나의 행과 일치시킵니다.
1. 그런 다음 경로 또는 사용 중인 테이블과 열이 연결되는 방식을 정의해야 합니다. `Select a table and column` 드롭다운을 클릭합니다.
1. 필요한 경로를 사용할 수 없으므로 새 경로를 만들어야 합니다. **[!UICONTROL Create new Path]**&#x200B;을(를) 클릭합니다.
1. 표시되는 창에서 `Many` 쪽을 `orders.order\_id`(으)로 설정하거나 주문 ID가 포함된 `orders` 테이블의 열을 설정하십시오.
1. `One`측에서 `Google ECommerce` 테이블을 찾은 다음 열을 `transactionID`(으)로 설정합니다.

   ![](../../assets/google-ecommerce-table.png)

1. 경로를 만들려면 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.
1. 경로가 추가되면 **[!UICONTROL Select table and column]** 드롭다운을 다시 클릭합니다.
1. `ECommerce` 테이블을 찾은 다음 `Source` 열을 클릭합니다. 이렇게 하면 주문이 소스 정보에 연결됩니다.
1. 테이블 스키마로 돌아오면 **[!UICONTROL Save]**&#x200B;을(를) 다시 클릭하여 차원을 만듭니다.

전체 프로세스를 살펴보겠습니다.

![](../../assets/help_center.gif)

**주문의 [!DNL Google Analytics] 미디어** 및 `campaign`을(를) 만들어 보세요. 이러한 차원에 대한 변경 사항은 많지 않으므로 시도해 보십시오. 하지만 문제가 발생하면 [이 문서의 끝](#stuck)을(를) 확인하여 차이점을 확인할 수 있습니다.

### Customers 테이블 {#customers}

이 예제에서는 **고객의 첫 번째 주문 [!DNL Google Analytics] 소스** 차원을 빌드합니다.

1. Data Warehouse의 테이블 목록에서 고객 정보가 포함된 테이블(이 경우 `customers`)을 클릭합니다.
1. **[!UICONTROL Create a Column]**&#x200B;을(를) 클릭합니다.
1. 열 이름을 지정합니다.
1. 이 예제에서는 `is MAX`정의 드롭다운[에서 ](../../data-analyst/data-warehouse-mgr/calc-column-types.md) 정의를 선택합니다. 가능한 값이 하나만 있는 텍스트 열에 적용할 경우 `is MIN` 정의도 작동할 수 있습니다. 중요한 점은 필터를 제대로 설정했는지 확인하는 것입니다. 나중에 다시 설정할 수 있습니다.
1. **[!UICONTROL Select a table and column]** 드롭다운을 클릭하고 `orders` 테이블을 선택한 다음 `Order's [!DNL Google Analytics] source` 열을 선택합니다.
1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.
1. 테이블 스키마로 돌아간 후 `Options` 드롭다운을 클릭한 다음 `Filters`을(를) 클릭합니다.
1. **[!UICONTROL Add Filter Set]**&#x200B;을(를) 클릭한 다음 `Orders we count` 집합을 선택합니다. 필터 세트를 계산하는 주문에 포함된 주문만 포함할 수 있으므로 이 필터 세트를 선택하는 것이 중요합니다.
1. **[!UICONTROL Add Filter]**&#x200B;을(를) 클릭합니다. 고객의 첫 번째 주문 [!DNL Google Analytics] 소스를 찾으려고 하므로 필터를 추가해야 합니다.

   _orders.Customer&#39;s 주문 번호 = 1

   _
1. 차원을 만들려면 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

다음으로 **고객의 첫 번째 주문의 [!DNL Google Analytics] 매체** 및 `campaign`을(를) 만들어 보십시오. 이러한 차원에 대한 변경 사항은 많지 않으므로 시도해 보십시오. 하지만 문제가 발생하면 [이 문서의 끝](#stuck)을(를) 확인하여 차이점을 확인할 수 있습니다.

### 보너스: 주문 테이블, 2라운드

원한다면 여기에서 중지할 수 있지만, 이 섹션을 통해 **마지막 섹션[!DNL Google Analytics]에서 만든**&#x200B;고객의 첫 번째 주문 [ 차원](#customers)을(를) `orders` 테이블로 가져와 추가로 분석할 수 있습니다. 이 섹션에서 차원을 만들면 고객 첫 번째 주문의 `orders` 특성을 사용하여 `Revenue` 테이블에 빌드된 모든 지표(`Number of orders`, `Distinct buyers`, [!DNL Google Analytics] 등)를 분석할 수 있습니다.

이 예제에서는 `Customer's first order's [!DNL Google Analytics] source` 차원을 `orders` 테이블에 조인합니다.

1. Data Warehouse의 테이블 목록에서 주문 정보가 포함된 테이블(이 경우 `orders`)을 클릭합니다.
1. **[!UICONTROL Create a Column]**&#x200B;을(를) 클릭합니다.
1. 열 이름을 지정합니다.
1. 정의 드롭다운에서 `Joined Column`을(를) 선택합니다. 이전 섹션에서 만든 고객 차원을 `orders` 테이블에 조인합니다.
1. **[!UICONTROL Select a table and column]** 드롭다운을 클릭한 다음 `customers` 테이블과 `Customer's first order's [!DNL Google Analytics] source` 열을 선택합니다.
1. 경로가 자동으로 채워지지 않으면 고객과 주문 테이블을 가장 잘 연결하는 경로를 선택합니다.
1. 차원을 만들려면 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

전체 프로세스를 살펴보겠습니다.

![](../../assets/help_center2.gif)

`Customer's first order's` 미디어와 `campaign` 차원을 `orders` 테이블에 연결하여 완료하십시오. 차원에 참여하고 문제가 있으면 도움이 필요하면 [문서의 끝](#stuck)을 확인하십시오.

### 요약

차원 만들기를 완료했습니다. 즉, 이제 다양한 채널 및 캠페인의 성과를 추적하는 강력한 분석을 만들 수 있습니다. **새 열은 다음 업데이트가 완료되어야 사용할 수 있습니다**.

이 주제에서는 더 인기 있는 차원 중 일부를 다루지만, 무한합니다. 자신만의 차원을 만들어 보거나 다른 옵션을 탐색하는 데 도움이 필요하면 언제든지 알려 주십시오. 

### 추가 참고 사항

**`Orders`테이블 #1**: `Order's [!DNL Google Analytics]` 미디어와 `campaign` 차원을 만들 때 차이는 12단계에서 선택한 열입니다. 이 예제에서 열은 `Source`입니다.

**`Customers`테이블**: `Customer's first order's [!DNL Google Analytics]` 미디어와 `campaign` 차원을 만들 때 차이는 5단계에서 선택한 열입니다. 이 예제에서 열은 `Order's [!DNL Google Analytics]` 원본입니다.

**`Orders`테이블 #2**: `Customer's first order's [!DNL Google Analytics]` 미디어와 `campaign` 열을 `orders` 테이블에 조인할 때 차이는 5단계에서 선택한 열입니다. 이 예제에서 열은 `Customer's first order's [!DNL Google Analytics]` 원본입니다.
