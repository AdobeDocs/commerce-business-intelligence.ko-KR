---
title: 다른 광고 지출 데이터 가져오기
description: 오프라인 또는 기타 광고 지출 데이터를  [!DNL Commerce Intelligence](으)로 가져오는 방법을 알아봅니다.
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 다른 광고 지출 데이터 가져오기

광고 지출 데이터를 업로드하면 광고 비용과 캠페인에서 획득한 `customer lifetime value (CLV)`명의 사용자를 결합하여 캠페인 ROI를 측정할 수 있습니다.

## 광고 비용 데이터 업로드

광고 지출 데이터를 분석하는 첫 번째 단계는 데이터를 가져오는 것입니다. 대부분의 광고 플랫폼에서는 보고서를 내보낼 수 있으므로 Adobe은 광고 플랫폼에서 원시 데이터를 내보내고 아무런 조작 없이 직접 [!DNL Commerce Intelligence]에 업로드하는 것을 권장합니다. Data Warehouse의 데이터에 대한 작업을 수행할 수 있으므로 노력을 두 배로 늘릴 필요가 없습니다.

광고 지출 데이터를 내보낸 후 [`File Upload` 기능](../connecting-data/using-file-uploader.md)을(를) 사용하여 데이터를 Data Warehouse으로 가져옵니다. 시간이 지남에 따라 새 데이터를 동일한 [!DNL Commerce Intelligence] 테이블에 업로드할 수 있습니다.

## 오프라인 소스

온라인 캠페인 외에도 라디오나 광고판과 같이 오프라인으로도 광고를 할 수 있습니다. 이러한 경우 비용 데이터가 포함된 스프레드시트를 [!DNL Commerce Intelligence]에 수동으로 업로드할 수 있습니다.

데이터를 기록하고 소비할 `.csv` 파일을 만들 때는 아래 탐색된 테이블 구조를 사용하는 것이 좋습니다. 이 항목 아래쪽에는 템플릿 파일도 첨부되어 있어 예제로 사용됩니다. 권장되는 열은 다음과 같습니다.

* `ID` - 데이터베이스에서 기본 키로 사용하는 각 데이터 행에 대한 고유 식별자입니다. 모든 행에 대해 달라야 합니다.
* `Date` - yyyy-mm-dd 형식으로 캠페인이 실행된 날짜입니다.
* `Amount` - 캠페인에 사용한 금액입니다.
* `campaign` - 캠페인 이름입니다. [!DNL Google Analytics]을(를) 사용하여 다른 광고 지출 데이터를 추적하는 경우 utm\_campaign 이름과 일치해야 합니다.
* `source` - 소스 이름입니다. [!DNL Google Analytics]을(를) 사용하는 경우 `utm_source` 이름과 일치해야 합니다.
* `other`(선택 사항) - 캠페인 및 비용을 세그먼트화하는 데 도움이 되는 추가 열을 통합할 수도 있습니다. 또한 여러 가지 서로 다른 UTM 캠페인 이름을 추적 목적을 위한 하나의 일관된 캠페인으로 요약하는 방법이 될 수 있습니다. 이 설정을 수동으로 설정하는 대신, 두 번째 시트에 대한 V-Lookup을 사용하여 각 캠페인 이름을 기타 이름에 일치시키고 여기에서 동적으로 보고하는 것이 좋을 수 있습니다.

## 관련 항목

* [ [!DNL AdWords] 데이터 연결](../integrations/google-adwords.md)
* [광고 캠페인에 대한 ROI 향상](../../analysis/roi-ad-camp.md)
