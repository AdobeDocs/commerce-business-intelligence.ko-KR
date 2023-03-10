---
title: Mixpanel 연결
description: 사용자가 웹 사이트 및 앱을 탐색하고 사용하는 방법을 분석하는 방법에 대해 알아봅니다.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# 연결 [!DNL Mixpanel]

>[!NOTE]
>
>필요 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

포함 [!DNL Mixpanel], 사용자가 웹 사이트 및 앱을 탐색하고 사용하는 방법을 분석할 수 있습니다. 사용자 행동 데이터를 면밀히 살펴보면 설계 및 개발 결정이 더욱 스마트해져 전체적으로 더 나은 제품을 만들 수 있습니다. 연결 중 [!DNL Mixpanel] 끝 [!DNL MBI] 사용자가 어떻게 행동하고 그 행동이 어떻게 수익으로 해석되는지 분석할 수 있도록 해줍니다.

연결 중 [!DNL Mixpanel] 데이터 받는 사람 [!DNL MBI] 간단한 3단계 프로세스:

1. [를 엽니다. [!DNL Mixpanel] 의 자격 증명 페이지 [!DNL MBI]](#stepone)
1. [검색 [!DNL Mixpanel] API 자격 증명](#steptwo)
1. [다음을 입력하십시오. [!DNL Mixpanel] MBI의 API 자격 증명](#stepthree)

이 프로세스를 완료하려면 두 개의 브라우저 창 또는 탭을 열어야 합니다. [!DNL MBI], 다음에 대한 항목: [!DNL Mixpanel] 계정입니다.

## 열기 [!DNL Mixpanel] 자격 증명 페이지 {#stepone}

시작:

1. 로 이동 `Connections` 아래 페이지 **[!DNL Manage Data** > **Connections]**.
1. 클릭 **[!UICONTROL Add a New Source]**, 위의 화면 오른쪽에 있음 `Data Sources` 테이블.
1. 다음을 클릭합니다. [!DNL Mixpanel] 아이콘을 클릭하면 자격 증명 페이지가 열립니다.

지금은 이 페이지를 열어 두고 을(를) 사용하여 브라우저 창으로 전환합니다. [!DNL Mixpanel] 계정입니다.

## 검색 중 [!DNL Mixpanel] API 자격 증명 {#steptwo}

에 로그인하지 않은 경우 [!DNL Mixpanel] 아직 계정을 만든 후 다음을 수행합니다.

1. 클릭 **[!UICONTROL Account]** 오른쪽 상단 모서리입니다.
1. 표시된 대화 상자에서 **[!UICONTROL Projects]**.
1. API 자격 증명이 표시됩니다.

![Mixpanel API 자격 증명 검색 중](../../../assets/Mixpanel_API_creds.png)

열어 두십시오. 포장을 해야 합니다.

## 사용자 입력 [!DNL Mixpanel] 의 API 자격 증명 [!DNL MBI] {#stepthree}

1. 다음을 복사합니다. `API Key` 및 `Secret` 대상: [!DNL Mixpanel] 의 자격 증명 페이지 [!DNL MBI].
1. 클릭 **[!UICONTROL Connect to Mixpanel]** 설치를 완료합니다.

바로 그거야! 정상적으로 연결되면 _성공!_ 메시지가 페이지 맨 위에 표시됩니다.

### 관련 항목

* [예상 [!DNL Mixpanel] 데이터](../integrations/mixpanel-data.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
