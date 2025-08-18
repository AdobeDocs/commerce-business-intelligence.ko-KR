---
title: Zendesk 데이터 감사
description: Zendesk 데이터를 내보내는 단계에 대해 알아봅니다.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Zendesk 데이터 감사

[[!DNL Zendesk] 데이터](../integrations/exp-zendesk-data.md)에서 이상한 점을 발견했습니까? 문제를 정확히 파악하려면 데이터를 탐색해야 합니다. 이 작업은 [!DNL Zendesk] 데이터를 다운로드 가능한 파일로 내보내면 수행할 수 있습니다.

## 데이터 내보내기 활성화

현재 모든 [!DNL Zendesk] 계정에 대해 데이터 내보내기를 사용할 수 없습니다. 이 기능을 활성화하려면 [지원 티켓을 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)하고 [!DNL Zendesk] 하위 도메인 이름을 언급하십시오.

>[!NOTE]
>
>현재 `Enterprise` 및 `Plus` 계획만 이 기능에 액세스할 수 있습니다.

데이터 내보내기를 사용하도록 설정하면 특정 전자 메일 도메인의 관리자만 [!DNL Zendesk] 계정의 데이터를 내보낼 수 있습니다. 이 전자 메일 도메인은 일반적으로 [!DNL Zendesk]과(와) 동일한 전자 메일 도메인입니다. 계정 소유자의 이메일 도메인이 기본값으로 사용되지만 필요한 경우 도메인을 변경할 수 있습니다.

## 다운로드 가능한 파일로 내보내기

1. 사이드바에서 관리자 아이콘(톱니바퀴 로고)을 클릭하고 **[!UICONTROL Manage** > **Reports]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL Export]** 탭을 클릭합니다.
1. 아래 이미지에 표시된 대로 전체 XML 내보내기 옆의 **[!UICONTROL Request file]**&#x200B;을(를) 클릭합니다.

   이 시점에서 빌드가 시작됩니다. 빌드가 완료되면 이메일로 알림을 받습니다.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. 이메일 알림의 링크를 클릭하여 보고서가 포함된 zip 파일을 다운로드합니다.

   이 다운로드 링크는 최소 3일 동안 유효합니다.

이 프로세스는 티켓 데이터(댓글 포함), 사용자 데이터 및 계정 데이터를 포함하여 현재 [!DNL Zendesk] 계정에 저장된 모든 정보가 포함된 XML 파일을 만듭니다. 이 시점에서 데이터를 자세히 살펴볼 수 있도록 [지원 티켓을 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)할 수 있습니다(이 파일을 반드시 첨부하세요!). 파일이 너무 큰 경우 [!DNL Commerce Intelligence] 또는 [!DNL Dropbox]을(를) 통해 [!DNL Google Drive] 팀과 공유하십시오.

[!DNL Zendesk] 파일 내보내기에 대한 자세한 내용은 공식 [[!DNL Zendesk] 내보내기 설명서](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file)를 참조하세요.
