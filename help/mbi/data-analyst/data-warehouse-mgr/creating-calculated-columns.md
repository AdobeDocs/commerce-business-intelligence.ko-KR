---
title: 계산된 열 만들기
description: 다양한 소스의 데이터를 통합하는 방법을 알아보십시오.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/dGzhox6Xjuvc3goSxkF2W-5yBlkgKgnOJg7YcuD2Q0s
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 345
ht-degree: 0%

---

# 계산된 열 만들기

데이터를 분석할 때 다양한 소스의 데이터를 통합하는 것이 좋습니다. `orders` 테이블의 데이터와 [!DNL Google Analytics] 데이터를 연결하여 획득 소스별로 매출을 그룹화하시겠습니까? 세분화를 위해 고객 성별을 기준으로 매출을 그룹화하거나 거래 데이터에 고객 속성을 결합할 수 있습니다. 이 항목에서는 이 작업을 수행하는 방법에 대해 설명합니다.

시작하기 전에 [계산된 열 유형 안내서](../../data-analyst/data-warehouse-mgr/calc-column-types.md)를 검토하여 Data Warehouse Manager에서 만들 수 있는 열 유형과 해당 정의 및 예제를 살펴보는 것이 좋습니다.

1. 시작하려면 **[!DNL Manage Data > Data Warehouse]**&#x200B;을(를) 클릭하세요.

1. 열을 만들 테이블을 클릭합니다. 예를 들어 매출 세분화를 위해 `Customer Gender` 열을 만들려면 `sales_flat_order` 테이블을 선택합니다.

1. 테이블 구성표가 표시됩니다. **[!UICONTROL Create New Column]**&#x200B;을(를) 클릭합니다.

1. 열에 이름을 지정합니다. 예: `Customer Gender`.

1. 열에 대한 정의를 선택합니다. 여기에서 [계산된 열 유형 가이드](../data-warehouse-mgr/calc-column-types.md)를 사용할 수 있습니다.

1. 특정 열 유형의 경우 열을 제대로 만들려면 추가 정보가 필요합니다.

   * `One to Many`(조인됨) 및 `Many to One`(집계) 열의 경우 테이블 및 열을 선택해야 합니다.

   * `Same Table calculation`의 경우 드롭다운에서 원하는 날짜 필드를 선택해야 합니다.

`One to Many`(조인됨) 또는 `Many to One`(집계) 열을 만드는 경우 두 테이블을 연결할 경로를 선택해야 합니다. 이 단계에서는 기존 경로를 사용하거나 경로를 만들 수 있습니다.

>[!NOTE]
>
>표를 여러 개 또는 한 개로 올바르게 정의해야 합니다.

* 원하는 경우 [필터](../../data-user/reports/ess-manage-data-filters.md)를 새 열에 적용할 수 있습니다.

* 완료되면 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

새 열이 현재 테이블에 `Pending` 상태로 나타납니다. 다음 업데이트가 완료되면 지표 및 보고서에서 열을 사용할 수 있습니다.

## 핸디 참조 맵 {#map}

계산된 열을 만들 때 모든 입력을 기억하는 데 문제가 있는 경우, 작성 시 이 참조 맵을 근처에 보관해 보십시오.

![Data Warehouse Manager의 계산된 열 구성 예](../../assets/Calculated_Columns_Example.png)

## 관련 설명서

* [계산된 열 유형](../data-warehouse-mgr/calc-column-types.md)
* [고급 계산 열 유형](../data-warehouse-mgr/adv-calc-columns.md)
* [주문 및 고객 데이터를 사용하여  [!DNL Google ECommerce] 차원 작성](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
