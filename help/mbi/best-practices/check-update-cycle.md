---
title: 업데이트 주기 상태 확인
description: 업데이트 주기 상태를 확인하는 방법을 알아봅니다.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Developer, User
feature: Dashboards
TQID: https://experienceleague.adobe.com/FAK0W9Qf002Xsug4GLlHs3ChiliC9UXHHrF-Wdo0reo
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 336
ht-degree: 0%

---

# 업데이트 주기 진행률

[!DNL Adobe Commerce Intelligence] 대시보드에 로그인하면 마지막 업데이트 주기 상태를 확인하는 여러 가지 방법이 있습니다. 사용자가 보유한 [사용자 권한](../administrator/user-management/user-management.md)의 유형에 따라 다릅니다.

## 업데이트 주기 상태를 확인해야 하는 이유는 무엇입니까?

상태 업데이트 주기를 확인하는 것은 [!DNL Commerce Intelligence] 계정의 데이터를 감사할 때 유용합니다. [예상과 일치하지 않는 결과](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)가 표시되는 경우(예: [!DNL Commerce Intelligence]의 일일 매출이 전자 상거래 플랫폼 또는 [[!DNL Google] 전자 상거래 매출에 표시되는 내용과 일치하지 않음](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=ko)) 업데이트가 완료되면 마지막 데이터 포인트를 확인하여 문제가 해결되었는지 확인할 수 있습니다.

## [!UICONTROL Read-Only] 및 [!UICONTROL Standard] 사용자

`Read-only`명의 사용자가 대시보드에 로그인한 후 페이지 오른쪽 상단의 아이콘으로 마우스를 가져가면 데이터가 얼마나 최근에 업데이트되었는지 확인할 수 있습니다. 마지막 데이터 포인트를 가져온 시간을 보여 줍니다.

![인터페이스에 마지막으로 성공한 데이터 업데이트 타임스탬프가 표시됨](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin]명의 사용자

`Admin`명의 사용자가 대시보드에 로그인하면 계정 통합에 대한 간단한 상태 아이콘과 함께 위의 마지막 데이터 포인트를 볼 수 있습니다.

자세한 내용을 보려면 관리자가 **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**&#x200B;을(를) 클릭할 수 있습니다.

![연결 세부 정보 및 업데이트 상태를 표시하는 데이터 통합 관리 페이지](../../mbi/assets/detail-manage-data-integrations.png)

이 페이지에는 현재 업데이트 상태와 마지막으로 완료된 업데이트 시간이 표시됩니다.

업데이트가 진행 중인 경우 업데이트가 완료되면 이메일 알림을 요청하는 링크가 표시됩니다.

업데이트가 진행 중이 아닌 경우 업데이트를 강제로 시작하는 링크가 표시됩니다.

>[!NOTE]
>
>일시 중단 시간([!DNL Commerce Intelligence]에서 데이터를 업데이트하지 않으려는 시간)이 설정된 경우 강제로 업데이트를 수행하면 해당 일시 중단 시간의 제한을 고려하지 않는 업데이트 주기가 시작됩니다.


## API를 사용하여 업데이트 주기 상태 확인

**업데이트 주기 상태 API**&#x200B;를 사용하여 가장 최근에 완료된 업데이트 주기를 검색할 수 있습니다.

**요청**

```bash
curl -sS -H "X-RJM-API-Key: <EXPORT-API-KEY>" \
  https://api.rjmetrics.com/0.1/client/<CLIENT_ID>/fullupdatestatus
```

**응답(예)**

```json
{
  "clientId": 194,
  "lastCompletedUpdateJob": {
    "id": 13554,
    "type": { "id": 2, "name": "Full Update" },
    "start": "2025-12-09 03:26:25",
    "end": "2025-12-09 03:29:03",
    "status": { "id": 4, "name": "Completed Successfully" }
  },
  "lastCompletedUpdateJobWithDataSync": null,
  "timezoneAbbreviation": "EST"
}
```

매개 변수, 인증, 오류 및 속도 제한에 대해서는 개발자 설명서에서 [주기 상태 API 업데이트](https://developer.adobe.com/commerce/services/reporting/update-cycle/)를 참조하십시오.
