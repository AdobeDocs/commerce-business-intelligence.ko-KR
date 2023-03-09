---
title: Zendesk 데이터 감사
description: Zendesk 데이터를 내보내는 단계에 대해 알아봅니다.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Zendesk 데이터 감사

에서 이상한 점을 발견했습니다. [[!DNL Zendesk] 데이터](../integrations/exp-zendesk-data.md)? 문제를 정확히 파악하려면 데이터를 탐색해야 합니다. 이 작업은 를 내보내서 수행할 수 있습니다. [!DNL Zendesk] 데이터를 다운로드 가능한 파일로 복사합니다.

## 데이터 내보내기 활성화

데이터 내보내기가 현재 모든 항목에 대해 활성화되어 있지 않습니다. [!DNL Zendesk] 계정. 이 기능을 활성화하려면 [지원 티켓 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en), 사용자 이름 언급하기 [!DNL Zendesk] 하위 도메인 이름.

>[!NOTE]
>
>전용 `Enterprise` 및 `Plus` 플랜에는 현재 이 기능에 대한 액세스 권한이 있습니다.

데이터 내보내기가 활성화되면 특정 이메일 도메인의 관리자만 [!DNL Zendesk] 계정입니다. 이 이메일 도메인은 일반적으로 와(과) 동일한 이메일 도메인입니다. [!DNL Zendesk]. 계정 소유자의 이메일 도메인이 기본값으로 사용되지만 필요한 경우 도메인을 변경할 수 있습니다.

## 다운로드 가능한 파일로 내보내기

1. 사이드바에서 관리자 아이콘(톱니바퀴 로고)을 클릭하고 **[!UICONTROL Manage** > **Reports]**.
1. 다음을 클릭합니다. **[!UICONTROL Export]** 탭.
1. 클릭 **[!UICONTROL Request file]** 아래 이미지에 표시된 대로 전체 XML 내보내기 옆에 있습니다.

   이 시점에서 빌드가 시작됩니다. 빌드가 완료되면 이메일로 알림을 받습니다.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. 이메일 알림의 링크를 클릭하여 보고서가 포함된 zip 파일을 다운로드합니다.

   이 다운로드 링크는 최소 3일 동안 유효합니다.

이 프로세스는 현재 파일에 저장된 모든 정보를 포함하는 XML 파일을 작성합니다 [!DNL Zendesk] 티켓 데이터(댓글 포함), 사용자 데이터 및 계정 데이터를 포함한 계정. 이 시점에서 다음 작업을 수행할 수 있습니다. [지원 티켓 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) (이 파일을 첨부해야 합니다!) 따라서 데이터를 자세히 살펴볼 수 있습니다. 파일이 너무 큰 경우 [!DNL MBI] 팀 via [!DNL Dropbox] 또는 [!DNL Google Drive].

에 대한 자세한 내용 [!DNL Zendesk] 파일 내보내기, 공식 참조 [[!DNL Zendesk] 내보내기 설명서](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
