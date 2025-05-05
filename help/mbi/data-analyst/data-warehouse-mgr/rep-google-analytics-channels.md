---
title: 획득 소스를 사용하여 Google Analytics 채널 복제
description: 획득 소스를 사용하여 Google Analytics 채널을 복제하는 방법에 대해 알아봅니다.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# 획득 소스를 사용하는 [!DNL Google Analytics]

## 채널이란? {#channels}

다양한 트래픽이 수행되는 방식을 확인하고 트렌드를 관찰하기 위한 사용자 지정 세그먼트를 만드는 것은 [!DNL Google Analytics]에 가장 강력한 사용 중 하나입니다. [!DNL Google Analytics]에 기본적으로 존재하는 세그먼트 클래스 중 하나는 `Channels`입니다. 채널은 사람들이 사이트를 방문하는 일반적인 방법의 그룹입니다.  [!DNL Google Analytics]은(는) 소셜 미디어, 클릭당 과금, 전자 메일 또는 참조 링크이든 사용자를 획득하는 다양한 방법을 자동으로 정렬하여 버킷 또는 채널로 묶습니다.

## Commerce Intelligence에서 내 `channels`을(를) 보지 않는 이유는 무엇입니까? {#nochannels}

`Channels`은(는) 데이터의 간단한 집계 버킷입니다. 획득을 채널 버킷으로 정렬하려면 [!DNL Google]에서 특정 매개 변수를 사용하여 고유한 규칙과 정의를 설정합니다. 획득 [Source](https://support.google.com/analytics/answer/1033173?hl=en)(트래픽의 원본)과 획득 [Medium](https://support.google.com/analytics/answer/6099206?hl=en)(소스의 일반 범주)의 조합입니다.

이러한 버킷을 사용하면 트래픽이 발생하는 위치를 이해하는 데 도움이 될 수 있지만, 이 데이터는 채널별로 태그가 지정되지 않고 Source과 Medium의 조합으로 태그가 지정됩니다. [!DNL Google]이(가) 채널 정보를 두 개의 개별 데이터 지점으로 보내기 때문에 채널 그룹화가 [!DNL Commerce Intelligence]에 자동으로 표시되지 않습니다.

## 기본 채널 그룹화는 무엇입니까? 어떻게 만들어집니까?

기본적으로 [!DNL Google]은(는) 8개의 다른 채널을 설정합니다. 채널을 만드는 방법을 결정하는 규칙은 아래에 나와 있습니다.

| **채널** | **무엇입니까?** | **어떻게 만들어졌습니까?** |
|---|---|---|
| 직접 | 사이트로 직접 들어오는 모든 사용자. | Source = `Direct`<br>이고 Medium = `(not set); OR Medium = (none)` |
| 유기 검색 | 무급 검색 엔진에서 유기적으로 순위가 매겨진 트래픽. | Medium = `organic` |
| 레퍼러 | 유기 검색이 아닌 외부 링크 또는 소셜 네트워크가 아닌 웹 사이트에서 들어오는 트래픽입니다. | Medium = `referral` |
| 유료 검색 | 미디어가 &quot;cpc&quot;, &quot;ppc&quot; 또는 &quot;paidsearch&quot;인 UTM 추적 코드가 있고 &quot;콘텐츠&quot;와 일치하지 않는 광고 배포 네트워크인 트래픽입니다. | Medium = `^(cpc|ppc|paidsearch)$`<br>AND 광고 배포 네트워크 ≠ `Content` |
| 소셜 | 약 [400개의 소셜 네트워크](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/)에서 발생하고 광고로 태그가 지정되지 않은 참조 트래픽입니다. | 소셜 Source 참조 = `Yes`<br>또는 Medium = `^(social|social-network|social-media|sm|social network|social media)$` |
| 이메일 | &quot;이메일&quot; 미디어로 태그가 지정된 세션의 트래픽입니다. | Medium의 UTM 추적 코드 = `email` |
| 표시 | 미디어가 디스플레이 또는 cpm인 UTM 추적 코드가 있는 트래픽입니다. 광고 배포 네트워크가 &quot;콘텐츠&quot;와 일치하는 AdWords 상호 작용도 포함합니다. | Medium = `^(display|cpm|banner)$`<br>OR 광고 배포 네트워크 = `Content`<br>AND 광고 형식 ≠ `Text` |
| 기타 | &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm&quot;, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot;, &quot;affiliate&quot; 미디어로 태그가 지정된 다른 광고 채널(유료 검색 제외)의 세션. | Medium = `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## 내 Data Warehouse에서 이러한 채널 그룹화를 어떻게 다시 만들 수 있습니까? {#recreate}

이제 채널은 소스와 미디어의 조합일 뿐이므로 Data Warehouse에서 이러한 그룹화를 다시 만드는 것은 쉬운 3단계 프로세스입니다.

1. **통합 사용[!DNL Google ECommerce]2&rbrace;**

   [활성화하면](../importing-data/integrations/google-ecommerce.md)Data Warehouse에서 [동기화](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) **중간** 및 **소스** 필드를 확인하십시오. 이 작업이 완료되면 중간 및 소스 획득 데이터를 Data Warehouse으로 가져옵니다.

1. **Google의 채널 그룹 매핑 업로드**

   Adobe Commerce에서 [다운로드](../../assets/ga-channel-mapping.csv)할 수 있는 파일로 매핑된 기본 그룹화가 있는 표를 만듭니다.

   [!DNL Google Analytics] Pro이고 고유한 채널을 만든 경우 파일을 [!DNL Commerce Intelligence]에 업로드하기 전에 특정 규칙을 매핑 테이블에 추가할 수 있습니다.

   [파일 업로드](../importing-data/connecting-data/using-file-uploader.md)(으)로 Data Warehouse에 가져옵니다.

   ![](../../assets/Setting_Primary_Keys.png)

1. **매핑 파일 업로드[!DNL Google ECommerce]와(과)** 간의 관계를 설정합니다.

   [!DNL Google ECommerce]과(와) 매핑 테이블 간의 관계를 설정하려면 데이터 분석가 팀에 [지원 요청을 제출](../../guide-overview.md#Submitting-a-Support-Ticket)하고 이 항목을 참조하십시오. 분석가는 ECommerce 테이블에서 **채널**&#x200B;이라는 새 계산된 열을 만듭니다. **전체 업데이트 주기**&#x200B;가 끝나면 `Filter` 또는 `Group by`에서 이 열을 사용할 수 있습니다.

이제 Data Warehouse에 [!DNL Google Analytics Channel]개의 그룹화가 있으므로 새로운 관점에서 데이터를 분석할 수 있습니다.

![채널별 주문 수 지표 세그먼트화](../../assets/GA_Channel_Gif.gif)

이 예제에서는 **주문 수** 지표를 **채널**&#x200B;로 세그먼트화하는 간단한 작업을 시작했습니다. 새 열을 테스트하여 [!DNL Google Analytics Channel] 데이터에서 식별할 수 있는 트렌드를 확인합니다.

## 관련 설명서

* [Report Builder 사용](../../tutorials/using-visual-report-builder.md)
* [[!DNL Google ECommerce]데이터가 필요합니다.](../importing-data/integrations/google-ecommerce-data.md)
* [주문 및 고객 데이터를 사용하여 [!DNL Google ECommerce]차원 작성](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [가장 중요한 확보 소스 및 채널은 무엇입니까?](../analysis/most-value-source-channel.md)
