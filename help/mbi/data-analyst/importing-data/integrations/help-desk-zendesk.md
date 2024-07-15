---
title: Zendesk용 헬프 데스크 보고
description: 가장 소중한 레퍼러 채널에 대해 알아봅니다.
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# [!DNL Zendesk]에 대한 안내 데스크 보고

>[!NOTE]
>
>`Pro` 플랜에 있으며 새 아키텍처를 사용하는 클라이언트에만 사용할 수 있습니다. 기본 도구 모음에서 `Manage Data`을(를) 선택한 후 `Data Warehouse Views` 섹션을 사용할 수 있는 경우 새 아키텍처를 사용합니다.

트랜잭션 데이터베이스에 [!DNL Zendesk] 데이터를 통합하면 고객이 영업 팀 또는 고객 성공 팀과 상호 작용하는 방식을 더 잘 이해할 수 있습니다. 또한 지원 플랫폼을 사용하는 고객 유형을 파악하는 데 도움이 됩니다. 이 항목에서는 대시보드를 설정하여 [!DNL Zendesk] 성능 및 트랜잭션 고객의 관계에 대한 세부 보고서를 얻는 방법을 보여 줍니다.

시작하기 전에 [[!DNL Zendesk]](../integrations/zendesk.md)에 연결해야 합니다. 이 분석에는 [고급 계산 열](../../data-warehouse-mgr/adv-calc-columns.md)이(가) 포함되어 있습니다.

<!-- Getting Started -->

## 시작

### 추적할 열

* `audits` 테이블
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` 테이블
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` 테이블
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` 테이블
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### 생성할 필터 세트

* `[!DNL Zendesk] Tickets` 테이블
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## 계산된 열

### 생성할 열

* **`[!DNL Zendesk] user's`** 테이블
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `null` and `A!=`end-user` then `Yes` when `B`이(가) `null`이(가) 아닌 경우 `B` like `%@magento.com` then `Yes` else `No` end

      * `@magento.com`을(를) 도메인으로 바꾸기

      * `Datatype` - `String`

* **`[!DNL Zendesk] audits_~_events`** 테이블
   * 정의 선택: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * [!UICONTROL table] 선택: `[!DNL Zendesk] users`
   * [!UICONTROL column] 선택: `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[!DNL Zendesk] audits`** 테이블
   * 정의 선택: `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[!DNL Zendesk] audits._id`

   * [!UICONTROL table] 선택: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * 정의 선택: `Exists`
   * [!UICONTROL table] 선택: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[!DNL Zendesk] Tickets`** 테이블
   * 정의 선택: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * [!UICONTROL table] 선택: `[!DNL Zendesk] users`
   * [!UICONTROL column] 선택: `email`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 정의 선택: `Joined Column`
   * [!UICONTROL table] 선택: `[!DNL Zendesk] users`
   * [!UICONTROL column] 선택: `role`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 정의 선택: `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[!DNL Zendesk] tickets.id`

   * [!UICONTROL table] 선택: `[!DNL Zendesk] audits`
   * [!UICONTROL column] 선택: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status`이(가) `solved = 1`(으)로 변경됨

   * 정의 선택: `Min`
   * [!UICONTROL table] 선택: `[!DNL Zendesk] audits`
   * [!UICONTROL column] 선택: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * 
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` - `created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` - `created_at`

* **`Requester's ticket number`**
   * 
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * 
      * `Column type` - &quot;같은 테이블 > 계산&quot;

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype` - 정수

* **`Ticket created_at (day of week)`**
   * 
      * `Column type` - &quot;같은 테이블 > 계산&quot;

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

     *`Datatype` - `String`

* **`customer_entity`** 테이블
   * 정의 선택: `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.email`
   * 
     [!UICONTROL One]: `customer_entity.email`

   * [!UICONTROL table] 선택: `[!DNL Zendesk] tickets`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type` - &quot;같은 테이블 > 계산&quot;

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` - `String`

* **`[!DNL Zendesk] Tickets`** 테이블
   * 정의 선택: `Joined Column`
   * [!UICONTROL table] 선택: `customer_entity`
   * [!UICONTROL column] 선택: `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## 지표

* 새 티켓 **[!DNL Zendesk]개**
   * `Tickets we count`

* **`[!DNL Zendesk] tickets`** 테이블에서
* 이 지표는 **Count**&#x200B;을 수행합니다.
* **`id`** 열에서
* **`created_at`** 타임스탬프로 정렬됨
* [!UICONTROL Filter]:

* 해결된 티켓 **[!DNL Zendesk]개**
   * `Tickets we count`
   * `closed, solved`의 상태

* **`[!DNL Zendesk] tickets`** 테이블에서
* 이 지표는 **Count**&#x200B;을 수행합니다.
* **`id`** 열에서
* **`created_at`** 타임스탬프로 정렬됨
* [!UICONTROL Filter]:

* **[!DNL Zendesk]명의 고유 사용자가 티켓을 정리함**
   * `Tickets we count`

* **`[!DNL Zendesk] tickets`** 테이블에서
* 이 지표는 **고유 개수**&#x200B;를 수행합니다.
* **`requester_id`** 열에서
* **`created_at`** 타임스탬프로 정렬됨
* [!UICONTROL Filter]:

* **[!DNL Zendesk]평균/중간 티켓 확인 시간**
   * `Tickets we count`
   * `closed, solved`의 상태

* **`[!DNL Zendesk] tickets`** 테이블에서
* 이 지표는 **평균(또는 중간값)**&#x200B;을 수행합니다.
* **`Seconds to resolution`** 열에서
* **`created_at`** 타임스탬프로 정렬됨
* [!UICONTROL Filter]:

* **[!DNL Zendesk]첫 번째 응답까지의 평균/중간 시간**
   * 카운트되는 티켓
   * 상태 IN 닫힘, 해결됨

* **`[!DNL Zendesk] tickets`** 테이블에서
* 이 지표는 **평균(또는 중간값)**&#x200B;을 수행합니다.
* **`Seconds to first response`** 열에서
* **`created_at`** 타임스탬프로 정렬됨
* [!UICONTROL Filter]:

>[!NOTE]
>
>새 보고서를 작성하기 전에 [모든 새 열을 지표에 차원으로 추가](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md)하십시오.

### 보고서

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * `new, open, pending`의 상태

* 지표 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * `solved, closed`의 상태

* 지표 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* 지표 `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * `solved, closed`의 상태

* 지표 `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric]: `New Tickets`

* 지표 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `status`
* `Chart Type`: `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`

   * [!UICONTROL Metric]: `New Tickets`

* 지표 `A`: `New tickets`
* 지표 `B`: `Solved tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* 지표 `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * `solved, closed`의 상태

* 지표 `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric]: `Distinct users filing tickets`

* 지표 `A`: `Distinct users filing tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric]: `New Tickets`

* 지표 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (day of week)`
* `Chart Type`: `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]:`New Tickets`

   * `Show top/bottom`: `Top 100% sorted by created_at (hour of the day)`

* 지표 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (hour of the day)`
* `Chart Type`: `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 지표 `A`: `Average lifetime revenue`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * 
     [!UICONTROL 지표]: Users

* 지표 `A`: `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
