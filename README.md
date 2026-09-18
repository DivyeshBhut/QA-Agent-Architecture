# 🤖 Autonomous SDET Agent Architecture

Welcome to the **Autonomous SDET Agent** architectural repository. This project outlines the complete system design for an autonomous, multi-agent AI framework that ingests tabular test cases and generates production-ready, self-healing **Playwright C# NUnit** automation suites.

---

## 📚 Architecture Documents

We have structured the architecture into two dedicated documents depending on your audience:

| Document | Purpose & Target Audience | Key Contents |
| :--- | :--- | :--- |
| [**High-Level Architecture**](file:///c:/Users/bhutd/Desktop/AI%20Agent/high-level-architecture.md) | **Presentations, Stakeholders & Leadership** | System topology diagram, value proposition, 5-phase lifecycle, comparison matrix, and parallel team model |
| [**Detailed Architecture Overview**](file:///c:/Users/bhutd/Desktop/AI%20Agent/detailed-architecture-overview.md) | **Engineering Deep-Dive & Implementation** | 5 Markdown artifact contracts, Complex UI Engine, Regression Guard, Playwright Traces, Roslyn AST mining & FSM |

---

## ⚡ Quick Summary: The Markdown-First Pipeline

```
[Test Sheet (Excel/CSV) + Target URL + C# Repository]
                         │
                         ▼
      ┌──────────────────────────────────────┐
      │       Master SDET Supervisor         │
      └──────────────────┬───────────────────┘
                         │
                         ▼
        ┌──────────────────────────────────┐
        │  Shared Markdown Workspace       │
        │  (/artifacts/*.md)               │
        ├──────────────────────────────────┤
        │ • 01-action-plan.md              │ <── Subagent 1 (Planner)
        │ • 02-test-data.md                │ <── Subagent 2 (Data Synthesizer)
        │ • 03-codebase-spec.md            │ <── Subagent 3 (Codebase Analyst)
        │ • 04-locator-catalog.md          │ <── Subagent 4 (Browser Explorer & Complex UI)
        │ • 05-execution-report.md         │ <── Subagent 6 (Runner, Healer & Evidence)
        └────────────────┬─────────────────┘
                         │
                         ▼
        ┌──────────────────────────────────┐
        │ Subagent 5: C# Code Synthesizer  │
        │ • Writes Pages/*Page.cs          │
        │ • Writes Tests/*Tests.cs         │
        └────────────────┬─────────────────┘
                         │
                         ▼
        ┌──────────────────────────────────┐
        │ Subagent 6: Test Runner & Healer │
        │ • Runs 'dotnet test'             │
        │ • Regression Guard on POMs       │
        │ • Bundles screenshots & traces   │
        └──────────────────────────────────┘
```

---

## 🌟 Enterprise Highlights

1. **Markdown-First Contracts**: Subagents communicate through clean `.md` documents, avoiding C# quote-escaping bugs and cutting token overhead by ~35%.
2. **Complex UI Primitives Engine**: Native support for nested iFrames (`FrameLocator`), Shadow DOM piercing, dynamic comboboxes (Select2/Radix), and file uploads.
3. **Shared POM Regression Guard**: Modifying a shared Page Object automatically triggers tests on all dependent consumer test fixtures to guarantee zero regression.
4. **Visual Evidence & Traces**: Every failure and healed test run bundles embedded screenshots and Playwright Trace Viewer files (`trace.zip`).
5. **Parallel Team Development**: Decoupled workstreams enable 6 engineers to build all 6 subagents concurrently using mock Markdown files.

*Read the [Detailed Architecture Overview](file:///c:/Users/bhutd/Desktop/AI%20Agent/detailed-architecture-overview.md) for full contracts and workstream assignments.*
