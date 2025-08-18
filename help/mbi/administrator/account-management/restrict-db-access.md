---
title: 데이터베이스에 대한 액세스 제한
description: 액세스를 제한하여 데이터베이스를 저장하는 서버로 액세스를 제한하는 방법에 대해 알아봅니다.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 액세스 제한

서버에 대한 SSH 터널을 만들 때 [!DNL Adobe Commerce Intelligence]에서 데이터베이스 이외의 항목에 액세스할 필요가 없습니다. [!DNL Commerce Intelligence]이(가) 데이터베이스를 보관하는 서버에 대한 전체 액세스를 허용하지 않도록 하려면 [!DNL Commerce Intelligence Linux] 사용자를 [제한된 기본 셸](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html)로 강제 설정하여 액세스를 제한할 수 있습니다.

이름에서 추측했을 수도 있지만 표준 셸보다 더 잘 제어되는 환경을 설정하는 데 제한된 기본 셸이 사용됩니다. 이 유형의 셸에서 중요한 것은 제한된 셸 사용자가 시스템 기능에 액세스하거나 수정할 수 없다는 것입니다.

[!DNL Commerce Intelligence Linux] 사용자를 제한하려면 다음 두 가지 작업을 수행해야 합니다.

1. PATH 환경 변수를 빈 문자열로 변경합니다. 즉, 사용자가 시스템 실행 파일에 액세스할 수 없습니다.

1. 실행된 셸이 `bash -r`인지 확인하십시오.

이 두 작업은 모두 사용자의 홈 `authorized_keys` 디렉터리에 있는 `dir/.ssh` 파일 내에서 사용자가 로그인할 때 실행되는 명령의 일부로 수행할 수 있습니다. 다음과 같습니다.

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

이 작업이 완료되면 [!DNL Commerce Intelligence]에 대해 만든 사용자는 시스템을 변경할 수 없습니다.
