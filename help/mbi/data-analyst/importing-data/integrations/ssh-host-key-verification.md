---
title: SSH 호스트 키 확인
description: Commerce Intelligence에서 SSH 호스트 키를 등록하는 방법, 새로 고치는 방법, 오류 문제 해결 및 SSH 터널 연결 지원에 문의하는 시기에 대해 알아봅니다.
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
source-git-commit: b51e9fceba0c62f4ef3dde340d26cd78641ef3a2
workflow-type: tm+mt
source-wordcount: 1130
ht-degree: 0%

---

# SSH 호스트 키 확인 {#ssh-host-keys}

[!DNL Commerce Intelligence]은(는) [MySQL](mysql-via-ssh-tunnel.md), [MongoDB](mongodb-via-ssh-tunnel.md) 및 [PostgreSQL](postgresql.md)을(를) 포함하여 암호화된(SSH 터널) 데이터베이스 연결에 대해 엄격한 SSH 호스트 키 확인을 사용합니다.

**[!UICONTROL Save & Test]** 동안 시스템에서는 연결에 대한 SSH 기본 호스트 키를 등록하고 연결별로 안전하게 저장합니다. 등록 후 복제 및 터널링은 라이브 요새 호스트 키가 등록된 키와 일치하는 경우에만 성공합니다.

이 모델은 중간자 공격 및 예기치 않은 호스트 변경을 차단하여 보안을 향상시킵니다. 또한 호스트 키 회전, 누락된 신뢰 자료 또는 인프라 변경 사항이 일반 터널 오류 대신 연결에 SSH 호스트 키 오류로 나타날 수 있음을 의미합니다.

>[!NOTE]
>
>**관리자**&#x200B;는 달리 명시되지 않는 한 Adobe 조직 콘솔이 아닌 [!DNL Commerce Intelligence] 계정에 대한 관리자 권한이 있는 사용자를 의미합니다. 관리자만 **[!UICONTROL Refresh SSH Host Keys]**&#x200B;을(를) 실행할 수 있습니다. 이 컨트롤이 표시되지 않으면 계정의 관리자에게 새로 고침 실행을 요청하거나 Adobe 지원에 문의하십시오.

`known_hosts`개 파일을 편집, 업로드 또는 관리하지 않습니다. 계정에 할당된 Adobe 인프라에서 등록 및 새로 고침 실행.

>[!IMPORTANT]
>
>호스트 키 순환을 사용하려면 관리자가 **[!UICONTROL Refresh SSH Host Keys]**&#x200B;을(를) 실행해야 합니다. 요새 호스트 키가 변경되었거나 요새 ID(호스트 이름, IP 또는 포트)가 변경된 경우 **[!UICONTROL Save & Test]**&#x200B;을(를) 다시 실행하거나 연결을 다시 저장해도 등록된 키가 업데이트되지 않습니다. 관리자가 호스트 키를 새로 고칠 때까지 연결이 계속 실패할 수 있습니다.

## 저장 및 테스트 {#save-and-test}

**[!UICONTROL Save & Test]**&#x200B;은(는) **초기 SSH 호스트 키 등록만 수행합니다**. 이 함수는 기본적으로 사용되며 연결에 이미 등록된 키를 회전하거나 덮어쓰지 않습니다.

| 등록된 호스트 키 상태 | 저장 및 테스트의 기능 |
| --- | --- |
| 호스트 키가 아직 등록되지 않았습니다. | **[!UICONTROL Save & Test]**&#x200B;이(가) Bastion 호스트 및 포트를 검색하고 호스트 키를 등록하여 이 연결에 대해 저장합니다. |
| 호스트 키가 이미 등록되었습니다. | **[!UICONTROL Save & Test]**&#x200B;에서 등록을 건너뜁니다. 라이브 기준 키가 더 이상 일치하지 않는 경우에도 등록된 기존 키를 덮어쓰거나, 회전하거나, 삭제하지 않습니다. |
| 등록된 키가 없거나 비어 있거나 잘못되었습니다. | **[!UICONTROL Save & Test]**&#x200B;은(는) 잘못된 신뢰 자료를 자체적으로 복구하지 않습니다. 관리자는 **[!UICONTROL Refresh SSH Host Keys]**&#x200B;을(를) 실행하거나 오류가 계속되는 경우 지원 팀에 문의해야 합니다. |

첫 번째 등록이 성공적으로 완료되면 나중에 **[!UICONTROL Save & Test]**&#x200B;에서 자격 증명 및 연결 설정을 실행하지만 등록된 SSH 호스트 키는 변경되지 않습니다.

## SSH 호스트 키 새로 고침 {#refresh-ssh-host-keys}

