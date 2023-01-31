---
title: SQL 계산된 열 생성 및 사용
description: 새 MBI 아키텍처에 있는 SQL 계산 열 형태로 고급 열을 만드는 방법을 알아봅니다.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# SQL 계산된 열 만들기

이 항목에서는 의 목적과 사용에 대해 간략하게 설명합니다 `Calculation` 열 유형: 를 사용하여 표에 추가할 수 있습니다. [Data Warehouse 관리자](../data-warehouse-mgr/tour-dwm.md). 다음은 SQL 계산의 동작, 계산 사용 이유, SQL 계산 생성 프로세스 및 두 가지 예에 대한 설명입니다.

**설명**

과거에, `advanced` 의 고객 성공 팀의 분석가가 수행해야 합니다. [!DNL MBI]. 이제 모든 전원이 최종 사용자에게 전달되며 고급 열은 `SQL Calculation` 새 페이지의 열 [!DNL MBI] 아키텍처.

다음 `Calculation` 이제 Data Warehouse 관리자에서 옵션으로 사용할 수 있는 열 유형은 PostgreSQL 논리를 사용하여 테이블의 열을 변형할 수 있는 동일한 테이블 작업입니다. 에서 사용할 수 있는 함수 및 연산자에 대한 설명서입니다. `Calculatio`n 열 유형은 PostgreSQL 웹 사이트에서 찾을 수 있습니다. [여기](https://www.postgresql.org/docs/9.6/static/functions.html).

로 만들 수 있는 다양한 열 `Calculation` 열은 거의 무제한으로 만들어지지만 대부분의 열은 IF-THEN 문과 기본 산술 값을 사용하여 만들 수 있으며 아래 예제에 사용됩니다.

**예제 1: 고객의 마지막 주문입니까?**

대부분의 계정에는 `Is customer's last order?` 그들의 `orders` 반복 구매율 및 조정된 고객에 대한 분석을 수행하는 테이블입니다. 계정이 새 아키텍처에 있는 경우 이 열은 `Calculation` 열이 있고 아래 스크린샷에 표시될 수 있습니다.

![](../../assets/Is_customer_s_last_order.png)

다음 `Is customer's last order?` 열은 입력을 사용합니다 `Customer's lifetime number of orders` 및 `Customer's order number` 별칭 `A` 및 `B` 각각 사용할 수 있습니다.

라인별, PostgreSQL의 의미:

* 사례: 이렇게 하면 일련의 If - Then 문이 시작됩니다
* when `A` is null 또는 `B` null이면 null입니다. 입력이 비어 있으면 출력도 비어 있어야 합니다. SQL 오류를 방지하기 위한 것입니다
* when `A=B` 그런 다음 `Yes`: If `Customer's lifetime number of orders` 다음과 같음 `Customer's order number` 이 행에 대해 를 반환한 다음 `Yes`. 고객이 4개의 주문을 제출하면 4번째 주문에 대한 행이 반환됩니다 `Yes` 대상 `Is customer's last order?`
* else `No`: 문이 충족될 때 다른 문이 없으면 를 반환합니다 `No`
* 종료: 이렇게 하면 If - Then 문이 종료됩니다

이 열(`NULL`, `Yes`, `No`)에는 숫자가 아닌 문자가 포함되어 있으므로 여기에서 데이터 유형은 String입니다.

**예제 2: 주문 품목 합계 값(수량 * 가격)**

많은 Adobe 고객은 품목 수준에서 매출을 분석하여 다음과 같은 필드에 따라 분류하고 싶어합니다 `product name` 또는 `category`. 대부분의 데이터베이스는 실제로 제품 수익을 순서대로 제공하지 않습니다. 대신 주문 판매량과 품목 가격을 제공합니다.

제품 매출 분석을 활성화하기 위해 대부분의 계정에는 `Order item total value (quantity * price)` 그들의 `Orders Items` 테이블. 계정이 새 아키텍처에 있는 경우 이 열도 `Calculation` 열이 있고 아래 스크린샷에 표시될 수 있습니다.

![](../../assets/Order_item_total_value.png)

상거래 스키마에서 `Order item total value (quantity * price)` 열은 입력을 사용합니다 `qty ordered` 및 `base price` 별칭 `A` 및 `B` 각각 사용할 수 있습니다.

이 새 열에서 반환되는 값은 1달러 및 1센트이므로 올바른 데이터 유형은 다음과 같습니다. `Decimal(10,2)`.

**역학**

새로운 `Calculation` 열은 로 이동하여 테이블에 추가할 수 있습니다 **[!DNL Manage Data > Data Warehouse]** 아래와 같이 아래와 같습니다.

![](../../assets/blobid2.png)

여기에서 새 항목을 만들 수 있습니다 `Calculation` 열은 아래 단계에 따라 다릅니다.

1. 추가할 테이블을 선택합니다 `Calculation` 열.
1. 올바른 테이블에서 **[!UICONTROL Create New Column]** 화면 오른쪽 상단에 있습니다.
1. 에서 `Select a definition` 드롭다운, 선택 `Same Table`.
1. 선택 `Calculation` 로서의 `column definition equation`.
1. 열 이름을 입력합니다.
1. 을(를) 선택합니다 `input` 새 열에 대한 논리에 사용할 테이블의 열. 추가하는 각 열에는 문자 별칭이 부여되므로 첫 번째 열은 `A`로 설정되면 두 번째는 `B` 기타.
1. 창에서 입력의 문자 별칭을 사용하여 새 열에 대한 PostgreSQL 논리를 입력합니다. SQL 계산은 SQL 쿼리의 SELECT 및 FROM 문 사이의 모든 논리를 포함하여 단일 열 정의로 제한해야 합니다. 입력 문자를 사용하는 SQL 키워드는 소문자로 입력해야 합니다. 예를 들어 `CASE` 문, 소문자로 작성해야 합니다. - `case`. 시스템은 대문자로 가정합니다 `A` 는 입력 중 하나를 나타냅니다.
1. 적절한 데이터 유형을 선택합니다.
   * `Integer` - 전체 번호
   * `Decimal(10,2)` - 총숫자가 10개인 십진수 중 그 숫자는 소수점 오른쪽에 있습니다
   * `String` - 숫자를 사용하지 않는 모든 유형의 텍스트 또는 일련의 문자
   * `Datetime` - yyyy-MM-dd hh:mm:s 형식

1. 클릭 **[!UICONTROL test column]**. 이렇게 하면 각 입력에 대해 5개의 테스트 값 목록이 생성되고, 각 테스트 값 세트에 대해 6단계의 논리 결과가 표시됩니다. SQL의 어떤 부분에서든 오류가 발생하면 해당 오류 메시지가 반환됩니다. 모든 입력 열이 기본 필드인 경우에만 샘플 결과를 생성할 수 있습니다. 입력 열이 계산된 경우 지표를 추가하고 시각적 Report Builder에서 보기를 수행하여 결과를 확인해야 합니다
1. 결과에 만족하면 **[!UICONTROL Save]**, 및 열을 사용할 수 있습니다.
