---
title: Zendesk에 대한 안내 데스크
description: 가장 가치 있는 참조 채널에 대해 알아봅니다.
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# 지원 센터 보고 [!DNL Zendesk]

>[!NOTE]
>
>이 기능은 `Pro` 새로운 아키텍처를 계획하고 사용합니다. 다음 단계에 있습니다. [새로운 아키텍처](https://support.magento.com/hc/en-us/articles/360016503052-New-Architecture-FAQ) 만약 `Data Warehouse Views` 선택 후 사용 가능한 섹션 `Manage Data` 기본 도구 모음에서 를 클릭합니다.

통합 [!DNL Zendesk] 트랜잭션 데이터베이스를 사용한 데이터는 고객이 영업 또는 고객 성공 팀과 상호 작용하는 방식과 지원 플랫폼을 활용하는 고객 유형을 보다 잘 이해할 수 있는 좋은 방법입니다. 이 문서에서는 사용자 관련 세부 보고서를 얻기 위해 대시보드를 설정하는 방법을 보여줍니다 [!DNL Zendesk] 트랜잭션 고객의 성능 및 연결

시작하기 전에 [[!DNL Zendesk]](../integrations/zendesk.md). 이 분석에는 다음이 포함됩니다 [고급 계산 열](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## 시작하기

### 추적할 열

* `audits` 표
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` 표
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` 표
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` 표
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### 만들 필터 세트

* `[!DNL Zendesk] Tickets` 표
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## 계산된 열

### 만들 열

* **`[!DNL Zendesk] user's`** 표
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `null` and `A!=`end-user` 그런 다음 `Yes` when `B` is not `null` 및 `B` 좋아요 `%@magento.com` 그런 다음 `Yes` else `No` end

      * 바꾸기 `@magento.com` 도메인 사용

      * `Datatype` - `String`

* **`[Zendesk] audits_~_events`** 표
   * 정의를 선택합니다. `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[Zendesk] users.id`

   * 선택 [!UICONTROL table]: `[Zendesk] users`
   * 선택 [!UICONTROL column]: `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[Zendesk] audits`** 표
   * 정의를 선택합니다. `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[Zendesk] audits._id`

   * 선택 [!UICONTROL table]: `[Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events._id_of_parent = [Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * 정의를 선택합니다. `Exists`
   * 선택 [!UICONTROL table]: `[Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events._id_of_parent = [Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[Zendesk] Tickets`** 표
   * 정의를 선택합니다. `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[Zendesk] users.id`

   * 선택 [!UICONTROL table]: `[Zendesk] users`
   * 선택 [!UICONTROL column]: `email`
   * [!UICONTROL Path]: `[Zendesk] tickets.requester_id = [Zendesk] users.id`

   * 정의를 선택합니다. `Joined Column`
   * 선택 [!UICONTROL table]: `[Zendesk] users`
   * 선택 [!UICONTROL column]: `role`
   * [!UICONTROL Path]: `[Zendesk] tickets.requester_id = [Zendesk] users.id`

   * 정의를 선택합니다. `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[Zendesk] tickets.id`

   * 선택 [!UICONTROL table]: `[Zendesk] audits`
   * 선택 [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[Zendesk] audits.ticket_id = [Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` 다음으로 변경 `solved = 1`

   * 정의를 선택합니다. `Min`
   * 선택 [!UICONTROL table]: `[Zendesk] audits`
   * 선택 [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[Zendesk] audits.ticket_id = [Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * 
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` 빼기 `created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` 빼기 `created_at`

* **`Requester's ticket number`**
   * 
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * 
      * `Column type` - &quot;동일한 테이블 > 계산&quot;

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype` - 정수

* **`Ticket created_at (day of week)`**
   * 
      * `Column type` - &quot;동일한 테이블 > 계산&quot;

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

      *`Datatype` - `String`


* **`customer_entity`** 표
   * 정의를 선택합니다. `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] tickets.email`
   * 

      [!UICONTROL One]: `customer_entity.email`

   * 선택 [!UICONTROL table]: `[Zendesk] tickets`
   * [!UICONTROL Path]: `[Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type` - &quot;동일한 테이블 > 계산&quot;

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` - `String`

* **`[Zendesk] Tickets`** 표
   * 정의를 선택합니다. `Joined Column`
   * 선택 [!UICONTROL table]: `customer_entity`
   * 선택 [!UICONTROL column]: `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## 지표

* **[!DNL Zendesk]새 티켓**
   * `Tickets we count`

* 에서 **`[Zendesk] tickets`** 표
* 이 지표는 다음을 수행합니다 **카운트**
* 설정 **`id`** 열
* 정렬 기준 **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]해결 티켓**
   * `Tickets we count`
   * 상태 입력 `closed, solved`

* 에서 **`[Zendesk] tickets`** 표
* 이 지표는 다음을 수행합니다 **카운트**
* 설정 **`id`** 열
* 정렬 기준 **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]티켓을 예매하는 고유 사용자**
   * `Tickets we count`

* 에서 **`[Zendesk] tickets`** 표
* 이 지표는 다음을 수행합니다 **고유 개수**
* 설정 **`requester_id`** 열
* 정렬 기준 **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]평균/중간값 티켓 해결 시간**
   * `Tickets we count`
   * 상태 입력 `closed, solved`

* 에서 **`[Zendesk] tickets`** 표
* 이 지표는 다음을 수행합니다 **평균(또는 중간값)**
* 설정 **`Seconds to resolution`** 열
* 정렬 기준 **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]첫 번째 응답에 대한 평균/중간 시간**
   * 우리가 세는 티켓
   * 상태 입력, 해결됨

* 에서 **`[Zendesk] tickets`** 표
* 이 지표는 다음을 수행합니다 **평균(또는 중간값)**
* 설정 **`Seconds to first response`** 열
* 정렬 기준 **`created_at`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>다음을 확인하십시오 [새 열을 지표에 차원으로 추가](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 새 보고서를 작성하기 전에

### 보고서

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * 상태 입력 `new, open, pending`

* 지표 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * 상태 입력 `solved, closed`

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
   * 상태 입력 `solved, closed`

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
   * 상태 입력 `solved, closed`

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

      [[!UICONTROL 지표]: Users

* 지표 `A`: `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
