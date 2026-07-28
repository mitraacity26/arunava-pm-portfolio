# 🤖 AI PM Workflow

> An AI-powered Product Management workflow that transforms a business idea into complete product artifacts using Prompt Engineering and Claude Skills.

---

## 🚀 Overview

This repository demonstrates an end-to-end AI-assisted Product Management workflow.

Starting with a business idea, the workflow automates product discovery, strategy, planning, and execution to generate high-quality product artifacts.

You can execute the workflow in two ways:

- 📝 **Prompt Library** – Run each prompt independently.
- 🤖 **Claude Skill (Recommended)** – Install the Claude Skill to automatically orchestrate the complete workflow.

---

# 📂 Repository Structure

```
pm-discovery-to-execution artifact generator/
│
├── pm-discovery-to-execution/     # Claude Skill + reusable prompt library
│       ├── SKILL.md                             # Claude Skill definition (orchestrates the workflow)
│       └── references/                          # Standalone prompts, one per PM activity
│           ├── 01-discovery.md
│           ├── 02-persona-mapping.md
│           ├── 03-empathy-map.md
│           ├── 04-customer-journey-map.md
│           ├── 05-business-model-canvas.md
│           ├── 06-goals-measurement.md
│           ├── 07-strategic-alternatives.md
│           ├── 08-prioritization.md
│           ├── 09-mvp-scope-identifier.md
│           ├── 10-prd.md
│           ├── 11-roadmap.md
│           ├── 12-gtm.md
│           ├── 13-feature-detail.md
│           ├── 14-feature-story.md
│           └── 15-pmf.md
│
├── sample input (business context)/             # Sample business inputs
├── sample output/                                # Generated product artifacts
└── README.md
```

---

# 🔄 Workflow

<p align="center">
    <img src="https://github.com/mitraacity26/arunava-pm-portfolio/tree/main/03_product-artifacts/Discovery_to_Execution_Workflow.jpg"
         alt="AI PM Workflow"
         width="950"/>
</p>

The workflow begins with a **Business Context**, processes it using either the **Prompt Library** or the **Claude Skill**, and generates complete Product Management deliverables.

---

# 📥 Input

Provide a business context containing:

- Product Vision
- Problem Statement
- Target Users
- Business Goals
- Constraints

---

# ⚙️ Execution

## Option 1 — Prompt Library

Execute the prompts sequentially.

```
Business Context
        │
        ▼
Prompt Library
        │
        ▼
PM Workflow
        │
        ▼
Product Artifacts
```

---

## Option 2 — Claude Skill ⭐ Recommended

**Setup (one-time):**

1. Zip the `pm-discovery-to-execution` folder (it contains `SKILL.md` and the `references/` prompt files).
2. In Claude, go to **Settings → Features → Skills** and upload the zip file (requires code execution to be enabled; available on Free, Pro, Max, Team, and Enterprise plans).

Once installed, provide only the business context.

The skill automatically executes the required prompts and generates the complete output.

```
Business Context
        │
        ▼
Claude Skill
        │
        ▼
Prompt Library
        │
        ▼
PM Workflow
        │
        ▼
Product Artifacts
```

---

# 📤 Output

The workflow generates:

- 📄 Product Requirement Document (PRD)
- 📖 User Stories
- ✅ Acceptance Criteria
- 🛣️ Product Roadmap
- 🎯 Product Strategy
- 📊 KPIs & Success Metrics
- 👥 User Personas
- 🗺️ Customer Journey Map
- 🚀 Go-To-Market (GTM) Plan
- 🧪 Product Experiments
- 📱 Product Teardowns
- 📈 Product-Market Fit Assessment

---

# 🎯 Purpose

The objective of this repository is to demonstrate how Prompt Engineering and Claude Skills can automate the Product Management lifecycle, producing consistent, high-quality deliverables from a single business context.

---

**If you found this repository useful, consider giving it a ⭐.**