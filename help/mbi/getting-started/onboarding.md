---
title: Adobe Commerce Intelligence 온보딩
description: Adobe Commerce Intelligence 온보딩에 대해 알아봅니다.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# 온보딩 [!DNL Adobe Commerce Intelligence]

관련 온보딩 질문 `store` 및 `database` 설정은 보고를 올바로 설정하도록 합니다. 이러한 답변을 통해 Adobe은 스토어의 설정에 정확하게 맞는 보고서를 제공합니다.

## 스토어 설정

- *손님 체크아웃이 가능합니까?* - 선택 **예** 고객이 계정에 등록하지 않고도 스토어에서 구매할 수 있도록 허용하는 경우.

- `Timezone` - 다음을 선택합니다. `timezone` 보고 내용을 표시합니다.

- `Currency` - 다음을 선택합니다. `currency` 상점이 운영되는 지점입니다.

- `Your week starts on...` - 보고서에서 한 주의 시작으로 사용할 요일을 선택합니다.

- *어떤 버전의 Commerce를 사용합니까?* - 다음을 선택합니다. `currency` 상점이 운영되는 지점입니다.

- *당신 가게는 유럽 연합에 본사를 두고 있나요?* - 답변하는 경우 `Yes` 이 질문에 대해 Adobe은 GDPR을 준수하여 Data Warehouse 및 모든 데이터를 유럽 연합에서 호스팅합니다.

## 데이터베이스 설정

- `Database name` - 이란? *이름 [!DNL MySQL] 데이터베이스* 상거래 트랜잭션 데이터가 있는 위치

- `Table prefix (optional)` - Commerce 데이터베이스에 포함된 테이블 앞에 다음 문자가 추가됨(예: `store_`)? 이는 일반적으로 해당되지 않지만, 만들 수 있는 사용자 지정입니다.