보루가 변경되었거나 트러스트 자료를 복구해야 하는 경우 **[!UICONTROL Refresh SSH Host Keys]**&#x200B;에서 등록된 SSH 호스트 키를 업데이트합니다. 관리자가 **[!UICONTROL Data]** > **[!UICONTROL Connections]**&#x200B;의 연결에서 새로 고침을 시작합니다.

새로 고침은 계정에 할당된 Adobe 인프라에서 비동기적으로 실행됩니다. [!DNL Commerce Intelligence]은(는) 새로 고침이 대기된 후에 반환됩니다. 워크스테이션에서 검사를 실행하지 않습니다.

다음 조건 중 하나가 참인 경우에만 **다시 쓰기** 새로 고침이 등록된 호스트 키:

* 등록된 호스트 키가 누락되었습니다.
* 등록된 호스트 키가 비어 있음
* 등록된 호스트 키를 읽을 수 없음
* 등록된 호스트 키의 유효성 검사 실패
* 새 검사가 등록된 키와 다른 호스트 키 행을 반환합니다.
* 스캔의 지문과 등록된 키가 일치하지 않음

등록된 키가 최신 상태이고 유효하면 변경하지 않고 새로 고침이 완료됩니다.

>[!TIP]
>
>팀이 베이션에서 SSH 호스트 키를 회전하고 베이션 호스트 이름 또는 IP를 변경하거나 SSH 끝점을 바꾼 후 **[!UICONTROL Refresh SSH Host Keys]**&#x200B;을(를) 실행합니다. 잠시 기다린 후 **[!UICONTROL Save & Test]**&#x200B;을(를) 실행하여 연결을 확인합니다.

## 계정 마이그레이션 {#migration}

계정 마이그레이션을 트리거하지 않습니다. Adobe은 유지 관리 또는 크기 조정 중에 데이터 서버 이동을 수행하고 등록된 SSH 호스트 키를 복사하므로 이동 후에도 엄격한 확인이 계속 작동합니다.

Adobe에서 마이그레이션이 완료되었다는 알림을 받은 후:

1. **[!UICONTROL Save & Test]**&#x200B;을(를) 실행하여 연결을 확인합니다. 키가 성공적으로 복사된 경우 등록을 건너뜁니다.
1. SSH 호스트 키 오류가 지속되면 관리자에게 **[!UICONTROL Refresh SSH Host Keys]**&#x200B;을(를) 실행하도록 요청하고 몇 분 기다린 다음 **[!UICONTROL Save & Test]**&#x200B;을(를) 다시 실행하십시오.
1. **[!UICONTROL Save & Test]**&#x200B;번 및 최대 두 번의 **[!UICONTROL Refresh SSH Host Keys]**&#x200B;번 시도 후에도 오류가 계속되면 Adobe 지원 팀에 문의하십시오.

## SSH 호스트 키 오류 메시지 {#ssh-host-key-errors}

연결 상태는 사용자에게 친숙한 단일 SSH 호스트 키 메시지를 보여 줍니다. 원시 OpenSSH 오류는 대시보드에 표시되지 않습니다.

다음 표에는 일반적인 메시지가 가능한 원인 및 일반적인 다음 단계에 매핑되어 있습니다.

