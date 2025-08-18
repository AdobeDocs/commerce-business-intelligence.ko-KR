---
title: Report Builder 선택
description: Report Builder를 선택하는 방법을 알아봅니다.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Report Builder 선택

>[!NOTE]
>>[관리자 권한](../../administrator/user-management/user-management.md)이 필요합니다.

이제 분석을 만드는 데 사용할 수 있는 옵션이 더 많으므로 필요에 맞는 Report Builder의 기능을 정확히 아는 것이 어려울 수 있습니다. 이 항목에서는 분석을 작성하는 가장 좋은 방법을 선택하는 과정을 안내합니다.

## [!DNL SQL Report Builder]은(는) 언제 사용해야 합니까? {#whensql}

[!DNL SQL Report Builder]에서 [!DNL traditional Report Builder]을(를) 사용하는 일반적인 이유 중 일부를 살펴보십시오.

### [!DNL SQL]별 함수를 사용하려는 경우...

[!DNL SQL Report Builder]의 장점 중 하나는 현재 Data Warehouse 관리자에서 사용할 수 없는 기능을 사용할 수 있다는 것입니다. 과거에는 분석가가 여러분의 비전을 완전히 실현할 수 있도록 도와주기 위해 개입해야 했을 수도 있습니다.

[!DNL SQL Report Builder]은(는) 이전에 사용할 수 없었던 [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) 및 [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html)과(와) 같은 함수를 지원합니다. [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html)에 액세스할 수 있지만 일부 다른 SQL 관련 함수에는 다음이 포함됩니다.

* [`Bitwise aggregate`개 함수](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` 연산자](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### 테스트를 수행하려는 경우...

분석에 가장 적합한 방법을 찾기 위해 다양한 기술과 전략을 시도하려는 경우 [!DNL SQL Report Builder]을(를) 사용할 수 있습니다. Data Warehouse Manager에서 열을 작성하려면 시간이 걸리고 DWM을 사용하여 만드는 열은 업데이트 주기에 따라 다릅니다.

기껏해야 열을 사용하기 전에 하나의 업데이트 주기를 기다려야 합니다. 열을 잘못 작성한 경우 *2* 주기 동안 기다려야 합니다. 하나는 처음에 열을 채우고 다른 한 주기는 수정 내용을 전파합니다.

### 새 열을 한 번만 사용하는 경우

위의 섹션에서 언급했듯이 Data Warehouse Manager에서 열을 만드는 데에는 시간이 소요됩니다. 한 보고서에서 만든 열만 사용할 계획이라면 Adobe에서는 [!DNL SQL Report Builder]을(를) 사용하는 것이 좋습니다. 따라서 업데이트 주기가 완료될 때까지 기다릴 필요가 없어 보다 신속하게 작업을 수행할 수 있습니다.

### 일대다 관계가 있는 데이터로 작업하는 경우...

데이터 구조를 통해 [!DNL SQL Report Builder]을(를) 보다 효율적이고 논리적으로 선택하여 분석을 빌드할 수도 있습니다. 일대일 관계에 대한 열을 만드는 것은 Data Warehouse Manager에서 간단하지만, 일대다 관계를 처리할 때에는 상황이 약간 혼란스러울 수 있습니다.

단일 제품이 여러 제품 카테고리의 일부로 간주되며 각 제품의 각 카테고리와 관련된 수입을 보려 한다고 가정해 보겠습니다. DWM을 사용하여 이 관계를 만드는 것은 지루하고 어려울 수 있지만 [!DNL SQL] 쿼리를 작성하는 것이 좀 더 간단할 수 있습니다.

![](../../assets/When_should_I_use_the_RB_2.png)

## 언제 기존 Report Builder을 사용해야 합니까? {#whentraditionalrb}

[!DNL SQL Report Builder]을(를) 통해 이전에 사용할 수 없었던 기능에 대한 더 많은 제어와 액세스 권한을 얻을 수 있지만, 항상 올바른 선택은 아닐 수 있습니다. Adobe은 사용할 report builder의 향을 결정할 때 다음 사항도 고려하는 것이 좋습니다.

### 간단한 보고서를 작성하는 경우...

만들려는 내용이 간단하면 기존 Report Builder을 사용하는 것이 전체 [!DNL SQL] 쿼리를 작성하는 것보다 훨씬 빠를 수 있습니다. 이 기능은 분석을 생성해야 하는 열이 이미 Data Warehouse 관리자에 있는 경우에 유용합니다.

### 다른 사용자와 작업을 공유하는 경우...

조직 전체의 사용자가 이 분석을 사용/보고 있습니까? 작업을 누구와 공유하는지에 따라 시각적 Report Builder을 사용하는 것이 더 나을 수 있습니다. 사용자는 잠재적으로 긴 [!DNL Visual Report Builder] 쿼리를 읽는 대신 [!DNL SQL]의 정의를 빠르게 볼 수 있습니다.

보고서가 필요하지만 [!DNL SQL]에 익숙하지 않은 사람이 있다면 Adobe에서 Report Builder의 원래 맛을 사용할 것을 제안합니다. 그것은 그들에게 일을 더 쉽게 만듭니다.

## 요약 {#wrapup}

[!DNL SQL Report Builder]과(와) [!DNL Visual Report Builder] 모두 다양한 사용 사례에 적합합니다. 일반적으로 분석 요구 사항과 분석을 소비하는 사람에 따라 다릅니다.
