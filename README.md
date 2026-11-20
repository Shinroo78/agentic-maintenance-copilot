# 🏭 Agentic Factory OS — Interactive Concept Demo

![Status](https://img.shields.io/badge/status-demo%20%2F%20simulation-orange)
![Type](https://img.shields.io/badge/type-concept%20prototype-yellow)
![Production](https://img.shields.io/badge/production-not%20ready-red)
![Backend](https://img.shields.io/badge/backend-none%20%2F%20client--only-lightgrey)
![License](https://img.shields.io/badge/license-MIT-blue)
![Language](https://img.shields.io/badge/language-HTML%20%2B%20vanilla%20JS-blue)
![Modules](https://img.shields.io/badge/modules-12-informational)

A **single-file, browser-based interactive demo** showing how an *Agentic Factory OS* layer could sit above existing enterprise and OT systems — **without replacing them, and without ever touching control loops unsupervised**.

> ⚠️ **This is a demonstration prototype, not a working product.**
> It exists for **concept validation, portfolio presentation, and stakeholder walkthroughs** — not for evaluation, procurement decisions, or deployment in any real environment.

---

## ⚠️ Read this first — What this project is and is not

### ✅ What this is

- A **visual simulation** of a proposed three-layer agentic architecture.
- A **storytelling tool** for showing the *interaction pattern* between an AI reasoning layer, a deterministic policy engine, a human approver, and an append-only audit log.
- A **single HTML file** with **no backend, no external services, no telemetry, no tracking**.
- A **conversation starter** — a way for plant managers, controls engineers, CTOs, and compliance officers to argue about the same screen.

### ❌ What this is not

- ❌ Not connected to any real ERP, WMS, MES, SCADA, CMMS, HRIS, or PLC.
- ❌ Not using any real AI model, LLM, or machine learning — the "diagnosis" is hard-coded lookup logic.
- ❌ Not a functional OPC UA, Modbus, BAPI, OData, or B2B connector.
- ❌ Not a reference implementation you can adapt into production.
- ❌ Not audited, penetration-tested, or compliant with any industrial safety standard.
- ❌ Not a product, framework, library, or SDK.
- ❌ Not backed by any data — all machines, parts, suppliers, employees, and orders are **fictional**.

If you are looking for a production-grade industrial AI platform, this repository is **not it**.

---

## 🎯 Purpose of the project

Industrial AI projects usually fail *before* they reach production — not because the technology is missing, but because the **boundaries** between reasoning, execution, and human authority are never made explicit.

This demo exists to visualize one specific set of boundaries:

1. **The LLM (represented here by deterministic rules) may *suggest*, never *execute*.**
2. **A deterministic policy engine** — not the model's confidence — decides what is allowed.
3. **Every action has an autonomy level:** `AUTO` (L1), `HOLD` (L2), or `REJECT` (L3).
4. **A human approves anything that crosses a threshold** — the demo makes this visible with real buttons.
5. **Nothing is deleted or hidden** — every decision lands in an append-only audit log.

The goal is to make these boundaries tangible enough that all the stakeholders — technical and non-technical — can look at the same screen and argue productively.

---

## 🚀 Quick start

There is no installation, no build step, no dependency, and no server.

```bash
# Option 1 — clone and open
git clone https://github.com/<your-username>/agentic-factory-os-demo.git
cd agentic-factory-os-demo
open afos-demo-en.html      # macOS
# start afos-demo-en.html   # Windows
# xdg-open afos-demo-en.html # Linux
```

```text
# Option 2 — just download the file
Download afos-demo-en.html → double-click → it opens in your browser.
```

**Requirements:** any modern browser (Chrome, Edge, Firefox, Safari). JavaScript enabled. No internet connection needed after the first load (fonts are cached).

---

## 🧭 Guided walkthrough (7–10 minutes)

The demo is organized around **twelve tabs**, each illustrating one operational domain. The fastest way to see the whole thesis is to walk through them in this order:

| # | Tab | What to do | What it demonstrates |
|---|-----|-----------|----------------------|
| 1 | 🏭 **Factory** | Click the pump → watch the 4-stage pipeline | Grounded diagnosis with a quoted source, policy evaluation, auto vs. hold |
| 2 | 🏭 **Factory** | Click **Approve All** | Human-in-the-loop over L2 actions |
| 3 | 📺 **SCADA** | Click **Dedupe Alarm Flood** | Alarm reduction (12 → 3 root events) |
| 4 | 📺 **SCADA** | Click **Attempt SCADA Write** | L3 REJECT — no write path exists |
| 5 | 🏢 **ERP** | Click **Process Cost Booking** → **Approve** | Draft journal entry → budget updates |
| 6 | 🛒 **Procurement** | `BRG-6205` is OUT → **Create** → **Approve** | Auto-draft (L1) + human-approved PO (L2) |
| 7 | 💰 **Sales** | `SO-2001` → **Process** → **Approve** | Full-delivery proposal → order moves to "Ready to Ship" |
| 8 | 💰 **Sales** | `SO-2003` → **Process** | Partial delivery + backorder when stock is short |
| 9 | 👥 **CRM** | **Draft Response** → **Approve** | Context-aware reply to a customer complaint |
| 10 | 👤 **HR** | **Start Hiring** → **Approve** | Headcount +1, payroll rises |
| 11 | 👤 **HR** | **Calculate Payroll** → **Approve** | Gross / deductions / net, then posted |
| 12 | 👤 **HR** | **Attempt Automatic Termination** | L3 REJECT — the agent cannot fire anyone |
| 13 | 📦 **Inventory** | **Cycle Count** → **Approve** | Discrepancy detection + adjustment |
| 14 | 🗄 **RAG** | Click a preset query | Full retrieval trace with citation verification or abstention |
| 15 | 🔧 **CMMS** | **Draft WO from Alarm** → **Approve** → **Start** → **Close** | Full work-order lifecycle |
| 16 | 🔧 **CMMS** | **Attempt Auto-Close P1** | L3 REJECT — critical closure needs human evidence |
| 17 | 🛡 **Safety** | Click any prohibited button | Deterministic REJECT, independent of model confidence |
| 18 | 📋 **Audit** | Review the table | Every decision from every module, in one trail |

**Key observation:** in every tab, the same pattern repeats:
> *The reasoning layer proposes → the policy engine decides → the human approves or rejects → the audit log records.*

---

## 🧩 Feature breakdown by tab

### 🏭 Factory Floor
- Three fictional machines (`PUMP-01`, `MOTOR-02`, `PRESS-03`) in one production line.
- Click any machine (or a preset button) to trigger a simulated incident.
- Four-stage processing pipeline:
  1. **Edge Event** — event normalization, filtering, quality codes.
  2. **Diagnosis** — grounded hypothesis with a quoted source document, or **ABSTAIN** if no active source applies.
  3. **Policy Engine** — action proposal classified as `AUTO` / `HOLD`.
  4. **Action Gateway** — auto-actions executed, L2 actions awaiting human approval.

### 📺 SCADA
- Six live signals with quality codes and trend indicators.
- Three active alarms and a raw event stream (12/min).
- **Alarm deduplication demo** — reduces 12 raw events to 3 root events (75% reduction).
- **Attempt SCADA Write** — L3 REJECT: the OPC UA subscription is read-only by design.

### 🏢 ERP
- Three cost centers with live budget usage bars.
- Journal entry table with draft → posted states.
- **Process Cost Booking** — reads the cost center, drafts the journal entry, awaits human approval.
- Approving a draft posts it, updates the spent amount, and logs to the audit trail.

### 🛒 Procurement
- Spare parts table with current stock vs. minimum threshold.
- Automatic drafting of a purchase requisition (L1).
- PO issuance gated behind human approval (L2) → stock updates on approval.

### 💰 Sales
- Open customer orders with due dates.
- Availability check, full-delivery proposal (L2) or partial-delivery + backorder proposal (L2).
- Approval moves the order to *Ready to Ship*.

### 👥 CRM
- Three customer accounts with health indicators.
- Recent interactions table (complaints, orders, tickets).
- **Draft Response** — reads order history and tickets, drafts a context-aware reply, queues it for human approval.

### 👤 HR
- Employee directory with headcount, payroll total, departments, and pending drafts.
- **Start Hiring** — creates a DRAFT employee record (does **not** add to headcount yet). Approval moves it to ACTIVE and updates payroll.
- **Calculate Payroll** — computes gross, deductions (15%), and net. Approval posts the payment.
- **Leave request** — policy check auto-passes, manager approval moves employee to `ON_LEAVE` → excluded from next payroll.
- **Prohibited actions** — automatic termination, salary change, and promotion are all L3 REJECT.

### 📦 Inventory
- ABC classification (A = critical, B = medium, C = normal).
- **Cycle count** — randomly detects a discrepancy → adjustment requires L2 approval.
- **Inter-warehouse transfer** — proposal → L2 approval.

### 🗄 RAG
- Document library with lifecycle states: `ACTIVE`, `SUPERSEDED`, `DRAFT`.
- Retrieval simulator showing the full pipeline:
  1. Query
  2. Metadata pre-filter (ACTIVE only)
  3. Hybrid retrieval (dense + BM25 → RRF → rerank)
  4. Top match
  5. Citation verification
  6. Decision: `GROUNDED` or `ABSTAIN`
- If no active source matches, the system **abstains** instead of guessing.

### 🔧 CMMS
- Preventive maintenance schedule with `OK` / `DUE_SOON` / `OVERDUE` states.
- Work order table with full lifecycle: `DRAFT` → `APPROVED` → `IN_PROGRESS` → `CLOSED`.
- **Draft WO from Alarm** — creates a draft work order from the latest alarm (L1).
- **Draft PM** — creates a preventive maintenance draft from the schedule (L1).
- Approve, start, and close actions respect the L1/L2 pattern.
- **Attempt Auto-Close Critical WO** and **Delete Record** — both L3 REJECT.

### 🛡 Safety
- Eight explicitly prohibited actions (PLC write, setpoint change, start/stop, auto-PO, auto-schedule, stock write-off, price change, supplier addition).
- Each click returns a **deterministic REJECT** and is logged in the audit trail.
- **This is the most important tab** — it makes the safety case visible.

### 📋 Audit Log
- Unified, append-only log across all modules.
- Each entry contains: sequence ID, timestamp, module, action, level (`L1` / `L2` / `L3`), decision, actor, and note.

---

## 🏗️ Design principles illustrated

| Principle | How the demo shows it |
|-----------|----------------------|
| **Grounded diagnosis** | Every recommendation carries a quoted source document; if no active source matches, the system **ABSTAINs** instead of guessing. |
| **Deterministic execution** | All write actions pass through a policy engine that applies a fixed allow-list, not model confidence. |
| **Autonomy by risk, not by confidence** | Low-impact actions (`L1`) run automatically; anything touching money, schedule, machines, or people is `L2`; safety-critical and irreversible actions are `L3` / prohibited. |
| **Human-in-the-loop** | Real approve/reject buttons for every `HOLD` action. |
| **Append-only auditability** | Every decision is written to a visible log, with the actor, the level, and the reason. |
| **Separation of reasoning from execution** | The diagnosis stage produces *proposals*; only the Action Gateway produces *effects*. |
| **Irreversible actions are human-only** | Terminations, P1 work-order closures, SCADA writes, and supplier additions all require human sign-off. The agent cannot do them. |

---

## 🗺️ Architecture (as simulated in the demo)

The demo mirrors a three-layer architectural proposal:

```text
┌──────────────────────────────────────────────────────────┐
│  Layer 1 — IIoT Edge & Data Ingestion                    │
│  • Event normalization (JSON schema)                     │
│  • Edge filtering (deadband, debounce, dedupe)           │
│  • Quality codes, source attribution                     │
└──────────────────────────┬───────────────────────────────┘
                           │  standardized event
┌──────────────────────────▼───────────────────────────────┐
│  Layer 2 — Agentic Reasoning Core (simulated)            │
│  • Triage / Supervisor                                   │
│  • Diagnosis (grounded in a source document)             │
│  • Supply / Scheduling / Quality / Finance / HR agents   │
│  • Deterministic Critic + Policy Engine                  │
└──────────────────────────┬───────────────────────────────┘
                           │  proposed action + citations
┌──────────────────────────▼───────────────────────────────┐
│  Layer 3 — Action Gateway & Execution                    │
│  • Allow-list enforcement                                │
│  • Autonomy level (L1 / L2 / L3)                         │
│  • Human approval for L2                                 │
│  • Append-only audit log                                 │
└──────────────────────────────────────────────────────────┘
```

In the demo, **Layer 1** is a JavaScript object, **Layer 2** is a set of lookup rules and `if` statements, and **Layer 3** is a set of DOM buttons. The *behavior* mirrors the proposed architecture. The *implementation* is intentionally trivial.

---

## 🧪 What is simulated vs. what is real

| Component | In this demo | In a real pilot |
|-----------|--------------|-----------------|
| Event ingestion | JS object constructed in browser | OPC UA / Modbus / REST connectors with TLS |
| Edge filtering | Cosmetic labels (`deadband`, `debounce`) | Real stream processor at the industrial DMZ |
| Triage | Hard-coded severity logic | LLM-based triage with policy constraints |
| Diagnosis | Lookup in a hard-coded `KB` object | Hybrid RAG with document lifecycle (ACTIVE / SUPERSEDED) |
| Citation verification | Substring check on the quote | Deterministic validator + human-reviewed KB |
| Policy engine | `if` statements in JS | Formal rule engine with test suite |
| Human approval | DOM button | Enterprise approval workflow with roles and SLAs |
| Audit log | Array pushed to a `<table>` | Append-only store (e.g., Kafka + WORM storage) |
| HR data | Hard-coded employee list | HRIS with legal and compliance controls |
| Safety case | Conceptual | IEC 62443, FMEA, functional safety analysis |
| Models used | **None** | LLM + reranker + deterministic simulators |

---

## ⚠️ Known limitations

- **No AI, no LLM.** All "reasoning" is hard-coded for clarity and offline reliability.
- **No real integrations.** No OPC UA, Modbus, SAP, Odoo, WMS, CMMS, HRIS, Slack, Teams, etc.
- **No authentication.** It is a static demo page.
- **No persistence.** Reloading the page resets all state.
- **No test coverage** — the demo is meant to be read, clicked, and discussed.
- **Not a reference architecture.** A real implementation would need at minimum:
  - an industrial DMZ and IEC 62443-aligned zones,
  - a real policy engine with a formal test suite,
  - idempotency keys and compensating actions,
  - document lifecycle management for the RAG knowledge base,
  - per-event LLM token budgets and cost controls,
  - functional safety analysis for anything touching the OT layer,
  - legal and compliance review for anything touching HR data.

---

## 🗺️ Roadmap of the concept (not of the code)

The demo is intentionally static. The *concept* behind it has a longer roadmap:

- [x] Three-layer architecture and policy boundaries
- [x] Grounded diagnosis with abstention
- [x] Autonomy levels (`L1` / `L2` / `L3`)
- [x] Human-in-the-loop over L2
- [x] Append-only audit log
- [x] Twelve operational modules (Factory, SCADA, ERP, Procurement, Sales, CRM, HR, Inventory, RAG, CMMS, Safety, Audit)
- [ ] **Phase 0** — Read-only pilot on one line, 2–3 assets, 4–6 weeks
- [ ] **Phase 1** — Assisted mode: notifications + CMMS drafts + limited spare reservation
- [ ] **Phase 2** — Simulated replanning, ROI validation, gate review
- [ ] Real connectors (OPC UA, Modbus, BAPI/OData, CMMS REST, HRIS)
- [ ] Real evaluation harness (Top-K accuracy, Citation Precision, Abstention Rate, Latency P95, Token Cost)

If you are interested in the concept and want to discuss it, open an issue — but please understand this repository is a **portfolio piece**, not an engineering project accepting pull requests toward production.

---

## 📁 Repository structure

```text
agentic-factory-os-demo/
├── README.md              ← this file
├── afos-demo-en.html      ← English demo (this README refers to it)
├── afos-demo-ar.html      ← Arabic demo (same behavior, RTL layout)
├── LICENSE                ← MIT
└── docs/
    ├── walkthrough.md     ← extended 10-minute script
    └── architecture.md    ← longer design rationale
```

The demo is a **single self-contained HTML file**. There is no build, no bundler, no `node_modules`, no transpiler. Open it and it works.

---

## 🎓 Intended audience

This demo is aimed at:

- **Plant directors and CTOs** considering an "agentic" layer above their existing stack.
- **Maintenance and reliability engineers** who want to see how AI recommendations would look with source citations and abstention.
- **OT/IT security architects** who want to reason about the boundary between the LLM and the PLC.
- **HR and compliance leads** who want to see how AI-assisted workflows respect human authority.
- **Product managers and investors** evaluating whether this problem space is worth pursuing.

It is **not** aimed at engineers looking for a starter kit to adapt into production.

---

## 📝 License

Released under the **MIT License** — see [`LICENSE`](./LICENSE).

You are free to fork, remix, or reuse the demo for teaching, internal presentations, or portfolio use. Attribution is appreciated but not required.

---

## 🙏 Acknowledgements

This demo is inspired by the ongoing industry conversation around *agentic AI for industrial operations* — and by the practical experience that most industrial AI pilots stall not because the model is weak, but because the **boundaries are undefined**. The demo tries to make those boundaries obvious on a single screen.

---

**Last updated:** 2026-11-20
**Version:** 0.1.0 — Concept Prototype.
