---
title: 세그먼테이션 및 필터링에 대한 권장 데이터 Dimension
description: 세분화 및 필터링 모범 사례에 대해 알아봅니다.
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# 세분화 및 필터링

좋은 세분화는 표층 통계를 의사 결정을 유도하는 비즈니스 지표로 만드는 것입니다.

가장 소중한 고객이 누구인지 알고 싶으십니까? 가장 가치 있는 마케팅 채널은 무엇입니까? 어떤 제품이 더 빨리 움직이고 있으며 그 이유는 무엇입니까? 이러한 답변을 얻으려면 먼저 데이터를 세그먼트화해야 합니다.

이 항목에서는 고객에게 종종 권장되는 중요한 세그먼트를 다룹니다. 또한 이러한 세그먼트가 답변에 도움이 될 수 있는 질문에 대해서도 자세히 설명합니다. 기술적으로 세그먼트는 데이터베이스의 데이터 열입니다. [!DNL Adobe Commerce Intelligence]에서는 차원이라고 합니다.

![](../../mbi/assets/mbi-critical-segments.png)


## 사용자 세그먼트

사용자 세그먼트는 사용자가 누구이며 어떻게 행동하는지를 이해하는 데 도움이 됩니다.

* **연령/출생연도**: 사용자의 나이는 몇 세입니까? 가장 활동적인 사용자는 몇 살입니까? 일반적으로 보다 효과적인 분석을 위해 값을 범위로 버킷하는 것이 적절합니다.
* **성별**: 다른 성별이 웹 사이트에 다르게 참여합니까?
* **주소**: 사용자의 출처는 어디입니까? 특정 지역에 마케팅 노력을 집중해야 합니까? 최근 광고 캠페인이 대상 지역에서 예상대로 수행되었습니까?
* **고객 확보 원본**\: 사용자의 마케팅 채널을 알고 있습니까? 그들이 광고를 클릭하거나 검색으로 당신을 찾았습니까? [사용자 확보 소스별로 데이터 세그먼트화](../data-analyst/analysis/google-track-user-acq.md)은(는) 새 고객 확보를 최적화하는 첫 번째 단계입니다. 2단계는 일하는 것에 더 많은 돈을 쓰고 그렇지 않은 것을 죽이는 것이다.
* **등록 장치**: 사용자가 모바일 앱 또는 웹 사이트를 통해 등록했습니까? iOS 또는 Android™? 모바일 사용자 기반이 모바일 제품을 개발하기 위해 더 많은 리소스를 할당하기에 충분합니까? 아직 추적하지 않는 경우 이 항목 [사용자 장치 추적 정보](../data-analyst/analysis/track-usr-dev-browser.md)를 참조하세요.
* **추천인**: 영향력 있는 리더는 누구입니까? 다른 사용자가 직접 참조한 사용자는 몇 명입니까?
* **업종**: B2B 사업체라면 사용자는 어떤 업종에서 일합니까? 어떤 무역 단체들이 가입할 가치가 있는가?
* **설문 조사 응답**: 고객 설문 조사를 수행하는 경우 응답을 세그먼트로 사용하여 더 자세한 수준의 프로파일링을 만드십시오. 사용자에 대해 이미 알고 있는 내용을 보완하는 질문을 하거나 추측을 확인할 수 있습니다.
* **첫 번째 주문 금액 및 제품 범주**: 사용자의 첫 번째 주문과 향후 구매 패턴 사이에 상관 관계가 있습니까?

## 주문 / 이벤트 세그먼트

순서 및 이벤트 세그먼트는 시간 경과에 따른 사용자 동작 및 참여를 분석하는 데 도움이 됩니다.

