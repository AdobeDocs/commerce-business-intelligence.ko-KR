---
title: 투자자를 위한 대시보드 만들기
description: 투자자를 위한 대시보드를 만드는 방법을 알아봅니다.
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# 투자자 대시보드 작성

대부분의 Adobe 클라이언트는 투자자와 협력하고 있으며 플랫폼과 정보를 공유해야 하지만 일상적인 비즈니스 의사 결정을 위해 만드는 대시보드는 투자자가 찾는 것이 아닐 수 있습니다. 여기에서는 포괄적이지만 간단하며 활성 및 잠재적 투자자와 공유하는 데 이상적인 대시보드를 만드는 방법에 대한 몇 가지 모범 사례를 다룹니다.

다음은 투자자 대시보드에 대한 보고서를 만드는 데 필요한 사항입니다.

## 스칼라 보고서

* **[!UICONTROL All-time revenue]**
* **[!UICONTROL Distinct buyers]**
* **[!UICONTROL All-time number of orders]**
* **[!UICONTROL AOV]**
* **[!UICONTROL Items sold]**

## 시각적 보고서

* **[!UICONTROL Revenue by quarter]**
   * 지표 - 매출
* **[!UICONTROL Revenue from 1st time orders vs repeat orders]**
   * 지표 - 최초 주문 매출
   * 필터 - 사용자의 주문 번호가 1입니다.
   * 지표 2 - 반복 주문 매출
      * 필터 - 사용자의 주문 번호가 1보다 큼
   * 여러 Y축에 대한 상자의 선택을 취소합니다
   * 누적 열 차트로 변경
* **[!UICONTROL AOV by quarter]**
   * 지표 1 - 매출
      * 이 지표 숨기기
   * 지표 2 - 주문 수
      * 이 지표 숨기기
   * 공식 - AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * 지표 - 매출
   * 고객별로 그룹화 `utm_source`
* **[!UICONTROL Revenue from top 10 products]**
   * 지표 - 제품 매출
      * 차트 숨기기
      * 제품 이름별로 그룹화합니다. 모든 제품을 선택합니다.
      * 시간 범위를 모두 시간으로 설정
      * 시간 간격을 없음 로 설정합니다.
      * &quot;상위/하위 표시&quot;에서 제품 수익별로 정렬된 상위 10개만 표시합니다
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * 지표 - 개별 구매자
      * 원근 - 누적
* **[!UICONTROL Site visits - New vs. repeat by month]**
* 세션

다음 포함 [!DNL Google Analytics] 통합에는 다음과 같은 보고서가 포함됩니다.

* 사이트 방문 횟수
* 전환율

사용 [상거래 데이터 보강 서비스](https://business.adobe.com/products/magento/magento-commerce.html), 다음에 대한 보고서를 포함할 수 있습니다.

* 주/지역, 연령, 성별 고유 고객

## 기타 팁

* 명확하고 간결한 사용 [명명 규칙](../best-practices/naming-elements.md)
* 투자자 사용자와 대시보드 공유
* 또는 를 통해 전송 **[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)
* 대시보드를 하나만 만듭니다. 이를 통해 컨텐츠를 보다 쉽게 유지 관리할 수 있으며, 투자자가 어떤 내용을 보고 있는지 정확하게 파악할 수 있습니다.

보고서를 신중하게 구성하고 세부 사항에 주의하십시오. 완료되면 대시보드는 다음과 비슷합니다.

![](../../mbi/assets/investor-dboard-example.png)
