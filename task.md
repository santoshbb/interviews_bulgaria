# ERPNext System Design Task — AutoHaus Group

## Introduction

Thank you for your interest in the ERPNext Functional Consultant role. This take-home exercise asks you to produce a system design document for a fictional car dealership group that wants to adopt ERPNext. You may use any resources you like, including AI tools, documentation, and personal notes — but be prepared to explain and defend every decision in a follow-up conversation.

**Deliverable:** A single design document (PDF or Markdown), approximately **5–10 pages**.

---

## Company Profile — AutoHaus Group

AutoHaus Group is a car dealership business with the following characteristics:

- Operates **2 dealerships** in different cities, under the **same legal entity**.
- Sells **new cars** from a single manufacturer brand.
- Orders vehicles from the manufacturer via the **manufacturer's SAP system** (SAP S/4HANA).
- Currently tracks all operations in spreadsheets and wants to move to **ERPNext (self-hosted, on-premise)**.
- Approximately **10 users** across both locations: sales staff, a service manager, an accountant, and 1 IT admin.
- Occasionally takes **used vehicles as trade-ins**, but considers this a secondary concern.

---

## Business Requirements

### 1. Vehicle Ordering

Sales staff need to configure a car order by selecting the model, color, and options/packages, then submit it. The order must be transmitted to the manufacturer's SAP system. The manufacturer confirms the order with an estimated delivery date, and that confirmation must flow back into ERPNext.

### 2. Vehicle Inventory

Each dealership maintains a lot of vehicles in various states (e.g., in-transit from the manufacturer, in-stock on the lot). Management wants a **unified view of inventory across both locations**.

### 3. Customer Management

AutoHaus wants to track customers and link them to the vehicles they purchased, for future service and warranty work.

---

## Integration Constraints

The manufacturer's SAP system provides the following integration points:

| Integration Point | SAP IDoc Type | Direction |
|---|---|---|
| Purchase orders (vehicle orders) | ORDERS05 | ERPNext → SAP |
| Order confirmations | ORDRSP | SAP → ERPNext |
| Daily pricing updates | PRICAT | SAP → ERPNext |

Communication can happen over either of two channels — the manufacturer supports both:

- **SAP RFC** (Remote Function Call) — synchronous, program-to-program communication
- **Flat-file exchange via SFTP** — asynchronous, file-based batch communication
- **REST API calls**  - synchronous, program-to-program communication

**IF you don't have contextual SAP knowledge, treat this part of the task as any external system that exposes REST APIs for CRUD on car orders**

---

## What You Must Deliver

Your design document should cover the three parts described below. The suggested lengths are guidelines, not strict limits.

### Part 1: Data Model Design

- Which **standard ERPNext doctypes** you would use and which **custom doctypes** you would create for the vehicle domain.
- An **entity-relationship diagram** (hand-drawn, tool-generated, or text-based — all acceptable) showing how Vehicles, Customers, Orders, and Dealerships relate to each other.
- **Field-level detail** for the most critical custom doctype (e.g., a Vehicle doctype). List the key fields, their types, and their purpose.
- How the **2-dealership setup** is modeled within ERPNext.

### Part 2: Integration Architecture

- An **architecture diagram** showing ERPNext, SAP, and any middleware or integration layer you propose.
- **Data flow** for vehicle ordering (ERPNext → SAP) and order confirmation (SAP → ERPNext).
- **Data flow** for the daily pricing update (SAP → ERPNext).
- Your **choice and justification** of integration method (RFC vs. SFTP, or a combination).
- Your approach to **error handling** (e.g., what happens when an order transmission fails, how retries work, how errors are surfaced to users).

### Part 3: Assumptions & Open Questions

- **Assumptions** you made where the brief was unclear or incomplete, with your reasoning.
- **Questions** you would ask the customer before finalizing this design.
- Anything you consider **out of scope** for this design, with reasoning for why you excluded it.

---

## Evaluation Criteria

Your submission will be evaluated on three dimensions:

| Dimension | Weight | What We Look For |
|---|---|---|
| **Data Model Design** | 40% | Thoughtful use of standard ERPNext patterns, appropriate custom doctypes, clear entity relationships, practical multi-site modeling |
| **Integration Architecture** | 40% | Clear architecture with justified technology choices, well-defined data flows, realistic error handling |
| **Assumptions & Critical Thinking** | 20% | Identification of ambiguities in the brief, clearly stated assumptions, relevant questions for the customer, explicit scoping decisions |

---

## Practical Notes

- **Format:** PDF or Markdown. If you use Markdown and include diagrams, embed images or use a text-based diagramming notation (e.g., Mermaid, PlantUML, ASCII art).
- **Diagrams:** We value clarity over polish. A legible hand-drawn diagram photographed and embedded is perfectly acceptable.
- **AI usage:** You are welcome to use AI tools. We will discuss your design decisions in a follow-up conversation, so make sure you understand and can explain everything in your document.
- **ERPNext version:** Assume a recent stable version (v14 or v15). If your design depends on version-specific features, note the version.
- **No code required:** This is a design exercise, not an implementation task. Pseudocode or API call sketches are welcome where they clarify your design, but working code is not expected.

---

## Submission
 
 Send it as an email attachment or share a link with us in through the channel we've communicated with you.

Good luck!
