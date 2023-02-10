---
title: 광고 캠페인에 대한 ROI 증대
description: 캠페인 성과를 평가하는 몇 가지 다른 방법에 대해 알아봅니다.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# 광고 캠페인 및 ROI

MBI를 사용하면 쉽게 다음을 수행할 수 있습니다 [광고 비용 데이터 및 매출 데이터](../../data-analyst/importing-data/integrations/google-adwords.md) 데이터베이스 ROI가 가장 높은 캠페인을 식별하는 데 도움이 됩니다. 이 문서에서는 캠페인 성과를 평가하는 몇 가지 방법을 알아봅니다.

## 전제 조건

* 광고 비용 데이터를 가져옵니다:
   * [연결 [!DNL Google AdWords] to [!DNL MBI]](../importing-data/integrations/google-adwords.md): 그러면 자동으로 [!DNL Adwords] 지출 [!DNL MBI]
   * [다른 광고 비용 데이터 업로드](../importing-data/connecting-data/import-offline-ad-data.md): 직접 연결되는 커넥터가 없는 채널에 대해 권장됩니다 [!DNL MBI]
   * 여러 소스에서 비용 데이터를 가져오면 다음을 수행할 수 있습니다 [통합](../../best-practices/consolidating-your-tables.md) 의 데이터 [!DNL MBI]. 간단히 [지원 티켓 제출](../../guide-overview.md).
* [사용자 획득 채널 데이터 추적](../analysis/google-track-user-acq.md)

## 사용자 획득 캠페인

사용자 획득을 목표로 하는 캠페인은 다음을 포함하여 다양한 관점에서 측정할 수 있습니다.

1. 캠페인으로 획득한 새 사용자 수
1. 등록에서 캠페인 구매로의 전환율
1. 평균 사용자 라이프타임 값(LTV)을 기반으로 한 캠페인의 ROI

위의 분석(1) 및 (2)은 [상위 마케팅 채널 식별](../analysis/most-value-source-channel.md). 여기에서는 시간에 따른 캠페인 ROI를 측정하기 위해 분석(3)을 살펴봅니다. 이는 특정 캠페인에서 획득한 사용자가 자신의 획득 비용을 충당할 만큼 충분한 라이프타임 매출을 생성했는지 여부에 따라 달라집니다.

>[!NOTE]
>
>우리는 모든 캠페인 비용이 신규 사용자를 얻는 데 독점적으로 사용되었다고 가정합니다. 실제로 캠페인 비용은 전환되지 않은 방문, 반복 구매자 등을 획득하는 경우에도 공유됩니다. 그러나 등록된 신규 사용자를 확보하는 데 모든 비용이 사용된다고 가정하면 결과 ROI가 최악의 경우 시나리오(취득당 비용이 가장 많음)를 계산하므로 실제 ROI가 계산보다 높다는 것을 확인할 수 있습니다.
>
>예: 새 사용자 10명과 반복 구매자 10명을 생성한 캠페인에서 20달러를 사용한다고 가정할 경우, 신규 사용자당 실제 비용은 1달러이지만, 모든 비용이 신규 사용자를 획득하는 것으로 간주되는 경우, 획득당 비용은 2달러입니다.)

**1. 먼저 캠페인별로 광고 비용을 세그먼트화하는 차트를 만듭니다.**

1. 만들기 [!UICONTROL Metric] 시간 경과에 따른 비용을 합합니다
1. 이동 [!UICONTROL Data > Metrics]
1. 선택 `Add New Metric` 을(를) 선택하고 을(를) 선택합니다. [!DNL `Adwords...`] 기록되는 테이블 [!DNL AdWords] 비용 데이터.
1. 지표 편집기에서 지표에 이름을 지정합니다(예: [!UICONTROL AdWord Cost])
1. 드롭다운을 사용하여 다음을 수행합니다. **합계** on `adCost` 열 [!DNL Adwords...] 테이블(변경) `date` 열.
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. 이제 다 끝났어 클릭 `Back to Metric List` 맨 위에 있는 대시보드로 이동합니다.

1. 캠페인별로 세그먼트를 사용한 보고서를 만듭니다
1. 대시보드에서 [!UICONTROL Add Report > Create new report]
1. 을(를) 선택합니다 [!UICONTROL Adword Cost] 방금 만든 지표
1. 설정 [!UICONTROL Time period] to `All-time`, 및 [!UICONTROL Interval] to `None`
1. 아래에 `Group by` 탭, 추가 `campaign` 로서의 [!UICONTROL grouping field]를 클릭하고 `Add All` 상자에 표시합니다.
1. 이 보고서에는 항상 표시됩니다 [!DNL AdWords] 캠페인별 비용

