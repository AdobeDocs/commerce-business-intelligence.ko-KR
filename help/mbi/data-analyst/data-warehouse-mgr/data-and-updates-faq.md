---
title: 데이터 및 업데이트 정보
description: 업데이트 주기 상태를 확인하는 방법을 알아봅니다.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/qT3lojSuve8jHgNVKoJCUW82cN2QK497wFX8NVbptWI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 481
ht-degree: 0%

---

# 데이터 및 업데이트 정보

* [데이터가 변경된 이유는 무엇입니까?](#datachange)
* [정기 업데이트와 강제 업데이트의 차이점은 무엇입니까?](#regularforcedupdates)
* [업데이트 주기가 오래 걸리는 이유는 무엇입니까?](#updatecycletime)
* [업데이트 주기가 완료되면 알림을 받을 수 있습니까?](#notifyupdate)
* [&#x200B; [!DNL Google ECommerce] 데이터가 내 데이터베이스와 다른 이유는 무엇입니까?](#ecommdatabase)
* [데이터 불일치 문제를 해결하려면 어떻게 합니까?](#datadiscrepancy)

## 데이터가 변경된 이유는 무엇입니까? {#datachange}

새 데이터가 Data Warehouse에 동기화되어 차트 값이 하루 종일 변경될 수 있습니다. 또한 [다시 확인](../data-warehouse-mgr/cfg-data-rechecks.md)으로 인해 기존 데이터 열의 값이 변경될 수 있습니다. 다시 검사는 `open`에서 `shipped`(으)로 이동하는 주문 상태와 같이 데이터 열에서 변경된 값을 찾는 프로세스입니다.

사용자의 권한 설정에 따라 [업데이트 주기 상태를 확인](../../best-practices/check-update-cycle.md)하는 여러 가지 방법이 있습니다.

* **[!UICONTROL Read-Only]및 [!UICONTROL Standard]명의 사용자** - 페이지의 오른쪽 상단에 있는 아이콘 위로 마우스를 가져가면 마지막 데이터 포인트를 가져올 수 있습니다.
* **[!UICONTROL Admin]사용자** - 마지막 데이터 지점 및 계정 통합 상태 아이콘을 볼 수 있습니다. 자세한 내용을 보려면 **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**(으)로 이동하여 현재 업데이트 상태 및 마지막으로 완료된 업데이트 시간을 확인하십시오.
* **API 메서드** - 업데이트 주기 상태 API를 사용하여 가장 최근에 완료된 업데이트 주기를 검색할 수 있습니다.

업데이트 주기 상태 확인에 대한 자세한 내용은 [업데이트 주기 상태 확인](../../best-practices/check-update-cycle.md)을 참조하세요.

## 정기 업데이트와 강제 업데이트의 차이점은 무엇입니까? {#regularforcedupdates}

일반 업데이트는 **예약됨** 프로세스이고 강제 업데이트는 **수동 프로세스 시작**&#x200B;입니다. 일시 중단 시간(또는 [!DNL Commerce Intelligence]에서 데이터를 업데이트하지 말아야 하는 기간)이 있는 경우 강제로 업데이트를 수행하면 일시 중단 기간의 제한을 준수하지 않는 주기가 시작됩니다.

## 업데이트 주기가 오래 걸리는 이유는 무엇입니까? {#updatecycletime}

많은 요인으로 인해 이미 긴 업데이트 시간이 추가될 수 있습니다. 특정 [복제 메서드](../data-warehouse-mgr/cfg-replication-methods.md), [더 높은 재확인 빈도](../data-warehouse-mgr/cfg-data-rechecks.md) 및 대시보드 및 차트 수가 몇 가지 기여자에 불과합니다. Adobe에서는 업데이트 시간을 줄이려면 [일부 설정을 다시 구성](../../best-practices/reduce-update-cycle-time.md)하고 [분석을 위해 데이터베이스를 최적화](../../best-practices/opt-db-analysis.md)하는 것이 좋습니다.

## 업데이트 주기가 완료되면 알림을 받을 수 있습니까? {#notifyupdate}

업데이트가 진행 중인 경우 주기가 완료되면 이메일 알림을 요청하는 데 사용할 수 있는 링크가 **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]** 페이지에 있습니다. 업데이트가 진행 중이 아닌 경우 대신 업데이트를 시작하도록 하는 링크가 표시됩니다.

## [!DNL Google ECommerce]데이터가 내 데이터베이스와 다른 이유는 무엇입니까? {#ecommdatabase}

[!DNL Google Analytics]과(와) 데이터베이스 간의 불일치는 여러 가지 이유로 발생할 수 있습니다. 추적이 제대로 활성화되지 않음, 사용자가 시크릿 방문 및 클릭 이벤트가 제대로 작동하지 않는 것은 몇 가지 예에 불과합니다. 매출과 주문이 올바르게 표시되지 않으면 [이 항목을 참조](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=ko)하여 문제를 진단하십시오.

## 데이터 불일치 문제를 해결하려면 어떻게 합니까? {#datadiscrepancy}

Adobe은 일관되지 않은 데이터를 보는 것이 답답한 경험이 될 수 있다는 것을 알고 있습니다. [데이터 불일치 검사 목록](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=ko) 또는 [데이터 내보내기 자습서](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=ko)를 사용하여 문제를 진단해 보십시오. 여전히 문제가 있으면 [지원팀에 문의](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ko)하세요.
