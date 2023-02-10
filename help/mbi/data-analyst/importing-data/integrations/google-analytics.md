---
title: Google Analytics 연결
description: Google Analytics 연결 방법 알아보기 [!DNL MBI].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Connect [!DNL Google Analytics]

>[!NOTE]
>
>필요한 경우 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 는 인터넷에서 가장 널리 사용되는 웹 분석 서비스입니다. 구현 [!DNL Google Analytics] 웹 사이트에서는 방문자가 사이트를 사용하는 방법, 매력적인 콘텐츠, 방문자가 사이트를 나가는 위치 등을 추적할 수 있습니다. 에서 이러한 지표 분석 [!DNL MBI]를 다른 데이터 조각과 함께 사용하면 사이트의 전반적인 상태와 유용성을 향상시킬 수 있습니다.

이제 Adobe에 [!DNL Google Analytics] 자격 증명 [!DNL MBI]:

1. 로 이동합니다. **[!UICONTROL Manage Data** > **Integrations]** 페이지.
1. 클릭 **[!UICONTROL Add Integration]**, 화면 오른쪽에 있습니다.
1. 을(를) 클릭합니다. [!DNL Google Analytics] 아이콘. 이 옵션을 선택하면 [!DNL Google Analytics] 자격 증명 페이지.
1. 을(를) 입력합니다. [!DNL Google Analytics] 자격 증명. 인증 프로세스가 완료되면 다시 로 리디렉션됩니다. [!DNL MBI].
1. 프로필 ID 목록이 표시됩니다. 연결할 프로필을 확인합니다 [!DNL MBI]. 여러 개의 프로필이 있고 해당 프로필을 식별하는 데 도움이 필요한 경우 연결 다중 을 참조하십시오 [!DNL Google Analytics] 아래의 프로필 섹션에 자세히 설명되어 있습니다.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. 변경 내용이 자동으로 저장되므로 **연결로 돌아가기** 다 되면

## 다중 연결 [!DNL Google Analytics] 프로필

여러 웹 사이트가 한 사이트에 연결되어 있을 수 있습니다 [!DNL Google Analytics] account, 자체 식별 [!DNL Google Analytics] 프로필 ID. 이 경우 모든 프로필 ID를 포함할 수 있습니다. [!DNL MBI]. 프로필 선택 단계 동안 포함할 프로필 ID를 확인하면 됩니다.

특정 웹 사이트의 [!DNL Google Analytics] 프로필 ID:

1. 에 로그인합니다. [!DNL Google Analytics]
1. 특정 웹 사이트의 [!DNL Google Analytics] 대시보드
1. URL을 확인합니다. 프로필 ID는 다음 8개의 숫자에 해당합니다 `p` 줄 끝:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 연결 끊기 [!DNL Google Analytics] 변환 전: [!DNL MBI] {#disconnect}

1. 다음 방문 [!DNL Google Analytics] [계정 설정](https://www.google.com/accounts/) 페이지.
1. 아래에 `Security` 섹션을 클릭하고 **[!UICONTROL edit]** 다음 `Authorizing` 애플리케이션 및 사이트.
1. 클릭 **[!UICONTROL revoke access]** 다음 [!DNL MBI].

## 관련:

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [연결 중 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [웹 사이트 활동 및 고객 전환율 분석](../../analysis/web-act-cust-conversion.md)
* [을 사용하여 사용자 획득 데이터 추적 [!DNL Google Analytics] 쿠키](../../analysis/google-track-user-acq.md)
