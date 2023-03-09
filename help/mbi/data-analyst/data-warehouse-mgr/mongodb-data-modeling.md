---
title: MongoDB 데이터 모델링
description: 문제를 일으키는 데이터 패턴을 피하는 방법에 대해 알아봅니다.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# [!DNL MongoDB] 데이터 모델링

날짜 [!DNL MBI] 에서 가져오기 [!DNL MongoDB] 즉, 이 데이터는 관계형 모델로 변환됩니다.

나쁜 소식: 대부분의 데이터 패턴이 문제를 제기하지 않지만, 관계형 모델로의 변환으로 인해 몇 가지 문제가 발생합니다. [!DNL MBI] 은 을 지원하지 않습니다.

좋은 소식: 이러한 모든 패턴을 피할 수 있습니다.

## 하위 중첩 배열 {#subnested}

컬렉션이 아래 예제와 같으면 [!DNL MBI] 항목 배열의 데이터만 복제합니다. 하위 항목 배열의 데이터는 가져오지 않습니다.

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

변수 개체 키가 있는 개체가 포함된 컬렉션은에서 복제되지 않습니다. [!DNL MBI]. 예:

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
