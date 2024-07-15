---
title: Google Adwords 연결
description: 광고 비용과 캠페인에서 획득한 사용자의 CLV(고객 생애 가치)를 결합하여 캠페인 ROI를 측정하는 방법을 알아봅니다.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# [!DNL Google Adwords] 연결

>[!NOTE]
>
>[관리자 권한](../../../administrator/user-management/user-management.md)이 필요합니다.

![](../../../assets/Google_Adwords_logo.png)

조사를 했고, 광고를 만들었으며, [!DNL Google] 캠페인을 시작했습니다. 이제 광고 지출 데이터를 분석하고 비용이 효과적으로 지출되고 있는지 확인할 차례입니다. 광고 지출 데이터를 사용하여 [광고 비용과 캠페인에서 획득한 사용자의 CLV(고객 생애 가치)를 합산하여 캠페인 ROI를 측정할 수 있습니다](../../analysis/roi-ad-camp.md).

[!DNL Commerce Intelligence]에 [!DNL Google Adwords] 자격 증명을 입력하여 시작하십시오.

1. **데이터 관리 > 통합** 아래의 `Connections` 페이지로 이동합니다.
1. 화면 오른쪽 상단에 있는 **통합 추가**&#x200B;를 클릭합니다.
1. **[!DNL Google Adwords]** 아이콘을 클릭합니다. [!DNL Google Adwords] 자격 증명 페이지가 열립니다.
1. [!DNL Google Analytics] 자격 증명을 입력하십시오. 인증 프로세스가 완료되면 다시 [!DNL Commerce Intelligence](으)로 리디렉션됩니다.
1. 프로필 ID 목록이 표시됩니다. [!DNL Commerce Intelligence]에 연결할 프로필을 확인하십시오.

   ![](../../../assets/cnnct-profile.png)

1. 변경 사항이 자동으로 저장되므로 완료되면 **[!UICONTROL Back to Connections]**&#x200B;을(를) 클릭하십시오.

프로필이 여러 개이고 어떤 프로필인지 확인하는 데 도움이 필요한 경우 아래의 `Connecting Multiple Google Analytics profiles` 섹션을 참조하십시오.

## 여러 [!DNL Google Analytics]개의 프로필 연결 중

하나의 [!DNL Google Analytics] 계정에 여러 웹 사이트가 연결되어 있으며, 해당 웹 사이트가 [!DNL Google Analytics] 프로필 ID로 식별될 수 있습니다. 이 경우 [!DNL Commerce Intelligence]에 모든 프로필 ID를 포함할 수 있습니다. 프로필 선택 단계에서 포함할 프로필 ID를 확인합니다.

**특정 웹 사이트의 Google Analytics 프로필 ID를 식별하려면:**

1. [!DNL Google Analytics]에 로그인
1. 특정 웹 사이트의 [!DNL Google Analytics] 대시보드로 이동
1. URL을 확인합니다. 프로필 ID는 줄 끝에 있는 `p` 뒤에 오는 8개의 숫자에 해당합니다.

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## [!DNL Google Adwords] 연결 끊기

1. [!DNL Google] [계정 설정](https://www.google.com/account/about/?hl=en) 페이지를 방문하세요.
1. `Security` 섹션에서 `Authorizing`개의 응용 프로그램 및 사이트 옆에 있는 **[!UICONTROL edit]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL revoke access]**&#x200B;을(를) 클릭합니다.

## 관련 항목

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [ [!DNL Google ECommerce]을(를) 통해 주문 참조 원본 추적](../integrations/google-ecommerce.md)
* [데이터베이스에서 사용자 조회 소스 추적](../../analysis/google-track-user-acq.md)
* [가장 가치 있는 확보 소스 및 채널 살펴보기](../../analysis/most-value-source-channel.md)
* [광고 캠페인에 대한 ROI 향상](../../analysis/roi-ad-camp.md)
* [ [!DNL Google Analytics] UTM 속성은 어떻게 작동합니까?](../../analysis/utm-attributes.md)
