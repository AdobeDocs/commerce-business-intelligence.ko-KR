---
title: Zendesk 연결
description: ' [!DNL Commerce Intelligence]에서 헬프 데스크 보고를 통합하는 방법을 알아봅니다.'
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KBUuqTDD9s3qXDktcV3RzLx4zxtAFwAkKPbsQE2YGtI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 261
ht-degree: 0%

---

# [!DNL Zendesk] 연결

>[!NOTE]
>
>[관리자 권한](../../../administrator/user-management/user-management.md)이 필요합니다.

![Zendesk 로고](../../../assets/Zendesk_logo.png)

[!DNL Zendesk] 데이터를 연결하면 [!DNL Commerce Intelligence]에서 헬프 데스크 보고를 통합할 수 있습니다. 이를 통해 고객 지원을 최적화하고 매출과 함께 헬프 데스크 성과를 모니터링할 수 있습니다.

[!DNL Zendesk] 데이터 연결은 간단한 3단계 프로세스입니다.

1. [&#x200B; [!DNL Zendesk] 에서  [!DNL Commerce Intelligence]자격 증명 페이지 열기](#stepone)
1. [&#x200B; [!DNL Zendesk] API 토큰 검색](#steptwo)
1. [&#x200B; [!DNL Zendesk] 에  [!DNL Commerce Intelligence]로그인 정보 및 토큰 입력](#stepthree)

이 프로세스를 완료하려면 두 개의 브라우저 창 또는 탭을 열어야 합니다. 하나는 [!DNL Commerce Intelligence]에 대한 것이고 다른 하나는 [!DNL Zendesk] 계정에 대한 것입니다.

## [!DNL Zendesk]에서 [!DNL Commerce Intelligence] 자격 증명 페이지를 엽니다. {#stepone}

1. `Integrations`데이터 원본&#x200B;**[!UICONTROL Manage Data** > **&#x200B; > {통합&#x200B;**&#x200B;의 **0} 페이지로 이동합니다.]**
1. 화면 오른쪽에 있는 **[!UICONTROL Add Integration]**&#x200B;을(를) 클릭합니다.
1. [!DNL Zendesk] 아이콘을 클릭합니다. [!DNL Zendesk] 자격 증명 페이지가 열립니다.

## [!DNL Zendesk] API 토큰 검색 {#steptwo}

1. [!DNL Zendesk] 계정에 로그인한 창/탭에서 화면 왼쪽 아래 모서리에 있는 설정(톱니바퀴) 아이콘을 클릭합니다.
1. `Settings` 메뉴가 표시되면 `Channels` 섹션을 찾습니다. 이 섹션에서 **[!UICONTROL API]**&#x200B;을(를) 클릭합니다.
1. 이 페이지의 `Token Access` 섹션에서 `Enabled` 옆에 있는 확인란을 클릭합니다. 활성 API 토큰 목록이 표시됩니다.
1. **[!UICONTROL Add New Token]**&#x200B;을(를) 클릭합니다.
1. 메시지가 표시되면 토큰에 대한 레이블을 입력합니다. Adobe에서는 토큰을 사용하는 응용 프로그램을 한눈에 알 수 있도록 `Commerce Intelligence`을(를) 사용하는 것이 좋습니다.
1. **[!UICONTROL Create]**&#x200B;을(를) 클릭합니다.
1. API 토큰이 만들어집니다. 이 토큰을 복사하십시오. 다음 단계에서 사용됩니다.

## [!DNL Zendesk]에 [!DNL Commerce Intelligence] 로그인 정보 및 API 토큰 입력 {#stepthree}

1. [!DNL Zendesk]의 [!DNL Zendesk] 자격 증명 페이지에 [!DNL Commerce Intelligence] 사이트 접두사 및 로그인 전자 메일을 입력하십시오.
1. API 토큰을 입력합니다.
1. **[!UICONTROL Save & Connect]**&#x200B;을(를) 클릭합니다. 연결이 성공하면 *연결이 성공합니다!* 메시지가 화면 맨 위에 표시됩니다.

## 관련 항목:

* [&#x200B; [!DNL Zendesk] 데이터가 필요합니다.](../integrations/exp-zendesk-data.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
