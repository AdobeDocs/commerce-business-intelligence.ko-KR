---
title: Google Analytics 웨어하우징 연결
description: 방문자가 사이트를 사용하는 방법, 매력적인 콘텐츠, 방문자가 종료하는 위치 등을 추적하는 방법에 대해 알아봅니다.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# [!DNL Google Analytics Warehoused] 연결

>[!NOTE]
>
>[관리자 권한](../../../administrator/user-management/user-management.md)이 필요합니다.

![Google Analytics 로고](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics]은(는) 인터넷에서 가장 널리 사용되는 웹 분석 서비스입니다. 웹 사이트에 [!DNL Google Analytics]을(를) 구현하면 방문자가 사이트를 사용하는 방법, 매력적인 콘텐츠, 방문자가 종료하는 위치 등을 추적할 수 있습니다. [!DNL Google Analytics Warehoused]은(는) 기존 [!DNL Google Analytics] 통합과 별도의 통합입니다. 기존 [!DNL Google Analytics] 통합의 라이브 피드와 다른 [!DNL Google Analytics] 데이터가 Data Warehouse에 있으므로 더 나은 분석을 수행할 수 있습니다. 다른 데이터와 함께 [!DNL Commerce Intelligence]에서 이러한 지표를 분석하면 사이트의 전반적인 상태와 유용성이 향상됩니다.

## GA 웨어하우스와 라이브 통합의 차이점

주요 차별화 요소는 하나의 통합이 저장되며([!DNL Google Analytics Warehoused]), 다른 통합은 저장되지 않는다는 점입니다([!DNL Google Analytics Live]). [!DNL Google Analytics Warehoused]의 경우 [!DNL Google Analytics] 데이터를 조작할 수 있으므로 [!DNL Google Analytics]과(와) 다른 데이터 소스를 결합하여 통찰력 있는 보고를 만들 수 있습니다.

[!DNL Google Analytics] 광고 캠페인에서 조작 관점에서 수행할 수 있는 작업의 예를 살펴보십시오. 이름이 다른 4분기 광고 캠페인이 여러 개 있다고 가정해 봅시다. 캠페인은 특정 마케팅 이니셔티브의 결과였습니다. 웨어하우스된 데이터를 사용하여 해당 캠페인 이름을 찾고 4분기 이니셔티브 이름 `Operation Dumbo`을(를) 반환하는 열을 만들 수 있습니다.

결합 측면을 사용하면 분석을 수행하기 위해 [!DNL Google Analytics] 데이터를 다른 데이터에 결합할 수 있습니다. 예를 들어, `Total Time On Site By Ad Campaign`의 [!DNL Google Analytics] 데이터를 가져와서 `Total Spent Per Campaign`의 [!DNL Facebook Ads] 데이터와 함께 참여하면 참여로 인해 비용이 얼마나 많이 소요되는지 전체적으로 파악할 수 있습니다.

반면에 [!DNL Google Analytics Live] 통합을 사용하면 모든 [!DNL Google Analytics] 차트는 Data Warehouse에 저장되지 않은 작은 사일로와 같습니다.

## [!DNL Google Analytics Warehoused] 연결 중

>[!INFO]
>
>[!DNL Google Analytics Warehoused]은(는) `Premium` 통합입니다. 이 통합을 구독에 추가하려면 [지원팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)하세요.

1. `Connections` 아래의 **[!UICONTROL Admin** > **Integrations]** 페이지로 이동합니다.
1. 오른쪽에 있는 **[!UICONTROL Add an Integration]**&#x200B;을(를) 클릭합니다.
1. [!DNL Google Analytics Warehoused] 아이콘을 클릭합니다. [!DNL Google Analytics] 자격 증명 페이지가 열립니다.
1. [!DNL Google Analytics] 자격 증명을 입력하십시오. 인증 프로세스가 완료되면 다시 [!DNL Commerce Intelligence]&#x200B;(으)로 리디렉션됩니다.
1. 프로필 ID 목록이 표시됩니다. [!DNL Commerce Intelligence]에 연결할 프로필을 확인하십시오. 프로필이 여러 개이고 어떤 프로필인지 식별하는 데 도움이 필요한 경우 아래의 여러 [!DNL Google Analytics] 프로필 연결 섹션을 참조하십시오.

## 여러 [!DNL Google Analytics]개의 프로필 연결 중

하나의 [!DNL Google Analytics] 계정에 여러 웹 사이트가 연결되어 있으며, 해당 웹 사이트가 [!DNL Google Analytics] 프로필 ID로 식별될 수 있습니다. 이 경우 [!DNL Commerce Intelligence]에 모든 프로필 ID를 포함할 수 있습니다. 프로필 선택 단계에서 포함할 프로필 ID를 확인합니다.

특정 웹 사이트의 [!DNL Google Analytics] 프로필 ID를 식별하려면 다음을 수행하십시오.

1. [!DNL Google Analytics]에 로그인
1. 특정 웹 사이트의 [!DNL Google Analytics] 대시보드로 이동
1. URL을 확인합니다. 프로필 ID는 줄 끝에 있는 `p` 뒤에 오는 8개의 숫자에 해당합니다

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## [!DNL Google Analytics Warehoused]에서 [!DNL Commerce Intelligence]의 연결을 끊는 중 {#disconnect}

1. [!DNL Google Analytics] [계정 설정](https://myaccount.google.com/intro) 페이지를 방문하세요.
1. `Security` 섹션 아래에서 **[!UICONTROL edit]**&#x200B;개의 응용 프로그램 및 사이트 옆에 있는 `Authorizing`을(를) 클릭합니다.
1. **[!UICONTROL revoke access]** 옆에 있는 [!DNL Commerce Intelligence]을(를) 클릭합니다.

## 관련 설명서

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [&#x200B; [!DNL Google Adwords] 연결 중](../integrations/google-adwords.md)
* [웹 사이트 활동 및 고객 전환율 분석](../../analysis/web-act-cust-conversion.md)
* [&#x200B; [!DNL Google Analytics] 쿠키를 사용하여 사용자 획득 데이터 추적](../../analysis/google-track-user-acq.md)
