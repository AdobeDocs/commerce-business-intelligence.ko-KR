---
title: MongoDB 데이터 모델링
description: 문제를 일으키는 데이터 패턴을 피하는 방법에 대해 알아봅니다.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/L9xlGE4hAQssTHJzzxQD9EGUVaIZFY-2-ALOLM9vym4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 129
ht-degree: 1%

---

# [!DNL MongoDB] 데이터 모델링

[!DNL Adobe Commerce Intelligence]이(가) [!DNL MongoDB] 데이터를 가져오면 해당 데이터가 관계형 모델로 변환됩니다.

나쁜 소식: 대부분의 데이터 패턴에 문제가 있는 것은 아니지만, 관계형 모델로의 변환으로 인해 [!DNL Commerce Intelligence]에서 지원하지 않는 몇 가지 데이터 패턴이 있습니다.

좋은 소식: 이러한 모든 패턴을 피할 수 있습니다.

## 하위 중첩 배열 {#subnested}

컬렉션이 아래 예제와 같으면 [!DNL Commerce Intelligence]은(는) 항목 배열의 데이터만 복제합니다. 하위 항목 배열의 데이터는 가져오지 않습니다.

```bash
    {
        _id: 0000000000000001
        items: [
            {
                _id: 0000000000000002
               subItems: [
                   {
                       _id: 0000000000000003
                      name: "Donut"
                      description: "glazed"
                   }
               ]
            }
        ]
    }
```

## 변수 개체 키 {#varobjectkeys}

변수 개체 키가 있는 개체가 포함된 컬렉션은 [!DNL Commerce Intelligence]에서 복제되지 않습니다. For example:

```bash
    {
        _id: 0000000000000001
        friends: {
            0000000000000002: "Jimmy",
            0000000000000004: "Roger",
            0000000000000005: "Susan"
        },
    }
```

일반적으로 개체가 사용되고 배열이 더 적합한 경우에 발생합니다. 이제 위의 예제를 다시 실행하십시오.

```bash
    {
        _id: 0000000000000001
        friends: [
            { friend_id: 0000000000000002, name: "Jimmy" },
            { friend_id: 0000000000000004, name: "Roger" },
            { friend_id: 0000000000000005, name: "Susan"}
        ]
    }
```
