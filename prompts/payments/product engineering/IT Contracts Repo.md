## Role and Context

You are a **procurement** professional working in a **FinTech** organisation.  

Your task is to design and document a **master contract repository** for all **IT-related contracts** (software, hardware, SaaS, services, etc.).[1][2][3]

***

## Objectives

1. Define an approach for creating a **centralised contract repository**, including folder / data structures.[2][1]

2. Describe how to **ingest and reconcile** data from **Accounts Payable (AP)**, including **purchase orders (POs)** and **requisitions**, to identify suppliers and associated contracts.[4][5][6][7][8][9]

3. Specify how to **match** AP, PO, and requisition data to contract records and **extract metadata** from contracts.[10][11][1][4]

4. Design a **tracking database schema** for key contract attributes and linked financial / PO information.[12][13][14][15][1]

5. Provide:

   - A **flow chart** of the end‑to‑end process.[11][16]

   - A **sequence diagram** of interactions between system components.[16][17][18][10]

   - A **hypothetical HTML summary page** layout for an interactive front end.[15][11]

***

## Assumptions

- AP data includes at least: supplier name, supplier ID, invoice number, **PO number**, requisition number (if available), amounts, dates, and cost centre or GL code.[5][6][7][8][9][4]

- PO / requisition data includes: PO ID, requisition ID, supplier, line items (description, quantity, unit price), currency, category, project / cost centre, and **linked contract ID where present**.[6][19][4][5]

- Existing contracts may be:

  - Stored in various network folders or SharePoint locations.

  - In multiple formats (PDF, DOCX, scanned images).[1][2]

- You can use or design:

  - A database (e.g. SQL) or CLM-style repository to hold structured metadata.[11][15][1]

  - An OCR / parsing service to extract contract metadata from documents.[13][14][12][1]

***

## Task 1 – Repository Structure and Taxonomy

Design the **logical structure** of the repository. At minimum, define:

