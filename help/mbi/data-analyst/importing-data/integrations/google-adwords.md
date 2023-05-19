---
title: Google Adwords 연결
description: 광고 비용과 캠페인에서 획득한 사용자의 CLV(고객 생애 가치)를 결합하여 캠페인 ROI를 측정하는 방법을 알아봅니다.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 연결 [!DNL Google Adwords]

>[!NOTE]
>
>필요 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

조사를 했고, 광고를 만들고, [!DNL Google] 캠페인. 이제 광고 지출 데이터를 분석하고 비용이 효과적으로 지출되고 있는지 확인할 차례입니다. 광고 지출 데이터를 사용하여 다음과 같은 작업을 수행할 수 있습니다 [광고 비용과 고객 생애 가치(CLV)를 결합하여 캠페인 ROI를 측정합니다.](../../analysis/roi-ad-camp.md) 캠페인에서 획득한 사용자 수

다음을 입력하여 시작하기 [!DNL Google Adwords] 자격 증명 대상 [!DNL Commerce Intelligence].

1. 로 이동 `Connections` 아래 페이지 **데이터 관리 > 통합**.
1. 클릭 **통합 추가**, 화면의 오른쪽 상단에 있습니다.
1. 다음을 클릭합니다. **[!DNL Google Adwords]** 아이콘. 이렇게 하면 [!DNL Google Adwords] 자격 증명 페이지입니다.
1. 다음을 입력하십시오. [!DNL Google Analytics] 자격 증명. 인증 프로세스가 완료되면 다시 로 리디렉션됩니다. [!DNL Commerce Intelligence].
1. 프로필 ID 목록이 표시됩니다. 연결할 프로필을 확인하십시오. [!DNL Commerce Intelligence].

   ![](../../../assets/cnnct-profile.png)

1. 변경 사항이 자동으로 저장되므로 **[!UICONTROL Back to Connections]** 완료되었을 때.

프로필이 여러 개 있고 어떤 프로필인지 식별하는 데 도움이 필요한 경우 다음을 참조하십시오. `Connecting Multiple Google Analytics profiles` 아래 섹션.

## 여러 개 연결 중 [!DNL Google Analytics] 프로필

하나의 웹 사이트에 여러 개의 웹 사이트가 연결되어 있을 수 있습니다. [!DNL Google Analytics] 계정, 자체 식별 [!DNL Google Analytics] 프로필 ID. 이 경우 모든 프로필 ID를 포함할 수 있는 옵션이 있습니다 [!DNL Commerce Intelligence]. 프로필 선택 단계에서 포함할 프로필 ID를 확인합니다.

**특정 웹 사이트의 Google Analytics 프로필 ID를 식별하려면 다음을 수행하십시오.**

1. 에 로그인 [!DNL Google Analytics]
1. 특정 웹 사이트로 이동 [!DNL Google Analytics] 대시보드
1. URL을 확인합니다. 프로필 ID는 다음 8개의 숫자에 해당합니다. `p` 줄 끝:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## 연결 끊기 [!DNL Google Adwords]

1. 다음을 방문하십시오. [!DNL Google] [계정 설정](https://www.google.com/account/about/?hl=en) 페이지를 가리키도록 업데이트하는 중입니다.
1. 아래 `Security` 섹션, 클릭 **[!UICONTROL edit]** 다음에 `Authorizing` 애플리케이션 및 사이트
1. 클릭 **[!UICONTROL revoke access]**.

## 관련 항목

* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [다음을 통해 주문 참조 소스 추적 [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [데이터베이스에서 사용자 조회 소스 추적](../../analysis/google-track-user-acq.md)
* [가장 가치 있는 확보 소스 및 채널 살펴보기](../../analysis/most-value-source-channel.md)
* [광고 캠페인에 대한 ROI 향상](../../analysis/roi-ad-camp.md)
* [은 어떻게 합니까? [!DNL Google Analytics] UTM 속성이 작동합니까?](../../analysis/utm-attributes.md)