**2. 그러면 캠페인별로 새 사용자를 계산하는 보고서를 만듭니다.**

1. 대시보드에서 **[!UICONTROL Add Report > Create new report]**
1. 을(를) 선택합니다 `New users` 시간 경과에 따라 등록된 새 사용자의 수를 계산하는 지표
1. 설정 [!UICONTROL Time period] to `All-time`, 및 [!UICONTROL Interval] to `None`
1. 아래에 `Group by` 탭, 추가 `campaign` 로서의 `grouping field`를 클릭하고 **`Add All`** 상자에서
1. 이 보고서는 캠페인별로 등록된 모든 사용자를 보여줍니다

**3. 캠페인별로 평균 사용자 LTV를 세그먼트화하는 보고서를 만들겠습니다.**

1. 대시보드에서 **[!UICONTROL Add Report > Create new report]**
1. 을(를) 선택합니다 `Average lifetime revenue` 평균 사용자의 라이프타임 매출을 계산하는 지표
1. 설정 [!UICONTROL Time period] to `All-time`, 및 [!UICONTROL Interval] to `None`
1. 아래에 `Group by` 탭, 추가 `campaign` 또는 `utm\_campaign` 로서의 [!UICONTROL grouping field]를 클릭하고 `Add All` 상자에서
1. 이 보고서는 캠페인별 평균 사용자 라이프타임 매출을 보여줍니다

**마지막으로 다음 세 가지 분석을 하나의 보고서에 통합하여 캠페인 ROI를 계산합니다.**

1. 대시보드에서 **[!UICONTROL Add Report > Create new report]**
1. 를 입력으로 추가하여 위에 사용한 세 개의 지표를 사용하게 됩니다. 각각 문자(예:\[)가 할당됩니다`A`\], \[`B`\] 및 \[`C`\])
1. [!UICONTROL Cost]: 지표 AdWords 비용을 추가합니다. 변수 \[A\]입니다. 이렇게 하면 캠페인별로 비용이 반환됩니다.
1. [!UICONTROL Users]: 지표를 추가합니다. 새 사용자 - 변수 \[B\]입니다. 이렇게 하면 캠페인별 사용자 수가 반환됩니다.
1. [!UICONTROL LTV]: 지표 추가 평균 라이프타임 매출 - 변수 \[`C`\] 이렇게 하면 캠페인에서 LTV를 반환하게 됩니다.

1. 표에 집중할 수 있도록 차트 단어 옆에 있는 숨기기 아이콘을 클릭합니다
1. 이제 `Add Formula` 다음과 같이 이러한 지표를 결합하려면,
1. [!UICONTROL ROI]: 공식을 입력합니다 `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, \[ 인 경우`A`\] 는 `Ad Cost by Campaigns`, \[`B`\] 는 `New users by campaigns`, 및 \[`C`\] `LTV by campaigns`. 이 경우 비율(평균 사용자 LTV - 획득당 평균 비용) / (획득당 평균 비용)이 반환됩니다
1. [!UICONTROL Avg Return per User]: 공식을 입력합니다 **\[`C`\]-(\[`A`\]/\[`B`\])**. 이를 통해 사용자가 계산(평균 사용자 LTV) - (획득당 평균 비용)을 통해 수행한 평균 마진을 반환합니다.
1. [!UICONTROL CPA]: 공식을 입력합니다 **`\[A\]/\[B\]`**. 이렇게 하면 실제 캠페인의 획득당 비용이 반환됩니다.
1. 포함할 다른 잠재적 지표 [!DNL AdWords] 데이터에는 합계가 포함됩니다  `Impressions` 및 `adClicks` (부터) [!DNL AdWords] 데이터), `number of orders` 특정 캠페인을 통해 수행될 수 있습니다.
1. 사용자가 등록하거나 처음 구매한 후 30일 및 90일 후의 LTV를 기반으로 ROI를 계산하는 것도 흥미로울 수 있습니다.

1. 자유롭게 지표와 수식을 클릭하여 드래그하여 보고서의 열을 재정렬할 수 있습니다
1. 보고서 이름을 지정하고 표로 저장해야 합니다.

## 제품 캠페인

제품별 광고를 하고 있습니까? 그럴 경우 특정 제품에 대한 수입/비용을 계산하여 해당 캠페인의 ROI를 측정할 수 있습니다.

>[!NOTE]
>
>모든 캠페인 비용이 특정 제품의 구매를 생성하는 데 독점적으로 사용되었다고 가정합니다. 구매 생성에 모든 비용이 사용되었다고 가정할 경우, 결과 ROI는 최악의 경우 시나리오(구매당 가장 높은 비용)를 차지하므로 실제 ROI가 이 계산보다 높다는 것을 확인할 수 있습니다. 예: 새 사용자 10명과 구매 10명을 생성한 캠페인에서 20달러를 소비한 것으로 가정할 경우 구매당 실제 비용은 1달러이지만, 모든 비용이 새 사용자를 확보했다고 가정할 때 구매당 비용은 2달러입니다.)*

시작하기 전에 [지원 티켓 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 라인 항목 테이블에 다음 차원을 조인하려면`sales\_flat\_order\_item, order\_item`):

* 주문 출처(사용자 수준에서 참조 소스만 추적하는 경우 사용자 소스에 가입)
* 주문 캠페인(사용자 수준에서 참조 소스만 추적하는 경우 사용자 캠페인에 가입)
* 주문 매체(사용자 수준에서 참조 소스만 추적하는 경우 사용자 매체에 가입)

**1. 이제 특정 제품에 대한 캠페인당 매출을 반환하는 차트를 만들어 시작합니다.**

1. 대시보드에서 **[!UICONTROL Add Report > Create new report]**
1. 을(를) 선택합니다 `Revenue by items` 라인 항목 수준에서 매출을 계산하는 지표
1. 설정 [!UICONTROL Time period] to `All-time`, 및 [!UICONTROL Interval] to `None`
1. 아래에 `Filter by` 탭, 추가 `product name 'IN'` 제품 `A`, 제품 `B`, 제품 `C`,..&quot; 캠페인에서 타겟팅한 모든 제품 이름을 쉼표로 구분하여 포함합니다(예: `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. 아래에 `Group by` 탭, 추가 `order's campaign` 또는 `order's utm\_campaign` 로서의 `grouping` 필드를 입력하고 **[!UICONTROL Add All]** 상자에서
1. 이 보고서는 캠페인별 특정 제품에 대한 매출액을 보여줍니다

