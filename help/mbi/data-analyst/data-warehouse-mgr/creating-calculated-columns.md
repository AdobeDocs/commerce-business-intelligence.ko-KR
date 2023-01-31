---
title: 계산된 열 만들기
description: 다양한 소스의 데이터를 통합하는 방법을 알아봅니다.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# 계산된 열 만들기

데이터를 분석할 때 다른 소스의 데이터를 통합하는 것이 좋습니다. 매출을 획득 소스별로 그룹화하고 주문 테이블과 Google Analytics의 데이터를 연결하시겠습니까? 또는 고객 성별별로 매출을 그룹화하거나 세분화를 위해 고객 특성을 거래 데이터에 결합하는 것은 어떻습니까?

이 가이드가 그 방법을 가르쳐 줄 거예요. 시작하기 전에 다음을 확인하시기 바랍니다 [계산된 열 유형 안내서](../../data-analyst/data-warehouse-mgr/calc-column-types.md). 다음 _계산된 열 유형 안내서_ 정의 및 예와 함께 Data Warehouse 관리자에서 만들 수 있는 열 유형에 대해 설명합니다.

1. 시작하려면 **[!DNL Manage Data > Data Warehouse]** 을 클릭합니다.

1. 에서 열을 만들 테이블을 클릭합니다. 예를 들어 `Customer Gender` 수입 세분화를 위해 열 중에서 `sales_flat_order` 테이블.

1. 테이블 구성표가 표시됩니다. 클릭 **[!UICONTROL Create New Column]**.

1. 열에 이름을 지정합니다(예: ). `Customer Gender`.

1. 열에 대한 정의를 선택합니다. 여기에서 [계산된 열 유형 안내서](../data-warehouse-mgr/calc-column-types.md) 도움이 될 거야!

1. 특정 유형의 열의 경우, 열을 올바르게 만들려면 몇 가지 추가 정보가 필요합니다.
   * 대상 `One to Many` (연결됨) 및 `Many to One` (합계) 열에서 테이블과 열을 선택해야 합니다.
   * 대상 `Same Table calculation`: 드롭다운에서 원하는 날짜 필드를 선택해야 합니다.

다음을 만드는 경우 `One to Many` (가입) 또는 `Many to One` (합계) 열에서 두 테이블을 연결하는 경로를 선택해야 합니다. 이 단계에서는 기존 경로를 사용하거나 새 경로를 만들 수 있습니다.

>[!NOTE]
>
>테이블을 하나 또는 여러 개로 적절히 정의해야 합니다.

* 원하는 경우 적용할 수 있습니다 [필터](../../data-user/reports/ess-manage-data-filters.md) 새 열에 추가합니다.
* 완료되면 를 클릭합니다 **[!UICONTROL Save]**.

바로 그거야! 새 열이 현재 테이블에 `Pending` 상태. 다음 업데이트가 완료되면 지표 및 보고서에서 열을 사용할 수 있습니다.

## 편리한 참조 맵 {#map}

계산된 열을 만들 때 모든 입력을 기억하는 데 약간 문제가 있다면 다음 참조 맵을 빌드할 때 바로 보관해 보십시오.

![](../../assets/Calculated_Columns_Example.png)

## 관련 설명서

* [계산된 열 유형](../data-warehouse-mgr/calc-column-types.md)
* [고급 계산 열 유형](../data-warehouse-mgr/adv-calc-columns.md)
* [빌딩 [!DNL Google ECommerce] 주문 및 고객 데이터를 사용한 차원](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
