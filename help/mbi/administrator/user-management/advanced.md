---
title: 고급 사용자 관리
description: 데이터 가시성 향상, 보고 간소화, 사용자 그룹별 맞춤식 액세스, 대시보드 공유 간소화, 조직의 보안 및 확장성 보장
role: Admin, User
feature: User Management
source-git-commit: 42871886d12b97ee52aa270da6f0186a9a4eaddc
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---


# 고급 사용자 관리

[!DNL Advanced User Management] 기능은 향상된 데이터 가시성 컨트롤을 제공하며 사용자 그룹(조직 영역)을 기반으로 논리적 데이터 필터링을 지원합니다. 이를 통해 사용자 그룹에 따라 데이터 가시성을 조정할 수 있으며, 비즈니스가 새로운 지역으로 확장될 때마다 지역별 보고 요구 사항을 충족하기 위해 기존 대시보드의 복제본을 생성할 필요가 없습니다.

[!DNL Advanced User Management]은(는) 대규모 조직의 보안 및 확장성을 보장하면서 대시보드 공유 및 데이터 가시성을 간소화합니다. 사용자 그룹, 역할 및 권한을 유연하게 구성할 수 있으므로 Commerce Intelligence은 엔터프라이즈 수준 요구 사항을 위한 강력한 도구입니다.

[!DNL Advanced User Management]이(가) 활성화되면 관리 사용자만 다음을 설정할 수 있습니다.

- 지표
- Visual Report Builder
- SQL 기반 보고서
- 이메일 요약
- 원시 내보내기

## 기능 매트릭스

[!DNL Advanced User Management]은(는) Commerce Intelligence의 여러 기능에 영향을 줍니다. 다음 표에서는 활성화 또는 비활성화되는 기능에 따라 다양한 역할에 대한 기능, 권한 및 사용 가능 여부에 대해 설명합니다.

<table><thead>
  <tr>
    <th colspan="3" rowspan="2">Commerce Intelligence 기능</th>
    <th colspan="6">AUM(고급 사용자 관리) 기능</th>
  </tr>
  <tr>
    <th colspan="3">비활성화됨</th>
    <th colspan="3">활성화됨</th>
  </tr></thead>
<tbody>
  <tr>
    <td>기능 그룹</td>
    <td>기능</td>
    <td>권한</td>
    <td>관리자</td>
    <td>표준</td>
    <td>읽기 전용</td>
    <td>관리자</td>
    <td>표준</td>
    <td>읽기 전용</td>
  </tr>
  <tr>
    <td rowspan="7">사용자 관리(모든 관리자가 액세스할 수 있으며 모든 역할에 영향)</td>
    <td>사용자 그룹 구성</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>사용자 초대</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>권한 탭 - 역할 매핑</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>권한 탭 - 사용자 그룹 매핑 (AUM)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>권한 탭 - 저장소 하위 집합 매핑(AUM)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>지표 탭</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>공유 대시보드 탭</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Report Builder</td>
    <td>Visual Report Builder</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>SQL REPORT BUILDER</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">이메일 요약</td>
    <td>데이터 분할 없이 이메일 요약 만들기</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>AUM(데이터 분할)을 사용하여 이메일 요약 만들기</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="4">대시보드  - 공유</td>
    <td>여러 역할에서 사용자와 대시보드 공유</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>AUM(사용자 그룹 및 관리자)과 대시보드 공유</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">대시보드 공유 - 권한</td>
    <td>편집</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>보기</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="18">대시보드 - 보기(주어진 권한으로 공유 대시보드 열기)</td>
    <td rowspan="2">공유 대시보드 다시 공유</td>
    <td>편집</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>보기</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">날짜 필터(EDIT TIME Options 기능 플래그 없음)</td>
    <td>편집</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>보기</td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">날짜 필터(EDIT TIME Options 기능 플래그 포함)</td>
    <td>편집</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>보기</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
  </tr>
  <tr>
    <td rowspan="2">저장소 필터(EDIT TIME Options 기능 플래그 없음)</td>
    <td>편집</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>보기</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">저장소 필터(EDIT TIME Options 기능 플래그 포함)</td>
    <td>편집</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>보기</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">대시보드 데이터 - AUM(사용자 그룹 매핑)을 기반으로 보고서 데이터 필터링</td>
    <td>편집</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>보기</td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
  </tr>
  <tr>
    <td rowspan="2">보고서 - 편집</td>
    <td>편집</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>보기</td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">보고서 내보내기(CSV, XLSX)</td>
    <td>편집</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>보기</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
  </tr>
  <tr>
    <td rowspan="2">보고서 - 원시 내보내기</td>
    <td>편집</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>보기</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</tbody></table>

## 관리자 제어

관리자는 다음 작업을 관리할 수 있습니다.

- 사용자 그룹 구성
- 개별 사용자에게 역할 및 사용자 그룹 할당
- 대시보드 수준 권한을 가진 사용자 그룹 또는 다른 관리자와 대시보드 공유
- 사용자 그룹 수준의 데이터 필터링을 사용하여 이메일 요약 예약

### 사용자 그룹 구성

사용자 그룹은 특정 저장소 필터에 매핑된 영역의 논리 그룹입니다(예: 대륙, 국가 및 지역 이름을 기반으로 생성된 사용자 그룹).

