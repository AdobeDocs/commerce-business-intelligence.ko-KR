---
title: ' [!DNL Commerce Intelligence] 환경 이해'
description: ' [!DNL Commerce Intelligence] 환경 작업 및 개선에 대해 알아봅니다.'
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# [!DNL Adobe Commerce Intelligence] 환경

상거래 데이터를 분석할 때 이러한 요인과 일반적인 오해에 대해 알아두십시오. Commerce 스키마를 올바르게 사용하고 있는지 확인하는 데 도움이 필요하면 [지원에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ko)하십시오.

## [!DNL entity\_id]

많은 테이블에 이름이 `entity\_id`인 열이 포함되어 있습니다. `entity\_id`을(를) 포함하는 각 테이블에서 해당 열은 고유한 행을 식별하는 데 사용됩니다.

예를 들어 `sales\_order` 테이블의 각 행은 고유한 순서입니다. 이 테이블의 기본 키는 `entity\_id`입니다. 이 열은 `order\_id`(으)로 생각할 수 있습니다. 별도의 테이블 `customer\_entity`에서 각 행은 고유한 고객을 나타냅니다. 이 테이블의 기본 키는 `customer\_id`(으)로 생각할 수 있는 `entity\_id`이라고도 합니다.

해당 테이블에서 `sales\_order.entity\_id`은(는) `customer\_entity.entity\_id`과(와) 같지 않습니다. `entity\_id`이(가) 포함된 모든 테이블 집합에 대해 true입니다. `table\_A.entity\_id`이(가) `table\_B.entity\_id`과(와) 같지 않습니다.

## [!DNL Guest orders]

고객이 계정(게스트 주문)을 가지고 있지 않고 사이트에서 주문하도록 허용하는 경우 해당 고객은 `customer\_entity` 표에 행으로 채워지지 않습니다. 또한 게스트가 주문한 각 주문의 `sales\_order` 테이블에 null `customer\_id` 값이 있습니다.

따라서 시간에 따른 게스트 동작을 추적하려면 `customer\_email`과(와) 같은 고객 식별자를 사용하여 `sales\_order` 테이블에서 모든 고객 수준 열을 계산해야 합니다.

`sales\_order` 테이블을 고객 테이블로 사용하는 경우 고객 수준 지표를 만들 때 주의해야 합니다. 예를 들어 평균 라이프타임 매출 지표를 고려하십시오. 이 지표는 고객 기반 전반의 평균 라이프타임 매출을 식별하는 데 사용됩니다. 먼저 각 고객에 대해 라이프타임 수익을 반환하는 새 열이 필요합니다. 그런 다음 고객의 평균 라이프타임 매출을 얻으려면 이 열의 평균을 구해야 합니다.

`customer\_entity` 테이블을 사용할 수 있는 경우 각 행은 단일 고객이며 각 고객은 해당 테이블에 한 번만 존재합니다. 따라서 라이프타임 매출 열이 있는 경우 평균 지표를 생성하기만 하면 됩니다. 그러나 `sales\_order` 테이블을 고객 테이블로 사용하는 경우 고객이 여러 행에 있을 수 있습니다. 라이프타임 수익 열을 설정한 후에는 주어진 고객이 수행한 각 주문(행)에 해당 고객의 라이프타임 수익이 표시되지만 전체 평균 지표에 해당 고객을 한 번만 포함시키려고 합니다.

여기에서 중요한 것은 각 고객을 한 번만 포함하도록 하는 필터를 지표에 추가해야 한다는 것입니다. Adobe은 **고객 주문 번호 = 1**&#x200B;에 대해 필터링하는 **고객 수**&#x200B;를 만들어 사용할 것을 권장합니다(다른 필터 중 원치 않는 고객을 제외해야 할 수도 있음). 이 필터를 추가하면 고객 수준 지표에서 각 고객을 한 번만 포함할 수 있습니다.

## 제품 및 카테고리

제품은 여러 카테고리를 가질 수 있으며, 카테고리는 둘 이상의 제품에 대해 사용될 수 있다. 따라서 카테고리 수준 분석을 설정할 때는 올바른 정의를 사용해야 합니다. 최상위 범주를 원하십니까? 두 번째 수준 카테고리? 제품이 여러 최상위 범주에 속할 수 있다면 어떻게 해야 합니까?

Commerce 구현에서 정의한 &#39;의류&#39;(최상위), &#39;겉옷&#39;(두 번째 수준), &#39;바지&#39;(세 번째 수준)의 세 가지 카테고리 수준에 해당하는 한 쌍의 청바지를 상상해 보십시오. 판매된 단위 수별로 카테고리 성능을 분석할 수 있습니다. 이 분석에 필요한 지표는 `sales\_order\_item` 표에 빌드된 _판매된 항목_&#x200B;입니다. 따라서 범주 수준 정보를 항목 테이블로 이동해야 합니다. `sales\_order\_item` 테이블의 각 행에는 연결된 `product\_id`이(가) 있으므로 제품과 관련된 범주를 알고 있으면 해당 정보를 원하는 테이블로 가져올 수 있습니다.

데이터를 이동하기 전에 먼저 적절한 조인과 필터를 알고 있어야 올바른 범주를 잡을 수 있습니다. 어떤 분석에서는 &#39;바지&#39;를 알아야 할 수 있지만, 다른 분석에서는 &#39;의류&#39;가 더 적합할 수 있다. 이는 별도로 식별되는 고유한 범주입니다. 각 범주 수준이 정의되는 방식을 알면 단위 판매를 특정 분석에 적합한 범주에 귀속시킬 수 있습니다.

이제 웹 사이트의 홈 페이지에 `Our Favorites` 최상위 수준의 범주가 있다고 가정해 보겠습니다. 이 청바지를 `Clothing` 범주와 `Our Favorites` 범주 모두에 포함하도록 Commerce 스토어를 구현했을 수 있습니다. 그렇다면, 이 청바지는 하나 이상의 최고 수준의 카테고리를 가지고 있습니다. 이 경우 여러 옵션이 있으므로 단일 최상위 범주를 `sales\_order\_item` 테이블로 이동하는 것은 적절하지 않습니다. 이를 설명하기 위해 Adobe은 특정 범주를 확인하는 예/아니요 열을 생성할 것을 제안합니다. 예를 들어 `Is product in Clothing category?` 및 `Is product in Our Favorites category?` 열을 사용하면 제품이 특정 범주에 속하는지 확인할 수 있습니다.