* **[!UICONTROL Billing / Shipping Address]**: 대부분의 주문은 어디에서 제공됩니까? 청구와 배송 주소에 차이가 있습니까?
* **[!UICONTROL Status]**: 몇 개의 주문을 완료하지 못했습니까? 지난 7일 동안 보류 중인 주문의 비율은 얼마입니까?
* **[!UICONTROL Customer acquisition source]**: 사용자 수준에서 사용자 획득 데이터를 추적하는 것 외에 주문 또는 이벤트 수준에서 [추적할 수도 있습니다](../data-analyst/analysis/google-track-user-acq.md). 하나의 소스를 통해 등록한 사용자는 다른 소스를 통해 사이트에 계속 액세스할 수 있습니다.
* **[!UICONTROL Device]**: 모바일 주문 수가 증가하고 있습니까? 모바일 구매를 통해 창출되는 매출의 양은 얼마입니까? (아직 추적하지 않는 경우 이 항목 [추적 순서 장치 데이터 정보](../data-analyst/analysis/track-usr-dev-browser.md)를 참조하세요.
* **[!UICONTROL Fulfillment Center]**: 가장 많은 매출을 창출하고 있는 이행 센터 중 하나 주문 시간과 배송 시간의 차이를 분석한다면 어떤 이행 센터가 가장 반응이 좋습니까?
* **[!UICONTROL Delivery Carrier]**: 가장 인기 있는 통신사는 어디입니까? 반품되는 물품이 가장 적은 항공사는 어디인가요?
* **[!UICONTROL Discount / Coupon Codes]**: 프로모션으로 인해 추가 비즈니스가 발생합니까? 할인 상품 이외에 추가로 몇 개의 상품을 구매하셨습니까? 쿠폰은 평균 주문 금액에 어떤 영향을 줍니까? 할인된 것과 할인되지 않은 것의 평균 마진은 얼마입니까?
* **[!UICONTROL Satisfaction / Rating]**: 고객이 주문에 대해 얼마나 만족하고 있습니까? 고객이 비즈니스를 귀하에게 추천할 것 같습니까?

## 제품 세그먼트

제품 세그먼트는 머천다이징 결정을 내리는 데 도움이 됩니다.

* **[!UICONTROL Merchant / Brand]**: 특정 브랜드의 판매가 다른 브랜드보다 빠릅니까? 성과가 낮은 브랜드는 무엇입니까?
* **[!UICONTROL Type / Category]**: 다른 사용자 세그먼트가 다른 유형의 제품을 사용합니까? 가장 많이 반복되는 비즈니스를 창출하는 제품 범주는 무엇입니까?
* **[!UICONTROL Discount / Coupon Codes]**: 프로모션으로 인해 할인되지 않은 제품의 판매가 손상됩니까? 쿠폰은 제품의 인식 가치에 어떤 영향을 줍니까?
* **[!UICONTROL Social Activity]**: 소셜 미디어에서 생성된 버즈와 제품 판매 수량 간에 상관 관계가 있습니까?
* **[!UICONTROL Size / Variant]**: 각 변형에 필요한 재고 비율은 얼마입니까? 할인된 가격으로 판매할 수 있는 변종은 무엇입니까?

머천다이징에 관심이 있는 경우 [제품 세그먼트를 사용하여 반복 비즈니스를 추진하는 방법](../data-analyst/analysis/most-value-source-channel.md)을 확인하십시오.

## 고객 프로필 설정

세분화 전문가는 1차원 슬라이스를 넘어 실제 고객 프로필을 설정하기를 원할 수 있습니다. 예를 들어 모바일 기기를 통해 등록한 13세에서 24세 사이의 사람들은 &quot;Young &amp; Mobile&quot; 그룹에 가입했습니다. 이 그룹의 행동은 사용자의 나머지 사용자 기반과 어떻게 비교됩니까?

이런 종류의 분석은 Fortune지 선정 1000대 기업의 마케터들이 하루 종일 하는 일입니다. [!DNL Commerce Intelligence]과(와) 같은 클라우드 기반 비즈니스 인텔리전스 플랫폼이 등장하기 전에는 대부분 우리 모두에게 미치지 못했습니다. 다행스럽게도, 그것은 더 이상 사실이 아니다.

## 새 세그먼트 추적

위의 차원으로 지표를 세그먼트화하는 첫 번째 단계는 데이터베이스에서 이 데이터를 추적하고 있는지 확인하는 것입니다. 추적되지 않는 경우 기술 팀과 만나 이 데이터 추적을 시작하는 방법을 찾으십시오.

데이터베이스에서 데이터가 추적되는지 확인한 후 [지원 팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ko)하여 [!DNL Commerce Intelligence] 지표 및 차트로 차원을 푸시합니다. *필드 관리* 도구를 사용하여 [!DNL Commerce Intelligence]에서 이러한 필드를 추적할 수도 있습니다.

## 관련 항목

* [분석을 위해 데이터베이스 최적화](../best-practices/opt-db-analysis.md)
