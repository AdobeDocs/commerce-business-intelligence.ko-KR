---
title: 필요한 Zendesk 데이터
description: Zendesk 데이터에 대한 추가 설명서에 대한 링크를 포함하여 Zendesk에서 MBI로 가져올 수 있는 기본 데이터 테이블을 알아봅니다.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# 필요한 Zendesk 데이터

후 [연결 [!DNL Zendesk] account](../integrations/zendesk.md)를 사용하여 다음을 수행할 수 있습니다. [Data Warehouse 관리자](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 분석을 위한 관련 데이터 필드를 쉽게 추적할 수 있습니다.

이 문서에서는 가져올 수 있는 기본 데이터 테이블을 살펴봅니다 [!DNL Zendesk] 변환 [!DNL MBI], 다음에 대한 추가 설명서 링크 포함 [!DNL Zendesk] 데이터.

| 테이블 이름 | 설명 |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | 다음 `Audits` 상태 변경 및 고객 및 에이전트 응답을 포함하여 티켓과 연관된 테이블 레코드 활동입니다. 이 표에는 `Tickets` 테이블: 각 티켓에 대해 첫 번째 응답 시간 및 해결 시간을 분석할 수 있습니다. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | 다음 `audit_~\_events` 표는 의 하위 항목입니다. `audits` 표 및 는 티켓 이벤트의 추가 세부 사항을 기록합니다. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | 다음 `Organizations` 표는 이름, ID, 관련 도메인 이름, 태그 및 사용자 지정 필드와 같은 최종 사용자에 대한 회사 정보를 기록합니다. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | 다음 `Tickets` 표는 다음을 포함하여 모든 티켓 세부 사항을 기록합니다 `created_at` 타임스탬프 및 `requester\_id` 및 `assignee\_id`를 설정하는 경우 `Users` 표를 각각 사용합니다. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | 다음 `ticket fields` 표에는 기본 텍스트 필드와 계정에 있는 사용자 지정 티켓 필드에 대한 정보가 포함되어 있습니다. 이 테이블의 속성에는 필드가 포함됩니다 `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, 에이전트 및 최종 사용자별 정보, 생성 및 업데이트 정보 |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | 다음 `Users` 이 표에는 개인 이름 및 이메일을 포함하여 최종 사용자 및 에이전트에 대한 모든 세부 사항이 포함되어 있습니다. 이를 통해 최종 사용자의 참여와 에이전트의 성능을 모두 분석할 수 있습니다. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | 그룹은 Zendesk 계정에서 에이전트를 구성하는 방법입니다. 다음 `Groups` 테이블 레코드 정보(예: `group ID`, `URL`, `name`, 및 정보를 만들고 업데이트합니다. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | 매크로는 티켓 필드의 값을 수정하는 사용자가 정의한 작업입니다. 이 표에는 매크로의 제목, ID, 작업, 제한 사항, 만들기 및 업데이트 정보 등의 특성이 포함되어 있습니다. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | 다음 `Tags` 표에는 계정에 있는 모든 태그 목록이 포함되어 있습니다. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | 이 표에는 티켓 지표에 대한 데이터가 포함되어 있습니다. 필드에는 `ticket ID`, `URL`, 및 그룹, 담당자, 재열기, 회신, 회신 시간(분), 전체 해결 시간 및 마지막 업데이트(예: 상태, 담당자 또는 요청자) 정보 수. |

{style=&quot;table-layout:auto&quot;}

## 관련

* [Zendesk 연결](../integrations/zendesk.md)
* [통합 재인증](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
