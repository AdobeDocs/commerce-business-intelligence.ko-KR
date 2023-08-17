---
title: Zendesk 연결
description: 에서 헬프 데스크 보고를 통합하는 방법을 알아봅니다. [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# 연결 [!DNL Zendesk]

>[!NOTE]
>
>필요 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

연결 중 [!DNL Zendesk] 데이터를 통해 헬프 데스크 보고를 통합할 수 있습니다. [!DNL Commerce Intelligence]. 이를 통해 고객 지원을 최적화하고 매출과 함께 헬프 데스크 성과를 모니터링할 수 있습니다.

연결 중 [!DNL Zendesk] 데이터는 다음과 같은 간단한 3단계 프로세스입니다.

1. [를 엽니다. [!DNL Zendesk] 의 자격 증명 페이지 [!DNL Commerce Intelligence]](#stepone)
1. [검색 [!DNL Zendesk] API 토큰](#steptwo)
1. [다음을 입력하십시오. [!DNL Zendesk] 로그인 정보 및 토큰: [!DNL Commerce Intelligence]](#stepthree)

이 프로세스를 완료하려면 두 개의 브라우저 창 또는 탭을 열어야 합니다. [!DNL Commerce Intelligence], 다음에 대한 항목: [!DNL Zendesk] 계정입니다.

## 를 엽니다. [!DNL Zendesk] 의 자격 증명 페이지 [!DNL Commerce Intelligence] {#stepone}

1. 로 이동 `Integrations` 아래 페이지 **[!UICONTROL Manage Data** > **&#x200B;데이터 소스&#x200B;**> **통합]**.
1. 클릭 **[!UICONTROL Add Integration]**&#x200B;을 클릭합니다.
1. 다음을 클릭합니다. [!DNL Zendesk] 아이콘. 이렇게 하면 [!DNL Zendesk] 자격 증명 페이지입니다.

## 검색 [!DNL Zendesk] API 토큰 {#steptwo}

1. 에 로그인되어 있는 창/탭 [!DNL Zendesk] 계정에서 화면 왼쪽 아래 모서리에 있는 설정 (톱니바퀴) 아이콘을 클릭합니다.
1. 다음의 경우 `Settings` 메뉴가 표시되면 `Channels` 섹션. 클릭 **[!UICONTROL API]** 이 섹션에서 참조할 수 있습니다.
1. 다음에서 `Token Access` 이 페이지의 섹션에서 옆에 있는 확인란을 클릭합니다. `Enabled`. 활성 API 토큰 목록이 표시됩니다.
1. 클릭 **[!UICONTROL Add New Token]**.
1. 메시지가 표시되면 토큰에 대한 레이블을 입력합니다. Adobe은 다음을 권장합니다. `Commerce Intelligence`따라서 한 눈에 토큰을 사용하는 애플리케이션이 무엇인지 알 수 있습니다.
1. 클릭 **[!UICONTROL Create]**.
1. API 토큰이 만들어집니다. 이 토큰을 복사하십시오. 다음 단계에서 사용됩니다.

## 입력 [!DNL Zendesk] 에 로그인 정보 및 API 토큰 [!DNL Commerce Intelligence] {#stepthree}

1. 다음을 입력하십시오. [!DNL Zendesk] 의 사이트 접두사 및 로그인 이메일 [!DNL Zendesk] 의 자격 증명 페이지 [!DNL Commerce Intelligence].
1. API 토큰을 입력합니다.
1. 클릭 **[!UICONTROL Save & Connect]**. 정상적으로 연결되면 *연결 성공!* 화면 맨 위에 메시지가 표시됩니다.

## 관련 항목:

* [예상 [!DNL Zendesk] 데이터](../integrations/exp-zendesk-data.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
