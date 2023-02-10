---
title: Google 전자 상거래 연결
description: 가장 가치 있는 참조 채널에 대해 알아봅니다.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Connect [!DNL Google ECommerce]

>[!NOTE]
>
>필요한 경우 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

지속적인 트래픽 및 주문 흐름이 있으며 이는 고객에게 효과적으로 도달하고 획득하고 있음을 의미합니다. 하지만 가장 가치 있는 추천 채널은 무엇입니까? 한 소스와 다른 소스에서 획득한 고객의 평균 라이프타임 값은 얼마입니까? 주문 참조 소스 데이터를 [!DNL Google ECommerce] to [!DNL MBI]을 생성할 수 있습니다. [가장 가치 있는 마케팅 채널](../../../data-analyst/analysis/most-value-source-channel.md).

이제 Adobe에 [!DNL Google ECommerce] 자격 증명 [!DNL MBI]:

1. 로 이동합니다. `Connections` 아래의 페이지 **[!UICONTROL Admin** > **Connections]**.
1. 클릭 **[!UICONTROL Add a New Source]**- 화면 오른쪽 위의 `Data Sources` 테이블.
1. 을(를) 클릭합니다. [!DNL Google ECommerce] 아이콘. 이 옵션을 선택하면 [!DNL Google ECommerce] 자격 증명 페이지.
1. 을(를) 입력합니다. [!DNL Google Analytics] 자격 증명. 인증 프로세스가 완료되면 다시 로 리디렉션됩니다. [!DNL MBI].
1. 프로필 ID 목록이 표시됩니다. 연결할 프로필을 확인합니다 [!DNL MBI].

   여러 개의 프로필이 있고 해당 프로필을 식별하는 데 도움이 필요한 경우 **다중 연결 을 참조하십시오 [!DNL Google Analytics] 아래의 프로필 섹션에 자세히 설명되어 있습니다.

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. 변경 내용은 자동으로 저장되므로 **[!UICONTROL Back to Connections]** 끝나면

## 다중 연결 [!DNL Google Analytics] 다음으로 프로필 [!DNL MBI]

여러 웹 사이트가 한 사이트에 연결되어 있을 수 있습니다 [!DNL Google Analytics] account, 자체 식별 [!DNL Google Analytics] 프로필 ID. 이 경우 모든 프로필 ID를 포함할 수 있습니다. [!DNL MBI]. 프로필 선택 단계 동안 포함할 프로필 ID를 확인하면 됩니다.

특정 웹 사이트의 [!DNL Google Analytics] 프로필 ID:

1. 에 로그인합니다. [!DNL Google Analytics]
1. 특정 웹 사이트의 [!DNL Google Analytics] 대시보드
1. URL을 확인합니다. 프로필 ID는 다음 8개의 숫자에 해당합니다 `p` 줄 끝에

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 연결 끊기 [!DNL Google ECommerce] 변환 전: [!DNL MBI] {#disconnect}

1. 다음 방문 [!DNL Google Analytics] [계정 설정](https://www.google.com/accounts/) 페이지.
1. 아래에 `Security` 섹션을 클릭합니다. **[!UICONTROL edit]** 다음 `Authorizing` 애플리케이션 및 사이트.
1. 클릭 **[!UICONTROL revoke access]** 다음 [!DNL MBI].

## 관련:

* [예상됨 [!DNL Google ECommerce] 데이터](../integrations/google-ecommerce-data.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [설정 [!DNL Google ECommerce] 추적](https://support.google.com/analytics/answer/1009612?hl=en)
* [가장 가치 있는 획득 소스 및 채널 살펴보기](../../analysis/most-value-source-channel.md)
* [광고 캠페인에 대한 ROI 향상](../../analysis/roi-ad-camp.md)
