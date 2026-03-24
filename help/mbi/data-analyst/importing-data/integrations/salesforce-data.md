---
title: 예상 Salesforce 데이터
description: Salesforce 데이터에서 지원되는 오브젝트 및 지원되지 않는 오브젝트에 대해 알아봅니다.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/eBX3Y0luu60A8PSAF43H6O3fsYjJnSWzyIybSOcSELE
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 117
ht-degree: 0%

---

# [!DNL Salesforce]개의 데이터가 필요합니다.

[[!DNL Salesforce] 설정](../integrations/salesforce.md)이 완료되면 각 쿼리 가능한 [개체](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm)&#x200B;(이름 `sf_/\{sobject-name}`)에 대한 테이블이 Data Warehouse에 만들어집니다.

>[!NOTE]
>
>각 테이블의 구조(열)는 객체에 포함된 필드에 따라 다릅니다.

조직에서 사용할 수 있는 개체 목록을 가져오려면 [!DNL Salesforce] [개체 목록 가져오기](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm)를 참조하십시오. 개체 목록이 있으면 [ 설명서의 ](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm)ERD(Entity Relationship Diagram) 섹션[!DNL Salesforce]을 확인하여 엔터티가 서로 관련되는 방식을 확인하십시오.

## 지원되지 않는 개체

현재 [!DNL Salesforce]은(는) API에 다음 개체를 표시하지 않습니다.

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [외부 개체란?](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
* `CollaborationGroupRecord`
* `ContentDocument`
* `ContentDocumentLink`
* `FeedItem`
* `FieldDefinition`
* `IdeaComment`
* `ListViewChartInstance`
* `Order`
* `PlatformAction`

* `KnowledgeArticleVersion`
* `NewsFeed`
* `RecentlyViewed`
* `TopicAssignment`
* `UserRecordAccess`
* `UserProfileFeed`
* `Vote`

## 관련 항목:

* [ [!DNL Salesforce] 연결 중](../integrations/salesforce.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
