---
title: 빌드[!DNL Google ECommerce]차원
description: eCommerce 데이터를 주문 및 고객 데이터와 연결하는 차원을 빌드하는 방법을 알아봅니다.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 0%

---

# 빌드 [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>필요한 경우 [관리자 권한](../../administrator/user-management/user-management.md).

이제 다 끝냈으니 [연결[!DNL Google ECommerce]account](../../data-analyst/importing-data/integrations/google-ecommerce.md), 의 해당 데이터로 수행할 수 있는 작업 [!DNL MBI]? 이 문서에서는 eCommerce 데이터를 주문 및 고객 데이터와 연결하는 차원 작성을 안내합니다.

우리가 다루는 차원을 통해 다음과 같은 분석을 구축할 수 있습니다 [마케팅 채널 및 캠페인에 대한 중요한 질문에 답변합니다.](../../data-analyst/analysis/most-value-source-channel.md). 각 출처에서 얻는 수익률은 무엇입니까? facebook의 라이프타임 값과 고객이 얻은 라이프타임 값을 비교할 때 어떻게 됩니까? [!DNL Google]?

## 사전 요구 사항 및 개요

이 문서에서 차원을 만들려면 [!DNL Google ECommerce] 표, `orders` 테이블 및 `customers` 테이블. 그 테이블들은 [data warehouse에 동기화됨](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 차원을 빌드하기 전에 동기화된 표는 `Synced Tables` 섹션 `Data Warehouse Manager`.

다음은 리프레셔가 필요한 경우 테이블 및 열 동기화를 간략히 살펴보겠습니다.

![](../../assets/Syncing_New_Columns.gif)

에서 조인을 만든 후 `orders` 표 [!DNL Google eCommerce] 표, 아래 목록에 처음 세 개의 차원을 만듭니다. 다음으로, 이 차원을 사용하여 `customers` 테이블. 마무리를 위해 우리는 그 기둥들을 `orders` 테이블.

다음은 Dell이 다루는 차원입니다.

* **주문 테이블**

* 주문 [!DNL Google Analytics] 소스
* 주문 [!DNL Google Analytics] 중간
* 주문 [!DNL Google Analytics]캠페인
* 고객의 최초 주문 [!DNL Google Analytics] 소스
* 고객의 최초 주문 [!DNL Google Analytics] 중간
* 고객의 최초 주문 [!DNL Google Analytics] campaign

* **고객 테이블**

* 고객의 최초 주문 [!DNL Google Analytics] 소스
* 고객의 최초 주문 [!DNL Google Analytics] 중간
* 고객의 최초 주문 [!DNL Google Analytics] campaign

## 차원 만들기

차원을 생성하려면 [Data Warehouse 관리자](../data-warehouse-mgr/tour-dwm.md) 를 클릭합니다. **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### 주문 테이블, 1라운드

이 예에서는 **주문 [!DNL Google Analytics] 소스** 차원.

1. Data Warehouse의 표 목록에서 표를 클릭합니다(여기서는 `orders`) 내의 아무 곳에나 삽입할 수 있습니다.
1. 클릭 **[!UICONTROL Create a Column]**.
1. 열 이름을 지정합니다.
1. 선택 `Joined Column` 에서 [정의 드롭다운](../data-warehouse-mgr/calc-column-types.md). 이 예제에서는 [일대일 관계](../data-warehouse-mgr/table-relationships.md)와 일치 `eCommerce.transactionID` 열을 정확히 하나의 행으로 `orders` 테이블.
1. 그런 다음 사용 중인 테이블과 열이 어떻게 연결되는지를 정의해야 합니다. 을(를) 클릭합니다. `Select a table and column` 드롭다운.
1. 필요한 경로를 사용할 수 없으므로 새 경로를 만들어야 합니다. 클릭 **[!UICONTROL Create new Path]**.
1. 표시되는 창에서 `Many` 다음으로 `orders.order\_id`또는 페이지의 `orders` 주문 ID가 포함된 테이블입니다.
1. 설정 `One` 옆을 찾아 `Google ECommerce` 표를 만든 다음 열을 로 설정합니다. `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. 클릭 **[!UICONTROL Save]** 경로 생성
1. 경로가 추가되면 **[!UICONTROL Select table and column]** 드롭다운을 다시 클릭합니다.
1. 을(를) 찾습니다 `ECommerce` 표를 클릭한 다음 `Source` 열. 이렇게 하면 주문 정보가 소스 정보에 연결됩니다.
1. 테이블 스키마로 돌아가면 **[!UICONTROL Save]** 차원을 다시 생성합니다.

다음은 전체 프로세스를 살펴보겠습니다.

![](../../assets/help_center.gif)

다음을 만들어 보십시오 **주문 [!DNL Google Analytics] 중간** 및 `campaign`. 이 차원에는 큰 변화가 없을 테니 한번 시도해 보세요. 하지만 꼼짝 못하게 되면 체크아웃할 수 있어요 [이 문서의 끝](#stuck) 뭐가 다른지 보려고

### 고객 테이블 {#customers}

이 예에서는 **고객의 최초 주문 [!DNL Google Analytics] 소스** 차원.

1. Data Warehouse의 표 목록에서 표를 클릭합니다(여기서는 `customers`)에 사용할 수 있습니다.
1. 클릭 **[!UICONTROL Create a Column]**.
1. 열 이름을 지정합니다.
1. 이 예제에서는 `is MAX` 다음에서 정의 [정의 드롭다운](../../data-analyst/data-warehouse-mgr/calc-column-types.md). 다음 `is MIN` 가능한 값이 하나만 있는 텍스트 열에 적용되는 경우에도 정의가 작동할 수 있습니다. 중요한 것은 필터를 제대로 설정하도록 하는 것입니다. 나중에 이렇게 합니다.
1. 을(를) 클릭합니다. **[!UICONTROL Select a table and column]** 드롭다운을 선택하고 을(를) 선택합니다. `orders` 표, `Order's [!DNL Google Analytics] source` 열.
1. 클릭 **[!UICONTROL Save]**.
1. 테이블 스키마로 돌아가면 `Options` 드롭다운 `Filters`.
1. 클릭 **[!UICONTROL Add Filter Set]** 그런 다음 `Orders we count` 설정합니다. Adobe에서는 카운트 필터 세트에 포함된 주문만 포함할 수 있으므로 이 필터 세트를 선택해야 합니다.
1. 클릭 **[!UICONTROL Add Filter]**. 고객의 첫 번째 주문을 찾고 싶습니다 [!DNL Google Analytics] 소스. 따라서 필터를 추가해야 합니다.

   _orders.고객의 주문 번호 = 1

   _
1. 클릭 **[!UICONTROL Save]** 차원을 생성합니다.

다음을 만들어 보십시오 **고객의 최초 주문 [!DNL Google Analytics] 중간** 및 `campaign`. 이 차원에는 큰 변화가 없을 테니 한번 시도해 보세요. 하지만 꼼짝 못하게 되면 체크아웃할 수 있어요 [이 문서의 끝](#stuck) 뭐가 다른지 보려고

### 보너스: 주문 테이블, 2라운드

원할 경우 여기에서 정지할 수 있지만, 이 섹션에서는 **고객의 최초 주문 [!DNL Google Analytics] 차원** 우리는 [마지막 섹션](#customers) 로 `orders` 테이블. 이 섹션에서 차원을 만들면 `orders` 표 - `Revenue`, `Number of orders`, `Distinct buyers`, 등 - 사용 [!DNL Google Analytics] 고객의 첫 번째 주문 속성.

이 예에서는 와 함께 합니다 `Customer's first order's [!DNL Google Analytics] source` 차원을 `orders` 테이블.

1. Data Warehouse의 표 목록에서 표를 클릭합니다(여기서는 `orders`) 내의 아무 곳에나 삽입할 수 있습니다.
1. 클릭 **[!UICONTROL Create a Column]**.
1. 열 이름을 지정합니다.
1. 선택 `Joined Column` 정의 드롭다운에서 을 클릭합니다. 이 경우 이전 섹션에서 만든 고객 차원이 `orders` 테이블.
1. 을(를) 클릭합니다. **[!UICONTROL Select a table and column]** 드롭다운을 선택한 다음 `customers` 테이블 및 `Customer's first order's [!DNL Google Analytics] source` 열.
1. 경로가 자동으로 채워지지 않는 경우 고객과 주문 테이블을 가장 잘 연결하는 경로를 선택합니다.
1. 클릭 **[!UICONTROL Save]** 차원을 생성합니다.

다음은 전체 프로세스를 살펴보겠습니다.

![](../../assets/help_center2.gif)

에 참여하여 마무리하십시오. `Customer's first order's` 미디어 및 `campaign` 차원을 `orders` 테이블. 한번 시도해 보고, 우리가 전에 언급했듯이, 체크아웃하세요 [그 기사의 끝](#stuck) 도움이 필요하시면

### 포장

차원 만들기를 완료했으므로 다양한 채널 및 캠페인의 성과를 추적하는 강력한 분석을 만들 수 있습니다. 당신이 시작하기를 열망한다는 것을 알지만, **새 열은 다음 업데이트가 완료될 때까지 사용할 수 없습니다**.

이 문서에서 가장 인기 있는 차원 중 일부를 다루었지만, 목표는 한계입니다. 원하는 항목을 직접 만들거나 다른 선택 사항을 탐색하는 데 도움이 되면 자유롭게 ping을 할 수 있습니다. 

### 나 끼었어! 뭐가 다르죠? {#stuck}

**`Orders`표 #1:** 만들 때 `Order's [!DNL Google Analytics]` 미디어 및 `campaign` 차원에는 12단계에서 선택한 열이 다릅니다. 이 예제에서는 열이 `Source`.

**`Customers`표:** 만들 때 `Customer's first order's [!DNL Google Analytics]` 미디어 및 `campaign` 차원. 차이가 5단계에서 선택한 열이 됩니다. 이 예제에서는 열이 `Order's [!DNL Google Analytics]` 소스.

**`Orders`표 #2:** 가입 시 `Customer's first order's [!DNL Google Analytics]` 미디어 및 `campaign` 열 `orders` 표 차이가 5단계에서 선택한 열이 됩니다. 이 예제에서는 열이 `Customer's first order's [!DNL Google Analytics]` 소스.
