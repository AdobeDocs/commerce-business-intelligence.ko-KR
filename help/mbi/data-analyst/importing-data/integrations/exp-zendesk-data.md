---
title: 예상 Zendesk 데이터
description: Zendesk 데이터에 대한 추가 설명서 링크를 포함하여 Zendesk에서 Commerce Intelligence으로 가져올 수 있는 기본 데이터 표에 대해 알아봅니다.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# [!DNL Zendesk]개의 데이터가 필요합니다.

[계정 [!DNL Zendesk] 연결](../integrations/zendesk.md)한 후 [Data Warehouse 관리자](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)를 사용하여 분석할 관련 데이터 필드를 쉽게 추적할 수 있습니다.

이 항목에서는 [!DNL Zendesk] 데이터에 대한 추가 설명서에 대한 링크를 포함하여 [!DNL Adobe Commerce Intelligence]에서 [!DNL Zendesk]&#x200B;(으)로 가져올 수 있는 기본 데이터 테이블을 살펴봅니다.

| 테이블 이름 | 설명 |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | `Audits` 테이블은 상태 변경 및 고객 및 에이전트 응답을 포함하여 티켓과 연결된 활동을 기록합니다. 이 테이블에는 `Tickets` 테이블로 다시 연결되는 티켓 ID가 포함되어 있으므로 각 티켓에 대한 첫 번째 응답 시간과 해결 시간을 분석할 수 있습니다. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | `audit_~\_events` 테이블은 `audits` 테이블의 하위 테이블이며 티켓 이벤트에 대한 추가 세부 정보를 기록합니다. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | `Organizations` 테이블은 이름, ID, 연결된 도메인 이름, 태그 및 사용자 지정 필드 등 최종 사용자에 대한 회사 정보를 기록합니다. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | `Tickets` 테이블은 `created_at` 타임스탬프와 `requester\_id` 및 `assignee\_id`을(를) 포함하여 모든 티켓 세부 정보를 기록하며, 이를 통해 티켓을 `Users` 테이블의 최종 사용자 및 에이전트에 각각 연결할 수 있습니다. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | `ticket fields` 표에는 계정의 기본 텍스트 필드와 사용자 지정 티켓 필드에 대한 정보가 들어 있습니다. 이 테이블의 특성에는 필드 `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, 에이전트 및 최종 사용자별 정보, 만들기 및 업데이트 정보가 포함됩니다. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | `Users` 표에는 개인 이름 및 전자 메일을 포함하여 최종 사용자 및 에이전트에 대한 모든 세부 정보가 포함되어 있습니다. 이를 통해 최종 사용자의 참여도와 에이전트의 성능을 모두 분석할 수 있습니다. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | 그룹은 Zendesk 계정에서 에이전트가 구성되는 방식입니다. `Groups` 테이블은 `group ID`, `URL`, `name` 및 만들기 및 업데이트 정보와 같은 정보를 기록합니다. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | 매크로는 티켓 필드의 값을 수정하는 사용자가 정의한 작업입니다. 이 표에는 매크로 제목, ID, 작업, 제한 사항, 만들기 및 업데이트 정보 등의 특성이 포함되어 있습니다. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | `Tags` 테이블에는 계정의 모든 태그 목록이 있습니다. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | 이 표에는 티켓 지표에 대한 데이터가 포함되어 있습니다. 필드에는 `ticket ID`, `URL` 및 그룹 수, 할당자, 다시 열기, 회신, 회신 시간(분), 전체 해결 시간 및 마지막 업데이트(예: 상태, 할당자 또는 요청자) 정보가 포함됩니다. |

{style="table-layout:auto"}

## 관련 항목

* [Zendesk 연결하기](../integrations/zendesk.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ko)
