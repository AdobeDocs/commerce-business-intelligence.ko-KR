---
title: 데이터베이스에 대한 액세스 제한
description: 액세스를 제한하여 데이터베이스를 수용하는 서버에 대한 액세스를 제한하는 방법을 알아봅니다.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# 액세스 제한

서버에 SSH 터널을 만들 때는 [!DNL MBI] 데이터베이스를 제외한 모든 항목에 액세스할 수 있습니다. 원한다면 [!DNL MBI] 데이터베이스를 수용하는 서버에 대한 전체 액세스 권한을 가지려면 [!DNL MBI Linux] 사용자가 [제한된 bash 셸](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

이름에서 짐작했을 수도 있지만, 제한된 bash 쉘은 표준 쉘보다 제어된 환경을 설정하는 데 사용됩니다. 이러한 유형의 셸에 대한 중요한 점은 제한된 셸 사용자는 시스템 기능에 액세스하거나 어떠한 종류의 수정도 할 수 없다는 것입니다.

를 제한하려면 [!DNL MBI Linux] 사용자는 다음 두 가지 작업을 수행해야 합니다.

1. PATH 환경 변수를 빈 문자열로 변경합니다. 즉, 사용자가 시스템 실행 파일에 액세스할 수 없습니다.

1. 셸이 실행되었는지 확인합니다. `bash -r`

이 두 작업 모두 내에서 수행할 수 있습니다 `authorized_keys` 사용자의 홈에 있는 파일 `dir/.ssh` 디렉토리 는 사용자가 로그인할 때 실행되는 명령의 일부로 사용됩니다. 다음과 같이 표시됩니다.

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

이 작업이 완료되면 사용자를 만든 다음 [!DNL MBI] 는 시스템을 변경할 수 없습니다.
