# 🤖 AI PM Copilot

> An AI-powered Product Management workflow that helps Product Managers generate high-quality product artifacts using reusable prompts or a Claude Skill.

Instead of manually writing Product Requirements Documents (PRDs), User Stories, Product Teardowns, Roadmaps, or other PM artifacts, this repository provides a structured workflow that leverages prompt engineering and Claude Skills to accelerate product discovery and documentation.

---

# 🚀 Features

- 📄 Generate Product Requirement Documents (PRDs)
- 📚 Create User Stories & Acceptance Criteria
- 🔍 Perform Product Teardowns
- 📈 Build Product Roadmaps
- 📊 Generate KPI Trees & Metrics
- 🧪 Create Product Experiments
- 🎯 Prioritize Features
- 🤖 Use either standalone prompts or a Claude Skill

---

# 📁 Repository Structure

```
AI PM Copilot
│
├── reference-prompts/
│   ├── prompt-01.md
│   ├── prompt-02.md
│   ├── prompt-03.md
│   └── ...
│
├── claude-skill/
│   ├── skill.md
│   └── README.md
│
├── sample-input/
│   └── business-context.md
│
├── sample-output/
│   └── generated-artifacts.md
│
└── README.md
```

---

# 🧠 Two Ways to Use

## Option 1 – Standalone Prompts

Each prompt inside **reference-prompts** can be executed independently.

Example workflow

```
Business Context
        │
        ▼
Prompt 1
        │
        ▼
Prompt 2
        │
        ▼
Prompt 3
        │
        ▼
Final PM Artifact
```

This approach is useful when you want complete control over each step of the workflow.

---

## Option 2 – Claude Skill (Recommended)

Instead of copying and executing each prompt individually, install the provided Claude Skill.

The skill automatically orchestrates the workflow by invoking the appropriate prompts in the correct sequence.

```
Business Context
        │
        ▼
Claude Skill
        │
        ▼
Reference Prompts
        │
        ▼
Generated Product Artifact
```

This approach is faster, reusable, and provides a consistent output.

---

# 📂 Folder Guide

## reference-prompts/

Contains reusable prompt templates.

These prompts can be used independently or as part of the Claude Skill workflow.

Examples

- PRD Generator
- Product Discovery
- User Story Generator
- Acceptance Criteria
- KPI Generator
- Product Teardown
- Feature Prioritization
- Roadmap Generator

---

## claude-skill/

Contains the complete Claude Skill (`skill.md`).

The skill orchestrates the entire workflow and automatically references the prompt library.

Once installed in Claude, users only need to provide the business context to generate complete product documentation.

---

## sample-input/

Contains sample business context used to initiate the workflow.

Example

- Product vision
- Problem statement
- Target users
- Business goals
- Constraints

---

## sample-output/

Contains the generated deliverables after running the workflow.

Examples

- PRD
- User Stories
- Acceptance Criteria
- Product Roadmap
- KPIs
- Product Teardown
- Prioritized Backlog

---

# 🔄 Workflow

```
Business Context
        │
        ▼
Reference Prompts
(or Claude Skill)
        │
        ▼
AI Processing
        │
        ▼
Generated PM Deliverables
```

---

# 🎯 Who is this for?

- Product Managers
- Associate Product Managers
- Product Owners
- Business Analysts
- Startup Founders
- AI Product Builders

---

# 🛠️ Technologies

- Claude
- Prompt Engineering
- Claude Skills
- Markdown
- Product Management Frameworks

---

# 💡 Why This Project?

Traditional product documentation is often repetitive and time-consuming.

This repository demonstrates how AI can streamline Product Management workflows by combining structured prompts with reusable Claude Skills to generate consistent, high-quality product artifacts.

---

# 📜 License

This repository is intended for learning, experimentation, and portfolio demonstration purposes.