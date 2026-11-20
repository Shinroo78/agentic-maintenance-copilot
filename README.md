# 🏭 Agentic Factory OS — Maintenance & Replanning Copilot

![Status](https://img.shields.io/badge/status-demo%20%2F%20simulation-orange)
![Type](https://img.shields.io/badge/type-concept%20prototype-yellow)
![Production](https://img.shields.io/badge/production-not%20ready-red)
![Backend](https://img.shields.io/badge/backend-none%20%2F%20client--only-lightgrey)
![License](https://img.shields.io/badge/license-MIT-blue)
![Language](https://img.shields.io/badge/language-HTML%20%2B%20vanilla%20JS-blue)

A **single-file, browser-based interactive demo** that illustrates how an *Agentic Factory OS* layer could sit above existing ERP / WMS / SCADA / MES / CMMS systems to support maintenance, procurement, sales, and inventory operations — **without replacing them and without touching OT control loops**.

> ⚠️ **This is a demonstration prototype, not a working product.**
> It is intended for **concept validation, portfolio presentation, and stakeholder walkthroughs** — not for evaluation, procurement decisions, or deployment in any real environment.

---

## ⚠️ Read this first — What this project is and is not

### ✅ What this is

- A **visual simulation** of a proposed three-layer agentic architecture.
- A **storytelling tool** to demonstrate the *interaction pattern* between:
  - an AI reasoning layer that proposes actions,
  - a deterministic policy engine that decides,
  - a human approver who signs off,
  - an append-only audit log that records everything.
- A **client-side HTML file** with **no backend, no external services, no telemetry**.
- A **conversation starter** for evaluating whether such a system makes sense for a real industrial context.

### ❌ What this is NOT

- ❌ Not connected to any real ERP, WMS, MES, SCADA, CMMS, or PLC.
- ❌ Not using any real AI model, LLM, or machine learning — the "diagnosis" is hard-coded lookup logic.
- ❌ Not a functional OPC UA, Modbus, or B2B connector.
- ❌ Not a reference implementation you can adapt directly into production.
- ❌ Not audited, penetration-tested, or compliant with any industrial safety standard.
- ❌ Not a product, not a framework, not a library, not an SDK.
- ❌ Not backed by any data — all parts, machines, suppliers, orders, and inventories are **fictional**.

If you are looking for a production-grade industrial AI platform, this repository is **not it**.

---

## 🎯 Purpose of the project

Industrial AI projects usually fail *before* they reach production — not because the technology is missing, but because the **boundaries** between reasoning, execution, and human authority are not made explicit.

This demo exists to visualize one specific set of boundaries:

1. **The LLM (represented here by deterministic rules) may *suggest*, never *execute*.**
2. **A deterministic policy engine** — not the model's confidence — decides what is allowed.
3. **Every write action has an autonomy level:** `AUTO` (L1), `HOLD` (L2), or `REJECT` (L3).
4. **A human approves anything that crosses a threshold** — the demo makes this visible with real buttons.
5. **Nothing is deleted or hidden** — every decision lands in an append-only audit log.

The goal is to make these boundaries tangible enough that a plant manager, a maintenance engineer, a controls engineer, and a CTO can all look at the same screen and argue productively.

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

**Requirements:** any modern browser (Chrome, Edge, Firefox, Safari). JavaScript enabled. No internet connection needed.

---

## 🧭 Guided walkthrough (7 minutes)

The demo is organized around **six tabs**, each illustrating one operational domain. The fastest way to see the whole thesis is to walk through them in order:

| # | Tab | What to do | What it demonstrates |
|---|-----|-----------|----------------------|
| 1 | 🏭 **Factory Floor** | Click the pump → watch the pipeline run | Grounded diagnosis with a quoted source document |
| 2 | 🏭 **Factory Floor** | Click **Approve All** | Human-in-the-loop over L2 actions |
| 3 | 🛒 **Procurement** | `BRG-6205` is OUT → **Create Requisition** → **Approve & Issue** | Auto-draft (L1) + human-approved PO (L2) → stock updates |
| 4 | 💰 **Sales** | `SO-2001` → **Process** → **Approve** | Full delivery proposal → status becomes *Ready to Ship* |
| 5 | 💰 **Sales** | `SO-2003` → **Process** | Partial delivery + backorder when stock is insufficient |
| 6 | 📦 **Inventory** | **Cycle Count** → **Approve** adjustment | Discrepancy detection requires human sign-off |
| 7 | 📦 **Inventory** | **Warehouse Transfer** → **Approve** | Inter-warehouse move gated by policy |
| 8 | 🚫 **Safety** | Click any prohibited button | Deterministic **REJECT** — model confidence is irrelevant |
| 9 | 📋 **Audit Log** | Review the table | Every decision, every level, every actor, in one place |

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

### 🛒 Procurement
- Spare parts table with current stock vs. minimum threshold.
- Automatic drafting of a purchase requisition (`L1`).
- PO issuance gated behind human approval (`L2`) → stock updates on approval.

### 💰 Sales
- Open customer orders with due dates.
- Availability check, full-delivery proposal (`L2`) or partial-delivery + backorder proposal (`L2`).
- Approval moves the order to *Ready to Ship*.

### 📦 Inventory
- ABC classification (A = critical, B = medium, C = normal).
- Cycle count that randomly detects a discrepancy → adjustment requires `L2` approval.
- Inter-warehouse transfer proposal → `L2` approval.

### 🚫 Safety
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
| **Autonomy by risk, not by confidence** | Low-impact actions (`L1`) run automatically; anything touching money, schedule, or machines is `L2`; safety-critical actions are `L3` / prohibited. |
| **Human-in-the-loop** | Real approve/reject buttons for every `HOLD` action. |
| **Append-only auditability** | Every decision is written to a visible log, with the actor, the level, and the reason. |
| **Separation of reasoning from execution** | The diagnosis stage produces *proposals*; only the Action Gateway produces *effects*. |

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
│  • Supply / Scheduling / Quality sub-agents (in pilot)   │
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
| Safety case | Conceptual | IEC 62443, FMEA, functional safety analysis |
| Models used | **None** | LLM + reranker + deterministic simulators |

---

## ⚠️ Known limitations

- **No AI, no LLM.** All "reasoning" is hard-coded for clarity and offline reliability.
- **No real integrations.** No OPC UA, Modbus, SAP, Odoo, Odoo, WMS, CMMS, Slack, Teams, etc.
- **No authentication.** It is a static demo page.
- **No persistence.** Reloading the page resets all state.
- **No test coverage** — the demo is meant to be read, clicked, and discussed.
- **Not a reference architecture.** A real implementation would need at minimum:
  - an industrial DMZ and IEC 62443-aligned zones,
  - a real policy engine with a formal test suite,
  - idempotency keys and compensating actions,
  - document lifecycle management for the RAG knowledge base,
  - per-event LLM token budgets and cost controls,
  - functional safety analysis for anything touching the OT layer.

---

## 🗺️ Roadmap of the concept (not of the code)

The demo is intentionally static. The *concept* behind it has a longer roadmap:

- [x] Three-layer architecture and policy boundaries
- [x] Grounded diagnosis with abstention
- [x] Autonomy levels (`L1` / `L2` / `L3`)
- [x] Human-in-the-loop over L2
- [x] Append-only audit log
- [ ] **Phase 0** — Read-only pilot on one line, 2–3 assets, 4–6 weeks
- [ ] **Phase 1** — Assisted mode: notifications + CMMS drafts + limited spare reservation
- [ ] **Phase 2** — Simulated replanning, ROI validation, gate review
- [ ] Real connectors (OPC UA, Modbus, BAPI/OData, CMMS REST)
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
    └── walkthrough.md     ← optional: extended 7-minute script
```

The demo is a **single self-contained HTML file**. There is no build, no bundler, no `node_modules`, no transpiler. Open it and it works.

---

## 🎓 Intended audience

This demo is aimed at:

- **Plant directors and CTOs** considering an "agentic" layer above their existing stack.
- **Maintenance and reliability engineers** who want to see how AI recommendations would look with source citations and abstention.
- **OT/IT security architects** who want to reason about the boundary between the LLM and the PLC.
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
**Version:** 0.1.0 — Demo / Concept Prototype
