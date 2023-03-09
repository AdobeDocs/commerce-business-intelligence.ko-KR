---
title: 투자자를 위한 대시보드 구축
description: 투자자를 위한 대시보드를 작성하는 방법에 대해 알아봅니다.
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# 투자자 대시보드 작성

많은 고객이 투자자와 협력하고 플랫폼에서 정보를 공유해야 하지만 일상적인 비즈니스 결정을 내리기 위해 생성하는 대시보드는 투자자가 찾고 있는 것이 아닐 수 있습니다. 아래에서는 포괄적이지만 단순하며 활성 투자자와 공유할 때 이상적인 대시보드를 만드는 방법에 대한 몇 가지 모범 사례에 대해 설명합니다.

투자자 대시보드에 대한 보고서를 만드는 데 필요한 사항은 다음과 같습니다.

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
   * 필터 - 사용자의 주문 번호가 1과 같음
   * 지표 2 - 반복 주문 매출
      * 필터 - 사용자의 주문 번호가 1보다 큼
   * 다중 Y축 확인란을 선택 취소합니다
   * 누적 세로 막대형 차트로 변경
* **[!UICONTROL AOV by quarter]**
   * 지표 1 - 매출
      * 이 지표 숨기기
   * 지표 2 - 주문 수
      * 이 지표 숨기기
   * 공식 - AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * 지표 - 매출
   * 고객별 그룹화 `utm_source`
* **[!UICONTROL Revenue from top 10 products]**
   * 지표 - 제품 매출
      * 차트 숨기기
      * 제품 이름별로 그룹화합니다. 모든 제품을 선택합니다.
      * 시간 범위를 All-Time으로 설정
      * 시간 간격을 없음으로 설정
      * &quot;위쪽/아래쪽 표시&quot;에서 제품 수익별로 정렬된 상위 10만 표시합니다.
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * 지표 - 개별 구매자
      * 관점 - 누적
* **[!UICONTROL Site visits - New vs. repeat by month]**
* 세션

포함 [!DNL Google Analytics] 통합하면 다음에 대한 보고서를 포함할 수 있습니다.

* 사이트 방문 횟수
* 전환율

포함 [상거래 데이터 보강 서비스](https://business.adobe.com/products/magento/magento-commerce.html), 다음에 대한 보고서를 포함할 수 있습니다.

* 주/지역, 연령, 성별 고유 고객.

## 기타 팁

* 명확하고 간결하게 사용하기 [명명 규칙](../best-practices/naming-elements.md)
* 투자자 사용자와 대시보드 공유
* 또는 를 통해 전송 **[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)
* 대시보드를 하나만 만듭니다. 이렇게 하면 콘텐츠를 유지 관리하기 쉬워지며 투자자가 보고 있는 내용을 정확하게 알 수 있습니다.

보고서를 신중하게 구성하고 세부 사항에 주의하십시오. 완료되면 대시보드는 다음과 유사합니다.

![](../../mbi/assets/investor-dboard-example.png)
