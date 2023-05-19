---
title: 광고 캠페인에 대한 ROI 향상
description: 캠페인 성과를 평가하는 몇 가지 방법에 대해 알아봅니다.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# 광고 캠페인 및 ROI

[!DNL Adobe Commerce Intelligence] 을 통해 다음을 쉽게 수행할 수 있습니다. [광고 비용 데이터 및 매출 데이터 결합](../../data-analyst/importing-data/integrations/google-adwords.md) 을 참조하십시오. 이를 통해 ROI(투자 수익률)가 가장 높은 캠페인을 식별할 수 있습니다. 이 항목에서는 캠페인 성과를 평가하는 몇 가지 다른 방법에 대해 알아봅니다.

## 전제 조건

* 광고 비용 데이터 가져오기:
   * [연결 [!DNL Google AdWords] 끝 [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md): 와 동기화됩니다. [!DNL Adwords] 지출 [!DNL Commerce Intelligence]
   * [기타 광고 비용 데이터 업로드](../importing-data/connecting-data/import-offline-ad-data.md): 다음에 대한 직접 커넥터가 없는 채널에 권장됩니다. [!DNL Commerce Intelligence]
   * 여러 소스에서 비용 데이터를 가져오는 경우 다음을 수행할 수 있습니다. [통합](../../best-practices/consolidating-your-tables.md) 의 데이터 [!DNL Commerce Intelligence]. 간단히 [지원 티켓 제출](../../guide-overview.md#Submitting-a-Support-Ticket).
* [사용자 획득 채널 데이터 추적](../analysis/google-track-user-acq.md)

## 사용자 확보 캠페인

사용자 획득을 목표로 하는 캠페인은 다음을 포함하여 다양한 관점에서 측정할 수 있습니다.

1. 캠페인에서 획득한 새 사용자 수
1. 캠페인의 등록에서 구매로의 전환율
1. 평균 사용자 라이프타임 값(LTV)을 기반으로 한 캠페인의 ROI

위의 (1) 및 (2) 분석은 [상위 마케팅 채널 식별](../analysis/most-value-source-channel.md). 여기서는 시간 경과에 따른 캠페인 ROI를 측정하기 위한 분석 (3)을 살펴봅니다. 이는 특정 캠페인에서 획득한 사용자가 획득 비용을 충당할 만큼 충분한 라이프타임 수익을 생성했는지 여부에 대해 설명합니다.

>[!NOTE]
>
>이 예제에서는 모든 캠페인 비용이 신규 사용자를 확보하기 위해 독점적으로 사용되었다고 가정합니다. 실제로 캠페인 비용은 전환되지 않은 방문, 반복 구매자 등을 획득하는 데에도 공유됩니다. 모든 비용이 신규 등록 사용자를 취득하는 데 사용된다고 가정할 경우, 결과 ROI는 최악의 경우(취득당 가장 높은 비용)를 차지합니다. 실제 ROI는 계산보다 더 높습니다.
>
>예: 신규 사용자 10명과 반복 구매자 10명을 생성한 캠페인에 $20를 지출했다고 가정할 때 신규 사용자당 실제 비용은 $1입니다. 그러나 모든 비용이 신규 사용자를 취득하는 데 사용되었다고 가정할 경우, 취득당 비용은 2달러입니다.

**1. 먼저 캠페인별로 광고 비용을 세그먼트화하는 차트를 만듭니다.**

1. 만들기 [!UICONTROL Metric] 시간에 따른 지출을 합산합니다.
1. 다음으로 이동 [!UICONTROL Data > Metrics]
1. 선택 `Add New Metric` 및 선택 [!DNL `Adwords...`] 을(를) 기록하는 테이블 [!DNL AdWords] 비용 데이터.
1. 지표 편집기에서 지표에 이름을 지정합니다(예: [!UICONTROL AdWord Cost])
1. 드롭다운을 사용하여 다음을 수행합니다 **합계** 다음에 있음 `adCost` 열의 [!DNL Adwords...] 테이블(변경) 정렬: `date` 열.
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. 클릭 `Back to Metric List` 을 클릭하고 대시보드로 이동합니다.

1. 캠페인별로 세그먼트를 보내는 보고서 만들기
1. 대시보드에서 을(를) 클릭합니다. [!UICONTROL Add Report > Create report]
1. 다음 항목 선택 [!UICONTROL Adword Cost] 방금 생성한 지표
1. 설정 [!UICONTROL Time period] 끝 `All-time`, 및 [!UICONTROL Interval] 끝 `None`
1. 아래 `Group by` 탭, 추가 `campaign` 다음으로: [!UICONTROL grouping field], 및 클릭 `Add All` 상자에 있습니다.
1. 이 보고서에는 사용자의 모든 시간이 표시됩니다. [!DNL AdWords] 캠페인별 비용

**2. 캠페인별로 새 사용자를 계산하는 보고서를 만듭니다.**

1. 대시보드에서 을(를) 클릭합니다. **[!UICONTROL Add Report > Create report]**
1. 다음 항목 선택 `New users` 시간 경과에 따라 새로 등록된 사용자의 수를 계산하는 지표
1. 설정 [!UICONTROL Time period] 끝 `All-time`, 및 [!UICONTROL Interval] 끝 `None`
1. 아래 `Group by` 탭, 추가 `campaign` 다음으로: `grouping field`, 및 클릭 **`Add All`** 상자 내
1. 이 보고서는 캠페인별로 등록된 모든 사용자를 표시합니다.

**3. 캠페인별로 평균 사용자 LTV를 세그먼트화하는 보고서를 만듭니다.**

1. 대시보드에서 을(를) 클릭합니다. **[!UICONTROL Add Report > Create report]**
1. 다음 항목 선택 `Average lifetime revenue` 평균 사용자의 라이프타임 수익을 계산하는 지표
1. 설정 [!UICONTROL Time period] 끝 `All-time`, 및 [!UICONTROL Interval] 끝 `None`
1. 아래 `Group by` 탭, 추가 `campaign` 또는 `utm\_campaign` 다음으로: [!UICONTROL grouping field], 및 클릭 `Add All` 상자 내
1. 이 보고서는 캠페인별 평균 사용자 라이프타임 매출을 보여 줍니다

**마지막으로, 다음 세 가지 분석을 하나의 보고서에 통합하여 캠페인 ROI를 계산합니다.**

1. 대시보드에서 을(를) 클릭합니다. **[!UICONTROL Add Report > Create new report]**
1. 입력으로 추가하려면 위에 사용된 3개의 지표를 사용하십시오. 각 사용자에게 문자가 할당됩니다(예:\[`A`\], \[`B`\] 및 \[`C`\])
1. [!UICONTROL Cost]: 지표 AdWords 비용을 추가합니다. 변수 \[A\]입니다. 캠페인별로 비용을 반환합니다.
1. [!UICONTROL Users]: 새 사용자 지표 추가 - 변수 \[B\]입니다. 캠페인별 사용자 수를 반환합니다.
1. [!UICONTROL LTV]: 지표 Average Lifetime Revenue를 추가합니다. \[`C`\]. 캠페인에 의한 LTV가 반환됩니다.

1. 차트에 포커스를 둘 수 있도록 차트 옆에 있는 숨기기 아이콘을 클릭합니다
1. 지금 사용 `Add Formula` 이러한 지표를 결합하려면 다음과 같이 하십시오.
1. [!UICONTROL ROI]: 공식 입력 `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, 경우 \[`A`\]은 다음을 나타냅니다. `Ad Cost by Campaigns`, \[`B`\]은 다음을 나타냅니다. `New users by campaigns`, 및 \[`C`\] `LTV by campaigns`. (평균 사용자 LTV - 획득당 평균 비용) / (획득당 평균 비용)의 비율을 반환합니다.
1. [!UICONTROL Avg Return per User]: 공식 입력 **\[`C`\]-(\[`A`\]/\[`B`\])**. (평균 사용자 LTV) - (획득당 평균 비용)을 계산하여 사용자에 대한 평균 마진을 반환합니다.
1. [!UICONTROL CPA]: 공식 입력 **`\[A\]/\[B\]`**. 획득당 실제 캠페인의 비용이 반환됩니다.
1. 포함할 기타 잠재적 지표 [!DNL AdWords] 데이터에는 다음의 합계가 포함됩니다.  `Impressions` 및 `adClicks` (출처: [!DNL AdWords] data), 합계 `number of orders` 특정 캠페인을 통해 만들어집니다.
1. 사용자가 등록하거나 첫 구매를 한 후 30일 및 90일 후에 LTV에 기초하여 ROI를 계산하는 것이 또한 흥미로울 수 있다.

1. 자유롭게 지표와 공식을 클릭하여 드래그하여 보고서의 열을 재정렬하십시오.
1. 보고서 이름을 지정하고 표로 저장하십시오.

## 제품 캠페인

제품별 광고를 하고 있습니까? 그럴 경우 특정 제품에 대한 수익/비용을 계산하여 해당 캠페인에 대한 ROI를 측정할 수 있습니다.

>[!NOTE]
>
>이 예에서는 모든 캠페인 비용이 특정 제품 구매를 생성하는 데 독점적으로 사용되었다고 가정합니다. 모든 비용이 구매 생성에 사용되었다고 가정할 경우, 결과 ROI는 최악의 경우(구매당 최고 비용)를 차지합니다. 실제 ROI는 이 계산보다 더 높습니다. 예: 10명의 새 사용자와 10개의 구매를 생성한 캠페인에 $20를 지출했다고 가정할 때 구매당 실제 비용은 $1입니다. 모든 비용이 신규 사용자를 확보하는 데 들어갔다는 가정 하에 구매 당 비용은 $2이다.

시작하기 전에, [지원 티켓 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 라인 항목 테이블에 다음 차원을 조인하려면(`sales\_flat\_order\_item, order\_item`):

* 주문 출처(사용자 레벨에서만 조회 출처를 추적하는 경우 사용자 출처에 가입)
* 주문 캠페인(사용자 수준에서 추천 소스만 추적하는 경우 사용자의 캠페인에 참여)
* 주문의 매체(사용자 수준에서 조회 출처만 추적하는 경우 사용자의 매체에 가입)

**1. 이제 특정 제품에 대한 캠페인당 매출을 반환하는 차트를 만들어 보십시오.**

1. 대시보드에서 을(를) 클릭합니다. **[!UICONTROL Add Report > Create new report]**
1. 다음 항목 선택 `Revenue by items` 라인 항목 수준에서 매출을 계산하는 지표
1. 설정 [!UICONTROL Time period] 끝 `All-time`, 및 [!UICONTROL Interval] 끝 `None`
1. 아래 `Filter by` 탭, 추가 `product name 'IN'` 제품 `A`, 제품 `B`, 제품 `C`, ...&quot; 및 쉼표로 구분된 캠페인의 타겟팅된 모든 제품 이름(예: `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. 아래 `Group by` 탭, 추가 `order's campaign` 또는 `order's utm\_campaign` 다음으로: `grouping` 필드 및 클릭 **[!UICONTROL Add All]** 상자 내
1. 이 보고서는 캠페인별 특정 제품의 매출을 보여줍니다

**2. ROI를 계산하기 위해 지표를 한 개의 보고서에 다시 결합합니다.**

1. 대시보드에서 을(를) 클릭합니다. **[!UICONTROL Add Report > Create new report]**
1. 추가 `Revenue by items` 지표 를 클릭하고 위의 특정 제품에 대한 캠페인 보고서에서 지침 별로 필터 및 그룹화 를 클릭한 다음 **[!UICONTROL Hide]** 지표의 스칼라 값 아래
1. 이제 추가 [!DNL AdWords Cost] 지표 를 참조하십시오. `Ad cost by campaigns` 에서 탐색한 보고서 `User acquisition campaigns` 위의 섹션; 그런 다음 클릭 **[!UICONTROL Hide]** 지표의 스칼라 값 아래
1. 이러한 지표를 사용하여 공식을 추가합니다.
1. [!UICONTROL ROI]: 공식 입력 `\[A\]/\[B\]`, `\[A\]` 은(는) 을 나타냅니다. `Revenue per campaign for specific product(s)` 및 `\[B\]` 은(는) 을 나타냅니다. `Ad cost by campaigns`. (특정 제품의 수입) / (캠페인 비용)의 비율을 반환합니다.
1. [!UICONTROL Return]: 공식 입력 `\[A\]-\[B\]`. (평균 사용자 LTV) - (획득당 평균 비용)을 계산하여 사용자에 대한 평균 마진을 반환합니다.
1. (선택 사항) [!UICONTROL Revenue]: 숨김 해제 `Revenue by items` 캠페인당 특정 제품의 매출을 보기 위한 지표
1. (선택 사항) [!UICONTROL Cost]: 숨김 해제 `AdWords Cost` 캠페인 비용 보기 지표

1. 보고서에 이름을 지정하고 표로 저장하십시오

**3. 광고한 각 제품 또는 제품 그룹에 대해 위의 1단계와 2단계를 반복합니다.**

## 관련 설명서

* [다음을 통해 주문 참조 소스 추적 [!DNL Google Analytics] 전자 상거래](../importing-data/integrations/google-ecommerce.md)
* [데이터베이스에서 사용자 조회 소스 추적](../analysis/google-track-user-acq.md)
* [데이터베이스에서 사용자 장치, 브라우저 및 OS 데이터 추적](../analysis/track-usr-dev-browser.md)
* [가장 가치 있는 확보 소스 및 채널 살펴보기](../analysis/most-value-source-channel.md)
* [연결 [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [은 어떻게 합니까? [!DNL Google Analytics] UTM 속성이 작동합니까?](../analysis/utm-attributes.md)
* [의 UTM 태그 지정에 대한 5가지 우수 사례 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
