---
title: Google Adwords 연결
description: 캠페인에서 획득한 사용자의 광고 비용과 CLV(고객 라이프타임 값)와 결혼하여 캠페인 ROI를 측정하는 방법을 알아봅니다.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Connect [!DNL Google Adwords]

>[!NOTE]
>
>필요한 경우 [관리자 권한](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

연구를 하고 광고를 만들고 캠페인을 시작했습니다. 이제 광고 비용 데이터를 분석하고 비용이 효과적으로 사용되고 있는지 확인할 차례입니다. 광고 비용 데이터를 사용하여 다음을 수행할 수 있습니다 [광고 비용과 CLV(고객 생애 가치)와 결혼하여 캠페인 ROI를 측정합니다](../../analysis/roi-ad-camp.md) 캠페인에서 획득한 사용자 수.

이제 Adobe에 [!DNL Google Adwords] 자격 증명 [!DNL MBI]:

1. 아래의 Connections 페이지로 이동합니다. **데이터 관리 > 통합**.
1. 클릭 **통합 추가**&#x200B;화면의 오른쪽 상단에 있습니다.
1. 을(를) 클릭합니다. **[!DNL Google Adwords]** 아이콘. 이 옵션을 선택하면 [!DNL Google Adwords] 자격 증명 페이지.
1. 을(를) 입력합니다. [!DNL Google Analytics] 자격 증명. 인증 프로세스가 완료되면 다시 로 리디렉션됩니다. [!DNL MBI].
1. 프로필 ID 목록이 표시됩니다. 연결할 프로필을 확인합니다 [!DNL MBI].

   ![](../../../assets/cnnct-profile.png)

1. 변경 내용이 자동으로 저장되므로 **[!UICONTROL Back to Connections]** 다 되면

프로필이 여러 개 있고 어떤 프로필을 식별해야 하는지 식별하는 데 도움이 필요한 경우 `Connecting Multiple Google Analytics profiles` 섹션을 참조하십시오.

## `Connecting multiple Google Analytics profiles`

여러 웹 사이트가 한 사이트에 연결되어 있을 수 있습니다 [!DNL Google Analytics] account, 자체 식별 [!DNL Google Analytics] 프로필 ID. 이 경우 모든 프로필 ID를 포함할 수 있습니다. [!DNL MBI]. 프로필 선택 단계 동안 포함할 프로필 ID를 확인하면 됩니다.

**특정 웹 사이트의 Google Analytics 프로필 ID를 식별하려면 다음을 수행하십시오.**

1. 에 로그인합니다. [!DNL Google Analytics]
1. 특정 웹 사이트의 [!DNL Google Analytics] 대시보드
1. URL을 확인합니다. 프로필 ID는 다음 8개의 숫자에 해당합니다 `p` 줄 끝:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## 연결 끊기 [!DNL Google Adwords]

1. 다음 방문 [!DNL Google] [계정 설정](https://www.google.com/accounts/) 페이지.
1. 아래에 `Security` 섹션을 클릭하고 **[!UICONTROL edit]** 다음 `Authorizing` 애플리케이션 및 사이트.
1. 클릭 **[!UICONTROL revoke access]** 다음 [!DNL MBI].

## 관련

* [통합 재인증](https://support.magento.com/hc/en-us/articles/360016733151)
* [를 통해 주문 참조 소스 추적 [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [데이터베이스에서 사용자 참조 소스 추적](../../analysis/google-track-user-acq.md)
* [데이터베이스에서 사용자 장치, 브라우저 및 OS 데이터 추적](https://support.magento.com/hc/en-us/articles/360016732911)
* [가장 가치 있는 획득 소스 및 채널 살펴보기](../../analysis/most-value-source-channel.md)
* [광고 캠페인에 대한 ROI 향상](../../analysis/roi-ad-camp.md)
* [어떻게 [!DNL Google Analytics] UTM 속성 작업?](../../analysis/utm-attributes.md)
