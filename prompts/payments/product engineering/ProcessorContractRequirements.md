***

## Project overview

You are a global **ecommerce payment gateway** serving ISVs and enterprise merchants, and operating as a card-present ISO for SMBs in multiple geographies. You currently rely on multiple U.S. processors via legacy contracts inherited from small-company acquisitions, which are no longer aligned with your current scale, risk profile, or product roadmap.

The objective of this engagement is to (1) map the relevant U.S. processor landscape and capabilities and (2) design a modern, scalable contractual framework to govern processor and other critical third-party relationships (change, operations, incident, compliance, performance, and data handling), with explicit emphasis on **full data visibility for scheme messaging** and **pass‑through of issuer decline codes**.

***

## Objectives

- Assess the U.S. processing landscape relevant to an omnichannel, ISV-focused payment gateway and ISO.  
- Identify best-practice contractual mechanisms for managing critical outsourced services in payments (processors and other key vendors).  
- Design a proposed clause structure and detailed requirement set that can be used to renegotiate and consolidate U.S. processor agreements.  
- Ensure the future-state contracts guarantee:  
  - Full scheme message data visibility to your organization (including auth, clearing, and chargeback messages, where applicable).  
  - Accurate and timely pass-through of issuer decline codes and related response data to you and, where appropriate, to your merchants.

***

## Scope of work

### 1. U.S. processor landscape analysis

Focus on processors and platforms most relevant to card-present and card-not-present traffic for ISVs, enterprise ecommerce, and SMB ISO portfolios.

- Map and profile at minimum: TSYS; Fiserv Omaha, North, Compass.  
- For each processor, document:  
  - Functional capabilities: card-present vs CNP, omni-channel support, tokenization, recurring/billing, dispute tools, ISV/embedded payments support.  
  - Technical characteristics: API models, certification processes, sandbox availability, versioning and change management practices.  
  - Operational services: settlement cycles, funding options, reporting, reconciliation support, service levels, and support models.  
  - **Data visibility and messaging:**  
    - Access to full scheme message fields (authorization, clearing, and, where applicable, chargeback messages).  
    - Ability to receive raw or normalized issuer response and decline codes, including mapping tables and maintenance processes.  
    - Availability of real-time and batch data feeds, data lakes, and reporting APIs that expose scheme and issuer-level data.  
  - Compliance and risk features: PCI DSS posture, fraud tools, KYC/AML services, data residency options, and data transfer mechanisms.  
  - Commercial constructs: typical fee structures, minimums, volume commitments, exclusivity, and termination provisions.  

### 2. Best-practice outsourcing and third-party governance

Identify and synthesize best-practice patterns for contracts governing critical payment processors and similar outsourced services.

- Review regulatory and industry expectations for third-party risk management in payments.  
- Summarize common structures from high-quality outsourcing and managed services contracts used by leading PSPs and ISV-oriented payment platforms.  
- Focus on clause patterns for:  
  - Governance, reporting, and audit rights.  
  - Change management (product changes, technical changes, pricing changes, regulatory-driven changes).  
  - Service operations and SLAs (availability, performance, capacity, maintenance windows) and associated service credits.  
  - Incident and problem management (detection, escalation, communications, RFO, remediation).  
  - Data protection, privacy, and cross-border data transfers.  
  - Business continuity and disaster recovery.  
  - Information security, encryption, and fraud/risk controls.  
  - Subcontracting and use of sub-processors.  
  - Term, termination rights, and exit/transition assistance.  
- Explicitly address best practices around:  
  - Full transparency of transaction lifecycle data, including scheme messaging.  
  - Ensuring that all issuer approval/decline information (including precise decline codes and, where applicable, additional data such as soft decline indicators) is preserved and passed through, not masked or generalized by the processor.

### 3. Proposed contract clause set (first-level outline)

Develop a recommended clause architecture for renewed U.S. processor agreements; this will form the basis of eventual negotiation.

Illustrative headings (to be refined):

- Scope of Services and Processing Activities.  
- Service Levels, Availability, and Performance Metrics.  
- Change Management and Roadmap Alignment.  
- Operational Processes and Support (including onboarding, certification, and deployment).  
- Incident, Problem, and Crisis Management.  
- **Data Visibility, Scheme Messaging, and Decline Code Handling** (new explicit section).  
- Data Protection, Privacy, and Cross-Border Transfers.  
- Information Security and PCI DSS Compliance.  
- Compliance with Laws and Network Rules.  
- Reporting, Audit, and Right to Inspect.  
- Subcontracting and Use of Sub-Processors.  
- Business Continuity and Disaster Recovery.  
- Commercial Terms, Pricing, and Benchmarking.  
- Term, Termination, and Exit Support.

For the **Data Visibility, Scheme Messaging, and Decline Code Handling** section, define its purpose as ensuring you have end-to-end visibility and control over transaction data, including all relevant scheme message fields and unaltered issuer decline codes, to support risk, routing, analytics, and merchant experience.

### 4. Detailed candidate requirements per clause

Once the clause outline is agreed, expand each section into concrete, testable requirements that can be dropped into contract drafting.

For the new data-specific dimension, include requirements such as:

- **Full data visibility for scheme messaging**  
  - Processor must provide access (via APIs, data feeds, or reporting) to all relevant scheme message fields for authorization, clearing, and, where applicable, chargeback messages, subject to network and regulatory constraints.  
  - No material scheme fields may be suppressed, redacted, or aggregated without your prior written approval, other than where mandated by law or the card networks.  
  - Processor must maintain and share complete and current documentation of all scheme fields exposed, including any transformations or normalizations applied.  

- **Pass-through of issuer decline codes**  
  - Processor must pass through issuer response and decline codes in full fidelity, without downgrading, remapping, or generalizing them, except where explicitly agreed and documented.  
  - Any mapping or translation layer used (e.g., into normalized error/decline taxonomies) must retain the original issuer code and make it available to you in all relevant data feeds and logs.  
  - Processor must notify you in advance of any network-driven or processor-driven changes to decline code formats, availability, or mappings, and must provide updated mapping tables in a timely manner.  
  - SLAs should cover the timeliness and completeness of issuer response data propagation across online auth responses, logs, reporting, and data exports.

For the broader clause set, continue to define:

- Specific obligations for the processor.  
- Your rights and controls.  
- Measurable KPIs, SLAs, and service credit mechanisms.  
- Compliance and security requirements.  
- Requirements for documentation, playbooks, and runbooks.  
- Transition and exit requirements, including data extraction (with full scheme message and issuer code history) and certification of data handling at termination.

***

