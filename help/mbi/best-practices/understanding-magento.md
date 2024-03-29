---
title: 이해 [!DNL Commerce Intelligence] 환경
description: 을(를) 사용하여 작업하고 개선하는 방법에 대해 알아봅니다. [!DNL Commerce Intelligence] 환경.
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# 사용자 [!DNL Adobe Commerce Intelligence] 환경

상거래 데이터를 분석할 때 이러한 요인과 일반적인 오해에 대해 알아두십시오. 상거래 스키마를 올바르게 사용하고 있는지 확인하는 데 도움이 필요한 경우 주저하지 말고 [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## [!DNL entity\_id]

많은 테이블에 이름이 인 열이 포함되어 있습니다. `entity\_id`. 을 포함하는 각 테이블에서 `entity\_id`: 해당 열은 고유한 행을 식별하는 데 사용됩니다.

예를 들어, `sales\_order` 테이블은 고유한 순서입니다. 이 테이블의 기본 키를 호출합니다. `entity\_id`. 이 열은 다음과 같이 생각할 수 있습니다. `order\_id`. 별도의 테이블에서, `customer\_entity`, 각 행은 고유한 고객을 나타냅니다. 이 테이블의 기본 키도 호출됩니다. `entity\_id`로 생각할 수 있습니다. `customer\_id`.

그 테이블들, `sales\_order.entity\_id` 다음과 같지 않음 `customer\_entity.entity\_id`. 이 값은 가 포함된 모든 테이블 집합에 대해 true입니다. `entity\_id`: `table\_A.entity\_id` 다음과 같지 않음 `table\_B.entity\_id`.

## [!DNL Guest orders]

고객이 계정(게스트 주문)을 보유하지 않고 사이트에서 주문하도록 허용하는 경우 해당 고객은 의 행으로 채워지지 않습니다. `customer\_entity` 테이블. 또한, 손님이 주문한 각 주문은 null입니다 `customer\_id` 다음에 대한 값 `sales\_order` 테이블.

따라서 시간이 지남에 따라 게스트의 행동을 추적하려면 모든 고객 수준 열을 `sales\_order` 테이블, 고객 식별자 사용 `customer\_email`.

를 사용하는 경우 `sales\_order` 테이블을 고객 테이블로 사용하는 경우 고객 수준 지표를 만들 때 주의해야 합니다. 예를 들어 평균 라이프타임 매출 지표를 고려하십시오. 이 지표는 고객 기반 전반의 평균 라이프타임 매출을 식별하는 데 사용됩니다. 먼저 각 고객에 대해 라이프타임 수익을 반환하는 새 열이 필요합니다. 그런 다음 고객의 평균 라이프타임 매출을 얻으려면 이 열의 평균을 구해야 합니다.

다음을 사용할 수 있는 경우 `customer\_entity` 테이블, 각 행은 단일 고객이며 각 고객은 해당 테이블에만 한 번만 존재합니다. 따라서 라이프타임 매출 열이 있는 경우 평균 지표를 생성하기만 하면 됩니다. 그러나 를 사용하는 경우 `sales\_order` 표는 고객 표로, 고객은 잠재적으로 수많은 행에 존재할 수 있습니다. 라이프타임 수익 열을 설정한 후에는 주어진 고객이 수행한 각 주문(행)에 해당 고객의 라이프타임 수익이 표시되지만 전체 평균 지표에 해당 고객을 한 번만 포함시키려고 합니다.

여기에서 중요한 것은 각 고객을 한 번만 포함하도록 하는 필터를 지표에 추가해야 한다는 것입니다. Adobe을 사용하면 이름이 인 필터 세트를 만들고 사용할 수 있습니다. **We가 카운트하는 고객** 다음에 대한 필터 **고객의 주문 번호 = 1** (다른 필터 중에서 원하지 않는 고객을 제외해야 할 수도 있습니다.) 이 필터를 추가하면 고객 수준 지표에서 각 고객을 한 번만 포함할 수 있습니다.

## 제품 및 카테고리

제품은 여러 카테고리를 가질 수 있으며, 카테고리는 둘 이상의 제품에 대해 사용될 수 있다. 따라서 카테고리 수준 분석을 설정할 때는 올바른 정의를 사용해야 합니다. 최상위 범주를 원하십니까? 두 번째 수준 카테고리? 제품이 여러 최상위 범주에 속할 수 있다면 어떻게 해야 합니까?

상거래 구현에 정의된 대로 &#39;의류&#39;(최상위), &#39;겉옷&#39;(두 번째 수준), &#39;바지&#39;(세 번째 수준)의 세 가지 카테고리 수준에 해당하는 한 쌍의 청바지를 상상해 보십시오. 판매된 단위 수별로 카테고리 성능을 분석할 수 있습니다. 이 분석에 필요한 지표는 다음과 같습니다. _판매된 항목_: `sales\_order\_item` 테이블. 따라서 범주 수준 정보를 항목 테이블로 이동해야 합니다. 의 각 행 `sales\_order\_item` 테이블에 연결된 이(가) 있습니다 `product\_id`, 따라서 제품과 관련된 카테고리를 알고 있는 경우 해당 정보를 원하는 테이블로 가져올 수 있습니다.

데이터를 이동하기 전에 먼저 적절한 조인과 필터를 알고 있어야 올바른 범주를 잡을 수 있습니다. 어떤 분석에서는 &#39;바지&#39;를 알아야 할 수 있지만, 다른 분석에서는 &#39;의류&#39;가 더 적합할 수 있다. 이는 별도로 식별되는 고유한 범주입니다. 각 범주 수준이 정의되는 방식을 알면 단위 판매를 특정 분석에 적합한 범주에 귀속시킬 수 있습니다.

이제, 여러분도 또한 `Our Favorites` 웹 사이트의 홈 페이지에 있는 최상위 카테고리입니다. 이 청바지를 두 제품에 모두 포함하도록 Commerce 스토어를 구현했을 수 있습니다. `Clothing` 범주 및 `Our Favorites` 범주. 그렇다면, 이 청바지는 하나 이상의 최고 수준의 카테고리를 가지고 있습니다. 이 경우 단일 최상위 범주를 (으)로 이동 `sales\_order\_item` 여러 가지 옵션이 있으므로 표는 적절하지 않습니다. 이를 설명하기 위해 Adobe은 특정 범주를 확인하는 예/아니요 열을 생성할 것을 제안합니다. 예를 들어, `Is product in Clothing category?` 및 `Is product in Our Favorites category?` 열을 사용하면 제품이 특정 범주에 속하는지 확인할 수 있습니다.
