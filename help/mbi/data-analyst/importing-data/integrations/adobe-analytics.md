---
title: Adobe Analytics 연결
description: ' [!DNL Adobe Analytics] 의 엔드 투 엔드 고객 여정 포커스와  [!DNL Commerce Intelligence]에서 의존하는 전자 상거래 포커스를 통합하는 방법을 알아봅니다.'
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# [!DNL Adobe Analytics] 연결

>[!NOTE]
>
>[관리자 권한](../../../administrator/user-management/user-management.md)이 필요합니다.

![Adobe Analytics 로고](../../../assets/adobe-analytic-slogo.png)

[!DNL Adobe Analytics]에 대한 [!DNL Adobe Commerce Intelligence] 통합을 통해 [!DNL Adobe Analytics]의 엔드 투 엔드 고객 여정 포커스와 [!DNL Commerce Intelligence]에서 의존하는 전자 상거래 포커스를 통합할 수 있습니다. 이렇게 하면 스토어의 전반적인 성능을 전체적으로 파악할 수 있습니다.

특히 [!DNL Adobe Analytics]에 대한 [!DNL Commerce Intelligence] 통합은 판매자가 [!DNL Adobe Commerce]과(와) [!DNL Adobe Analytics] 데이터 집합을 결합하는 기능을 제공합니다.

- 기존 [!DNL Adobe Analytics] 계정에서 [!DNL Commerce Intelligence]&#x200B;(으)로 연결을 만듭니다.

- 하나의 보고서 세트에서 최대 25개의 지표 및 차원을 선택하여 Data Warehouse에 복제합니다.

- 모든 표준 [!DNL Commerce Intelligence] 기능을 사용하여 복제된 [!DNL Adobe Analytics] 데이터를 변환, 조인 및 보고합니다.

## 연결 사전 요구 사항

연결하려면 다음 정보가 필요합니다.

- [!DNL Adobe Analytics] 로그인 자격 증명

- 데이터를 복제할 보고서 세트 `Name`개 중 `ID` 및/또는 [!DNL Adobe Analytics]

- [!DNL Commerce Intelligence]에 복제할 지표 및 차원 목록

## [!DNL Adobe Analytics]에 대한 [!DNL Commerce Intelligence] 통합 연결 중

1. `Integrations` 아래의 **[!DNL Manage Data** > **Integrations]** 페이지로 이동합니다.

1. **[!UICONTROL Add an Integration]**&#x200B;을(를) 클릭합니다.

1. **[!UICONTROL Adobe Analytics]** 계정 연결을 승인할 수 있는 페이지에 액세스하려면 [!DNL Adobe Analytics] 아이콘을 클릭하십시오.

1. **[!UICONTROL Authorize with Adobe Analytics]**&#x200B;을(를) 클릭합니다.

1. [!DNL Adobe Analytics] 자격 증명을 입력하십시오. 인증에 성공하면 [!DNL Commerce Intelligence]&#x200B;(으)로 다시 리디렉션됩니다.

1. 사용 가능한 보고서 세트 목록이 표시됩니다. 데이터를 가져올 보고서 세트를 선택한 다음 **[!UICONTROL Continue]**&#x200B;을(를) 클릭합니다.

1. 지표 및 차원 선택 화면이 표시됩니다. 최소 하나 이상의 지표와 차원을 선택합니다. 총 25개의 지표와 차원을 조합할 수 있습니다. 이름으로 검색하거나 스크롤하여 구성 요소를 찾은 다음 확인란을 클릭하여 선택합니다. **[!UICONTROL Continue]**&#x200B;을(를) 클릭합니다.

1. 선택한 보고서 세트가 테이블에 표시됩니다. **[!UICONTROL Save]**&#x200B;을(를) 클릭하여 선택 내용을 확인합니다.

1. 통합이 승인되었음을 [!DNL Commerce Intelligence] [지원 팀](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ko)에 알리고 초기 연결 프로세스를 실행합니다.

초기 연결 프로세스가 실행되면 Data Warehouse 페이지의 `All Tables` 탭에서 테이블을 사용할 수 있습니다. 복제할 열을 선택하면 다음 전체 업데이트 후에 데이터가 표시됩니다.
