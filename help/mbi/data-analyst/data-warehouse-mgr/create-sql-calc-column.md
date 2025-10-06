---
title: SQL 계산 열 생성 및 사용
description: 새 Adobe Commerce Intelligence 아키텍처에서 고급 열을 SQL 계산 열 형태로 만드는 방법을 알아봅니다.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, SQL Report Builder, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# SQL 계산 열 만들기

이 항목에서는 `Calculation`Data Warehouse 관리자[를 사용하여 표에 추가할 수 있는 ](../data-warehouse-mgr/tour-dwm.md) 열 유형의 용도와 사용에 대해 간략하게 설명합니다. 아래에서는 SQL 계산의 기능, 계산 사용 이유, SQL 계산 생성 프로세스에 대해 설명하고 두 가지 예를 포함합니다.

**설명**

이전에는 `advanced`(으)로 간주되는 열을 [!DNL Adobe Commerce Intelligence]의 고객 지원 팀의 분석가만 수행할 수 있었습니다. 이제 모든 기능을 최종 사용자가 사용할 수 있으며 새 `SQL Calculation` 아키텍처에서 [!DNL Commerce Intelligence] 열 형태로 고급 열을 만들 수 있습니다.

이제 Data Warehouse 관리자에서 옵션으로 사용할 수 있는 `Calculation` 열 유형은 PostgreSQL 논리를 사용하여 테이블의 열을 변환할 수 있는 동일한 테이블 작업입니다. `Calculation` 열 유형에서 사용할 수 있는 함수 및 연산자에 대한 설명서는 PostgreSQL 웹 사이트 [여기](https://www.postgresql.org/docs/9.6/functions.html)에서 찾을 수 있습니다.

`Calculation` 열로 만들 수 있는 다른 열은 거의 무제한이지만 대부분의 열은 아래 예제에서 사용하는 IF-THEN 문과 기본 산술을 사용하여 만들 수 있습니다.

**예 1: 고객의 마지막 주문입니까?**

대부분의 계정에는 `Is customer's last order?` 테이블에 `orders`(이)라는 열이 있어 반복 구매율과 이탈된 고객에 대한 분석을 수행합니다. 계정이 새 아키텍처에 있는 경우 이 열은 `Calculation` 열을 사용하여 작성되며 아래 스크린샷에서 볼 수 있습니다.

고객의 마지막 주문을 식별하기 위한 ![SQL 계산 열 정의](../../assets/Is_customer_s_last_order.png)

`Is customer's last order?` 열은 각각 `Customer's lifetime number of orders` 및 `Customer's order number`(으)로 별칭이 지정된 입력 `A` 및 `B`을(를) 사용합니다.

PostgreSQL의 의미는 한 줄에 하나씩 표시됩니다.

* case: 일련의 If - Then 문이 시작됩니다.
* `A`이(가) null이거나 `B`이(가) null이면 null: 입력이 비어 있으면 출력도 비어 있어야 합니다. SQL 오류를 방지하기 위한 것입니다.
* `A=B`일 때 `Yes`: `Customer's lifetime number of orders`이(가) 이 행의 `Customer's order number`과(와) 같으면 `Yes`을(를) 반환합니다. 따라서 고객이 4개의 주문을 했다면 4번째 주문의 행은 `Yes`에 대해 `Is customer's last order?`을(를) 반환합니다.
* else `No`: 다른 when 문이 충족되지 않으면 `No`을(를) 반환합니다.
* end: If - Then 문을 종료합니다.

이 열(`NULL`, `Yes`, `No`)에서 반환할 수 있는 값에는 숫자가 아닌 문자가 포함되어 있으므로 여기에 있는 데이터 형식은 String입니다.

**예 2: 주문 항목 총 값(수량 * 가격)**

많은 클라이언트가 `product name` 또는 `category`과(와) 같은 필드로 슬라이스하여 항목 수준에서 매출을 분석하기를 원합니다. 대부분의 데이터베이스는 실제로 주문에서 제품의 수익을 제공하지 않습니다. 대신 주문에서 판매된 수량과 품목의 가격을 제공합니다.

제품 매출 분석을 활성화하기 위해 대부분의 계정에 `Order item total value (quantity * price)` 테이블에 `Orders Items`(이)라는 열이 있습니다. 계정이 새 아키텍처에 있는 경우 이 열도 `Calculation` 열을 사용하여 작성되며 아래 스크린샷에서 볼 수 있습니다.

![주문 항목 총 값에 대한 SQL 계산 열 정의](../../assets/Order_item_total_value.png)

Commerce 스키마에서 `Order item total value (quantity * price)` 열은 각각 `qty ordered` 및 `base price`(으)로 별칭이 지정된 `A` 및 `B` 입력을 사용합니다.

이 새 열에서 반환되는 값은 달러/센트 단위이므로 올바른 데이터 형식은 `Decimal(10,2)`입니다.

**기계**

아래와 같이 `Calculation`(으)로 이동하여 테이블에 새 **[!DNL Manage Data > Data Warehouse]** 열을 추가할 수 있습니다.

![계산된 열 결과를 보여 주는 표 보기](../../assets/blobid2.png)

여기에서 아래 단계에 따라 `Calculation` 열을 만들 수 있습니다.

1. `Calculation` 열을 추가할 테이블을 선택하십시오.
1. 올바른 테이블에 있는 동안 화면 오른쪽 상단의 **[!UICONTROL Create New Column]**&#x200B;을(를) 클릭합니다.
1. `Select a definition` 드롭다운에서 `Same Table`을(를) 선택합니다.
1. `Calculation`을(를) `column definition equation`(으)로 선택합니다.
1. 열 이름을 입력합니다.
1. 테이블에서 새 열의 논리에 사용되는 `input`개의 열을 선택합니다. 추가하는 각 열에는 문자 별칭이 있으므로 첫 번째 열은 `A`이고 두 번째 열은 `B`입니다.
1. 창에서 입력의 문자 별칭을 사용하여 새 열에 대한 PostgreSQL 논리를 입력합니다. SQL 계산은 SQL 쿼리의 SELECT 문과 FROM 문 사이의 모든 논리를 포함하는 단일 열 정의로 제한되어야 합니다. 입력 문자를 사용하는 SQL 키워드는 소문자여야 합니다. 예를 들어 `CASE` 문을 사용하는 경우 소문자로 작성해야 합니다. `case`. 시스템에서는 대문자 `A`이(가) 입력 중 하나를 참조한다고 가정합니다.
1. 적절한 데이터 유형을 선택합니다.
   * `Integer` - 정수
   * `Decimal(10,2)` - 총 10자리의 십진수이며, 이 중 2는 소수점 오른쪽에 있습니다.
   * `String` - 숫자가 아닌 모든 텍스트 유형 또는 일련의 문자
   * `Datetime` - `yyyy-MM-dd hh:mm:ss` 형식

1. **[!UICONTROL test column]**&#x200B;을(를) 클릭합니다. 이렇게 하면 각 입력에 대해 5개의 테스트 값 목록이 생성되고 각 테스트 값 세트에 대해 6단계의 논리 결과가 표시됩니다. SQL의 어느 부분에서든 오류가 발생하면 적절한 오류 메시지가 반환됩니다. 모든 입력 열이 기본 필드인 경우에만 샘플 결과를 생성할 수 있습니다. 입력 열이 계산된 열인 경우 지표에 열을 추가하고 Visual Report Builder에서 표시하여 결과를 확인해야 합니다

1. 결과가 만족스러우면 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다. 이 열은 을 사용할 수 있도록 설정합니다.
