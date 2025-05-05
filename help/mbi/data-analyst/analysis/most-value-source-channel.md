---
title: 가장 중요한 마케팅 소스 및 채널 식별
description: 가장 중요한 마케팅 채널을 파악하는 데 사용할 수 있는 몇 가지 보고서에 대해 알아봅니다.
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# 성공적인 마케팅 소스 식별

대상을 조사하고, 캠페인을 만들고, 몇 가지 마케팅 채널에 투자했습니다. 이제 시간이 좀 지났는데, 그 채널들은 어떻게 수행하고 있습니까? 어떤 채널에서 가장 새로운 사용자를 확보했습니까? 전체 매출에 가장 많은 기여를 한 소스는 무엇입니까?

[!DNL Adobe Commerce Intelligence]을(를) 사용하면 [[!DNL [Google Analytics' UTM fields]]](https://support.google.com/analytics/answer/1191184?hl=en)에 해당하는지 또는 사용자 지정 데이터 필드에 해당하는지 여부에 관계없이 조회 원본별로 매출과 사용자를 쉽게 세그먼트화할 수 있습니다. 이 세그먼테이션을 사용하면 가장 성과가 좋은 채널을 찾아 마케팅 예산을 더 잘 투자할 수 있습니다.

이 주제에서는 가장 가치 있는 마케팅 채널을 파악하는 데 사용할 수 있는 몇 가지 보고서에 대해 알아봅니다.

* [소스별 새 사용자](#newusersbysource)
* [사용자 소스별 평균 라이프타임 수익](#avglifetimerev)
* [사용자 소스별 평균 주문 가격](#avgorderval)
* [사용자 등록 날짜 및 소스별 매출](#revbyregdateandsource)
* [사용자 소스별 반복 주문](#repeatordersbysource)

## 전제 조건 {#prereqs}

이 주제에서 분석을 작성하려면 마케팅 획득/참조 소스 데이터에 액세스해야 합니다. 아직 추적하지 않는 경우 [주문 참조 소스 데이터를  [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)에서 [!DNL Adobe Commerce Intelligence] (으)로 가져와야 계속할 수 있습니다. 또한 사용자 장치 정보를 분석에 추가하면 추천에서 사용 중인 기술을 확인할 수 있습니다.

## 소스별 새 사용자 {#newusersbysource}

추천 소스의 성과를 평가하는 것은 가장 가치 있는 채널을 결정하는 데 핵심입니다. 이 보고서는 시간이 지남에 따라 획득 소스별로 새로 등록된 사용자 수를 표시하므로 신규 등록된 사용자를 획득하는 데 있어 조회 소스의 성과를 추적할 수 있습니다.

[Report Builder](../../tutorials/using-visual-report-builder.md)에서 이 보고서를 만들려면 **새 사용자** 지표(또는 시간에 따라 새 사용자의 수를 계산하는 해당 지표)를 보고서에 추가하십시오. 그런 다음 다음을 수행합니다.

1. [!UICONTROL Time Period]을(를) 분석할 등록 기간으로 설정합니다.
1. [!UICONTROL Interval]을(를) 월별로 설정합니다.
1. [!UICONTROL Group By]을(를) 획득(또는 참조) 소스로 설정하고 포함할 소스를 선택하십시오.
1. 이 예제에서는 `stacked columns` [!UICONTROL chart type]을(를) 사용합니다.

다음은 시각적 연습입니다.

![소스 보고서별 새 사용자 만들기.](../../assets/New_Users_by_source.gif)

## 사용자 소스별 평균 라이프타임 수익 {#avglifetimerev}

새로운 사용자를 유도하는 채널을 찾는 것도 중요하지만, 이러한 추천이 전체적으로 얼마나 가치가 있습니까? 이 보고서는 시간에 따른 특정 획득 소스에서 가져온 사용자의 평균 라이프타임 수익을 보여줍니다. 즉, 특정 소스에서 가져온 사용자가 다른 소스에서 가져온 사용자 그룹보다 라이프타임 동안 사용자와 더 많이 시간을 보내는지 여부를 확인할 수 있습니다.

Report Builder에서 이 보고서를 만들려면 보고서에 **평균 라이프타임 수익** 지표를 추가하십시오. 그런 다음 다음을 수행합니다.

1. [!UICONTROL Time Period]을(를) 분석할 기간으로 설정합니다.
1. [!UICONTROL Interval]을(를) 월별로 설정합니다.
   획득(또는 참조) 소스로 [!UICONTROL Group By]하고 포함할 소스를 선택하십시오.
1. 이 예제에서는 `line chart` 형식을 사용합니다.

다음은 시각적 연습입니다.

![사용자 원본별 평균 수명 수익 만들기](../../assets/Lifetime_revenue_by_user_source.gif).

이 예제에서는 라이프타임 매출만 살펴보지만, 이 분석을 복제하여 조회 원본별로 [!UICONTROL Number of orders] 또는 [!UICONTROL Distinct buyers]을(를) 살펴볼 수도 있습니다.

## 사용자 소스별 평균 주문 가격 {#avgorderval}

특정 획득 소스의 사용자가 지출하는 금액에 대해 더 잘 이해하기 위해, 평균 주문 값을 조회하는 보고서를 작성할 수 있습니다. 이를 통해 특정 소스에서 가져온 사용자가 다른 소스의 사용자보다 주문당 더 많은 비용을 지출하는지 여부를 추적할 수 있습니다.

Report Builder에서 이 보고서를 만들려면 **평균 순서 값** 지표를 추가한 후 다음을 수행하십시오.

1. [!UICONTROL Time Period]을(를) 분석할 등록 기간으로 설정합니다.
1. [!UICONTROL Time Interval]을(를) 월별로 설정합니다.
1. [!UICONTROL Group By]을(를) 획득(또는 참조) 소스로 설정하고 포함할 소스를 선택하십시오.
1. 이 예제에서는 **스택 열** 차트 유형을 사용합니다.

다음은 시각적 연습입니다.

![사용자 원본별 평균 주문 값을 만드는 중입니다.](../../assets/Average_order_value_by_source.gif)

## 사용자 등록 날짜 및 소스별 총 수익 {#revbyregdateandsource}

앞에서 다룬 라이프타임 수익 분석을 통해 다양한 소스에서 획득한 사용자의 평균 라이프타임 수익을 살펴볼 수 있지만, 전체 라이프타임 수익은 어떻게 됩니까? 이 보고서를 통해 특정 시간 동안 및 특정 소스에서 등록한 전체 수익 사용자가 얼마나 많이 생성하는지 식별할 수 있습니다.

Report Builder에서 이 보고서를 만들려면 `Revenue by user registration date` 지표를 추가하십시오. [이 지표를 아직 만들지 않은 경우](../../data-user/reports/ess-manage-data-metrics.md) `Revenue` 지표를 복제하고 `time stamp`을(를) 사용자의 `creation date`(으)로 변경하면 됩니다. 지표를 추가한 후 다음을 수행합니다.

1. [!UICONTROL Time Period]을(를) 분석할 등록 기간으로 설정합니다.
1. [!UICONTROL Time Interval]을(를) 월별로 설정합니다.
1. [!UICONTROL Group By]을(를) 획득(또는 참조) 소스로 설정하고 포함할 소스를 선택하십시오.
1. 이 예제에서는 `stacked columns` 차트 유형을 사용합니다.

다음은 시각적 연습입니다.

![사용자 등록 날짜 및 원본 보고서별 총 매출을 만드는 중입니다.](../../assets/Revenue_by_user_registration_date_and_source.gif)

## 사용자 소스별 반복 주문 {#repeatordersbysource}

평균 주문 가격 보고서는 특정 출처에서 획득한 사용자가 주문을 할 때 소비한 금액을 평균적으로 보여줍니다. 그러나 이 보고서는 동일한 사용자가 반복 고객인 경우에는 표시하지 않습니다. 그러나 사용자 소스에 의한 반복 주문 수를 통해 특정 소스의 사용자가 반복 구매를 더 많이 하는지 또는 더 적게 하는지를 확인할 수 있습니다.

[Report Builder](../../tutorials/using-visual-report-builder.md)에서 이 보고서를 만들려면 **주문 수** 지표를 추가하고 다음을 수행하십시오.

1. [!UICONTROL Time Period]을(를) 분석할 등록 기간으로 설정합니다.
1. [!UICONTROL Time Interval]을(를) 월별로 설정합니다.
1. 반복 주문이 있는 사용자만 포함하도록 [!UICONTROL filter]을(를) 추가합니다.

   사용자 주문 번호가 1보다 큼

1. [!UICONTROL Group By]을(를) 획득(또는 참조) 소스로 설정하고 포함할 소스를 선택하십시오.
1. 이 예제에서는 `stacked columns` 차트 유형을 사용합니다.

다음은 시각적 연습입니다.

![사용자 원본별 반복 주문 보고서를 만드는 중입니다.](../../assets/Repeat_orders_by_user_source.gif)


## 요약 {#wrapup}

이 주제는 획득 및 마케팅 채널의 가치를 분석하는 데 사용할 수 있는 몇 가지 분석에 대해 언급했지만, 이는 빙산의 일각에 불과합니다.

## 관련 항목 {#related}

* [ [!DNL Google ECommerce]을(를) 통한 주문 조회 원본 추적](../importing-data/integrations/google-ecommerce.md)
* [ [!DNL Google Adwords] 계정 연결 중](../importing-data/integrations/google-adwords.md)
* [주문 및 고객 데이터를 사용하여  [!DNL Google ECommerce] 차원 작성](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [ [!DNL Google Analytics]의 UTM 태그 지정에 대한 우수 사례](../../best-practices/utm-tagging-google.md)
