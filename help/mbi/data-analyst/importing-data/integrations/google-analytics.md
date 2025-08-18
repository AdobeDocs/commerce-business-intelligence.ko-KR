---
title: Google Analytics 연결
description: ' [!DNL Commerce Intelligence]과(와) Google Analytics 연결에 대해 알아봅니다.'
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# [!DNL Google Analytics] 연결

>[!NOTE]
>
>[관리자 권한](../../../administrator/user-management/user-management.md)이 필요합니다.

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics]은(는) 인터넷에서 가장 널리 사용되는 웹 분석 서비스입니다. 웹 사이트에 [!DNL Google Analytics]을(를) 구현하면 방문자가 사이트를 사용하는 방법, 매력적인 콘텐츠, 방문자가 종료하는 위치 등을 추적할 수 있습니다. 다른 데이터와 함께 [!DNL Commerce Intelligence]에서 이러한 지표를 분석하면 사이트의 전반적인 상태와 유용성이 향상됩니다.

[!DNL Google Analytics]에 [!DNL Commerce Intelligence] 자격 증명을 입력하여 시작하십시오.

1. **[!UICONTROL Manage Data** > **Integrations]**(으)로 이동합니다.

1. 화면 오른쪽에 있는 **[!UICONTROL Add Integration]**&#x200B;을(를) 클릭합니다.

1. [!DNL Google Analytics] 아이콘을 클릭합니다. [!DNL Google Analytics] 자격 증명 페이지가 열립니다.

1. [!DNL Google Analytics] 자격 증명을 입력하십시오. 인증 프로세스가 완료되면 [!DNL Commerce Intelligence]&#x200B;(으)로 다시 리디렉션됩니다.

1. 프로필 ID 목록이 표시됩니다. [!DNL Commerce Intelligence]에 연결할 프로필을 확인하십시오. 프로필이 여러 개이고 어떤 프로필인지 식별하는 데 도움이 필요한 경우 아래의 여러 [!DNL Google Analytics] 프로필 연결 섹션을 참조하십시오.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. 변경 사항이 자동으로 저장되므로 완료되면 **연결로 돌아가기**&#x200B;를 클릭하세요.

## 여러 [!DNL Google Analytics]개의 프로필 연결 중

하나의 [!DNL Google Analytics] 계정에 여러 웹 사이트가 연결되어 있으며, 해당 웹 사이트가 [!DNL Google Analytics] 프로필 ID로 식별될 수 있습니다. 이 경우 [!DNL Commerce Intelligence]에 모든 프로필 ID를 포함할 수 있습니다. 프로필 선택 단계에서 포함할 프로필 ID를 확인합니다.

특정 웹 사이트의 [!DNL Google Analytics] 프로필 ID를 식별하려면 다음을 수행하십시오.

1. [!DNL Google Analytics]에 로그인
1. 특정 웹 사이트의 [!DNL Google Analytics] 대시보드로 이동
1. URL을 확인합니다. 프로필 ID는 줄 끝에 있는 `p` 뒤에 오는 8개의 숫자에 해당합니다.

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## [!DNL Google Analytics]에서 [!DNL Commerce Intelligence]의 연결을 끊는 중 {#disconnect}

1. [!DNL Google Analytics] [계정 설정](https://accounts.google.com/) 페이지를 방문하세요.
1. `Security` 섹션 아래에서 **[!UICONTROL edit]**&#x200B;개의 응용 프로그램 및 사이트 옆에 있는 `Authorizing`을(를) 클릭합니다.
1. **[!UICONTROL revoke access]** 옆에 있는 [!DNL Commerce Intelligence]을(를) 클릭합니다.

## 관련 항목:

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ko)
* [ [!DNL Google Adwords] 연결 중](../integrations/google-adwords.md)
* [웹 사이트 활동 및 고객 전환율 분석](../../analysis/web-act-cust-conversion.md)
* [ [!DNL Google Analytics] 쿠키를 사용하여 사용자 획득 데이터 추적](../../analysis/google-track-user-acq.md)
