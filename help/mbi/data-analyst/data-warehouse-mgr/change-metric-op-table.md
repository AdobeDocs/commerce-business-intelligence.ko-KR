---
title: 지표의 작업 테이블 변경
description: 지표가 작업을 수행하는 데 사용하는 데이터 테이블을 변경하는 방법을 알아봅니다.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 지표의 작업 테이블 변경

특정 경우에 지표가 작업을 수행하는 데 사용하는 데이터 테이블을 변경하도록 결정할 수 있습니다. 예를 들어 새 사용자 테이블이 있는 경우 `Users\_Old` 테이블에서 사용자 관련 지표를 마이그레이션하여 `Users\_New` 테이블을 대신 사용할 수 있습니다.

1. **[!UICONTROL Data]** > **[!UICONTROL Metrics]**(으)로 이동
1. **[!UICONTROL Edit]** 테이블을 전환할 지표 옆의 `operational`을(를) 클릭합니다.
1. 편집기에서 **[!UICONTROL Change]**&#x200B;을(를) 클릭합니다.

   ![작동 테이블 설정을 표시하는 지표 정의 페이지](../../assets/change-metrics-1.png)
1. 이 지표의 기반으로 사용할 새 테이블을 선택합니다.
1. 기존 데이터 차원을 새 테이블의 해당 차원과 일치시킵니다. 예를 들어, 이름이 `User's registration date`인 열이 있는 경우 새 테이블에서 동일한 날짜 데이터를 기록하는 열을 선택하면 됩니다. (새 테이블에 일치하는 열이 없는 경우 다음 단계 참조)

   ![사용 가능한 테이블을 표시하는 테이블 선택 드롭다운](../../assets/change-metrics-2.png)

1. 새 테이블에 일치하는 열이 없는 경우 **데이터 테이블에서 만들거나** [에서 만든 계산 열 또는 차원인 경우 &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ko)지원 팀에 문의[!DNL Commerce Intelligence]할 수 있습니다. **지표에서 차원을 삭제**&#x200B;할 수도 있습니다. 더 이상 필요하지 않은 차원을 삭제하려면 지표 편집기로 돌아가 `Dimensions`에서 삭제할 차원을 선택하면 됩니다.

   ![작동 열 선택 드롭다운 메뉴](../../assets/change-metrics-3.png)