| 메시지 또는 상태 | 의미 | 가능한 원인 | 일반적인 다음 단계 |
| --- | --- | --- | --- |
| SSH 호스트 키 확인 실패 | 요새 호스트 키가 등록된 키와 일치하지 않거나 트러스트 자료를 사용할 수 없습니다. | SSH 호스트 키가 베이션에서 회전됨, 베이션 호스트 이름, IP 또는 포트가 변경됨, 등록된 키가 누락, 비어 있음, 잘못됨 또는 읽을 수 없음 | **원격 주소** 및 **SSH 포트**&#x200B;를 확인합니다. 인프라 팀에 Bastion 호스트 키가 변경되었는지 문의하십시오. 관리자에게 **[!UICONTROL Refresh SSH Host Keys]**&#x200B;을(를) 실행하도록 요청하여 몇 분 기다린 다음 **[!UICONTROL Save & Test]**&#x200B;을(를) 실행합니다. |
| SSH 호스트 키를 등록할 수 없습니다. | **[!UICONTROL Save & Test]**&#x200B;에서 저장소 호스트 키를 검사하거나 저장할 수 없습니다. | Adobe 인프라에서 요새에 연결할 수 없음, DNS 오류, 방화벽이 [!DNL Commerce Intelligence] IP 주소를 차단함, 잘못된 **원격 주소** 또는 **SSH 포트**, 요새에서 호스트 키 검사 오류 | 데이터베이스 자격 증명 페이지에서 [!DNL Commerce Intelligence] IP 주소를 사용하여 방화벽 허용 목록에 추가를 확인합니다. 베이션이 구성된 포트에서 SSH를 허용하는지 확인합니다. 연결 필드를 수정하고 **[!UICONTROL Save & Test]**&#x200B;을(를) 다시 실행하십시오. |
| SSH 호스트 키가 없거나 잘못되었습니다. | 등록된 트러스트 자료가 없거나 손상되어 엄격한 확인으로 터널이 차단되었습니다. | 첫 번째 연결이 등록을 완료하지 않음, 이전 새로 고침 실패, 마이그레이션이 키를 복사하지 않음, Adobe 인프라 문제 | 관리자에게 **[!UICONTROL Refresh SSH Host Keys]**&#x200B;을(를) 실행한 다음 **[!UICONTROL Save & Test]**&#x200B;을(를) 실행하도록 요청하십시오. 오류가 지속되면 지원 센터에 문의하십시오. |
| SSH 호스트 키 새로 고침을 완료할 수 없음 | 새로 고침이 등록된 키를 업데이트하지 않았습니다. | 새로 고침 중 네트워크, DNS 또는 스캔 실패, Adobe 인프라 문제 | 몇 분 정도 기다리세요. 관리자에게 **[!UICONTROL Refresh SSH Host Keys]**&#x200B;을(를) 다시 실행하도록 요청하십시오(첫 번째 작업이 실패한 경우 두 번째 시도). 요새에 연결할 수 있는지 및 허용 목록에 추가를 확인합니다. 새로 고침을 두 번 시도하고 **[!UICONTROL Save & Test]**&#x200B;을(를) 시도한 후에도 연결에 계속 실패하는 경우 지원 센터에 문의하십시오. |

## 문제 해결 체크리스트 {#troubleshooting}

1. **원격 주소**, **SSH 포트** 및 Linux 사용자 설정이 기준 설정과 일치하는지 확인하십시오.
1. 방화벽에서 데이터베이스 자격 증명 페이지에 표시되는 [!DNL Commerce Intelligence] IP 주소를 허용하는지 확인하십시오.
1. 인프라 팀에 베이스의 SSH 호스트 키가 최근에 변경되었는지 확인합니다.
1. 아직 설정이 없는 경우 **[!UICONTROL Save & Test]**&#x200B;을(를) 실행하여 설정의 유효성을 검사하고 키를 등록하십시오.
1. 관리자에게 **[!UICONTROL Refresh SSH Host Keys]**&#x200B;을(를) 실행하도록 요청하고 몇 분 정도 기다린 후 **[!UICONTROL Save & Test]**&#x200B;을(를) 다시 실행하십시오. 첫 번째 새로 고침으로 오류가 해결되지 않으면 이 단계를 반복합니다.
1. 두 번 새로 고친 후에도 연결에 SSH 호스트 키 오류가 계속 표시되면 연결 페이지(또는 계정 지원 채널)에서 **[!UICONTROL Contact Support]**&#x200B;을(를) 클릭합니다.

## Adobe 지원에 문의해야 하는 경우 {#contact-support}

다음의 경우 지원 센터에 문의:

* 관리자가 **[!UICONTROL Refresh SSH Host Keys]**&#x200B;을(를) 두 번 실행하고 **[!UICONTROL Save & Test]**&#x200B;이(가) 실패한 후에도 SSH 호스트 키 오류가 계속됩니다.
* **[!UICONTROL Refresh SSH Host Keys]**&#x200B;이(가) 완료되지 않거나 15~30분 후에도 연결 상태가 변경되지 않습니다.
* Adobe에서 계정 마이그레이션 또는 데이터 서버 유지 관리에 대해 알린 직후 오류가 시작되었습니다
* 베이션 설정 및 방화벽 허용 목록에 추가가 올바르며 팀이 호스트 키를 회전하지 않았으므로 계속 연결할 수 없습니다.
* **[!UICONTROL Refresh SSH Host Keys]**&#x200B;을(를) 실행하려면 관리자가 필요하지만 계정에 사용 가능한 관리자가 없습니다.

연결 이름, 마지막 **[!UICONTROL Save & Test]** 또는 새로 고침 시도의 대략적인 시간 및 요새 호스트 키가 최근에 변경되었는지 여부를 포함합니다. 개인 키 또는 암호를 보내지 마십시오.

## 관련 항목 {#related}

* [SSH 터널을 통해 MySQL 연결](mysql-via-ssh-tunnel.md)
* [SSH 터널을 통해 MongoDB 연결](mongodb-via-ssh-tunnel.md)
* [SSH 터널을 통해 PostgreSQL 연결](postgresql.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
