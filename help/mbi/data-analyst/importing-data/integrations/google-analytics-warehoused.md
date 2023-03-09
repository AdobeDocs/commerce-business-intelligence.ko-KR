---
title: 웨어하우징 된 Google Analytics 연결
description: 방문자가 사이트를 사용하는 방법, 매력적인 콘텐츠, 방문자가 종료하는 위치 등을 추적하는 방법에 대해 알아봅니다.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# 연결 [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>필요 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 는 인터넷에서 가장 널리 사용되는 웹 분석 서비스입니다. 구현 [!DNL Google Analytics] 웹 사이트에서 방문자가 사이트를 사용하는 방법, 매력적인 콘텐츠, 방문자가 종료하는 위치 등을 추적할 수 있습니다. [!DNL Google Analytics Warehoused] 는 기존 통합과 별개입니다. [!DNL Google Analytics] 통합. 다음과 같은 기능이 있으므로 더 나은 분석이 가능합니다. [!DNL Google Analytics] 기존 의 라이브 피드와 다른 Data Warehouse의 데이터 [!DNL Google Analytics] 통합. 에서 이러한 지표 분석 [!DNL MBI]는 다른 데이터와 함께 사이트의 전반적인 건강과 유용성을 향상시킵니다.

## GA 웨어하우스와 라이브 통합의 차이점

주요 차별화 요소는 한 개의 통합이 저장된다는 것입니다([!DNL Google Analytics Warehoused]) 및 다른 하나는 ([!DNL Google Analytics Live]). 의 경우에는 [!DNL Google Analytics Warehoused], 이렇게 하면 을 조작할 수 있습니다. [!DNL Google Analytics] 데이터 및 를 결합하여 [!DNL Google Analytics] 통찰력 있는 보고를 만드는 기타 데이터 소스.

다음 항목 보기 [!DNL Google Analytics] 광고 캠페인 : 조작 관점에서 수행할 수 있는 작업의 예입니다. 이름이 다른 4분기 광고 캠페인이 여러 개 있다고 가정해 봅시다. 캠페인은 특정 마케팅 이니셔티브의 결과였습니다. 웨어하우스된 데이터를 사용하여 해당 캠페인 이름을 찾고 의 Q4 이니셔티브 이름을 반환하는 열을 만들 수 있습니다. `Operation Dumbo`.

조합 측면이 허용하는 경우 [!DNL Google Analytics] 분석을 수행하기 위해 다른 데이터에 결합할 데이터. 예를 들어 다음을 수행합니다. `Total Time On Site By Ad Campaign` 데이터 출처: [!DNL Google Analytics] and join가입 it up against `Total Spent Per Campaign` 데이터 출처: [!DNL Facebook Ads] 약정에 얼마나 많은 비용이 소요되고 있는지 전체적으로 파악할 수 있습니다.

포함 [!DNL Google Analytics Live] 반면, 모든 [!DNL Google Analytics] 차트는 파일에 저장되지 않은 작은 사일로와 같습니다 [!DNL MBI] Data Warehouse.

## 연결 중 [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] 다음 값: `Premium` 통합. [지원 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 이 통합을 구독에 추가하려는 경우.

1. 로 이동 `Connections` 아래 페이지 **[!UICONTROL Admin** > **Integrations]**.
1. 클릭 **[!UICONTROL Add an Integration]**&#x200B;을 클릭합니다.
1. 다음을 클릭합니다. [!DNL Google Analytics Warehoused] 아이콘. 이렇게 하면 [!DNL Google Analytics] 자격 증명 페이지입니다.
1. 다음을 입력하십시오. [!DNL Google Analytics] 자격 증명. 인증 프로세스가 완료되면 다시 로 리디렉션됩니다. [!DNL MBI].
1. 프로필 ID 목록이 표시됩니다. 연결할 프로필을 확인하십시오. [!DNL MBI]. 프로필이 여러 개 있고 어떤 프로필인지 식별하는 데 도움이 필요한 경우 다중 연결을 참조하십시오 [!DNL Google Analytics] 아래의 프로필 섹션에 자세히 설명되어 있습니다.

## 여러 개 연결 중 [!DNL Google Analytics] 프로필

하나의 웹 사이트에 여러 개의 웹 사이트가 연결되어 있을 수 있습니다. [!DNL Google Analytics] 계정, 자체 식별 [!DNL Google Analytics] 프로필 ID. 이 경우 모든 프로필 ID를에 포함할 수 있는 옵션이 있습니다 [!DNL MBI]. 프로필 선택 단계에서 포함할 프로필 ID를 확인합니다.

특정 웹 사이트를 식별하려면 [!DNL Google Analytics] 프로필 ID:

1. 에 로그인 [!DNL Google Analytics]
1. 특정 웹 사이트로 이동 [!DNL Google Analytics] 대시보드
1. URL을 확인합니다. 프로필 ID는 다음 8개의 숫자에 해당합니다. `p` 줄 끝에

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 연결 끊기 [!DNL Google Analytics Warehoused] 출처: [!DNL MBI] {#disconnect}

1. 다음을 방문하십시오. [!DNL Google Analytics] [계정 설정](https://myaccount.google.com/intro) 페이지를 가리키도록 업데이트하는 중입니다.
1. 아래 `Security` 섹션, 클릭 **[!UICONTROL edit]** 다음에 `Authorizing` 애플리케이션 및 사이트
1. 클릭 **[!UICONTROL revoke access]** 다음에 [!DNL MBI].

## 관련 설명서

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [연결 중 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [웹 사이트 활동 및 고객 전환율 분석](../../analysis/web-act-cust-conversion.md)
* [다음을 사용하여 사용자 획득 데이터 추적 [!DNL Google Analytics] 쿠키](../../analysis/google-track-user-acq.md)
