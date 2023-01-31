---
title: 온보딩
description: 온보딩에 대해 알아봅니다.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# 온보딩

관련 온보딩 질문 `store` 및 `database` 설정은 우리가 보고를 올바르게 설정하도록 합니다. 이러한 답변을 통해 Adobe는 고객의 스토어 설정에 맞게 정확한 보고서를 제공할 것입니다.

## 스토어 설정

- *손님 체크아웃이 가능한가요?* - 선택 **yes** 고객이 계정에 등록하지 않고 상점에서 구매를 하도록 허용하는 경우.

- `Timezone` - 을(를) 선택합니다 `timezone` 추가 콘텐츠에서 보고서를 볼 수 있습니다.

- `Currency` - 을(를) 선택합니다 `currency` 네 가게가 네 가게라고

- `Your week starts on...` - 보고서에서 요일을 시작하려는 요일을 선택합니다.

- *어떤 버전의 상거래를 사용하십니까?* - 을(를) 선택합니다 `currency` 네 가게가 네 가게라고

- *당신 가게는 유럽연합에 기반을 두고 있나요?* 답하면 `Yes` 이 질문을 하기 위해 Adobe에서는 GDPR을 준수하는 Data Warehouse 및 유럽 연합의 모든 데이터를 호스팅합니다.

## 데이터베이스 설정

- `Database name` - 정의 *MySQL 데이터베이스 이름* 상거래 트랜잭션 데이터가 있는 위치

- `Table prefix (optional)` - 전자 상거래 데이터베이스에 들어 있는 표는 어떤 항목에나 포함되어 있습니다(예: `store_`)? 이는 일반적으로 문제가 아니지만 사용자 지정할 수 있습니다.
