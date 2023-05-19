---
title: Adobe Analytics 연결
description: 의 엔드 투 엔드 고객 여정 포커스를 통합하는 방법에 대해 알아봅니다. [!DNL Adobe Analytics] and the eCommerce focus you really 의존하는 from [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 연결 [!DNL Adobe Analytics]

>[!NOTE]
>
>필요 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

다음 [!DNL Adobe Analytics] 통합 대상 [!DNL Adobe Commerce Intelligence] 을(를) 통해 의 엔드 투 엔드 고객 여정 포커스를 통합할 수 있습니다. [!DNL Adobe Analytics] and the eCommerce focus you really 의존하는 from [!DNL Commerce Intelligence]. 이렇게 하면 스토어의 전반적인 성능을 전체적으로 파악할 수 있습니다.

특히, [!DNL Adobe Analytics] 통합 대상 [!DNL Commerce Intelligence] 판매자가 통합을 시작할 수 있는 기능을 제공합니다. [!DNL Adobe Commerce] 및 [!DNL Adobe Analytics] 데이터 세트.

- 기존 항목에서 연결 만들기 [!DNL Adobe Analytics] 계정 대상 [!DNL Commerce Intelligence].

- 하나의 보고서 세트에서 최대 25개의 Data Warehouse 및 차원을 선택하여 지표로 복제합니다.

- 모든 표준 사용 [!DNL Commerce Intelligence] 복제된 항목에 대한 변환, 조인 및 보고 기능 [!DNL Adobe Analytics] 데이터.

## 연결 사전 요구 사항

연결하려면 다음 정보가 필요합니다.

- [!DNL Adobe Analytics] 로그인 자격 증명

- `Name` 및/또는 `ID` / [!DNL Adobe Analytics] 데이터를 복제할 보고서 세트

- 복제할 지표 및 차원 목록 [!DNL Commerce Intelligence]

## 연결 중 [!DNL Adobe Analytics] 통합 대상 [!DNL Commerce Intelligence]

1. 로 이동 `Integrations` 아래 페이지 **[!DNL Manage Data** > **Integrations]**.

1. 클릭 **[!UICONTROL Add an Integration]**.

1. 다음을 클릭합니다. **[!UICONTROL Adobe Analytics]** 아이콘을 클릭하면 다음 권한이 부여되는 페이지에 액세스할 수 있습니다 [!DNL Adobe Analytics] 계정 연결.

1. 클릭 **[!UICONTROL Authorize with Adobe Analytics]**.

1. 다음을 입력하십시오. [!DNL Adobe Analytics] 자격 증명. 인증에 성공하면 다시 로 리디렉션됩니다. [!DNL Commerce Intelligence].

1. 사용 가능한 보고서 세트 목록이 표시됩니다. 데이터를 가져올 보고서 세트를 선택한 다음 **[!UICONTROL Continue]**.

1. 지표 및 차원 선택 화면이 표시됩니다. 최소 하나 이상의 지표와 차원을 선택합니다. 총 25개의 지표와 차원을 조합할 수 있습니다. 이름으로 검색하거나 스크롤하여 구성 요소를 찾은 다음 확인란을 클릭하여 선택합니다. 클릭 **[!UICONTROL Continue]**.

1. 선택한 보고서 세트가 테이블에 표시됩니다. 클릭 **[!UICONTROL Save]** 을 클릭하여 선택 항목을 확인합니다.

1. 다음 항목에 알림 [!DNL Commerce Intelligence] [지원 팀](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 통합을 승인하고 초기 연결 프로세스를 실행합니다.

초기 연결 프로세스가 실행되면 아래의 Data Warehouse 페이지에서 테이블을 사용할 수 있습니다. `All Tables` 탭. 복제할 열을 선택하면 다음 전체 업데이트 후에 데이터가 표시됩니다.
