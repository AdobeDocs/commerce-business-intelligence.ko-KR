---
title: 지표에 대한 목표 추적
description: 매출, 신규 등록 사용자, 시간 경과에 따른 주문 등 실제 데이터에 대해 비즈니스 목표를 추적하는 데 도움이 되는 대시보드를 설정하는 방법에 대해 알아봅니다.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# 성능 지표에 대한 목표 추적

대부분의 클라이언트가 **비즈니스 목표**&#x200B;를 추적하려고 하지만, [!DNL Adobe Commerce Intelligence]에서 이 작업이 가능하다는 것을 알지 못합니다. 이 항목에서는 매출, 새로 등록된 사용자 및 시간에 따른 주문을 포함하여 실제 데이터에 대해 비즈니스 목표를 추적하는 데 도움이 되는 대시보드를 설정하는 방법을 보여 줍니다. 또한 다음과 같은 대시보드에서 연도별 성과를 비교하는 방법을 배웁니다.

![](../../assets/Goals-_dashboard_2.png)

시작하기 전에 [파일 업로더](../importing-data/connecting-data/using-file-uploader.md)를 검토하여 지정된 기간 동안 비즈니스 목표를 정의했는지 확인해야 합니다.

## 시작

먼저 비즈니스에 대한 특정 일별/월별/분기별 타겟이 포함된 파일을 업로드해야 합니다.

[파일 업로더](../importing-data/connecting-data/using-file-uploader.md) 및 아래 이미지를 사용하여 파일 형식을 지정할 수 있습니다. [!DNL Commerce Intelligence]에서 클라이언트가 추적하는 가장 일반적인 대상에는 주문, 매출 및 새로 등록된 계정이 있습니다.

![](../../assets/Goals-_Excel.png)

## 지표

각 대상에 대해 하나의 새 지표를 만듭니다. 예를 들어 월별 매출 및 주문 목표를 업로드하는 경우 두 개의 새 지표를 생성해야 합니다.

* **월별 수익 목표**
* **`Monthly goals`** 테이블에서
* 이 지표는 **합계**&#x200B;를 수행합니다.
* **`Revenue target`** 열에서
* **`Month`** 타임스탬프로 정렬됨

* **월별 주문 대상**
* **`Monthly goals`** 테이블에서
* 이 지표는 **합계**&#x200B;를 수행합니다.
* **`Orders target`** 열에서
* **`Month`** 타임스탬프로 정렬됨

* **월별 새로 등록된 계정 대상**
* **`Monthly goals`** 테이블에서
* 이 지표는 **합계**&#x200B;를 수행합니다.
* **`New registered accounts target`** 열에서
* **`Month`** 타임스탬프로 정렬됨

## 보고서

타겟을 분석할 때 정적 값과 시각적 차트를 혼합하는 것이 유용합니다. 다음은 매출 성과 추적을 시작하는 세 가지 예제 보고서입니다.

* **목표를 달성하는 데 남은 수익**
* 지표 `A`: `Revenue`
* 
  [!UICONTROL 지표]: `Revenue`

* 지표 `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* 
  [!UICONTROL 공식]: `(B-A)`
* 
  [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]: (원하는 적절한 기간)
* 
  [!UICONTROL Interval]: `Month`
* 
  [!UICONTROL 차트 유형]: `Scalar`

* **매출 목표**
* 지표 `A`: `Revenue`
* 
  [!UICONTROL 지표]: `Revenue`

* 지표 `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* 지표 `C`: `Revenue (amount change since previous year)`(숨기기)
* 
  [!UICONTROL 지표]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]: (작년 이번 달)
* 
  [!UICONTROL 공식]: `(A-C)`
* 
  [!UICONTROL Format]: `Currency`

* `Multiple Y-Axes` 끄기
* [!UICONTROL Time period]: (원하는 적절한 기간)*
* 
  [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

매출 목표에 대한 위의 보고서를 완료하면 주문, 등록된 계정 또는 목표 파일 업로드에 포함한 다른 모든 값에 대한 동일한 보고서를 생성할 수 있습니다.

모든 보고서를 컴파일한 후 원하는 대로 대시보드에서 구성할 수 있습니다. 결과는 이 페이지 상단에 있는 이미지와 비슷할 수 있습니다.
