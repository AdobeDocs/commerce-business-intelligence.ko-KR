---
title: 가장 가치 있는 마케팅 소스 및 채널 식별
description: 가장 가치 있는 마케팅 채널을 파악하는 데 사용할 수 있는 몇 가지 보고서에 대해 알아봅니다.
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---

# 성공적인 마케팅 소스 식별

대상을 조사했고, 캠페인을 만들고, 몇 개의 마케팅 채널에 투자를 했습니다. 시간이 지남에 따라 해당 채널들은 어떻게 수행됩니까? 가장 새로운 사용자를 가져온 채널은 무엇입니까? 총 매출에 가장 많은 기여를 한 회사는?

사용 [!DNL MBI]과 같은 위치에 상관없이 참조 소스별로 매출과 사용자를 쉽게 세그먼트화할 수 있습니다 [!DNL [Google Analytics' UTM fields]](https://support.google.com/analytics/answer/1191184?hl=en) 또는 사용자 지정 데이터 필드를 사용합니다. 이 세그먼테이션을 사용하면 성과가 가장 좋은 채널을 찾고 마케팅 예산을 더 많이 투자할 수 있습니다.

이 문서에서는 가장 중요한 마케팅 채널을 파악하는 데 사용할 수 있는 몇 가지 보고서를 살펴봅니다.

* [소스별 새 사용자](#newusersbysource)
* [사용자 소스별 평균 라이프타임 매출](#avglifetimerev)
* [사용자 소스별 평균 주문 가격](#avgorderval)
* [사용자 등록 날짜 및 소스별 매출](#revbyregdateandsource)
* [사용자 소스별 주문 반복](#repeatordersbysource)

## 전제 조건 {#prereqs}

이 문서에서 분석을 빌드하려면 마케팅 획득/참조 소스 데이터에 액세스해야 합니다. 아직 추적하지 않은 경우 다음을 가져와야 합니다 [주문 참조 소스 데이터 [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) 변환 [!DNL MBI] 계속하기 전에 또한 사용자 장치 정보를 분석에 추가하면 레퍼러가 사용하는 기술을 확인할 수 있습니다.

## 소스별 새 사용자 {#newusersbysource}

참조 소스의 성능을 평가하는 것은 가장 중요한 채널을 파악하는 데 중요합니다. 이 보고서는 시간이 지남에 따라 획득 소스별로 새로 등록된 사용자 수를 보여주므로 등록된 새 사용자를 획득할 때 참조 소스의 성능을 추적할 수 있습니다.

에서 이 보고서를 만들려면 [Report Builder](../../tutorials/using-visual-report-builder.md), 추가 **새 사용자** 보고서에 대한 지표(또는 시간에 따른 새 사용자 수를 계산하는 것과 동일한 지표)입니다. 그런 다음 다음을 수행합니다.

1. 설정 [!UICONTROL Time Period] 을 입력합니다.
1. 설정 [!UICONTROL Interval] 을 매월
1. 설정 [!UICONTROL Group By] 획득(또는 참조) 소스를 확인하고 포함할 소스를 선택합니다.
1. 이 예제에서는 `stacked columns` [!UICONTROL chart type].

다음은 시각적으로 살펴보는 것입니다.

![소스 보고서별 새 사용자 만들기.](../../assets/New_Users_by_source.gif)

## 사용자 소스별 평균 라이프타임 매출 {#avglifetimerev}

새 사용자를 가져오는 채널을 찾는 것이 중요하지만, 이러한 조회는 전체적으로 얼마나 유용합니까? 이 보고서는 시간 경과에 따른 특정 획득 소스에서 온 사용자의 평균 라이프타임 매출을 보여줍니다. 즉, 특정 소스로부터 얻은 사용자가 다른 소스에서 획득한 사용자 그룹보다 평생 동안 사용자와 더 많이 사용하는지 여부를 확인할 수 있습니다.

Report Builder에서 이 보고서를 만들려면 **평균 라이프타임 매출** 지표를 생성합니다. 그런 다음 다음을 수행합니다.

1. 설정 [!UICONTROL Time Period] 분석할 기간입니다.
1. 설정 [!UICONTROL Interval] 을 매월
   [!UICONTROL Group By] 획득(또는 참조) 소스를 확인하고 포함할 소스를 선택합니다.
1. 이 예제에서는 `line chart` 유형.

다음은 시각적 연습입니다.

![사용자 소스별 평균 라이프타임 매출 생성](../../assets/Lifetime_revenue_by_user_source.gif).

이 예제에서는 라이프타임 매출만 확인하지만 이 분석을 복제하여 [!UICONTROL Number of orders] 또는 [!UICONTROL Distinct buyers] 참조 소스별

## 사용자 소스별 평균 주문 가격 {#avgorderval}

특정 획득 소스에서 사용자가 얼마나 많은 비용을 지출하는지 더 잘 이해하기 위해 평균 주문 가격을 보는 보고서를 작성할 수 있습니다. 이렇게 하면 특정 소스에서 획득한 사용자가 다른 소스의 사용자보다 주문당 더 많은 비용을 지출하는지 여부를 추적할 수 있습니다.

Report Builder에서 이 보고서를 만들려면 **평균 주문 가격** 지표를 만든 다음 다음을 수행합니다.

1. 설정 [!UICONTROL Time Period] 을 입력합니다.
1. 설정 [!UICONTROL Time Interval] 을 매월
1. 설정 [!UICONTROL Group By] 획득(또는 참조) 소스를 확인하고 포함할 소스를 선택합니다.
1. 이 예제에서는 **누적 열** 차트 유형입니다.

다음은 시각적 연습입니다.

![사용자 출처 보고서별 평균 주문 값 생성.](../../assets/Average_order_value_by_source.gif)

## 사용자 등록 날짜 및 소스별 총 매출액 {#revbyregdateandsource}

이전에 살펴본 라이프타임 매출 분석에서는 서로 다른 소스에서 획득한 사용자의 평균 라이프타임 매출을 확인할 수 있지만 총 라이프타임 매출에는 어떻게 됩니까? 이 보고서를 사용하면 특정 시간 동안 및 특정 소스에서 등록한 전체 매출 사용자가 생성하는 크기를 식별할 수 있습니다.

Report Builder에서 이 보고서를 만들려면 `Revenue by user registration date` 지표. 그렇지 않았다면 [이 지표 생성](../../data-user/reports/ess-manage-data-metrics.md) 이미 복제하면 됩니다 `Revenue` 지표 및 변경 `time stamp` 사용자 `creation date`. 지표를 추가한 후 다음을 수행합니다.

1. 설정 [!UICONTROL Time Period] 을 입력합니다.
1. 설정 [!UICONTROL Time Interval] 을 매월
1. 설정 [!UICONTROL Group By] 획득(또는 참조) 소스를 확인하고 포함할 소스를 선택합니다.
1. 이 예제에서는 `stacked columns` 차트 유형입니다.

다음은 시각적 연습입니다.

![사용자 등록 날짜 및 소스 보고서별 총 매출액 생성.](../../assets/Revenue_by_user_registration_date_and_source.gif)

## 사용자 소스별 주문 반복 {#repeatordersbysource}

평균 주문 가격 보고서는 평균 주문 배치 시 특정 출처로부터 획득한 사용자의 비용을 보여줍니다. 그러나 동일한 사용자가 반복 고객인지 여부는 이 보고서에 표시되지 않습니다. 그러나 사용자 소스별 반복 주문 을 사용하면 특정 소스의 사용자가 반복 구매를 하는지 여부를 확인할 수 있습니다.

에서 이 보고서를 만들려면 [Report Builder](../../tutorials/using-visual-report-builder.md), 추가 **주문 수** 지표를 만든 다음 다음을 수행합니다.

1. 설정 [!UICONTROL Time Period] 을 입력합니다.
1. 설정 [!UICONTROL Time Interval] 을 매월
1. 추가 [!UICONTROL filter] 따라서 반복 주문이 있는 사용자만 포함됩니다.

   사용자의 주문 번호가 1보다 큼

1. 설정 [!UICONTROL Group By] 획득(또는 참조) 소스를 확인하고 포함할 소스를 선택합니다.
1. 이 예제에서는 `stacked columns` 차트 유형입니다.

다음은 시각적 연습입니다.

![사용자 출처 보고서별 반복 주문 생성.](../../assets/Repeat_orders_by_user_source.gif)


## 포장 {#wrapup}

이 문서에서, 고객 확보 및 마케팅 채널의 가치를 분석하는 데 사용할 수 있는 몇 가지 분석에 대해 다루었지만, 이것은 빙산의 일각일 뿐입니다. 여기에서 다루지 않은 강력한 분석을 만들었다면, 주석에서 수행하는 작업을 알려주십시오.

## 관련 {#related}

* [를 통해 주문 참조 소스 추적 [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [연결 [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [빌딩 [!DNL Google ECommerce] 주문 및 고객 데이터를 사용하는 차원](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [의 UTM 태그 지정에 대한 우수 사례 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
