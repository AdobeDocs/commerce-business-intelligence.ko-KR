---
title: 데이터 마이그레이션 서비스
description: 요청을 제출하고 마이그레이션을 시작하는 데 필요한 모든 사항을 알아봅니다.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# 데이터 마이그레이션

새 데이터베이스 스키마, 서버 또는 보고 데이터베이스로 마이그레이션하는 것은 스트레스를 받을 필요가 없습니다. [[!DNL Adobe] 서비스 팀](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)에서 마이그레이션 지원을 제공합니다.

전환이 최대한 매끄럽게 진행되도록 하려면 마이그레이션 요청을 제출할 때 가능한 한 자세히 설명해야 합니다. 이 항목에는 요청을 제출하고 마이그레이션을 시작하는 데 필요한 모든 것이 있습니다. 귀하의 요구 사항에 대한 포괄적인 그림을 제공하면 프로젝트의 범위가 적절하고 예상치가 정확하다는 것을 보증할 수 있습니다.

## 시작 {#started}

시작하기 전에 다음 질문에 대한 답변을 알고 있어야 합니다.

* **새 서버에 새 데이터베이스가 있습니까?** 요청을 제출하기 전에 **[!UICONTROL Manage Data** > **Connections]**&#x200B;에서 데이터 연결의 설정을 업데이트하십시오. 이 작업을 수행하는 방법에 대한 새로 고침이 필요한 경우 [`Integrations`](../integrations/integrations.md) 섹션으로 이동하여 사용 중인 데이터베이스 유형에 대한 지침을 찾으십시오.

* **모든 이전 데이터가 새 데이터베이스에 있습니까, 아니면 마이그레이션해야 합니까?** 마이그레이션 프로세스 중에 이전 데이터와 새 데이터를 통합할 수 있습니다. 통합이 필요하지 않더라도 요청에 알려 주십시오.

위에 대한 답을 얻었으면 마이그레이션 유형을 알아야 합니다. 새 데이터베이스에 [`same`](#sameschema) 스키마가 있습니까? 아니면 [`different`](#newschema) 스키마가 있습니까? 아래 논의에서는 각 마이그레이션 유형에 대한 자세한 지침을 확인할 수 있습니다.

## 동일한 스키마를 사용하는 새 데이터베이스로 마이그레이션 {#sameschema}

요청을 제출할 때 데이터베이스 스키마가 변경되지 않고 [!DNL Adobe Commerce Intelligence]에 이미 연결이 설정되어 있는지 알려 주십시오.

데이터베이스에 새 이름이 있는 경우 대시보드를 올바르게 마이그레이션할 수 있도록 요청에 포함하십시오.

데이터베이스 이름이 변경되지 않으면 마이그레이션이 완료된 것입니다. 다음 전체 업데이트가 완료되면 대시보드 및 보고서가 새로 고쳐집니다.

## 다른 스키마를 사용하는 새 데이터베이스로 마이그레이션 {#newschema}

>[!IMPORTANT]
>
>새 데이터베이스의 특정 데이터 열에 동일한 열이 없는 경우 프로세스에서 특정 분석이 손실될 가능성이 있습니다.

이러한 유형의 마이그레이션을 성공적으로 완료하려면 기존 데이터 열을 새 데이터베이스의 해당 열과 일치시켜야 합니다. 이는 필수는 아니지만, 당사에 대해 일치를 수행하면 요청 전환 시간을 단축하고 마이그레이션 가격을 낮출 수 있습니다.

직접 일치를 수행하는 데 익숙하다면 다음 지침에 따라 완성된 스프레드시트를 요청에 첨부하십시오.

1. 현재 Data Warehouse(**[!UICONTROL Manage Data** > **Data Warehouse]**)와 동기화되는 모든 테이블 및 열을 검토합니다.

1. 스프레드시트에서 새 데이터베이스로 마이그레이션할 모든 테이블에 대한 탭을 만듭니다.

1. 각 탭에서 마이그레이션해야 하는 모든 기존 열에 대한 열을 만듭니다. Adobe에서는 이름을 `Existing column name`과(와) 같이 지정할 것을 권장합니다.

1. 스프레드시트의 각 탭에서 새 데이터베이스에 해당하는 열에 대해 다른 열을 만들어야 합니다. Adobe에서는 열 이름을 `New column name`과(와) 같이 지정할 것을 권장합니다.

1. 기존 열과 그에 해당하는 열을 입력합니다. 기존 열에 새로운 해당 열이 없으면 `N/A`을(를) 입력하십시오.

   또한 새 데이터베이스에서 동일한 정보를 계산하는 새로운 방법이 있으면 [`New column name`] 열에 입력합니다.

다음은 예입니다.

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>새 데이터베이스의 특정 데이터 열에 동일한 열이 없는 경우 프로세스에서 특정 분석이 손실될 가능성이 있습니다.

## 요청을 제출하는 방법 {#submitreq}

[지원 요청을 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)하면 연락할 수 있습니다.

이전 섹션의 단계에 따라 열과 일치하는 스프레드시트를 만들었다면 첨부하는 것을 잊지 마십시오.

## 다음은 무엇입니까? {#wrapup}

프로젝트 범위를 결정하려면 마이그레이션을 수행하는 Commerce 서비스 팀의 분석가와 공동 작업을 수행해야 합니다. 변경의 복잡성과 분석가의 응답성은 마이그레이션이 소요되는 시간에 직접적인 영향을 줍니다. 세부 사항을 파악한 후 타임라인이 설정되고 작업 명세서가 전송됩니다.
