---
title: Adobe Analytics 연결
description: 의 종단 간 고객 여정을 통합하는 방법 [!DNL Adobe Analytics] 그리고 사용자가 사용하는 eCommerce에 중점을 둡니다 [!DNL MBI].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# Connect [!DNL Adobe Analytics]

>[!NOTE]
>
>필요한 경우 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

다음 [!DNL Adobe Analytics] 통합 [!DNL MBI] 을 통해 [!DNL Adobe Analytics] 그리고 사용자가 사용하는 eCommerce에 중점을 둡니다 [!DNL MBI]를 입력하여 저장소의 전체 성과를 보다 정확하게 파악할 수 있습니다.

특히, [!DNL Adobe Analytics] 통합 [!DNL MBI] 는 상거래 및 Analytics 데이터 세트 결합을 시작할 수 있는 기능을 제공합니다.
- 기존 항목에서 연결 만들기 [!DNL Adobe Analytics] 계정 [!DNL MBI].
- 한 보고서 세트에서 최대 25개의 지표와 차원을 선택하여 [!DNL MBI] data warehouse.
- 모든 표준 사용 [!DNL MBI] 복제된 데이터를 변환, 결합 및 보고하는 기능 [!DNL Adobe Analytics] 데이터.

## 연결 사전 요구 사항

연결하려면 다음 정보가 필요합니다.
- [!DNL Adobe Analytics] 로그인 자격 증명
- `Name` 및/또는 `ID` 의 [!DNL Adobe Analytics] 보고서 세트에서 데이터 복제
- 복제할 지표 및 차원 목록 [!DNL MBI]

## 연결 [!DNL Adobe Analytics] MBI용 통합

1. 로 이동합니다. `Integrations` 아래의 페이지 **[!DNL Manage Data** > **Integrations]**.
1. 클릭 **[!UICONTROL Add an Integration]**, 화면 오른쪽에 있습니다.
1. 을(를) 클릭합니다. **[!UICONTROL Adobe Analytics]** 아이콘을 클릭하여 권한을 부여할 수 있는 페이지에 액세스합니다 [!DNL Adobe Analytics] 계정 연결.
1. 클릭 **[!UICONTROL Authorize with Adobe Analytics]**.
1. 을(를) 입력합니다. [!DNL Adobe Analytics] 자격 증명. 인증이 성공하면 [!DNL MBI].
1. 사용 가능한 보고서 세트 목록이 표시됩니다. 데이터를 가져올 보고서 세트를 선택한 다음 **[!UICONTROL Continue]**.
1. 지표 및 차원 선택 화면이 표시됩니다. 총 25개의 지표 및 차원을 합하여 하나 이상의 지표와 차원을 선택합니다. 이름이나 스크롤로 검색하여 구성 요소를 찾은 다음 확인란을 클릭하여 선택합니다. 클릭 **[!UICONTROL Continue]**.
1. 선택한 보고서 세트가 테이블에 표시됩니다. 클릭 **[!UICONTROL Save]** 을 클릭하여 선택 항목을 확인합니다.
1. 다음 사항에 알림 [!DNL MBI] 통합이 승인되고 초기 연결 프로세스가 실행되도록 지원 팀을 관리합니다.

초기 연결 프로세스가 실행되면 Data Warehouse 페이지의 `All Tables` 탭. 복제할 열을 선택하면 다음 전체 업데이트 후에 데이터가 표시됩니다.
