---
title: Connect Google Analytics Warehouse
description: 방문자가 사이트를 사용하는 방법, 매력적인 콘텐츠, 방문자가 사이트를 나가는 위치 등을 추적하는 방법을 알아봅니다.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Connect [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>필요한 경우 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 는 인터넷에서 가장 널리 사용되는 웹 분석 서비스입니다. 구현 [!DNL Google Analytics] 웹 사이트에서는 방문자가 사이트를 사용하는 방법, 매력적인 콘텐츠, 방문자가 사이트를 나가는 위치 등을 추적할 수 있습니다. [!DNL Google Analytics Warehoused] 는 기존 과 별도의 통합입니다 [!DNL Google Analytics] 통합. 이렇게 하면 [!DNL Google Analytics] 기존 Data Warehouse의 라이브 피드와 다른 데이터 [!DNL Google Analytics] 통합. 에서 이러한 지표 분석 [!DNL MBI]를 다른 데이터 조각과 함께 사용하면 사이트의 전반적인 상태와 유용성을 향상시킬 수 있습니다.

## GA Warehouse와 라이브 통합 간의 차이점

주요 차별화 요소는 하나의 통합이 저장된다는 것입니다([!DNL Google Analytics Warehoused])이고, 다른 것은 ([!DNL Google Analytics Live]). 의 경우 [!DNL Google Analytics Warehoused]이렇게 하면 사용자의 [!DNL Google Analytics] 데이터 및 는 [!DNL Google Analytics] 통찰력 있는 보고를 만드는 기타 데이터 소스

한번 봅시다 [!DNL Google Analytics] 광고 캠페인을 추가하여 조작 관점에서 수행할 수 있는 작업의 예를 알아봅니다. 이름이 다른 Q4에 대한 여러 광고 캠페인이 있다고 가정합니다. 캠페인은 특정 마케팅 이니셔티브의 결과였습니다. 웨어러블 데이터를 사용하여 문제가 있는 캠페인 이름을 찾아 다음과 같은 Q4 이니셔티브 이름을 반환하는 새 열을 만들 수 있습니다. `Operation Dumbo`.

조합 양상은 [!DNL Google Analytics] 분석을 수행하기 위해 다른 데이터에 결합할 데이터입니다. 예를 들어, `Total Time On Site By Ad Campaign` 데이터 [!DNL Google Analytics] 반대편에 서 `Total Spent Per Campaign` 데이터 [!DNL Facebook Ads] 비용이 얼마나 소요되는지 완전히 파악할 수 있습니다.

사용 [!DNL Google Analytics Live] 반면, 모든 [!DNL Google Analytics] 차트는 작은 사일로(Silo)와 같습니다 [!DNL MBI] data warehouse.

## 연결 중 [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] is `Premium` 통합. [지원 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 구독에 이 통합을 추가할 수 있는 경우.

1. 로 이동합니다. `Connections` 아래의 페이지 **[!UICONTROL Admin** > **Integrations]**.
1. 클릭 **[!UICONTROL Add a Add Integration]**, 화면 오른쪽에 있습니다.
1. 을(를) 클릭합니다. [!DNL Google Analytics Warehoused] 아이콘. 이 옵션을 선택하면 [!DNL Google Analytics] 자격 증명 페이지.
1. 을(를) 입력합니다. [!DNL Google Analytics] 자격 증명. 인증 프로세스가 완료되면 다시 로 리디렉션됩니다. [!DNL MBI].
1. 프로필 ID 목록이 표시됩니다. 연결할 프로필을 확인합니다 [!DNL MBI]. 여러 개의 프로필이 있고 해당 프로필을 식별하는 데 도움이 필요한 경우 연결 다중 을 참조하십시오 [!DNL Google Analytics] 아래의 프로필 섹션에 자세히 설명되어 있습니다.

## 다중 연결 [!DNL Google Analytics] 프로필

여러 웹 사이트가 한 사이트에 연결되어 있을 수 있습니다 [!DNL Google Analytics] account, 자체 식별 [!DNL Google Analytics] 프로필 ID. 이 경우 모든 프로필 ID를 포함할 수 있습니다. [!DNL MBI]. 프로필 선택 단계 동안 포함할 프로필 ID를 확인하면 됩니다.

특정 웹 사이트의 [!DNL Google Analytics] 프로필 ID:

1. 에 로그인합니다. [!DNL Google Analytics]
1. 특정 웹 사이트의 [!DNL Google Analytics] 대시보드
1. URL을 확인합니다. 프로필 ID는 다음 8개의 숫자에 해당합니다 `p` 줄 끝에

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 연결 끊기 [!DNL Google Analytics Warehoused] 변환 전: [!DNL MBI] {#disconnect}

1. 다음 방문 [!DNL Google Analytics] [계정 설정](https://www.google.com/accounts/) 페이지.
1. 아래에 `Security` 섹션을 클릭하고 **[!UICONTROL edit]** 다음 `Authorizing` 애플리케이션 및 사이트.
1. 클릭 **[!UICONTROL revoke access]** 다음 [!DNL MBI].

## 관련 설명서

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [연결 중 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [웹 사이트 활동 및 고객 전환율 분석](../../analysis/web-act-cust-conversion.md)
* [을 사용하여 사용자 획득 데이터 추적 [!DNL Google Analytics] 쿠키](../../analysis/google-track-user-acq.md)
