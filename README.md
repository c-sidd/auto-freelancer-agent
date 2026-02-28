# Auto-Freelancer Agent  
**Pinion OS Hackathon Submission**

An autonomous software agent that behaves like a freelancer:
it discovers paid tasks, decides whether they are profitable, executes them,
and pays for execution using **Pinion OS x402 micropayments**.

This project is designed to be **secure-by-default**, **demo-friendly**, and
**production-correct**.

---

## 🧠 Core Idea

Traditional software:
- Executes logic
- Humans handle payments

This agent:
- Executes logic **and**
- Handles payments autonomously

**Pinion OS** enables this by allowing software to pay for execution via
**x402 micropayments (USDC on Base)**.

---

## 🏗️ High-Level Architecture
Job Source
↓
Decision Engine (Is it profitable?)
↓
Executor
↓
Pinion OS (x402-paid skills)


- **Job Source**: Provides paid tasks
- **Decision Engine**: Accepts or rejects tasks based on economics
- **Executor**: Runs the task
- **Pinion OS**: Handles payment and skill execution

---

## 📂 Logical Structure (Conceptual)
index.js → Main agent loop
jobs.js → Paid task definitions
decision.js → Profitability logic
executor.js → Task execution
wallet.js → Pinion OS integration (real + demo)


> Note: Files are modular for clarity, but the system can also be run
> as a single-file demo.

---

## 🔑 How Pinion OS Is Used

Pinion OS is used as the **payment and skill execution layer**.

- The agent calls **x402-paid skills** via `PinionClient`
- Payments are settled in **USDC on Base**
- Gas fees are paid using **ETH on Base**

The agent **does not manage payments manually** — Pinion OS handles:
- x402 signing
- Payment verification
- Settlement

---

## 🧪 Demo Mode vs 💸 Real Mode

### 🧪 Demo Mode (Default)

Demo mode is used when:
- No `PINION_PRIVATE_KEY` is set
- The user wants to run without crypto
- Judges want a quick local demo

Behavior:
- No on-chain payments
- Skill results are simulated
- Full agent logic still runs
- Same execution flow as real mode

This allows **anyone** to run the project instantly.

---

### 💸 Real Mode (Optional)

Real mode is enabled when:
- `PINION_PRIVATE_KEY` is set
- Wallet has **ETH + USDC on Base**

Behavior:
- Each skill call triggers a **real x402 payment**
- ~$0.01 USDC per call
- ETH is used for gas
- Settlement is automatic

**No code changes are required** to switch from demo → real mode.

---

## ⚙️ How to Run

### Demo Mode (No Money Required)

```bash
npm install
node index.js

Expected output:
🤖 Auto-Freelancer Agent started
🔍 Found job: Fetch ETH price
✅ Job accepted
⚙️ Executing job
📊 ETH price: 2650.00
🔁 Execution mode: demo
💰 Job completed autonomously
