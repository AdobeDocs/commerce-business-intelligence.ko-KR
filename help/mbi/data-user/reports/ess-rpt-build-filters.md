---
title: 필터
description: 필터를 사용하는 방법을 알아봅니다.
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 0854d644cb72b3fc8b8b31a0bf7e8dca4cc99724
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# 필터

보고서 제작에 사용되는 데이터를 제한하기 위해 하나 이상의 필터를 추가할 수 있습니다. 각 필터는 연관된 테이블의 열, 연산자 및 값을 포함하는 표현식입니다. 예를 들어 반복 고객만 포함하려면 두 개 이상의 주문을 한 고객만 포함하는 필터를 만들 수 있습니다. 여러 필터를 논리 `AND/OR` 연산자와 함께 사용하여 보고서에 논리를 추가할 수 있습니다.

>[!TIP]
>
>보고서에는 최대 3,500개의 데이터 포인트가 포함될 수 있습니다. 데이터 포인트 수를 줄이려면 필터를 사용하여 보고서를 생성하는 데 사용되는 데이터의 양을 줄이십시오.

[!DNL Adobe Commerce Intelligence]에는 &quot;즉시 사용 가능한(OOTB)&quot;을 사용하거나 필요에 맞게 수정할 수 있는 다양한 필터가 포함되어 있습니다. 만들 수 있는 필터 수에는 제한이 없습니다.

## 필터를 추가하려면 다음 작업을 수행하십시오.

1. 차트에서 각 데이터 포인트 위로 마우스를 가져갑니다.

   이 보고서에서 각 데이터 포인트는 해당 월의 총 고객 수를 보여 줍니다.

1. 왼쪽 패널에서 필터(![](../../assets/magento-bi-btn-filter.png)) 아이콘을 클릭합니다.

   ![필터 추가](../../assets/magento-bi-report-builder-filter-add.png)

1. **[!UICONTROL Add Filter]**&#x200B;을(를) 클릭합니다.

   필터는 알파벳순으로 번호가 매겨져 있으며 첫 번째는 `[A]`입니다. 필터의 처음 두 부분은 드롭다운 옵션이고 세 번째 부분은 값입니다.

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * 필터의 첫 번째 부분을 클릭하고 표현식의 주제로 사용할 열을 선택합니다.

     ![필터의 첫 번째 부분 선택](../../assets/magento-bi-report-builder-filter-part1.png)

   * 필터의 두 번째 부분을 클릭하고 연산자를 선택합니다.

     ![연산자 선택](../../assets/magento-bi-report-builder-filter-part2.png)

   * 필터의 세 번째 부분에서 표현식을 완료하는 데 필요한 값을 입력합니다.

     ![값 입력](../../assets/magento-bi-report-builder-filter-part3.png)

   * 필터가 완료되면 **[!UICONTROL Apply]**&#x200B;을(를) 클릭합니다.

     이제 보고서에는 반복 고객만 포함되며, 보고서에 대해 검색된 고객 레코드 수가 33,000개에서 12,600개로 감소했습니다.

     ![필터링된 보고서](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. 사이드바에서 원근(![원근 아이콘](../../assets/magento-bi-btn-perspective.png)) 아이콘을 클릭합니다.

   ![관점](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. 설정 목록에서 `Cumulative`을(를) 선택합니다. **[!UICONTROL Apply]**&#x200B;을(를) 클릭합니다.

   ![누적 관점](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   `Cumulative` 큐브 뷰에서는 매월 들쭉날쭉한 위아래로 표시되지 않고 시간에 따라 변경 내용을 배포합니다.

1. 보고서에 대한 `Title`을(를) 입력하고 대시보드에 대한 `Chart`(으)로 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

   ![대시보드에 저장](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
