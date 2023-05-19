---
title: 예상 Salesforce 데이터
description: Salesforce 데이터의 지원되는 개체 및 지원되지 않는 개체에 대해 알아봅니다.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# 예상 [!DNL Salesforce] 데이터

다음 이후 [[!DNL Salesforce] 설정](../integrations/salesforce.md) 은(는) 완료 상태이며, 각 쿼리 가능 테이블에 대한 테이블입니다. [오브젝트](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) - 명명된 항목 `sf_/\{sobject-name}` - 은(는) Data Warehouse에서 만들어집니다.

>[!NOTE]
>
>각 테이블의 구조(열)는 객체에 포함된 필드에 따라 다릅니다.

조직에서 사용할 수 있는 객체 목록을 얻으려면 다음을 참조하십시오. [!DNL Salesforce] [개체 목록 가져오기 설명서](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). 개체 목록이 있으면 [ERD(엔티티 관계 다이어그램) 섹션](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) / [!DNL Salesforce] 엔티티가 서로 관련되는 방식을 확인할 수 있는 문서.

## 지원되지 않는 개체

현재, [!DNL Salesforce] 는 현재 API에 다음 개체를 표시하지 않습니다.

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [외부 객체란?](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
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

* [연결 중 [!DNL Salesforce]](../integrations/salesforce.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
