---
title: Salesforce 데이터가 필요합니다.
description: Salesforce 데이터에서 지원 및 지원되지 않는 개체에 대해 알아봅니다.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 예상됨 [!DNL Salesforce] 데이터

[다음 이후 [!DNL Salesforce] 설치가 완료되었습니다.](../integrations/salesforce.md), 각 쿼리 가능 테이블 [개체](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_concepts.htm) - 이름이 지정됨 `sf_/\{sobject-name}` - 는 data warehouse에서 만들어집니다.

>[!NOTE]
>
>각 테이블의 구조(열)는 객체에 포함된 필드에 따라 달라집니다.

조직에서 사용할 수 있는 객체 목록을 보려면 [!DNL Salesforce] [개체 목록 설명서 가져오기](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). 개체 목록이 있으면 [엔티티 관계 다이어그램(ERD) 섹션](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) 의 [!DNL Salesforce] 엔티티가 서로 어떻게 관련되는지를 확인하는 설명서입니다.

## 지원되지 않는 개체

지금, [!DNL Salesforce] 는 현재 API에 다음 개체를 표시하지 않습니다.

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [외부 객체란?](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_external_objects.htm)
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

## 관련:

* [연결 중 [!DNL Salesforce]](../integrations/salesforce.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
