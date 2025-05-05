---
title: Google Commerce 연결
description: 가장 소중한 레퍼러 채널에 대해 알아봅니다.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# [!DNL Google ECommerce] 연결

>[!NOTE]
>
>[관리자 권한](../../../administrator/user-management/user-management.md)이 필요합니다.

![](../../../assets/google-ecommerce-logo.png)

트래픽과 주문의 흐름이 일정하기 때문에 효과적으로 고객을 확보하고 있습니다. 하지만 가장 가치 있는 추천 채널은 무엇입니까? 한 소스에서 다른 소스에서 획득한 고객의 평균 라이프타임 값은 얼마입니까? 주문 참조 원본 데이터를 [!DNL Google ECommerce]에서 [!DNL Commerce Intelligence] (으)로 연결하면 [가장 가치 있는 마케팅 채널](../../../data-analyst/analysis/most-value-source-channel.md)을 식별하는 데 도움이 되는 분석을 빌드할 수 있습니다.

[!DNL Commerce Intelligence]에 [!DNL Google ECommerce] 자격 증명을 입력하여 시작하십시오.

1. **[!UICONTROL Admin** > **Connections]** 아래의 `Connections` 페이지로 이동합니다.

1. `Data Sources` 테이블 위의 화면 오른쪽에 있는 **[!UICONTROL Add a New Source]**&#x200B;을(를) 클릭합니다.

1. [!DNL Google ECommerce] 아이콘을 클릭합니다. [!DNL Google ECommerce] 자격 증명 페이지가 열립니다.

1. [!DNL Google Analytics] 자격 증명을 입력하십시오. 인증 프로세스가 완료되면 [!DNL Commerce Intelligence] (으)로 다시 리디렉션됩니다.

1. 프로필 ID 목록이 표시됩니다. [!DNL Commerce Intelligence]에 연결할 프로필을 확인하십시오.

   프로필이 여러 개이고 어떤 프로필인지 확인하는 데 도움이 필요한 경우 아래의 **여러 [!DNL Google Analytics] 프로필 연결 섹션을 참조하십시오.

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. 변경 사항은 자동으로 저장되므로 완료되면 **[!UICONTROL Back to Connections]**&#x200B;을(를) 클릭하십시오.

## [!DNL Commerce Intelligence]에 여러 [!DNL Google Analytics] 프로필을 연결하는 중

하나의 [!DNL Google Analytics] 계정에 여러 웹 사이트가 연결되어 있으며, 해당 웹 사이트가 [!DNL Google Analytics] 프로필 ID로 식별될 수 있습니다. 이 경우 [!DNL Commerce Intelligence]에 모든 프로필 ID를 포함할 수 있습니다. 프로필 선택 단계에서 포함할 프로필 ID를 확인합니다.

특정 웹 사이트의 [!DNL Google Analytics] 프로필 ID를 식별하려면 다음을 수행하십시오.

1. [!DNL Google Analytics]에 로그인합니다.
1. 특정 웹 사이트의 [!DNL Google Analytics] 대시보드로 이동합니다.
1. URL을 확인합니다. 프로필 ID는 줄 끝에 있는 `p` 뒤에 오는 8개의 숫자에 해당합니다.

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## [!DNL Commerce Intelligence]에서 [!DNL Google ECommerce]의 연결을 끊는 중 {#disconnect}

1. [!DNL Google Analytics] [계정 설정](https://www.google.com/account/about/?hl=en) 페이지를 방문하세요.
1. `Security` 섹션에서 `Authorizing`개의 응용 프로그램 및 사이트 옆에 있는 **[!UICONTROL edit]**&#x200B;을(를) 클릭합니다.
1. [!DNL Commerce Intelligence] 옆에 있는 **[!UICONTROL revoke access]**&#x200B;을(를) 클릭합니다.

## 관련 항목:

* [ [!DNL Google ECommerce] 데이터가 필요합니다.](../integrations/google-ecommerce-data.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [설정 [!DNL Google ECommerce] 추적](https://support.google.com/analytics/answer/1009612?hl=en)
* [가장 가치 있는 확보 소스 및 채널 살펴보기](../../analysis/most-value-source-channel.md)
* [광고 캠페인에 대한 ROI 향상](../../analysis/roi-ad-camp.md)
