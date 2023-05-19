---
title: 데이터베이스에 대한 액세스 제한
description: 액세스를 제한하여 데이터베이스를 저장하는 서버로 액세스를 제한하는 방법에 대해 알아봅니다.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 액세스 제한

서버에 대한 SSH 터널을 만들 때 [!DNL Adobe Commerce Intelligence] 데이터베이스 이외의 모든 항목에 액세스할 수 있습니다. 원하지 않으시면 [!DNL Commerce Intelligence] 데이터베이스를 저장하는 서버에 대한 전체 액세스를 허용하려면 [!DNL Commerce Intelligence Linux] 에 사용자 추가 [제한된 바스셸](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

이름에서 추측했을 수도 있지만 표준 셸보다 더 잘 제어되는 환경을 설정하는 데 제한된 기본 셸이 사용됩니다. 이 유형의 셸에서 중요한 것은 제한된 셸 사용자가 시스템 기능에 액세스하거나 수정할 수 없다는 것입니다.

을(를) 제한하려면 [!DNL Commerce Intelligence Linux] 사용자, 다음 두 가지 작업을 수행해야 합니다.

1. PATH 환경 변수를 빈 문자열로 변경합니다. 즉, 사용자가 시스템 실행 파일에 액세스할 수 없습니다.

1. 실행된 셸이 `bash -r`

이 두 가지 모두 다음 내에서 수행할 수 있습니다. `authorized_keys` 사용자의 홈 파일 `dir/.ssh` 사용자가 로그인할 때 실행되는 명령의 일부로 디렉토리. 다음과 같습니다.

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

이 작업이 완료되면 사용자가 만든 사용자 [!DNL Commerce Intelligence] 시스템을 변경할 수 없습니다.