사용자 그룹을 구성하려면 다음 작업을 수행하십시오.

1. 기존 사용자 그룹을 보려면 [!UICONTROL **사용자 관리**] > [!UICONTROL **User Groups]**로 이동하십시오.

   ![사용자 그룹 구성](../../assets/configure-user-groups.png)

1. [!UICONTROL **그룹 추가**]&#x200B;를 통해 관리자는 새 사용자 그룹을 만들 수 있습니다.

   - 그룹 이름을 입력합니다(예: &quot;Americas&quot;).

   - 사용자 그룹과 관련된 저장소 또는 필터를 선택합니다.

   - 구성을 저장합니다.

     ![사용자 그룹 추가](../../assets/add-group.png)

1. 관리자는 다음 작업을 수행할 수 있습니다.

   - 사용자 그룹을 편집하여 저장소 매핑을 업데이트하거나 명확하게 하기 위해 이름을 변경합니다.

   - 더 이상 필요하지 않은 사용자 그룹을 삭제합니다. 관리자는 삭제된 사용자 그룹에 매핑된 기존 사용자를 수동으로 다시 할당해야 합니다.

1. 기본 그룹:

   - [!UICONTROL **None]**: 아직 특정 그룹에 매핑되지 않은 사용자에 대한 대체 그룹입니다. 이러한 사용자는 적절한 그룹에 할당될 때까지 데이터를 볼 수 없습니다.

   - [!UICONTROL **모두**]: 모든 데이터에 무제한 액세스를 제공합니다(일반적으로 관리자 사용자용으로 예약됨).

### 사용자 그룹에 사용자 할당

관리자는 [!UICONTROL **사용자 초대**]&#x200B;를 사용하여 온보딩 중에 새 사용자를 관련 그룹에 매핑할 수 있습니다. 기존 사용자는 비즈니스 요구 사항에 따라 사용자 그룹에 다시 매핑할 수 있습니다.

![사용자 그룹에 사용자 할당](../../assets/assign-users-to-groups.png)

>[!TIP]
>
>- [!UICONTROL **Standard**] 또는 [!UICONTROL **읽기 전용**] 사용자가 관련 사용자 그룹에 할당될 때까지 대시보드 데이터에 실수로 액세스하지 않도록 [!UICONTROL **None**]&#x200B;에 할당하는 것이 안전합니다.
>
>- 비즈니스 요구 사항에 따라 사용자에게 권한을 할당하는 동안 그룹 내의 특정 저장소를 제한하여 향상된 제어를 할 수 있습니다.

관리자 사용자는 항상 기본적으로 [!UICONTROL **모든**] 저장소에 매핑되어 전체 저장소 보기로 대시보드를 볼 수 있습니다.

### 대시보드 공유

[!DNL Advanced User Management]은(는) 데이터 보안을 유지하면서 대시보드를 공유할 수 있는 강력한 옵션을 제공합니다.

- 관리자는 사용자 그룹은 물론 다른 관리 사용자와 대시보드를 공유하여 공동 작업을 수행할 수 있습니다. 이를 통해 대시보드를 중앙 집중식으로 관리하고 대규모 조직의 관리를 간소화합니다.

  ![대시보드 공유](../../assets/share-dashboards.png)

- 대시보드 공유 권한에는 다음이 포함됩니다.

   - [!UICONTROL **편집**]: 관리 사용자만 대시보드를 수정하거나, 데이터를 필터링하거나, 보고서를 수정하거나, 데이터를 내보낼 수 있습니다.

   - [!UICONTROL **보기**]: (특정 제한 사항)이 있는 모든 역할의 사용자가 사용할 수 있습니다.

   - [!UICONTROL **없음**]: 특정 사용자 그룹 또는 관리자에 대한 대시보드 액세스를 취소합니다.

  >[!NOTE]
  >
  >다양한 조합을 이해하기 위해 규칙 및 대시보드 권한에 따라 다양한 Commerce Intelligence 기능을 사용하려면 [기능 매트릭스](#feature-matrix)를 참조하세요.

#### 대시보드 보기

관리자 사용자는 모든 스토어에 대한 액세스 권한으로 대시보드 데이터를 볼 수 있습니다.

![대시보드 관리자 보기](../../assets/view-dashboard-admin.png)

그러나 사용자는 사용자 구성 중에 매핑된 저장소를 기반으로 필터링된 대시보드 데이터를 볼 수 있습니다.

![대시보드 관리자 보기](../../assets/view-dashboard-user.png)

>[!TIP]
>
>관리자는 공유 대시보드에 대한 날짜 필터를 활성화하여 사용자가 보고서 생성 중에 설정된 기본 시간 범위 대신 다양한 날짜 범위의 데이터를 볼 수 있도록 할 수 있습니다. 이 기능은 비즈니스 요구 사항에 따라 켜거나 끌 수 있습니다.

### 이메일 요약 예약

[!DNL Advanced User Management]이(가) 데이터 필터링 기능을 전자 메일 요약으로 확장합니다. 대상자에 따라 관리 사용자는 선택한 보고서를 필터링해야 하는 사용자 그룹을 지정할 수 있습니다.

![전자 메일 요약 예약](../../assets/schedule-email-summary.png)
