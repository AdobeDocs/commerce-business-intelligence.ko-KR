---
title: 지표에 대한 필터 세트 만들기
description: 저장된 필터 세트를 만들고 지표에 적용하는 방법을 알아봅니다.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# 필터 세트 만들기

에 여러 지표가 있는 경우 [!DNL MBI] 유사한 방식으로 필터링해야 하는 경우(예: 테스트 주문 필터링), 저장된 필터 세트를 만들어 지표에 적용할 수 있습니다. 따라서 지표를 만들거나 편집할 때 개별 필터를 추가할 필요가 없으므로 시간을 절약할 수 있습니다.

다음 문서를 참조하십시오 [교육 비디오](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html?lang=en) 추가 정보

>[!NOTE]
>
>필요한 경우 [관리자 권한](../../administrator/user-management/user-management.md).

1. 클릭 **[!DNL Manage Data** > **Filter Sets]** 을 클릭합니다.

   ![](../../assets/create-filter-sets.png)

1. 클릭 **[!UICONTROL Add Filter Set]** 를 클릭합니다.

1. 필터링할 지표가 포함된 테이블을 선택합니다.

   예를 들어 `Total number of orders` 지표 및 기본 `orders` 테이블에서 해당 테이블을 선택합니다.

1. 이름을 로 지정합니다 `Filter Set`.

1. 모든 관련 필터를 추가합니다.

   예를 들어, 완료 상태인 주문만 포함하려면 `Total number of orders` 지표, 상태가 없는 모든 주문을 제외하는 필터를 적용했습니다 = `complete`.

1. 필터 논리를 확인하고 괄호와 연산자가 올바르게 배치되었는지 확인합니다. 예 `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   필터가 올바르지 않으면 종종 데이터 불일치가 발생합니다 [!DNL MBI] 보고서 및 예상 결과.

1. 를 저장합니다 `Filter Set`.

필터 세트가 저장되면 동일한 테이블을 사용하는 모든 지표에 적용할 수 있습니다. 예를 들어 `Filter Set` on `orders` 테이블 위에 적용할 수 있습니다. *모든 지표* 이 표에 작성(예: ) `Revenue`.

>[!NOTE]
>
>`Filter Sets` 의 계산된 열에 적용할 수도 있습니다. [!DNL MBI]. 에서 만든 데이터 차원에 필터 세트를 적용하도록 요청할 수 있습니다 [!DNL MBI] 지원 센터에 연락하여 을 참조하십시오.

## 관련

* [세그먼테이션 및 필터링 우수 사례](../../best-practices/segment-filter.md)
