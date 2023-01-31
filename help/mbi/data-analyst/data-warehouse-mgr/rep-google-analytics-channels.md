---
title: 획득 소스를 사용하여 Google Analytics 채널 복제
description: 획득 소스를 사용하여 Google Analytics 채널을 복제하는 방법을 알아봅니다.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# 획득 소스를 사용한 Google Analytics

## 채널이란 무엇입니까? {#channels}

사용자 지정 세그먼트를 만들어 서로 다른 트래픽이 수행하고 트렌드를 따르는 방식을 확인합니다(더 좋거나 더 좋음!). 는 의 가장 강력한 사용 방법 중 하나입니다  [!DNL Google Analytics ]. 기본적으로 에 있는 세그먼트의 한 클래스 [!DNL Google Analytics ] is `Channels`. 채널은 사람들이 사이트를 방문하는 일반적인 방법의 그룹입니다.  [!DNL Google Analytics ] 사용자를 얻는 다양한 방법(소셜 미디어, 클릭당 과금, 이메일 또는 참조 링크)을 자동으로 정렬하여 버킷 또는 채널로 번들합니다.

## 왜 내가 `channels` MBI에? {#nochannels}

`Channels` 단순, 집계 데이터 버킷. 획득을 채널 버킷으로 정렬하려면 Google에서 특정 매개 변수를 사용하여 고유한 규칙 및 정의를 설정합니다. 획득 조합 [소스](https://support.google.com/analytics/answer/1033173?hl=en) (트래픽의 출처) 및 획득 [Medium](https://support.google.com/analytics/answer/6099206?hl=en) (소스의 일반 카테고리).

이러한 버킷이 있으면 트래픽이 발생하는 위치를 파악하는 데 도움이 될 수 있지만, 이 데이터는 실제로 채널별로 태그가 지정되지 않고 소스와 미디어의 조합으로 태그가 지정됩니다. Google이 채널 정보를 두 개의 개별 데이터 포인트로 전송하므로 채널 그룹화는 자동으로 표시되지 않습니다 [!DNL MBI].

## 기본 채널 그룹화란 무엇입니까? 어떻게 만들어집니까?

기본적으로 Google에서는 8개의 서로 다른 채널을 설정합니다. 규칙이 만들어지는 방법을 결정하는 규칙을 살펴보겠습니다.

| 채널 | 무슨 일이야? | 어떻게 만들어집니까? |
|---|---|---|
| 직접 | 사이트로 바로 들어오는 모든 사용자. | 소스 = `Direct`<br>AND Medium = `(not set); OR Medium = (none)` |
| 유기 검색 | 유료 검색 엔진에서 유기적으로 순위가 지정된 트래픽입니다. | Medium = `organic` |
| 참조 | Organic Search가 아닌 외부 링크 또는 소셜 네트워크가 아닌 웹 사이트에서 들어오는 트래픽입니다. | Medium = `referral` |
| 유료 검색 | 미디어가 &quot;cpc&quot;, &quot;ppc&quot; 또는 &quot;paidsearch&quot;인 UTM 추적 코드가 있고, &quot;컨텐츠&quot;와 일치하지 않는 광고 배포 네트워크인 트래픽입니다. | Medium = `^(cpc|ppc|paidsearch)$`<br>AND Ad Distribution Network ≠ `Content` |
| Social | 대략 다음 중 하나에서 발생하는 참조 트래픽 [400개의 소셜 네트워크](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) 및 에는 광고로 태그가 지정되지 않습니다. | 소셜 소스 참조 = `Yes`<br>또는 미디어 = `^(social|social-network|social-media|sm|social network|social media)$` |
| 이메일 | &quot;이메일&quot; 미디어로 태그가 지정된 세션의 트래픽입니다. | Medium의 UTM 추적 코드 = `email` |
| 표시 | 미디어가 표시 또는 cpm인 UTM 추적 코드가 있는 트래픽. 또한 광고 배포 네트워크가 &quot;컨텐츠&quot;와 일치하는 AdWords 상호 작용이 포함됩니다 | Medium = `^(display|cpm|banner)$`<br>또는 광고 배포 네트워크 = `Content`<br>AND 광고 형식 ≠ `Text` |
| 기타 | &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot;, &quot;제휴&quot;라는 미디어로 태그가 지정된 다른 광고 채널의 세션. | Medium = `^(cpv|cpa|cpp|content-text)$` |

{style=&quot;table-layout:auto&quot;}

## Data Warehouse에서 이러한 채널 그룹을 다시 만들 수 있습니까? {#recreate}

채널은 소스와 미디어의 조합일 뿐이므로 Data Warehouse에서 이러한 그룹화를 다시 만드는 쉬운 3단계 프로세스입니다.

1. **사용[!DNL Google ECommerce]통합**

   [활성화되면](../importing-data/integrations/google-ecommerce.md), 다음을 확인하십시오. [동기화](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) **중간** 및 **소스** Data Warehouse의 필드. 이 작업이 완료되면 미디어 및 소스 획득 데이터가 Data Warehouse으로 제공됩니다.

1. **Google의 채널 그룹화 매핑 업로드**

   시간을 절약하기 위해 Commerce에서 이미 사용 가능한 파일로 매핑된 기본 그룹화가 있는 테이블을 만들었습니다 [다운로드](../../assets/ga-channel-mapping.csv).

   Google Analytics 전문가이고 자신만의 채널을 만든 경우, 파일을 로 업로드하기 전에 매핑 테이블에 특정 규칙을 추가할 수 있습니다 [!DNL MBI].

   Data Warehouse으로 가져오기 [파일 업로드](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **상호 관계 설정[!DNL Google ECommerce]및 매핑 파일 업로드**

   Analytics Standard에서[!DNL Google ECommerce]매핑 테이블, [지원 요청 제출](../../guide-overview.md) data Analyst 팀에 문의하고 이 문서를 참조하십시오. 애널리스트는 새 계산된 열을 **채널** ( 전자 상거래 표)를 참조하십시오. **전체 업데이트 주기 후**: 이 열은 필터 또는 그룹화 방법에 사용할 수 있습니다.

축하합니다! 이제 Data Warehouse에 Google Analytics 채널 그룹이 있습니다. 즉, 새로운 관점에서 데이터를 분석할 수 있습니다.

![채널별 주문 수 지표 세그먼트화](../../assets/GA_Channel_Gif.gif)

이 예에서는 간단한 세그먼트화를 시작했습니다 **주문 수** 지표 기준 **채널**. 이제 차례입니다. 새 열을 테스트하여 Google Analytics 채널 데이터에서 식별할 수 있는 트렌드를 확인하십시오!

## 관련 설명서

* [Report Builder 사용](../../tutorials/using-visual-report-builder.md)
* [예상됨[!DNL Google ECommerce]데이터](../importing-data/integrations/google-ecommerce-data.md)
* [빌딩[!DNL Google ECommerce]주문 및 고객 데이터를 사용한 차원](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [가장 가치 있는 획득 소스 및 채널은 무엇입니까?](../analysis/most-value-source-channel.md)
