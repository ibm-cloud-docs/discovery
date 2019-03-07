---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2019-01-15"

subcollection: discovery

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:deprecated: .deprecated}
{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:hide-dashboard: .hide-dashboard}
{:apikey: data-credential-placeholder='apikey'} 
{:url: data-credential-placeholder='url'}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# Parsing contracts
{: #contract_parsing}

Element Classification returns parsed contracts with an analysis of each identified element.

The following sections describe how the returned JSON provides the analysis.

## Types
{: #contract_types}

The `types` array includes a number of objects, each of which contains `nature` and `party` keys whose values identify a couplet for the element.

The following tables list the possible values of the `nature` and `party` keys.

| `nature`         |Description                                                |
|:----------------:|-----------------------------------------------------------|
|`Definition`      |This element adds clarity for a term, relationship, or similar. No action is required to fulfill the element, nor is any party affected.|
|`Disclaimer`      |The `party` in the element is not obligated to fulfill the terms specified by the element but is not prohibited from doing so.|
|`Exclusion`       |The `party` in the element will not fulfill the terms specified by the element.|
|`Obligation`      |The `party` in the element is required to fulfill the terms specified by the element.|
|`Right`           |The `party` in the element is guaranteed to receive the terms specified by the element.|

Each `nature` key is paired with a `party` key, which will contain either the name or the role of the party or parties that apply to the nature (examples include, but are not limited to, `Buyer`, `IBM`, or `All Parties`). Note that for the `Definition` nature, the party is always `None`.

## Parties
{: #contract_parties}

The `parties` array specifies the participants that are listed in the contract. Each `party` object is associated with other objects that provide details about the party, including:

  - `role`: The party's role. Values are listed in the table that follows this list.
  - `importance`: The importance of the party. Possible values are `Primary` for a primary party and `Unknown` for a non-primary party.
  - `addresses`: An array that identifies addresses.
    - `text`: An address.
    - `location`: The location of the address as defined by its `begin` and `end` indexes.
  - `contacts`: An array that defines the names and roles of contacts that are identified in the input document.
    - `name`: The name of a contact.
    - `role`: The role of the contact.

The values of `role` that can be returned for contracts include, but are not limited to:

| `role`           |Description                                                |
|:----------------:|-----------------------------------------------------------|
|`Buyer`           |The party responsible for paying for the goods or services that are listed in the contract.|
|`End User`        |The party who interacts with the provided goods or services, explicitly distinguished from the `Buyer`.|
|`None`            |No party was identified for the element.|
|`Supplier`        |The party responsible for providing the goods or services that are listed in the contract.|

## Categories
{: #contract_categories}

The `categories` array defines the the subject matter of the sentence. 

The categories and descriptions in this table are based on United States law and might not apply in jurisdictions outside the United States.
{: important}

Currently supported categories include:

| `categories`     |Description                                                |
|:----------------:|-----------------------------------------------------------|
|`Amendments`      |Elements that specify changes to the contract after it has been signed, or alterations to a standard contract. Includes discussions of the conditions for changing the terms of a contract.|
|`Asset Use`       |Elements that refer to how one party may or may not use the assets of another party. This specifically applies to one party having access to or using assets such as licenses, equipment, tools, or personnel of the other party while in the process of conducting their duties under the agreement, including permissions and restrictions thereon.  This does not extend to specifications of a party's obligations or rights regarding any purchased goods, services, licenses, etc., as those are the party's own assets, rather than assets of another party.|
|`Assignments`     |Elements that describe the transfer of rights, obligations, or both to a third party.|
|`Audits`          |Elements referring to either the right of a party to examine or review compliance, or requirements that a party be available for inspection or compliance review. This includes references to record keeping (primarily as it relates to the right of inspection) and the maintenance and retention of activity records that may be examined.|
|`Business Continuity`|Elements referring to the consequences if the entire business of one of the parties is sold.|
|`Communication`  |Elements referring to requirements to communicate, respond, notify, or provide notice; contact information; or information regarding changes to the contract. Also includes references to details about communication methods, the act or process of exchanging information, and acceptable means of exchanging information between parties (as well as others who are not necessarily direct parties to the contract).|
|`Confidentiality` |Elements describing how parties can or cannot use information learned in the course of completing the contract and going forward. Also includes discussion of information that must be kept confidential, such as maintaining trade secrets or nondisclosure of business information.|
|`Deliverables`    |Elements specifying the items, such as goods or services, that one party provides to another under the terms of the contract, usually in exchange for payment. Includes discussion of preparation of deliverables.|
|`Delivery`        |Elements that specify the means or modes of transferring deliverables (things, as opposed to personal services) from one party to another. Includes discussions of characteristics of delivery, such as scheduling or location.|
|`Dispute Resolution`|Elements discussing provisions for settling any dispute (e.g., regarding labor, invoices, or billing) arising between contracting parties.  Provision examples may include settlement by a defined procedure such as an arbitration panel, a process for obtaining an injunction, waiving a right to trial, or prohibiting the pursuit of a class action. Also includes references to the contract's governing law or choice of law, such as a particular country or jurisdiction. |
|`Force Majeure`   |Elements that refer to unexpected or disruptive events outside a party's control that would relieve the party from performing their contractual obligation.|
|`Indemnification` |Elements that specify the remediation of certain liabilities, when one party of the contract becomes responsible for compensating another party as a result of incurred loss or damages during the term of, or arising from the circumstances of the contract. Also includes references to any legal exemptions from loss or damages.|
|`Insurance`       |Elements referring to insurance coverage or terms of coverage provided by one party to another party (including to third parties such as subcontractors or others). Includes a variety of insurance including, but not limited to, medical insurance.|
|`Intellectual Property`|Elements that discuss the assignment of rights (such as copyrights, patents, and trade secrets) to parties to the contract. Includes references to patents, rights to apply for patents, trademarks, trade names, service marks, domain names, copyrights, and all applications and registration of such schematics, industrial models, inventions, authorship, know-how, trade secrets, computer software programs, and other intangible proprietary information. Also includes discussion of the consequences of violation of intellectual property rights.|
|`Liability`       |Elements that describe the method for determining when and how fault attaches to any party. Examples may include, but are not limited to, statements regarding limitations of liability, third-party claims, and repairs, replacements, or reimbursements as required of the party at fault.|
|`Payment Terms & Billing`|Elements that detail how and when a party is to pay or get paid, as well as the items or fees the parties will be paying or billed for. Includes references to modes of payment or payment mechanisms.|
|`Pricing & Taxes` |Elements that refer to specific amounts or figures associated with individual deliverables that are exchanged (for example, how much something costs) as part of satisfying the terms of the contract. Includes references to specific figures or methods for calculating prices or tax amounts.|
|`Privacy`         |Elements that are particularly concerned with the treatment of sensitive personal information, usually regarding its protection (for example, in order to satisfy regulations such as GDPR).|
|`Responsibilities`|Elements that discuss tasks ancillary to the contract that are in only one party's control, specifically focused on discussion of employee oversight.|
|`Safety and Security`|Elements referring to physical safety or cybersecurity protection for people, data, or systems. Examples include discussions of background checks, safety precautions, workplace security, secure access protocols, and product defects that might pose a danger.|
|`Scope of Work`   |Elements that define what is in the contract versus is not in the contract; consequently, what is promised to be done. Examples include statements defining a particular order, or describing the goals or aims outlined in the contract.|
|`Subcontracts`    |Elements referring to the hiring of third parties to perform certain duties under the contract, and the permissions, rights, restrictions, and consequences thereto and arising therefrom.|
|`Term & Termination`|Elements referring to duration of the contract, the schedule and terms of contract termination, and any consequences of termination, including any obligations that apply at or after termination.|
|`Warranties`      |Elements that refer to ongoing promises and obligations made in the contract that are currently true and will continue to be true in the future. Also elements discussing the consequences of such promises or obligations being broken, and the rights to remedy the situation (for example, but not limited to, seeking damages). This category does not apply to elements that are purely concerned with representation statements (statements of fact about the past or the present), or to elements that lay out assumptions regarding things that occurred in the past.|

## Attributes
{: #attributes}

The `attributes` array specifies any attributes that are identified in the sentence. Each object in the array includes three keys: `type` (the type of attribute from the following table), `text` (the applicable text), and `location` (the `begin` and `end` indexes of the attribute in the input document). Currently supported attributes include:

| `attributes`     |Description                                                |
|:----------------:|-----------------------------------------------------------|
|`Address`         |A postal address.                                          |
|`Currency`        |Monetary value and units.                                  |
|`DateTime`        |A date, time, date range, or time range.                   |
|`Location`        |A geographical location or region.                         |
|`Organization`    |An organization.                                           |
|`Person`          |A person.                                                  |

## Effective dates
{: #effective_dates}

The `effective_dates` array identifies the dates during which the document is in effect.

| `effective_dates`|Description                                                |
|:----------------:|-----------------------------------------------------------|
|`text`            |An effective date, listed as a string.                     |
|`confidence_level`|The confidence level of the identification of the effective date. Possible values include `High`, `Medium`, and `Low`.|
|`location`        |The location of the date as defined by its `begin` and `end` indexes.|

## Contract amounts
{: #contract_amounts}

The `contract_amounts` array identifies the monetary amounts specified in the document.

| `contract_amounts`|Description                                               |
|:----------------:|-----------------------------------------------------------|
|`text`            |A contract amount, listed as a string.                  |
|`confidence_level`|The confidence level of the identification of the contract amount. Possible values include `High`, `Medium`, and `Low`.|
|`location`        |The location of the contract amount as defined by its `begin` and `end` indexes.|

## Termination dates
{: #termination_dates}

The `termination_dates` array identifies the document's termination dates.

| `contract_amounts`|Description                                               |
|:----------------:|-----------------------------------------------------------|
|`text`            |The termination date, listed as a string.                  |
|`confidence_level`|The confidence level of the identification of the termination date. Possible values include `High`, `Medium`, and `Low`.|
|`location`        |The location of the termination date as defined by its `begin` and `end` indexes.|

## Provenance
{: #provenance}

Each object in the `types` and `categories` arrays includes a `provenance_ids` array. The `provenance_ids` array has one or more keys. Each key is a hashed value that you can send to IBM to provide feedback or receive support.