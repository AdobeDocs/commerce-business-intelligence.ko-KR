---
title: 지표의 작업 테이블 변경
description: 지표가 작업을 수행하는 데 사용하는 데이터 테이블을 변경하는 방법을 알아봅니다.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 지표의 작업 테이블 변경

특정 경우에 지표가 작업을 수행하는 데 사용하는 데이터 테이블을 변경하도록 결정할 수 있습니다. 예를 들어 새 사용자 테이블이 있는 경우  `Users\_Old` 사용할 표 `Users\_New` 대신 테이블을 사용하십시오.

1. 다음으로 이동 **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. 클릭 **[!UICONTROL Edit]** 을(를) 전환하려는 지표 옆에 있는 `operational` 테이블.
1. 편집기에서 **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. 이 지표의 기반으로 사용할 새 테이블을 선택합니다.
1. 기존 데이터 차원을 새 테이블의 해당 차원과 일치시킵니다. 예를 들어 라는 열이 있는 경우 `User's registration date`새 테이블에서 동일한 날짜 데이터를 기록하는 열을 선택하면 됩니다. (새 테이블에 일치하는 열이 없는 경우 다음 단계 참조)

   ![](../../assets/change-metrics-2.png)

1. 새 테이블에 일치하는 열이 없는 경우 다음 중 하나를 수행할 수 있습니다 **데이터 테이블에서 생성** 또는 [연락처 지원](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 다음을 통해 만들어진 계산 열 또는 차원인 경우 [!DNL Commerce Intelligence]. 다음을 수행할 수도 있습니다. **지표에서 차원 삭제**. 더 이상 필요하지 않은 차원을 삭제하려면 지표 편집기로 돌아가 아래에서 삭제할 차원을 선택하면 됩니다 `Dimensions`.

   ![](../../assets/change-metrics-3.png)