**2. ROI를 계산하기 위해 한 보고서에 지표를 다시 결합합니다.**

1. 대시보드에서 **[!UICONTROL Add Report > Create new report]**
1. 추가 `Revenue by items` 지표, 위의 특정 제품에 대한 캠페인의 지침에 따라 필터 및 그룹을 수행한 다음 **[!UICONTROL Hide]** 지표의 스칼라 값 아래에 있습니다
1. 이제 를 추가합니다. [!DNL AdWords Cost] 지표, 다음에서 지침에 따라 필터 및 그룹화를 수행합니다 `Ad cost by campaigns` 우리가 조사한 보고서 `User acquisition campaigns` 위의 섹션 을 클릭한 다음 **[!UICONTROL Hide]** 지표의 스칼라 값 아래에 있습니다
1. 이러한 지표가 준비되면 이제 공식을 추가합니다.
1. [!UICONTROL ROI]: 공식을 입력합니다 `\[A\]/\[B\]`이면 `\[A\]` 표시 `Revenue per campaign for specific product(s)` 및 `\[B\]` 표시 `Ad cost by campaigns`. 이 경우 비율(특정 제품에 대한 수입) / (캠페인 비용)이 반환됩니다
1. [!UICONTROL Return]: 공식을 입력합니다 `\[A\]-\[B\]`. 이를 통해 사용자는 계산(평균 사용자 LTV) - (획득당 평균 비용)을 통해 평균 마진을 반환합니다
1. (선택 사항) [!UICONTROL Revenue]: 숨김 취소 `Revenue by items` 캠페인당 특정 제품에 대한 매출을 확인하는 지표
1. (선택 사항) [!UICONTROL Cost]: 숨김 취소 `AdWords Cost` 캠페인 비용 보기 지표

1. 보고서에 이름을 지정하고 표로 저장합니다

**3. 광고된 각 제품이나 제품 그룹에 대해 위의 1단계와 2단계를 반복합니다.**

## 관련 설명서

* [를 통해 주문 참조 소스 추적 [!DNL Google Analytics] 전자 상거래](../importing-data/integrations/google-ecommerce.md)
* [데이터베이스에서 사용자 참조 소스 추적](../analysis/google-track-user-acq.md)
* [데이터베이스에서 사용자 장치, 브라우저 및 OS 데이터 추적](../analysis/track-usr-dev-browser.md)
* [가장 가치 있는 획득 소스 및 채널 살펴보기](../analysis/most-value-source-channel.md)
* [연결 [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [어떻게 [!DNL Google Analytics] UTM 속성 작업?](../analysis/utm-attributes.md)
* [의 UTM 태깅에 대한 5가지 우수 사례 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
