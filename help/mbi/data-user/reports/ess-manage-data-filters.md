---
title: 지표에 대한 필터 세트 만들기
description: 저장된 필터 세트를 만들고 이를 지표에 적용하는 방법을 알아봅니다.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 필터 세트 만들기

에 여러 지표가 있는 경우 [!DNL Commerce Intelligence] 유사한 방식으로 필터링해야 하는 경우(예: 테스트 주문 필터링), 저장된 필터 세트를 생성하고 지표에 적용할 수 있습니다. 이렇게 하면 지표를 만들거나 편집할 때 개별 필터를 추가할 필요가 없어 시간을 절약할 수 있습니다.

다음을 참조하십시오. [교육 비디오](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html) 추가 정보.

>[!NOTE]
>
>필요 [관리자 권한](../../administrator/user-management/user-management.md).

1. 클릭 **[!DNL Manage Data** > **Filter Sets]** 를 클릭합니다.

   ![](../../assets/create-filter-sets.png)

1. 클릭 **[!UICONTROL Add Filter Set]** 을 클릭합니다.

1. 필터링할 지표가 포함된 테이블을 선택합니다.

   예를 들어 을(를) 필터링하려면 `Total number of orders` 지표를 기반으로 하며 `orders` 테이블, 해당 테이블을 선택합니다.

1. 이름 지정 `Filter Set`.

1. 모든 관련 필터를 추가합니다.

   예를 들어 완료 상태의 주문만 포함하려는 경우 `Total number of orders` 지표, 상태가 = 인 모든 주문을 제외하는 필터를 적용합니다. `complete`.

1. 필터 논리를 확인하고 괄호와 연산자가 올바르게 입력되었는지 확인합니다. 예: `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   잘못된 필터는 종종 간의 데이터 불일치의 원인입니다. [!DNL Commerce Intelligence] 보고서 및 예상 결과.

1. 저장 `Filter Set`.

필터 세트가 저장되면 동일한 테이블을 사용하는 모든 지표에 적용할 수 있습니다. 예를 들어 `Filter Set` 다음에 있음 `orders` 테이블, 다음에 적용할 수 있습니다. *모든 지표* 이 표에 만들어짐: `Revenue`.

>[!NOTE]
>
>`Filter Sets` 의 계산된 열에도 적용할 수 있습니다. [!DNL Commerce Intelligence]. 에서 만든 데이터 차원에 필터 세트를 적용하도록 요청할 수 있습니다. [!DNL Commerce Intelligence] 를 통해 고객 지원에 문의합니다.

## 관련 항목

* [세분화 및 필터링 우수 사례](../../best-practices/segment-filter.md)
