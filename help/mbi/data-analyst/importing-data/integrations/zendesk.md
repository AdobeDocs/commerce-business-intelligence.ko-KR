---
title: Zendesk 연결
description: 에서 헬프데스크 보고를 통합하는 방법을 알아봅니다. [!DNL MBI].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Connect [!DNL Zendesk]

>[!NOTE]
>
>필요한 경우 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

연결 [!DNL Zendesk] 데이터를 사용하면 도움말 데스크 보고의 [!DNL MBI]. 이를 통해 고객 지원을 최적화할 수 있으며 매출과 함께 헬프데스크 성능을 모니터링할 수 있습니다.

연결 [!DNL Zendesk] 데이터는 간단한 3단계 프로세스입니다.

1. [를 엽니다. [!DNL Zendesk] 자격 증명 페이지 [!DNL MBI]](#stepone)
1. [검색 [!DNL Zendesk] API 토큰](#steptwo)
1. [을(를) 입력합니다. [!DNL Zendesk] 로그인 정보 및 토큰 입력 [!DNL MBI]](#stepthree)

이 프로세스를 완료하려면 브라우저 창 또는 탭 두 개를 열어야 합니다. [!DNL MBI], 및에 대해 [!DNL Zendesk] 계정이 필요합니다.

## 를 엽니다. [!DNL Zendesk] 자격 증명 페이지 [!DNL MBI] {#stepone}

1. 로 이동합니다. `Integrations` 아래의 페이지 **[!UICONTROL Manage Data** > **&#x200B;데이터 소스&#x200B;**> **통합]**.
1. 클릭 **[!UICONTROL Add Integration]**, 화면 오른쪽에 있습니다.
1. 을(를) 클릭합니다. [!DNL Zendesk] 아이콘. 이 옵션을 선택하면 [!DNL Zendesk] 자격 증명 페이지.

## 검색 [!DNL Zendesk] API 토큰 {#steptwo}

1. 에 로그인한 창/탭에서 다음을 수행합니다 [!DNL Zendesk] 계정이 있는 경우 화면의 왼쪽 하단 모서리에 있는 설정(톱니바퀴) 아이콘을 클릭합니다.
1. 이 `Settings` 메뉴 표시, 찾기 `Channels` 섹션을 참조하십시오. 클릭 **[!UICONTROL API]** 참조하십시오.
1. 에서 `Token Access` 이 페이지의 섹션에서 옆에 있는 확인란을 클릭합니다. `Enabled`. 활성 API 토큰 목록이 표시됩니다.
1. 클릭 **[!UICONTROL Add New Token]**.
1. 메시지가 표시되면 토큰에 대한 레이블을 입력합니다. 을 사용하는 것이 좋습니다 `MBI`로 설정되면 어떤 애플리케이션에서 토큰을 사용하고 있는지 한 눈에 알 수 있습니다.
1. 클릭 **[!UICONTROL Create]**.
1. API 토큰이 만들어집니다. 이 토큰을 복사합니다. 다음 단계에서 사용됩니다.

## Enter 키 [!DNL Zendesk] 로그인 정보 및 API 토큰 [!DNL MBI] {#stepthree}

1. 을(를) 입력합니다. [!DNL Zendesk] 사이트 접두사 및 로그인 전자 메일 [!DNL Zendesk] 자격 증명 페이지 [!DNL MBI].
1. API 토큰을 입력합니다.
1. 클릭 **[!UICONTROL Save & Connect]**. 연결에 성공하면 *연결에 성공했습니다!* 화면 상단에 메시지가 표시됩니다.

## 관련:

* [예상됨 [!DNL Zendesk] 데이터](../integrations/exp-zendesk-data.md)
* [통합 재인증](https://support.magento.com/hc/en-us/articles/360016733151)
