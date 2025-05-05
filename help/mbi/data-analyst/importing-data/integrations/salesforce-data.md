---
title: 예상 Salesforce 데이터
description: Salesforce 데이터의 지원되는 개체 및 지원되지 않는 개체에 대해 알아봅니다.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# [!DNL Salesforce]개의 데이터가 필요합니다.

[[!DNL Salesforce] 설치](../integrations/salesforce.md)이(가) 완료되면 Data Warehouse에 쿼리할 수 있는 각 [개체](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm)(이름 `sf_/\{sobject-name}`)에 대한 테이블이 만들어집니다.

>[!NOTE]
>
>각 테이블의 구조(열)는 객체에 포함된 필드에 따라 다릅니다.

조직에서 사용할 수 있는 개체 목록을 가져오려면 [!DNL Salesforce] [개체 목록 가져오기](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm)를 참조하십시오. 개체 목록이 있으면 [!DNL Salesforce] 설명서의 [ERD(Entity Relationship Diagram) 섹션](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm)을 확인하여 엔터티가 서로 관련되는 방식을 확인하십시오.

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
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ko)
