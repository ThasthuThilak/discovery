---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 계약 구문 분석
{: #contract_parsing}

요소 분류는 식별된 각 요소에 대한 분석을 통해 구문 분석된 계약을 리턴합니다.

다음 절에서는 리턴된 JSON이 분석을 제공하는 방법에 대해 설명합니다. 

## 유형
{: #contract_types}

`types` 배열에는 다수의 오브젝트가 포함되며, 각각에는 요소의 커플릿을 식별하는 값을 가진 `nature` 및 `party` 키가 포함됩니다.

다음 표는 `nature` 및 `party` 키에 가능한 값을 나열합니다.

| `nature`         |설명                                                |
|:----------------:|-----------------------------------------------------------|
|`Definition`      |이 요소는 조항, 관계 또는 유사성에 대한 명확성을 추가합니다. 요소를 이행하는 데 필요한 조치는 없으며 영향을 주는 당사자도 없습니다.|
|`Disclaimer`      |요소의 `party`는 요소에서 지정한 조항을 이행할 의무가 없지만 이를 수행하는 것이 금지되어 있지는 않습니다.|
|`Exclusion`       |요소의 `party`는 요소에서 지정한 조항을 이행하지 않습니다.|
|`Obligation`      |요소의 `party`는 요소에서 지정한 조항을 이행해야 합니다.|
|`Right`           |요소의 `party`는 요소에서 지정한 조항을 받습니다.|

각 `nature` 키는 `party` 키와 쌍을 이루며, 네이처에 적용되는 당사자의 이름 또는 역할을 포함합니다(예를 들어 `Buyer`, `IBM` 또는 `All Parties`를 포함하지만 이에 한하지는 않음). `Definition` 네이처의 경우 당사자는 항상 `None`입니다.

## 당사자
{: #contract_parties}

개별 `parties` 배열은 계약에 나열되는 참가자를 지정합니다. 식별된 각 `party` 오브젝트는 이름으로 식별되는 당사자를 나열하며 `party` 오브젝트의 역할을 분류하는 `role`과 일치합니다. 계약에 대해 리턴될 수 있는 `role` 값은 다음을 포함하지만 이헤 한하지는 않습니다.

| `role`           |설명                                                |
|:----------------:|-----------------------------------------------------------|
|`Buyer`           |계약에 나열된 상품 또는 서비스의 비용을 지불해야 하는 당사자입니다.|
|`End User`        |제공된 상품 또는 서비스와 상호작용할 당사자입니다. 이는 `Buyer`와 명백하게 구분됩니다.|
|`None`            |요소에 대해 식별되는 당사자가 없습니다.|
|`Supplier`        |계약에 나열된 상품 또는 서비스를 제공해야 하는 당사자입니다.|

## 카테고리
{: #contract_categories}

`categories` 배열은 문장의 주제를 정의합니다. 현재 지원되는 카테고리는 다음과 같습니다.

| `categories`     |설명                                                |
|:----------------:|-----------------------------------------------------------|
|`Amendments`      |서명된 후 계약에 대한 변경사항을 지정하거나 표준 계약에 대한 변경을 지정하는 요소입니다. 계약 조항을 변경하는 조건에 대한 논의를 포함합니다.|
|`Asset Use`       |한 당사자가 다른 당사자의 자산을 사용하거나 사용하지 않을 수 있는 방법을 참조하는 요소입니다. 이는 특히 계약 하에서 의무를 수행하는 프로세스(앞에서 언급한 권한 및 제한사항 포함) 중에 다른 당사자의 라이센스, 장비, 도구 또는 작업자 같은 자산에 액세스할 수 있거나 해당 자산을 사용하는 당사자에게 적용됩니다. 이는 다른 당사자의 자산이 아닌 당사자 소유의 자산이기 때문에 구매한 상품, 서비스, 라이센스 등에 대한 당사자의 의무 또는 권한의 스펙으로 확장되지 않습니다.|
|`Assignments`     |서드파티에 권한, 의무 또는 둘 다를 전송하는 것을 설명하는 요소입니다.|
|`Audits`          |당사자의 권한을 참조하여 규제 준수를 검사 또는 검토하거나 당사자가 검사 또는 규제 준수 검토에 사용할 수 있는 요구사항을 검사 또는 검토할 수 있는 요소입니다. 여기에는 보존하고 있는 레코드에 대한 참조(주로 검사 권한과 관련됨) 및 검사할 수 있는 활동 레코드에 대한 유지보수 및 보존이 포함됩니다.|
|`Business Continuity`|당사자 중 하나의 전체 비즈니스가 판매되는 경우의 결과를 참조하는 요소입니다.|
|`Communication`  |주의사항, 계약 정보 또는 계약 변경 관련 정보에 대한 통신, 응답, 알림 또는 제공 작업의 요구사항을 참조하는 요소입니다. 또한 통신 방법, 정보 교환 조치 또는 프로세스, 당사자(또는 계약에 대한 직접 당사자가 아닌 다른 사람) 간에 정보 교환을 승인하는 방법에 대한 세부사항 참조도 포함됩니다.|
|`Confidentiality` |계약을 완료하고 진행하는 과정에서 당사자가 학습된 정보를 사용하거나 사용할 수 없는 방법을 설명하는 요소입니다. 또한 영업 비밀 유지 또는 비즈니스 정보 비공개와 같이 기밀을 유지해야 하는 정보에 대한 논의도 포함됩니다.|
|`Deliverables`    |계약 조항 하에서 당사자가 다른 당사자에게 제공하는 상품 또는 서비스와 같은 품목을 지정하는 요소입니다. 일반적으로 지불의 대가입니다. 인도물의 준비에 대한 논의가 포함됩니다.|
|`Delivery`        |한 당사자가 다른 당사자에게 인도물(인력 서비스와 반대되는 개념, 즉 물건)을 전달하는 방법이나 모드를 지정하는 요소입니다. 스케줄 또는 위치와 같은 전달 특성에 대한 논의가 포함됩니다.|
|`Dispute Resolution`|계약 당사자 간에 발생하는 분쟁(예: 노무, 송장 또는 요금 청구)을 해결하기 위한 조항을 논의하는 요소입니다. 조항 예에는 중재 패널, 금지 명령을 얻는 프로세스, 재판에 대한 권리 포기 또는 집단 소송 금지와 같은 정의된 절차에 의한 해결도 포함될 수 있습니다. 또한 특정 국가 또는 지역과 같이 계약의 지배법 또는 법률 선택에 대한 참조도 포함됩니다.|
|`Force Majeure`   |당사자의 통제에서 벗어나 예기치 못하거나 중단되는 이벤트를 참조하는 요소입니다. 이로 인해 당사자가 계약상의 의무를 수행하지 못하게 됩니다.|
|`Indemnification` |계약 상황에서 발생하거나 계약 기간 중에 계약이 손실되거나 손상된 결과로 계약의 한 당사자가 다른 당사자에게 보상해야 할 책임이 있는 경우 특정 채무의 재조정을 지정하는 요소입니다. 또한 손실 또는 손상으로부터의 법적 면제에 대한 참조도 포함됩니다.|
|`Insurance`       |한 당사자가 다른 당사자(하위 계약자 등의 서드파티 포함)에게 제공한 보험 적용 범위 또는 조건을 참조하는 요소입니다. 의료 보험(이에 한하지 않음) 등 다양한 보험이 포함됩니다.|
|`Intellectual Property`|계약 당사자에 대한 권한(예: 저작권, 특허 및 영업 비밀) 지정을 논의하는 요소입니다. 특허, 특허 신청 권한, 상표, 상호, 서비스 표시, 도메인 이름, 저작권 및, 스키매틱, 산업 모델, 발명, 저작자, 노하우, 영업 비밀, 컴퓨터 소프트웨어 프로그램 및 기타 무형의 독점 정보 등 모든 애플리케이션 및 등록에 대한 참조를 포함합니다. 지적 재산권을 위반한 결과에 대한 논의도 포함됩니다.|
|`Liability`       |당사자에게 언제 어떻게 결함이 발생하는지 판별하는 방법을 설명하는 요소입니다. 예를 들어 책임 제한, 서드파티 클레임 및 결함 발생 시 당사자의 요구에 따른 수리, 교체, 변제와 관련된 문구가 포함될 수 있습니다(이에 한하지 않음).|
|`Payment Terms & Billing`|당사자가 지불하거나 지급 받는 방법과 시기를 비롯하여 당사자가 지불하거나 청구하는 품목이나 요금을 자세히 설명하는 요소입니다. 지불 또는 지불 메커니즘 모드에 대한 참조를 포함합니다.|
|`Pricing & Taxes` |계약 조건을 충족하기 위해 교환되는 개별 인도물과 연관된 특정 금액이나 수치(예: 비용)를 참조하는 요소입니다. 가격이나 세금을 계산하기 위한 특정 수치나 방법에 대한 참조가 포함됩니다.|
|`Privacy`         |특히 민감한 개인 정보의 취급과 관련된 요소입니다. 일반적으로 보호와 관련되어 있습니다(예: GDPR과 같은 규정을 충족하기 위한 항목).|
|`책임`|한 당사자만 제어할 수 있는 계약의 보조 업무를 논의하는 요소입니다. 특히 직원 감독에 대한 토론에 중점을 둡니다.|
|`Safety and Security`|사람, 데이터 또는 시스템에 대한 물리적 안전 또는 사이버 보안 보호를 참조하는 요소입니다. 예를 들어 배경 검사, 안전 예방조치, 작업장 보안, 보안 액세스 프로토콜 및 위험을 초래할 수 있는 제품 결함에 대한 논의가 포함됩니다.|
|`Scope of Work`   |계약에 있는 것과 계약에 없는 것을 정의하는 요소입니다. 결과적으로 수행되어야 할 작업을 정의합니다. 예를 들어 특정한 주문을 정의하거나 계약서에서 요약 설명된 목표를 설명하는 문구가 포함됩니다.|
|`Subcontracts`    |계약에 따라 특정한 의무를 수행하기 위한 서드파티의 고용, 권한, 제한사항 및 그에 따른 결과 및 그로 인한 발생 상황을 참조하는 요소입니다.|
|`Term & Termination`|계약의 지속 기간, 계약 종료 스케줄 및 조건, 종료 결과를 참조하는 요소입니다(종료 시 또는 종료 후에 적용되는 의무 포함).|
|`Warranties`      |현재 참인 상태이고 이후에도 계속 참인 상태인 계약에서 지속되는 약속 및 의무를 참조하는 요소입니다. 또한 이러한 약속이나 의무를 위반하는 경우의 결과와 상황을 개선하는 권한을 논의하는 요소입니다(예를 들어 손해 배상이 포함되지만 이에 한하지 않음). 이 카테고리는 순수하게 표시 구문(과거 또는 현재의 사실에 대한 구문)과 관련된 요소 또는 과거에 발생한 일에 대한 가정을 설계하는 요소에는 적용되지 않습니다.|

## 속성
{: #attributes}

`attributes` 배열은 문장에서 식별되는 모든 속성을 지정합니다. 배열의 각 오브젝트에는 다음 세 가지 키가 포함됩니다. `type`(다음 표의 속성 유형), `text`(해당 텍스트) 및 `location`(입력 문서에서 속성의 `begin` 및 `end` 인덱스). 현재 지원되는 속성은 다음과 같습니다.

| `attributes`     |설명                                                |
|:----------------:|-----------------------------------------------------------|
|`Location`        |지리적 위치 또는 지역입니다.                         |
|`DateTime`        |날짜, 시간, 날짜 범위 또는 시간 범위입니다.                   |
|`Currency`        |금액 값과 단위입니다.                                  |

## 출처
{: #provenance}

`types` 및 `categories` 배열의 각 오브젝트에는 `provenance_ids` 배열이 포함됩니다. `provenance_ids` 배열에는 하나 이상의 키가 있습니다. 각 키는 피드백을 제공하거나 지원을 받기 위해 IBM에 보낼 수 있는 해시 값입니다.
