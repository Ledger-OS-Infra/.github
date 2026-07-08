# LedgerCore Ecosystem 

Welcome to the official home of **LedgerCore**—a production-grade, universal financial operations and automated payment reconciliation platform built during the **Nomba × DevCareer Hackathon 2026**.

We build tools that bridge the gap between raw, unstructured banking infrastructure and automated, immutable corporate ledger accounting.

---

## What We Do

Inbound bank transfers are fundamentally broken for business automation; notifications contain little more than a sender name, timestamp, and amount. Our core mission is removing human intervention from corporate accounting entirely. 

Our flagship project, **LedgerCore**, sits directly on top of fintech infrastructure (like Nomba Virtual Accounts) to capture inbound payment webhooks and instantly convert them into beautifully structured, audit-ready financial events.

Nomba Virtual Account Bank Transfer
                    │
                    ▼
     [ Express.js API Webhook Receiver ]
     ├── Signature Verification & Idempotency Check
     └── Enqueue Asynchronous Processing
                    │
                    ▼
     [ BullMQ Reconciliation Workers ] 
     ├── 3-Tier Cascade Matching (Exact ── Reference ── FIFO)
     └── Atomic DB Transaction Allocation
                    │
                    ▼
      PostgreSQL Immutable Ledger & Wallet

---

## Key Structural Pillars

*   **Financial Precision Engine:** We process money exclusively using integer kobo ($1 \text{ NGN} = 100 \text{ kobo}$) to entirely eliminate IEEE 754 floating-point rounding bugs.
*   **Immutable Accounting:** Our transaction core utilizes an append-only ledger architecture (`ledger_entries`). Financial logs are never updated or deleted; data corrections require deterministic balancing entries.
*   **Idempotency & Atomicity Guarantees:** Redis distributed locks guard against webhook duplication, while atomic database transactions protect data splits across ledgers, virtual profiles, and credit wallets.

---

## Tech Stack Ecosystem

We leverage robust, modern, and highly scalable technologies across our open-source repositories:

*   **Backend Core:** Node.js, Express 5, TypeScript
*   **Background Jobs & Automation:** BullMQ + Redis (Aiven Valkey)
*   **Data Persistence Layer:** PostgreSQL 16 (Aiven)
*   **Frontend Interfaces:** Next.js 14 (App Router), React Query, Tailwind CSS
*   **Observability & Telemetry:** Sentry (Full-Stack), Pino Structured JSON Logging
*   **Containerization & DevOps:** Docker, Docker Compose

---

## Flagship Project: LedgerCore MVP

Our primary repository contains the complete full-stack codebase for the LedgerCore engine. 

### ⚡ Core Capabilities Under the Hood
1.  **Automated VA Management:** On-demand generation and atomic rollbacks of customer virtual accounts via the Nomba API.
2.  **Flexible Obligation Profiles:** Engine handling for recurring subscriptions, singular invoices, levies, and custom fees.
3.  **3-Tier Matching Cascade:** Algorithmic prioritization that matches funds based on **Exact Match Balance** $\rightarrow$ **Narration Reference Code Verification** $\rightarrow$ **FIFO (First In, First Out)** line-item clearance.
4.  **Customer Credit Wallet:** Native overpayment routing that locks excess customer funds into a specialized digital wallet for automatic deduction on future invoices.

### Try the Live Platform
Our live deployment is open for interactive evaluation.

*   **Live App URL:** [https://velo-credit-ledger-core.vercel.app/auth/signup](https://velo-credit-ledger-core.vercel.app/auth/signup)
> 💡 **Testing Recommendations:** Log into the dashboard, create an invoice obligation for a pre-populated customer under the **Obligations** page, and simulate a payment webhook variation (Exact, Partial, or Overpayment) to track live state updates and automatic ledger entry append cycles.

---

## Platform Roadmap (Next Phase)

We are actively expanding LedgerCore from an engine into a complete financial operations portal. Contributions are welcome on the following vectors:

- [ ] **Developer Self-Service Webhook Panel:** Removing manual config steps so developers can assign, test, and cycle endpoint secrets on demand.
- [ ] **KYC-Free Sandbox Environment:** Full mock parity matching production capabilities for rapid engineering iterations without onboarding hurdles.
- [ ] **Merchant Pay-Outs:** Outbound payment infrastructure connecting directly to Nomba's payout API pipelines.
- [ ] **Customer Portal Experience:** Dedicated, read-only Next.js workspace for end-consumers to manage outstanding balances and statement archives.
- [ ] **Automated Dunning Rules:** Multi-channel notification dispatchers (Email, SMS) evaluating daily invoice decay trends.

---

## 🤝 Community & Contributions
We care deeply about developer experience. Our repositories are structured with **Conventional Commits**, **Husky pre-commit validation hooks**, and comprehensive Postman documentation environments. 

For security vulnerabilities or core infrastructure inquiries, please open an issue inside the respective project repository. Let's make financial engineering straightforward, automated, and reliable!
