---
title: 빌드[!DNL Google ECommerce] 치수
description: 전자 상거래 데이터를 주문 및 고객 데이터와 연결하는 차원을 빌드하는 방법을 알아봅니다.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# 빌드 [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>필요 [관리자 권한](../../administrator/user-management/user-management.md).

이제 완료되었으니 [연결 중[!DNL Google ECommerce] account](../../data-analyst/importing-data/integrations/google-ecommerce.md), 의 해당 데이터로 무엇을 할 수 있습니까? [!DNL Commerce Intelligence]? 이 항목에서는 전자 상거래 데이터를 주문 및 고객 데이터와 연결하는 차원을 빌드하는 방법을 설명합니다.

다루는 차원은 다음과 같은 분석을 빌드할 수 있는 기능을 제공합니다 [마케팅 채널 및 캠페인에 대한 중요한 질문에 답변합니다.](../../data-analyst/analysis/most-value-source-channel.md). 각 소스에서 발생하는 매출의 비율은 얼마입니까? 라이프타임 값 [!DNL Facebook] 후천적 고객은 다음에서 후천적 고객과 비교합니다. [!DNL Google]?

## 사전 요구 사항 및 개요

이 항목에서 차원을 생성하려면 [!DNL Google ECommerce] 테이블, `orders` 테이블 및 `customers` 테이블. 그 테이블들은 [Data Warehouse에 동기화됨](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 차원을 빌드하기 전에. 동기화된 표는 `Synced Tables` 의 섹션 `Data Warehouse Manager`.

다음은 새로 고침이 필요한 경우 테이블과 열을 동기화하는 방법을 간략하게 살펴보겠습니다.

![](../../assets/Syncing_New_Columns.gif)

에서 조인 생성 후 `orders` 테이블 대상 [!DNL Google eCommerce] 표는 아래 목록에서 처음 세 개의 차원을 생성합니다. 그런 다음 이러한 차원을 사용하여 `customers` 테이블. 완료하기 위해 해당 열을 `orders` 테이블.

다음 차원에 대해 설명합니다.

* **주문 테이블**

* 주문 [!DNL Google Analytics] 소스
* 주문 [!DNL Google Analytics] 중간
* 주문 [!DNL Google Analytics]캠페인
* 고객의 첫 번째 주문 [!DNL Google Analytics] 소스
* 고객의 첫 번째 주문 [!DNL Google Analytics] 중간
* 고객의 첫 번째 주문 [!DNL Google Analytics] campaign

* **Customers 테이블**

* 고객의 첫 번째 주문 [!DNL Google Analytics] 소스
* 고객의 첫 번째 주문 [!DNL Google Analytics] 중간
* 고객의 첫 번째 주문 [!DNL Google Analytics] campaign

## 차원 빌드

차원을 생성하려면 다음을 엽니다. [Data Warehouse 관리자](../data-warehouse-mgr/tour-dwm.md) 다음을 클릭: **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### 주문 테이블, 1라운드

이 예제는 **주문 [!DNL Google Analytics] 소스** 차원.

1. Data Warehouse의 테이블 목록에서 테이블을 클릭합니다(이 경우 `orders`)에 포함되어 있습니다.
1. 클릭 **[!UICONTROL Create a Column]**.
1. 열 이름을 지정합니다.
1. 선택 `Joined Column` 다음에서 [정의 드롭다운](../data-warehouse-mgr/calc-column-types.md). 이 예제는 [일대일 관계](../data-warehouse-mgr/table-relationships.md), 와 일치 `eCommerce.transactionID` 열을 정확히 한 행의 `orders` 테이블.
1. 그런 다음 경로 또는 사용 중인 테이블과 열이 연결되는 방식을 정의해야 합니다. 다음을 클릭합니다. `Select a table and column` 드롭다운입니다.
1. 필요한 경로를 사용할 수 없으므로 새 경로를 만들어야 합니다. 클릭 **[!UICONTROL Create new Path]**.
1. 표시되는 창에서 다음을 설정합니다. `Many` 사이드 투 `orders.order\_id`, 또는 의 열 `orders` 주문 ID가 포함된 테이블입니다.
1. 다음에서 `One` 측면, 찾기 `Google ECommerce` 테이블, 열을 다음으로 설정 `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. 클릭 **[!UICONTROL Save]** 을 클릭하여 경로를 만듭니다.
1. 경로가 추가되면 **[!UICONTROL Select table and column]** 드롭다운을 다시 실행하십시오.
1. 를 찾습니다. `ECommerce` 표를 클릭한 다음 `Source` 열. 이렇게 하면 주문이 소스 정보에 연결됩니다.
1. 테이블 스키마로 돌아간 후 **[!UICONTROL Save]** 다시 클릭하여 차원을 생성합니다.

전체 프로세스를 살펴보겠습니다.

![](../../assets/help_center.gif)

다음으로, 생성 시도 **주문 [!DNL Google Analytics] 중간** 및 `campaign`. 이러한 차원에 대한 변경 사항은 많지 않으므로 시도해 보십시오. 하지만 막히면 체크아웃하실 수 있어요 [이 문서의 끝](#stuck) 무엇이 다른지 보기 위해.

### Customers 테이블 {#customers}

이 예제는 **고객의 첫 번째 주문 [!DNL Google Analytics] 소스** 차원.

1. Data Warehouse의 테이블 목록에서 테이블을 클릭합니다(이 경우 `customers`)에 넣을 수 있습니다.
1. 클릭 **[!UICONTROL Create a Column]**.
1. 열 이름을 지정합니다.
1. 이 예에서는 `is MAX` 의 정의 [정의 드롭다운](../../data-analyst/data-warehouse-mgr/calc-column-types.md). 다음 `is MIN` 가능한 값이 한 개만 있는 텍스트 열에 적용할 경우에도 정의가 작동할 수 있습니다. 중요한 점은 필터를 제대로 설정했는지 확인하는 것입니다. 나중에 다시 설정할 수 있습니다.
1. 다음을 클릭합니다. **[!UICONTROL Select a table and column]** 드롭다운을 클릭하고 `orders` 테이블, 그런 다음 `Order's [!DNL Google Analytics] source` 열.
1. 클릭 **[!UICONTROL Save]**.
1. 테이블 스키마로 돌아간 후 `Options` 드롭다운, 그런 다음 `Filters`.
1. 클릭 **[!UICONTROL Add Filter Set]** 을(를) 선택한 다음 `Orders we count` 설정. 필터 세트를 계산하는 주문에 포함된 주문만 포함할 수 있으므로 이 필터 세트를 선택하는 것이 중요합니다.
1. 클릭 **[!UICONTROL Add Filter]**. 고객의 첫 번째 주문 [!DNL Google Analytics] 소스 - 필터를 추가해야 합니다.

   _orders.Customer&#39;s 주문 번호 = 1

   _
1. 클릭 **[!UICONTROL Save]** 을 눌러 차원을 생성합니다.

다음으로, 생성 시도 **고객의 첫 번째 주문 [!DNL Google Analytics] 중간** 및 `campaign`. 이러한 차원에 대한 변경 사항은 많지 않으므로 시도해 보십시오. 하지만 막히면 체크아웃하실 수 있어요 [이 문서의 끝](#stuck) 무엇이 다른지 보기 위해.

### 보너스: 주문 테이블, 2라운드

원할 경우 여기에서 중지할 수 있지만, 이 섹션에서는 다음을 가져와 추가로 분석할 수 있습니다. **고객의 첫 번째 주문 [!DNL Google Analytics] 치수** 다음 작업에서 을(를) 만들었습니다. [마지막 섹션](#customers) 대상: `orders` 테이블. 이 섹션에서 차원을 생성하면 을 기반으로 구축된 모든 지표를 분석할 수 있습니다. `orders` 표 - `Revenue`, `Number of orders`, `Distinct buyers`등 - 사용 [!DNL Google Analytics] 고객의 첫 번째 주문 속성.

이 예제는 `Customer's first order's [!DNL Google Analytics] source` 차원 대상 `orders` 테이블.

1. Data Warehouse의 테이블 목록에서 테이블을 클릭합니다(이 경우 `orders`)에 포함되어 있습니다.
1. 클릭 **[!UICONTROL Create a Column]**.
1. 열 이름을 지정합니다.
1. 선택 `Joined Column` 정의 드롭다운에서. 이렇게 하면 이전 섹션에서 만든 고객 차원이 `orders` 테이블.
1. 다음을 클릭합니다. **[!UICONTROL Select a table and column]** 드롭다운에서 `customers` 테이블 및 `Customer's first order's [!DNL Google Analytics] source` 열.
1. 경로가 자동으로 채워지지 않으면 고객과 주문 테이블을 가장 잘 연결하는 경로를 선택합니다.
1. 클릭 **[!UICONTROL Save]** 을 눌러 차원을 생성합니다.

전체 프로세스를 살펴보겠습니다.

![](../../assets/help_center2.gif)

다음을 참여하여 완료 `Customer's first order's` 중간 `campaign` 차원 대상: `orders` 테이블. 차원을 결합하고 문제가 있는 경우 체크 아웃합니다 [문서의 끝](#stuck) 도움이 필요하면

### 요약

차원 만들기를 완료했습니다. 즉, 이제 다양한 채널 및 캠페인의 성과를 추적하는 강력한 분석을 만들 수 있습니다. 다음 사항을 기억하십시오. **새 열은 다음 업데이트가 완료될 때까지 사용할 수 없습니다.**.

이 주제에서는 더 인기 있는 차원 중 일부를 다루지만, 무한합니다. 자신만의 차원을 만들어 보거나 다른 옵션을 탐색하는 데 도움이 필요하면 언제든지 알려 주십시오. 

### 추가 참고 사항

**`Orders`테이블 #1**: 를 만들 때 `Order's [!DNL Google Analytics]` 중간 `campaign` 차원, 차이점은 단계 12에서 선택한 열입니다. 이 예에서 열은 `Source`.

**`Customers`표**: 를 만들 때 `Customer's first order's [!DNL Google Analytics]` 중간 `campaign` 차원, 차이점은 5단계에서 선택한 열입니다. 이 예에서 열은 `Order's [!DNL Google Analytics]` 소스.

**`Orders`테이블 #2**: 가입 시 `Customer's first order's [!DNL Google Analytics]` 중간 `campaign` 열 대상 `orders` 표에서 차이점은 5단계에서 선택한 열입니다. 이 예에서 열은 `Customer's first order's [!DNL Google Analytics]` 소스.
