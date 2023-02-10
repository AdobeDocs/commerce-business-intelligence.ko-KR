---
title: 감사 Zendesk 데이터
description: Zendesk 데이터를 내보내는 단계를 알아봅니다.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 감사 Zendesk 데이터

네 집에서 이상한 걸 발견했어 [[!DNL Zendesk] 데이터](../integrations/exp-zendesk-data.md)? 그 문제를 정확히 알아내기 위해서는 여러분의 데이터를 살펴봐야 합니다. 이 작업은 를 내보내 수행할 수 있습니다 [!DNL Zendesk] 데이터를 다운로드 가능한 파일에 추가합니다.

## 데이터 내보내기 활성화

데이터 내보내기가 현재 모든 항목에 대해 활성화되어 있지 않습니다 [!DNL Zendesk] 계정. 이 기능을 활성화하려면 [지원 티켓 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en), 에 대한 [!DNL Zendesk] 하위 도메인 이름.

>[!NOTE]
>
>전용 `Enterprise` 및 `Plus` 계획은 현재 이 기능에 액세스할 수 있습니다.

데이터 내보내기가 활성화되면 특정 이메일 도메인의 관리자만 [!DNL Zendesk] 계정이 필요합니다. 이 이메일 도메인은 일반적으로 과 동일한 이메일 도메인입니다 [!DNL Zendesk]. 계정 소유자의 이메일 도메인이 기본값으로 사용되지만 필요한 경우 도메인을 변경할 수 있습니다.

## 다운로드 가능한 파일로 내보내기

1. 사이드바에서 Admin 아이콘(톱니바퀴 로고)을 클릭하고 을 선택합니다 **[!UICONTROL Manage** > **Reports]**.
1. 을(를) 클릭합니다. **[!UICONTROL Export]** 탭.
1. 클릭 **[!UICONTROL Request file]** 아래에 표시된 대로 전체 XML 내보내기 옆에 있습니다.

   이 시점에서 빌드가 시작됩니다. 완료되면 이메일을 통해 알림을 받게 됩니다.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. 보고서를 포함하는 zip 파일을 다운로드하려면 이메일 알림의 링크를 클릭합니다.

   이 다운로드 링크는 적어도 3일 동안 유효합니다.

이 프로세스에서는 현재 파일에 저장된 모든 정보가 들어 있는 XML 파일을 만듭니다 [!DNL Zendesk] 티켓 데이터(주석 포함), 사용자 데이터 및 계정 데이터를 포함한 계정. 이 시점에서 다음을 수행할 수 있습니다 [지원 티켓 제출](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) (이 파일을 첨부하십시오!) 따라서 데이터를 좀 더 자세히 살펴볼 수 있습니다. 파일이 너무 큰 경우 [!DNL MBI] 팀 비아 [!DNL Dropbox] 또는 [!DNL Google Drive].

에 대한 자세한 정보 [!DNL Zendesk] 파일 내보내기, 공식 [[!DNL Zendesk] 내보내기 설명서](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
