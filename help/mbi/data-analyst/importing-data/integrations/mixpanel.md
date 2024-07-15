---
title: Mixpanel 연결
description: 사용자가 웹 사이트 및 앱을 탐색하고 사용하는 방법을 분석하는 방법에 대해 알아봅니다.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# [!DNL Mixpanel] 연결

>[!NOTE]
>
>[관리자 권한](../../../administrator/user-management/user-management.md)이 필요합니다.

![](../../../assets/Mixpanel_logo.png)

[!DNL Mixpanel]을(를) 사용하면 사용자가 웹 사이트와 앱을 탐색하고 사용하는 방법을 분석할 수 있습니다. 사용자 행동 데이터를 면밀히 살펴보면 설계 및 개발 결정이 더욱 스마트해져 전체적으로 더 나은 제품을 만들 수 있습니다. [!DNL Mixpanel]을(를) [!DNL Commerce Intelligence]에 연결하면 사용자의 동작 방식과 이러한 동작이 매출로 전환되는 방식을 분석할 수 있습니다.

간단한 3단계 프로세스를 통해 [!DNL Mixpanel] 데이터를 [!DNL Commerce Intelligence]에 연결:

1. [ [!DNL Commerce Intelligence]에서  [!DNL Mixpanel] 자격 증명 페이지 열기](#stepone)
1. [ [!DNL Mixpanel] API 자격 증명 검색](#steptwo)
1. [ [!DNL Commerce Intelligence]에  [!DNL Mixpanel] API 자격 증명 입력](#stepthree)

이 프로세스를 완료하려면 두 개의 브라우저 창 또는 탭을 열어야 합니다. 하나는 [!DNL Commerce Intelligence]에 대한 것이고 다른 하나는 [!DNL Mixpanel] 계정에 대한 것입니다.

## [!DNL Mixpanel] 자격 증명 페이지를 여는 중 {#stepone}

시작:

1. **[!DNL Manage Data** > **Connections]** 아래의 `Connections` 페이지로 이동합니다.

1. `Data Sources` 테이블 위의 화면 오른쪽에 있는 **[!UICONTROL Add a New Source]**&#x200B;을(를) 클릭합니다.

1. [!DNL Mixpanel] 아이콘을 클릭하면 자격 증명 페이지가 열립니다.

지금은 이 페이지를 열어 두고 [!DNL Mixpanel] 계정이 있는 브라우저 창으로 전환하십시오.

## [!DNL Mixpanel] API 자격 증명을 가져오는 중 {#steptwo}

[!DNL Mixpanel] 계정에 아직 로그인하지 않은 경우 로그인한 후 다음을 수행합니다.

1. 오른쪽 상단의 **[!UICONTROL Account]**&#x200B;을(를) 클릭합니다.

1. 표시된 대화 상자에서 **[!UICONTROL Projects]**&#x200B;을(를) 클릭합니다.

1. API 자격 증명이 표시됩니다.

![Mixpanel API 자격 증명 검색](../../../assets/Mixpanel_API_creds.png)

이걸 열어 두시면 이걸 포장할 필요가 있어요.

## [!DNL Commerce Intelligence]에서 [!DNL Mixpanel] API 자격 증명 입력 {#stepthree}

1. `API Key` 및 `Secret`을(를) [!DNL Commerce Intelligence]의 [!DNL Mixpanel] 자격 증명 페이지에 복사합니다.
1. 설치를 완료하려면 **[!UICONTROL Connect to Mixpanel]**&#x200B;을(를) 클릭하십시오.

연결이 성공하면 _이(가) 성공합니다!_ 메시지가 페이지 맨 위에 표시됩니다.

### 관련 항목

* [ [!DNL Mixpanel] 데이터가 필요합니다.](../integrations/mixpanel-data.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
