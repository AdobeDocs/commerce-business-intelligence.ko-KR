---
title: Report Builder 선택
description: Report Builder를 선택하는 방법을 알아봅니다.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Report Builder 선택

>[!NOTE]
>>필요한 경우 [관리자 권한](../../administrator/user-management/user-management.md).


우리는 모두 선택권이 있는 것을 좋아한다. 하지만, 선택에 직면했을 때, 우리 중 몇몇은 결정을 해야 한다는 생각에 주저하고 얼어버릴지도 모릅니다. 선택 사항은 훌륭하지만, 그것들은 또한 압도적이고 혼란스러울 수 있습니다.

분석을 만드는 데 더 많은 선택 사항이 있으므로 필요에 따라 Report Builder의 풍미를 정확히 식별하기가 어려운 경우가 있습니다. 분석을 빌드하는 가장 좋은 방법을 선택하는 방법에 대한 지침이 필요한 경우 이 문서를 사용하는 것입니다.

## 언제 을 사용해야 합니까 `SQL Report Builder`? {#whensql}

기존 Report Builder에서 SQL Report Builder을 사용하는 일반적인 이유 중 몇 가지를 살펴보십시오.

### SQL별 함수를 사용하려면..

Part of the beauty of the beauty `SQL Report Builder` 현재는 Data Warehouse 관리자에서 사용할 수 없는 기능을 사용할 수 있도록 해줍니다. 과거에, 분석가가 여러분이 자신의 비전을 완전히 실현할 수 있도록 돕기 위해 개입해야 했을 수도 있습니다.

SQL Report Builder은 [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) 및 [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html)- 이전에는 사용할 수 없었습니다. 에 액세스할 수 있습니다 [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html)그러나 일부 다른 SQL 관련 함수는 다음과 같습니다.

* [`Bitwise aggregate` 함수](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` 연산자](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### 테스트해 보려면..

분석에 가장 적합한 기법을 찾기 위해 다른 기법과 전략을 사용하려는 경우 `SQL Report Builder`. Data Warehouse 관리자에서 열을 작성하면 DWM을 사용하여 생성하는 시간과 열이 업데이트 주기에 따라 달라집니다.

가장 좋은 방법은 열을 사용하려면 한 개의 업데이트 주기를 기다려야 합니다. 칼럼을 만드는 데 실수를 한 것을 깨달으면, 끝까지 기다려야 할 것이다 *2개* 주기: 하나는 처음에 열을 채우고 다른 하나는 개정 전달을 위한 주기입니다.

### 새 열을 한 번만 사용하는 경우...

위의 섹션에서 언급했듯이 Data Warehouse 관리자에서 새 열을 만드는 데에는 시간이 소요됩니다. 한 보고서에서 만든 열을 사용하려고 계획하는 경우에는 `SQL Report Builder`. 따라서 업데이트 주기가 완료될 때까지 기다릴 필요가 없으므로 보다 신속하게 작업을 수행할 수 있습니다.

### 일대다 관계가 있는 데이터로 작업하는 경우...

경우에 따라 데이터 구조가 `SQL Report Builder` 분석을 빌드할 보다 효율적이고 논리적인 선택. Data Warehouse 관리자에서 일대일 관계에 대한 열을 만드는 것은 매우 간단하지만 일대다 관계를 처리할 때는 약간 혼동될 수 있습니다.

단일 제품이 여러 제품 카테고리의 일부로 간주되며 각 제품의 각 카테고리와 연관된 매출을 보려는 경우 DWM을 사용하여 이 관계를 만들려고 하는 것은 지루하고 어려울 수 있지만 SQL 쿼리를 작성하는 것은 보다 간단할 수 있습니다.

![](../../assets/When_should_I_use_the_RB_2.png)

## 기존 Report Builder은 언제 사용해야 합니까? {#whentraditionalrb}

반면에 `SQL Report Builder` 이전에 사용할 수 없었던 기능을 보다 효과적으로 제어하고 액세스할 수 있도록 해 줍니다. 이 기능이 항상 올바른 것은 아닐 수 있습니다. 사용할 Report Builder의 향을 결정할 때 다음 사항을 고려해 보는 것이 좋습니다.

### 간단한 보고서를 작성하는 경우...

만들려는 것이 간단한 경우 기존 Report Builder을 사용하면 전체 SQL 쿼리를 작성하는 것보다 훨씬 빠르게 작업할 수 있습니다. 분석을 만들어야 하는 열이 Data Warehouse 관리자에 이미 있는 경우에도 도움이 됩니다.

### 작업을 다른 사용자와 공유할 경우...

조직 전체의 사용자가 이 분석을 사용/보고 있습니까? 작업을 공유하는 사람에 따라 Visual Report Builder을 사용하는 것이 일부 경우에 더 나을 수 있습니다. 사용자는 시각적 Report Builder에서 정의를 빠르게 볼 수 있으며, 이는 잠재적으로 긴 SQL 쿼리를 읽는 것과 같습니다.

보고서가 필요하지만 SQL에 익숙하지 않은 사람이 있는 경우 Report Builder의 원래 맛을 사용하는 것이 좋습니다. 그것은 그들에게 상황을 더 쉽게 만들 것입니다.

## 포장 {#wrapup}

둘 다 `SQL Report Builder` 및 `Visual Report Builder` 다양한 사용 사례에 적합합니다. 일반적으로 분석 요구 사항이 무엇이고 분석을 누가 소비하는지에 따라 다릅니다.
