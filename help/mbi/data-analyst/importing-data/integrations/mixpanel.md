---
title: Mixpanel 연결
description: 사용자가 웹 사이트 및 앱을 탐색하고 활용하는 방법을 분석하는 방법을 알아봅니다.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Connect [!DNL Mixpanel]

>[!NOTE]
>
>필요한 경우 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

사용 [!DNL Mixpanel], 사용자가 웹 사이트 및 앱을 탐색하고 활용하는 방법을 분석할 수 있습니다. 사용자 행동 데이터를 자세히 살펴보면 더 스마트한 디자인과 개발 의사 결정이 내려집니다. 이는 전반적으로 더 나은 제품을 의미합니다. 연결 중 [!DNL Mixpanel] to [!DNL MBI] 사용자의 동작 방식과 해당 행동이 매출로 변환되는 방식을 분석할 수 있도록 해줍니다.

연결 [!DNL Mixpanel] 다음으로 데이터 [!DNL MBI] 간단한 3단계 프로세스:

1. [를 엽니다. [!DNL Mixpanel] 자격 증명 페이지 [!DNL MBI]](#stepone)
1. [검색 [!DNL Mixpanel] API 자격 증명](#steptwo)
1. [을(를) 입력합니다. [!DNL Mixpanel] MBI의 API 자격 증명](#stepthree)

이 프로세스를 완료하려면 브라우저 창 또는 탭 두 개를 열어야 합니다. [!DNL MBI], 및에 대해 [!DNL Mixpanel] 계정이 필요합니다.

## 열기 [!DNL Mixpanel] 자격 증명 페이지 {#stepone}

시작하기:

1. 로 이동합니다. `Connections` 아래의 페이지 **[!DNL Manage Data** > **Connections]**.
1. 클릭 **[!UICONTROL Add a New Source]**- 화면 오른쪽 위의 `Data Sources` 테이블.
1. 을(를) 클릭합니다. [!DNL Mixpanel] 아이콘 및 자격 증명 페이지가 열립니다.

지금 이 페이지를 열어 두고 을 사용하여 브라우저 창으로 전환합니다. [!DNL Mixpanel] 계정이 필요합니다.

## 검색 [!DNL Mixpanel] API 자격 증명 {#steptwo}

로그인하지 않은 경우 [!DNL Mixpanel] 아직 계정을 설정하고 다음을 수행합니다.

1. 클릭 **[!UICONTROL Account]** 오른쪽 상단 모서리에서
1. 표시된 대화 상자에서 **[!UICONTROL Projects]**.
1. API 자격 증명이 표시됩니다.

![Mixpanel API 자격 증명 검색](../../../assets/Mixpanel_API_creds.png)

이것을 열어 두십시오. 이것을 마무리하기 위해서 필요합니다.

## 사용자 [!DNL Mixpanel] 의 API 자격 증명 [!DNL MBI] {#stepthree}

1. 를 복사합니다. `API Key` 및 `Secret` 로 [!DNL Mixpanel] 자격 증명 페이지 [!DNL MBI].
1. 클릭 **[!UICONTROL Connect to Mixpanel]** 를 클릭하여 설정을 완료합니다.

바로 그거야! 연결에 성공하면 _성공!_ 페이지 상단에 메시지가 표시됩니다.

### 관련

* [예상됨 [!DNL Mixpanel] 데이터](../integrations/mixpanel-data.md)
* [통합 재인증](https://support.magento.com/hc/en-us/articles/360016733151)