- **Top‑level segmentation** (e.g. by:

  - IT category: Infrastructure, SaaS, Software Licences, Professional Services, Telecoms, etc.

  - Business domain: Payments, Core Banking, Risk, Data, InfoSec, Corporate IT.[3][2]

- **Folder / entity hierarchy**, for example:

  - Organisation → Category → Supplier → Contract family → Contract versions.[2][1]

- **Standard metadata schema** (for repository indexing), including at least:

  - Contract ID

  - Supplier legal name

  - Contract title / description

  - Contract type (MSA, SOW, Licence, SLA, NDA, etc.)

  - Start date

  - Expiry date

  - Notice period

  - Renewal type (auto/manual)

  - Annual spend (from AP)

  - Contract owner (business / legal)

  - Risk / criticality rating

  - Data classification (e.g. PCI, PII, confidential)[3][15][1][2]

Clarify where a **single repository structure** is used versus where **multiple folder structures or views** are required based on data quality and accuracy (e.g. “staging” vs “golden” repository).[1][3]

***

## Task 2 – Data Ingestion from AP, PO, and Requisition Systems

Describe a **method to ingest and standardise**:

- **AP data feeds** (CSV, API, flat files) with all supplier spend for IT categories.[7][8][9][4][6]

- **PO data**:

  - Header (PO ID, supplier, currency, total value, dates, contract reference if present).

  - Line items (description, SKU, quantity, unit price, GL / cost centre).[19][4][5][6]

- **Requisition data**:

  - Requisition ID, requester, business unit, category, justification / business case text, and any referenced contract or quote.[4][5][19]

Key steps:

- Normalise and cleanse supplier 

  - Standardise supplier names.

  - Map to a **Supplier Master** with unique IDs.[2][4][11]

- Create a **linked data model**:

  - Requisition → PO → Invoice (AP) → Contract.[5][6][19][4]

- Use PO and requisition data to:

  - Identify which goods/services are **contract-based** (e.g. recurring SaaS, support, licences).[19][4][5]

  - Highlight candidate contracts when AP invoices or POs do not yet have an explicit contract link.[20][10][4]

Define rules for:

- Flagging AP or PO records with **no matched contract** (potential maverick spend).[15][3][4][2]

- Flagging contracts with **no corresponding POs or AP spend** in a defined period (potentially obsolete).[3][15]

***

## Task 3 – Matching AP, PO, and Requisition Data to Contracts

Design the **matching logic** to connect AP, PO, and requisition records with contract entries:

- Primary match keys:

  - Supplier ID / legal entity.

  - **PO number** linked to a known contract (using explicit “Linked Contract” field where available).[17][6][10][4]

  - Contract reference stored in PO header or lines.

  - Contract reference or keywords in requisition description / justification text.[4][5][19]

- Secondary / heuristic match keys:

  - Cost centre, category, and business owner.

  - Recurring spend patterns and description similarity between PO / invoice lines and contract descriptions.[6][19][4]

Handle scenarios:

- **One‑to‑many**:

  - One master contract with multiple POs and invoices under it.[10][17][20]

- **Many‑to‑one**:

  - Multiple requisitions and POs rolling up into a single framework or MSAs.[5][4]

Define quality rules:

- Confidence scoring for automated matches (e.g. supplier + PO contract field = high confidence; supplier only = low confidence).[19][4]

- Exception workflows for low‑confidence matches and manual review queues.[14][15][1][3]

Explain how matched data drives:

- Contract **annualised spend** (rolling 12‑month invoice data).[8][9][7]

- **PO consumption** against contract maximum value or committed volume.[6][4][5][19]

- Renewal / risk alerts when spend patterns or PO usage diverge from contract terms.[15][2][3]

***

## Task 4 – Using PO / Requisition Content to Locate and Extract Contract Documentation

Explicitly describe how **PO and requisition data** is used to **find and process contract documents**:

- Use PO fields (contract ID, supplier, category, description) to:

  - Search existing repositories and file shares for contracts matching supplier and keywords.

  - Prioritise contracts tied to **high‑value or high‑volume POs** for metadata extraction.[4][5][19]

- Use requisition meta

  - Free‑text justification often contains product names, SaaS platform names, and links or references to proposals / statements of work.

  - Mine these texts to infer likely contract document names or locations.[5][4]

- Build a **contract discovery job** that:

  - Takes as input: supplier, PO description, requisition text, and category.

  - Searches document stores and email archives (where permitted) for matching filenames, titles, and text snippets.[12][14][1][2]

Once candidate contract documents are identified:

- Pass them to the **metadata extraction service** (OCR / AI parser).[13][14][12]

- Extract key metadata (parties, term, renewals, pricing model, SLAs, data protection clauses, etc.).[14][12][13]

- Store a **link back to the originating POs and requisitions** to maintain full traceability from demand → purchase → invoice → contract.[17][10][4]

***

## Task 5 – Contract Metadata Extraction and Tracking Database

Define an approach for **metadata extraction** and the **tracking database**:

- Extraction:

  - Use AI / OCR tools to pull out fields such as: effective date, end date, renewal terms, payment terms, minimum spend, jurisdiction, and key clauses.[12][13][14]

- Data model (minimum tables):

  - Contract

  - Supplier (linked to Supplier Master)

  - PO (header + lines, linked to Contract where applicable)

  - Requisition

  - AP Invoice

  - Financial summary and usage metrics

  - Key dates / obligations[11][1][2][15][4]

- Governance:

  - Define which metadata fields are mandatory before a contract is considered “live”.

  - Implement periodic data quality checks and sampling (e.g. validate extracted renewal dates and notice periods).[14][1][3][15]

***

## Task 6 – Flow Chart (Process View)

Include in the flow chart the **PO / requisition analysis** stages. High‑level stages:[16][11][19][4][5]

1. Requisition creation and approval.  

2. PO creation from requisition (with optional contract link).  

3. AP invoice receipt and matching to PO (2‑way / 3‑way matching).  

4. Periodic extraction of AP, PO, and requisition data into the integration layer.  

5. Supplier normalisation and mapping to Supplier Master.  

6. Contract document collection / discovery based on supplier, PO, and requisition data.  

7. Contract metadata extraction (OCR / AI).  

8. Matching engine links contracts ↔ POs ↔ requisitions ↔ AP invoices.  

9. Data quality checks and exception handling.  

10. Repository update (metadata + document links).  

11. Reporting and dashboards (renewals, spend, PO consumption, non‑compliant spend).

For each step, specify inputs, outputs, and participating systems / roles.[16][11][4]

***

## Task 7 – Sequence Diagram (System Interaction)

In the sequence diagram, ensure you show **PO and requisition flows** explicitly. Include at least:[18][10][17][16][4]

- User (Requester / Approver / Procurement / Contract Manager)  

- Requisition / Procurement System  

- PO / ERP System  

- AP System  

- Supplier Master / ERP  

- Contract Repository / CLM  

- Metadata Extraction Service  

- Matching Engine / Integration Layer  

- Reporting / Dashboard UI  

Illustrate a scenario where:

1. User raises requisition in the procurement system.  

2. Requisition is approved and a PO is generated (with or without a contract link).  

3. Invoice arrives and is matched against the PO in AP (2‑ or 3‑way match).[6][19][4][5]

4. AP, PO, and requisition data are exported to the Matching Engine.  

5. Matching Engine queries Supplier Master and Contract Repository to find existing contracts.[10][17][4]

6. Where no contracts are linked, Matching Engine triggers contract discovery and metadata extraction.[13][12][14]

7. Contract Repository is updated and spend / PO consumption is reflected in dashboards.

***

## Task 8 – HTML Summary Page and Interactive Guide

In your HTML example, reflect **PO and requisition context**:

1. **Summary Page** should include:

   - KPIs: active IT contracts, annualised spend, % of spend covered by contracts, number of POs linked to contracts, number of invoices without a contract link.[2][3][15][4]

   - Filters for: supplier, IT category, business owner, renewal date, spend band, **PO presence (yes/no)**, requisition origin.  

   - Contract table with columns such as:

     - Contract ID, Supplier, Category

     - Annual Spend, Contract Value, PO Coverage (% of POs linked)

     - Expiry Date, Notice Period, Status.  

2. **Interactive Guide / Onboarding Panel** should explain:

   - How to view all POs and requisitions associated with a contract (“View related POs”, “View originating requisitions”).[17][10]

   - How AP / PO / requisition data influences metrics like spend, coverage, and contract utilisation.[4][6]

   - How to identify and fix POs or invoices not linked to any contract (e.g. guided workflow).[19][6][4]

Use simple HTML structures (`<header>`, `<section>`, `<nav>`, `<table>`, etc.) to illustrate layout and behaviour.[11][15]

***

## Deliverables

When answering this prompt, produce:

1. A **narrative description** of the method and design choices across Tasks 1–5, explicitly covering how PO and requisition data are analysed to find and link contract documents for metadata extraction.[12][13][14][4]

2. A **textual flow chart description** or diagram definition including PO / requisition stages for Task 6.[16][11][4]

3. A **sequence diagram definition** (e.g. UML or Mermaid) including requisition, PO, AP, and contract interactions for Task 7.[18][10][17][16][4]

4. A **sample HTML snippet** showing the summary page and interactive guide with PO / requisition‑aware views for Task 8.[15][11][4]

Sources

[1] End Contract Chaos: Repository Best Practices https://yousign.com/blog/contract-repository-best-practices-centralizing-searching-agreements

[2] The Complete Guide to Effective Contract Repository ... https://fynk.com/en/blog/contract-repository-management-guide/

[3] Contract repository: contract management guide https://contracko.com/blog/contract-repository-guide

[4] Purchase Order Matching | Fixing AP Bottlenecks at Scale https://rossum.ai/blog/purchase-order-matching-in-accounts-payable/

[5] Why Purchase Order Matching to Invoice Is Important https://www.artsyltech.com/blog/PO-matching

[6] Automated Purchase Order (PO) Matching https://approvalmax.com/ap-automation/po-matching

[7] 2-Way Matching in Accounts Payable [Complete Guide] https://www.brex.com/spend-trends/accounting/2-way-matching-in-accounts-payable

[8] How to incorporate three-way matching into your AP process https://mercury.com/blog/three-way-match-accounts-payable

[9] 3-Way Matching Explained: Essential UK Business Guide https://tipalti.com/en-uk/resources/learn/3-way-match/

[10] How to Link a PO to a Contract https://success.procurify.com/en/articles/9001600-how-to-link-a-po-to-a-contract

[11] What is the Contract Lifecycle Management Process Diagram? - Icertis https://www.icertis.com/contracting-basics/contract-lifecycle-management-process-diagram/

[12] What is Contract Data Extraction: 5 Key Steps to Implement it https://www.sirion.ai/library/contract-management/contract-data-extraction/

[13] How to extract and manage contract metadata with AI https://fynk.com/en/blog/contract-metadata-extraction/

[14] Contract Metadata Extraction: Efficient Methods Explained https://brightleaf.com/contract-metadata-extraction-efficient-methods-explained/

[15] 9 Contract Repository Management Best Practices https://www.aline.co/post/contract-repository-management-best-practices

[16] Sequence Diagram Tutorial - Complete Guide with Examples https://creately.com/guides/sequence-diagram-tutorial/

[17] How to Link POs to Master Contracts (2022) https://www.youtube.com/watch?v=vSnEu84RXxQ

[18] Contract Management System Sequence UML Diagram https://www.freeprojectz.com/uml-diagram/contract-management-system-sequence-diagram

[19] What types of purchase order matching are available? https://www.blue10.com/en/types-of-ordermatching/

[20] Link existing PO items to a contract item https://community.sap.com/t5/enterprise-resource-planning-q-a/link-existing-po-items-to-a-contract-item/qaq-p/10574330
End Contract Chaos: Repository Best Practices
Stop losing contracts in scattered folders. Learn how repositories centralise, secure, and streamline agreement management.
 