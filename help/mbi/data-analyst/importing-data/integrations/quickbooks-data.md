---
title: 예상 QuickBook 데이터
description: 분석을 위해 관련 데이터 필드를 쉽게 추적하는 방법에 대해 알아봅니다.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# [!DNL QuickBooks]개의 데이터가 필요합니다.

[계정 [!DNL QuickBooks] 연결](../../../data-analyst/importing-data/integrations/quickbooks.md)한 후 [Data Warehouse 관리자](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)를 사용하여 분석을 위해 관련 데이터 필드를 쉽게 추적할 수 있습니다. Data Warehouse에 다음 테이블이 만들어집니다.

추적에 사용할 수 있는 모든 필드를 보려면 테이블 이름 열의 링크를 클릭합니다.

## 거래 엔티티 {#transactionentities}

| **테이블 이름** | **설명** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | `bills` 테이블에는 AP 거래에 대한 정보 또는 서드파티의 결제 요청이 포함되어 있습니다. 속성에는 통화 유형, 환율, 총 금액, 만기 일자, 잔액 등이 포함됩니다. |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | `BillPayment` 엔터티는 공급업체로부터 받은 청구서의 최종 결제 거래입니다. 이 테이블에는 공급업체 정보, 결제 유형, 총 금액, 거래 일자 등이 포함됩니다. |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | `creditmemos` 테이블은 전체 및 부분 지급의 환불 또는 대변인 거래를 기록합니다. 일부 속성에는 고객 이름, 고객의 청구 및 배송 정보, 금액 및 날짜가 포함됩니다. |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits`에는 `Undeposited Funds` 계정에 보관된 후 Asset 계정으로 이동된 계좌 입금 및 고객 결제가 포함됩니다. 속성에는 금액, 예금 ID 및 날짜가 포함됩니다. |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates`은(는) 상품 또는 서비스에 대해 제안된 가격을 포함하는 고객에게 제공되는 거래입니다. 이 테이블에는 금액, 할인 정보, 고객 정보 및 일자가 기록됩니다. |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices`은(는) 고객이 나중에 지불하는 판매 양식입니다. 송장 테이블에는 모든 예금 정보, 일자, 라인 항목, 세금 정보 및 고객 정보가 기록됩니다. |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | `journalentries` 테이블은 저널 항목 ID, 트랜잭션 날짜 및 라인 항목 정보를 포함하여 AR 및 AP 계정 정보를 기록합니다. |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | `payment` 레코드에는 결제 ID, 적용된 금액 및 적용되지 않은 금액, 트랜잭션 날짜, 트랜잭션 유형 및 처리 상태와 같은 특성이 포함됩니다. |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | `purchases` 테이블은 비용을 나타내며 구매 ID, 결제 유형, 금액 및 모든 라인 항목 정보를 포함합니다. |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | `purchaseorders` 테이블에는 공급업체에 보낸 제품에 대한 요청이 들어 있습니다. 이 테이블에는 공급업체 정보, 구매 발주 ID, 트랜잭션 일자, 라인 품목 정보, 총액 및 AP 계정 정보가 포함됩니다. |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | `refundreceipts` 테이블은 고객에게 제공된 환불을 기록합니다. 속성에는 환불 수금 ID, 라인 품목 정보, 총 금액, 고객 정보 및 잔고가 포함됩니다. |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | `salesreceipts` 테이블은 고객에게 제공된 판매 영수증에 판매 영수증 ID, 품목 정보, 총액, 고객 정보, 거래 일자 및 예금을 포함하여 정보를 기록합니다. |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | `timeactivities` 테이블에는 공급업체 및/또는 직원의 시간 기록이 있으며 시간 활동 ID, 직원/공급업체 정보, 기록된 시간, 활동 설명 및 기록된 날짜가 포함됩니다. |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | `transfers` 테이블은 계정 간에 이동된 자금에 대한 정보를 기록합니다. 속성에는 이전 ID, 금액, 계정 정보 및 날짜가 포함됩니다. |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | 공급업체 크레딧은 환불 또는 공급업체에 제공된 크레딧인 AP 거래입니다. `vendorcredits` 테이블에는 공급업체 신용 ID, 품목 정보, 공급업체 정보, AP 계정, 총 금액 및 날짜가 포함됩니다. |

{style="table-layout:auto"}

## 이름 목록 엔티티 {#namelistentities}

| **테이블 이름** | **설명** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | 이 표에는 계정 ID, 이름, 상태, 유형, 잔액, 통화 및 생성 시간이 포함되어 있습니다. |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | 이 테이블은 예산 ID, 이름, 시작 및 종료 일자, 유형, 상태 및 상세내역을 포함하여 회사 예산과 관련된 모든 정보를 기록합니다. |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | 거래의 세부 정보 라인에 적용된 클래스를 사용하면 클라이언트나 프로젝트에 연결되지 않은 세그먼트를 추적할 수 있습니다. 이 테이블은 클래스 ID, 이름, 하위 클래스 및 상태를 기록합니다. |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | `customers` 테이블에는 고객의 ID, 이름, 청구 및 배송 주소, 전화 번호 및 전자 메일 주소를 포함하여 고객과 관련된 모든 정보가 들어 있습니다. |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | `departments` 테이블에는 부서 ID, 이름 및 유형(하위 부서와 최상위 부서)이 포함됩니다. |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | `employees` 테이블은 회사에 근무하는 사람들에 대한 정보를 기록합니다. 급여가 사용되는 회사의 경우 속성에는 사원 ID, 이름, 주소, 전화번호 및 청구 가능 정보가 포함됩니다. |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | `items` 테이블에는 회사에서 판매하는 제품 또는 서비스에 대한 세부 정보가 포함되어 있습니다. 이 테이블에는 품목 ID, 이름, 내용, 단가, 유형, 구매 정보, 현재고 수량, 소득 및 자산 계정 정보가 포함됩니다. |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | `paymentmethods` 테이블은 재화와 서비스에 대해 받은 결제 방법을 기록합니다. 여기에는 결제 ID, 유형 및 이름이 포함됩니다. |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | 이 테이블은 세무서 ID를 포함하여 세무서에 대한 정보와 구매 및 판매에 대한 세금에 대한 추적 정보를 기록합니다. |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | 세금 코드는 제품, 서비스 및 고객의 세금 상태(과세 및 비과세)를 추적하는 데 사용됩니다. `taxcodes` 테이블에는 세금 코드 ID, 이름, 설명, 상태, 과세 상태, 세율 및 세금 그룹이 포함됩니다. |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | 세율은 조세 부채를 계산하는 데 사용됩니다. 이 테이블에는 세율 ID, 이름, 설명, 세율, 세금 기관 등이 포함됩니다. |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | 이 개체는 판매가 이루어지는 조건을 나타냅니다. 용어 테이블에는 용어 ID, 이름, 유형, 할인율 및 만기일이 포함됩니다. |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | 공급업체 테이블에는 구매하는 공급업체에 대한 정보가 포함되어 있습니다. 테이블 속성에는 공급업체 ID, 회사 이름, 계정 번호, 계정 잔액, 1099 상태, 청구 주소, 전화 번호, 이메일 주소 및 웹 주소가 포함됩니다. |

{style="table-layout:auto"}

## 관련 항목:

* [ [!DNL QuickBooks] 연결 중](../integrations/quickbooks.md)
* [통합 재인증](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ko)
