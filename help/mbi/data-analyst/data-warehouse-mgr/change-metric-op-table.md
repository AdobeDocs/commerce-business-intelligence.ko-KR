---
title: 지표의 작업 테이블 변경
description: 지표가 작업을 수행하는 데 사용하는 데이터 테이블을 변경하는 방법을 알아봅니다.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/9yJ1Zc2NLDvXYO16UvDkeWE0hD1jx0-Ne3AyFFHX5ns
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 231
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

1. 새 테이블에 일치하는 열이 없는 경우 **데이터 테이블에서 만들거나** [에서 만든 계산 열 또는 차원인 경우 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)지원 팀에 문의[!DNL Commerce Intelligence]할 수 있습니다. **지표에서 차원을 삭제**&#x200B;할 수도 있습니다. 더 이상 필요하지 않은 차원을 삭제하려면 지표 편집기로 돌아가 `Dimensions`에서 삭제할 차원을 선택하면 됩니다.

   ![작동 열 선택 드롭다운 메뉴](../../assets/change-metrics-3.png)
