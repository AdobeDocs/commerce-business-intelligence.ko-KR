---
title: Adobe Commerce Intelligence 온보딩
description: Adobe Commerce Intelligence 온보딩에 대해 알아봅니다.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# [!DNL Adobe Commerce Intelligence] 온보딩

`store` 및 `database` 설정과 관련된 온보딩 질문을 통해 보고를 올바르게 설정했는지 확인하십시오. Adobe은 이러한 답변을 통해 스토어의 설정에 정확하게 맞는 보고서를 제공합니다.

## 스토어 설정

- *스토어에서 게스트 체크아웃을 허용합니까?* - 고객이 계정에 등록하지 않고 스토어에서 구매할 수 있도록 허용하려면 **예**&#x200B;를 선택하십시오.

- `Timezone` - 보고를 표시할 `timezone`을(를) 선택합니다.

- `Currency` - 스토어가 작동하는 `currency`을(를) 선택합니다.

- `Your week starts on...` - 보고서에서 원하는 요일을 선택합니다.

- *사용 중인 Commerce 버전은 무엇입니까?* - 스토어가 작동하는 `currency`을(를) 선택합니다.

- *상점이 유럽 연합에 기반을 두고 있습니까?* - 이 질문에 `Yes`이라고 답하면 Adobe에서 GDPR을 준수하여 유럽 연합에서 Data Warehouse 및 모든 데이터를 호스팅합니다.

## 데이터베이스 설정

- `Database name` - Commerce 트랜잭션 데이터가 있는 *데이터베이스의 [!DNL MySQL]이름*&#x200B;은(는) 무엇입니까?

- `Table prefix (optional)` - Commerce 데이터베이스에 포함된 테이블 앞에 `store_`이(가) 추가되어 있습니까? 이는 일반적으로 해당되지 않지만, 만들 수 있는 사용자 지정입니다.
