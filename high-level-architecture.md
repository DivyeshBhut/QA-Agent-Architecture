# 🚀 Autonomous SDET Agent: High-Level Architecture

> **An Autonomous Multi-Agent System for End-to-End Test Automation Engineering**  
> *From Tabular Test Cases to Production-Ready, Self-Healed C# Playwright NUnit Suites.*

---

## Executive Summary

The **Autonomous SDET Agent** is an enterprise-grade, multi-agent AI system designed to eliminate the manual overhead of authoring and maintaining automated browser test suites. 

By accepting four simple inputs:
1. **Test Case Sheet** (`.xlsx`, `.csv`)
2. **Target Web Application URL** (Staging, Pre-Prod, or Production)
3. **Target C# Automation Repository** (Existing .NET / NUnit codebase)
4. **Execution Configuration** (Credentials, Environment variables, Browser modes)

The system orchestrates a team of specialized worker subagents communicating via **Markdown-First Artifacts (`.md`)**. Built to withstand enterprise web applications, the architecture includes dedicated engines for **Complex UI Primitives (Shadow DOM, nested iFrames, dynamic comboboxes)**, a **Shared Page Object Regression Guard**, and **Playwright Trace/Screenshot Visual Evidence** for instant post-mortem debugging.

---

## 🎯 Core Value Proposition

```
┌───────────────────────────┐      ┌───────────────────────────┐      ┌───────────────────────────┐
│   Markdown-First Design   │      │   Complex UI Primitives   │      │  Zero-Regression Healing  │
│ Clean .md artifacts avoid │ ───► │ Native iFrames, Shadow    │ ───► │ Regression Guard re-tests │
│ escaping bugs and enable  │      │ DOM & custom combobox     │      │ shared POMs with bundled  │
│ parallel team sprints.    │      │ interaction strategies.   │      │ traces & screenshots.     │
└───────────────────────────┘      └───────────────────────────┘      └───────────────────────────┘
```

---

## 🏛️ System Architecture Topology

```mermaid
flowchart TB
    %% Styling definitions
    classDef inputStyle fill:#EBF5FB,stroke:#2980B9,stroke-width:2px,color:#1A5276;
    classDef coreStyle fill:#FEF9E7,stroke:#F39C12,stroke-width:2px,color:#7D6608;
    classDef subagentStyle fill:#E8F8F5,stroke:#16A085,stroke-width:2px,color:#0E6251;
    classDef artifactStyle fill:#F5EEF8,stroke:#8E44AD,stroke-width:2px,color:#4A235A;
    classDef envStyle fill:#FDEDEC,stroke:#E74C3C,stroke-width:2px,color:#78281F;

    %% 1. Ingestion Layer
    subgraph LayerInputs ["1. Ingestion Layer"]
        Sheet["📄 Test Case Sheet\n(Excel / CSV)"]:::inputStyle
        TargetApp["🌐 Target Web Application\n(Live URL)"]:::inputStyle
        TargetRepo["📁 C# Test Repository\n(.NET / NUnit Codebase)"]:::inputStyle
        Config["⚙️ Execution Config\n(Auth, Env, Headless Mode)"]:::inputStyle
    end

    %% 2. Agentic Orchestration Core
    subgraph LayerCore ["2. Agentic Orchestration Core"]
        Gateway["Hybrid Runtime Gateway\n(Developer CLI / REST & WebSocket API)"]:::coreStyle
        Orchestrator["🎯 Master SDET Supervisor Agent\n(State Machine, Scheduler & Circuit Breaker)"]:::coreStyle
        
        Gateway --> Orchestrator
    end

    %% 3. Specialized Worker Subagents
    subgraph LayerSubagents ["3. Specialized Worker Subagents"]
        direction TB
        Agent1["📋 Subagent 1: Test Ingestion & Planner\n• Parses human test steps\n• Emits: 01-action-plan.md"]:::subagentStyle
        Agent2["🎲 Subagent 2: Test Data Synthesizer\n• Dynamic data generation (Bogus / Faker)\n• Emits: 02-test-data.md"]:::subagentStyle
        Agent3["🔍 Subagent 3: Codebase Analyst (AST Miner)\n• Roslyn / Tree-Sitter syntax analysis\n• Emits: 03-codebase-spec.md"]:::subagentStyle
        Agent4["🌐 Subagent 4: Browser Explorer & Locator Engine\n• Complex UI Primitives: iFrames, Shadow DOM & Combos\n• Emits: 04-locator-catalog.md"]:::subagentStyle
        Agent5["💻 Subagent 5: C# Code Synthesizer\n• Generates idiomatic C# Page Objects & Tests\n• Writes: Pages/*Page.cs & Tests/*Tests.cs"]:::subagentStyle
        Agent6["🛡️ Subagent 6: Test Runner & Healer\n• Regression Guard on shared POMs\n• Emits: 05-execution-report.md + Traces & Screenshots"]:::subagentStyle
    end

    %% 4. Shared Markdown Artifacts & Evidence Layer
    subgraph LayerArtifacts ["4. Shared Markdown Workspace & Evidence (/artifacts)"]
        Art1["📄 01-action-plan.md"]:::artifactStyle
        Art2["📄 02-test-data.md"]:::artifactStyle
        Art3["📄 03-codebase-spec.md"]:::artifactStyle
        Art4["📄 04-locator-catalog.md"]:::artifactStyle
        Art5["📄 05-execution-report.md"]:::artifactStyle
        ArtMedia["📸 Screenshots & Traces\n(/screenshots & /traces/*.zip)"]:::artifactStyle
    end

    %% 5. Execution Sandboxes
    subgraph LayerSandboxes ["5. Execution Sandboxes"]
        BrowserEnv["🖥️ Playwright Browser Sandbox\n(Chromium / Firefox via CDP)"]:::envStyle
        DotnetEnv["⚡ .NET Execution Engine\n(dotnet CLI, Roslyn, NUnit)"]:::envStyle
    end

    %% Wiring Ingestion to Core
    Sheet --> Gateway
    TargetApp --> Gateway
    TargetRepo --> Gateway
    Config --> Gateway

    %% Orchestrator to Subagents
    Orchestrator --> Agent1
    Orchestrator --> Agent2
    Orchestrator --> Agent3
    Orchestrator --> Agent4
    Orchestrator --> Agent5
    Orchestrator --> Agent6

    %% Subagents write to Artifacts Workspace
    Agent1 --> Art1
    Agent2 --> Art2
    Agent3 --> Art3
    Agent4 --> Art4
    Agent6 --> Art5
    Agent6 --> ArtMedia

    %% Subagents read from Artifacts Workspace
    Art1 -.-> Agent4
    Art2 -.-> Agent4
    Art3 -.-> Agent5
    Art4 -.-> Agent5

    %% Subagent interactions with external environments
    Agent4 <-->|CDP Protocol / Live DOM| BrowserEnv
    BrowserEnv -->|Live Interaction & AOM| TargetApp
    Agent3 <-->|AST Code Inspection| TargetRepo
    Agent5 -->|Write *.cs Files| TargetRepo
    Agent6 <-->|Execute Build & Test| DotnetEnv
    DotnetEnv -->|Run Test Suite| TargetApp

    %% Self-Healing Feedback
    Agent6 -.->|Heal Locators| Agent4
    Agent6 -.->|Heal Code / Syntax| Agent5
```

---

## 🔄 The 5-Phase Markdown Lifecycle

```mermaid
graph LR
    P1["1. Ingest & Plan\n(Sheet → 01-action-plan.md)"] --> P2["2. Mine Codebase\n(AST → 03-codebase-spec.md)"]
    P2 --> P3["3. Explore & Locate\n(Complex UI Primitives → 04-locator-catalog.md)"]
    P3 --> P4["4. Synthesize Code\n(Artifacts → C# *.cs files)"]
    P4 --> P5["5. Verify & Heal\n(Regression Guard → 05-execution-report.md)"]
```

### Phase 1: Ingestion & Data Preparation
* Parses arbitrary test sheets using semantic mapping.
* Normalizes human-written steps into `01-action-plan.md`.
* Resolves dynamic placeholders (unique emails, boundary dates) into `02-test-data.md` using **Bogus**.

### Phase 2: Codebase Architectural Mining
* Performs static syntax analysis (Roslyn / Tree-sitter) on the existing C# repository.
* Discovers existing **BasePage**, **PageTest**, namespace structures, locator property formats, and builds a dependency graph of existing test fixtures.

### Phase 3: Live Browser Exploration (Complex UI Engine)
* Launches an active Playwright browser instance connected to the target application.
* Interactively steps through each user action on the live DOM.
* Handles **Shadow DOM**, **nested iFrames**, **custom floating comboboxes**, and **file uploads**.
* Generates `04-locator-catalog.md` with Playwright ARIA priority ranking.

### Phase 4: C# Code Synthesis
* Reads `04-locator-catalog.md` and `03-codebase-spec.md`.
* Writes or patches Page Object classes (`*Page.cs`) and NUnit test fixtures (`*Tests.cs`).
* Ensures 100% adherence to the mined architectural patterns without escaping or formatting errors.

### Phase 5: Closed-Loop Verification & Regression Guard
* Executes `dotnet build` and `dotnet test`.
* **Shared POM Regression Guard**: If a shared Page Object was modified, re-runs all dependent existing tests to guarantee zero regression.
* Automatically bundles **failure screenshots** and **Playwright Traces (`trace.zip`)** into `05-execution-report.md`.

---

## 👥 Parallel Team Development Model (Chunked Workstreams)

Because each subagent communicates through standardized **Markdown Artifacts**, your engineering team can build all subagents simultaneously without blocking:

```mermaid
flowchart TD
    Contracts["📐 Step 0: Team Agrees on Markdown Artifact Formats\n(01-action-plan.md, 03-codebase-spec.md, 04-locator-catalog.md)"]
    
    subgraph ParallelWorkstreams ["Parallel Independent Developer Sprints"]
        direction TB
        Dev1["🧑‍💻 Dev 1: Subagent 1 (Test Planner)\n• Input: Sample Excel/CSV\n• Builds: Parser that generates 01-action-plan.md"]
        Dev2["🧑‍💻 Dev 2: Subagent 2 (Test Data Synthesizer)\n• Input: Mock 01-action-plan.md\n• Builds: Bogus data generator for 02-test-data.md"]
        Dev3["🧑‍💻 Dev 3: Subagent 3 (Codebase Analyst)\n• Input: Sample C# NUnit repo\n• Builds: Roslyn/AST miner for 03-codebase-spec.md"]
        Dev4["🧑‍💻 Dev 4: Subagent 4 (Browser Explorer & Locators)\n• Input: Mock 01-action-plan.md + Live Web URL\n• Builds: Playwright CDP engine (iFrames/Shadow DOM)"]
        Dev5["🧑‍💻 Dev 5: Subagent 5 (C# Code Synthesizer)\n• Input: Mock 04-locator-catalog.md + 03-codebase-spec.md\n• Builds: Generator that outputs *.cs files"]
        Dev6["🧑‍💻 Dev 6: Subagent 6 & Master Orchestrator\n• Input: 'dotnet test' + Regression Guard + Traces\n• Builds: Runner, Healer & Supervisor pipeline"]
    end
    
    Contracts --> Dev1
    Contracts --> Dev2
    Contracts --> Dev3
    Contracts --> Dev4
    Contracts --> Dev5
    Contracts --> Dev6
    
    ParallelWorkstreams --> Integration["🔗 Integration Milestone: Replace Mock Markdown files with live Subagent outputs"]
```

---

## 🛡️ Key Architectural Guardrails

> [!IMPORTANT]
> **No Hallucinated Locators**  
> Locators are never guessed from raw HTML strings. The Browser Explorer Subagent physically interacts with the live element in a real browser and asserts `count == 1` and `isVisible == true` before documenting it in `04-locator-catalog.md`.

> [!TIP]
> **Shared Page Object Regression Guard**  
> Updating an existing Page Object for a new test will never break older tests. The regression guard automatically runs dependent test suites to guarantee backwards compatibility.

> [!NOTE]
> **Complex UI Primitives Native Support**  
> Handles enterprise web complexities natively: iFrames (`FrameLocator`), Shadow DOM piercing, custom React/Select2 comboboxes, and file uploads.

---

## 📈 System Metrics & Showcase Highlights

| Dimension | Traditional Manual SDET | Autonomous SDET Agent |
| :--- | :--- | :--- |
| **Inter-Agent Protocol** | N/A (Manual human handoffs) | **Markdown-First Artifacts (`.md`)** |
| **Time per Test Case** | 2 – 4 hours | 2 – 4 minutes |
| **Complex UI Handling** | Manual inspection of iFrames & Shadow DOM | **Automated Primitive Engine (FrameLocator/Combos)** |
| **Shared POM Safety** | High risk of breaking existing tests | **Automated Regression Guard on consumer tests** |
| **Visual Debugging** | Manual reproduction required | **Bundled failure screenshots & `trace.zip`** |
| **Team Parallelization** | High sequential dependencies | **Decoupled workstreams via mock `.md` files** |

---

*For full low-level technical specifications, Markdown schemas, locator decision trees, and AST mining rules, refer to [Detailed Architecture Overview](file:///c:/Users/bhutd/Desktop/AI%20Agent/detailed-architecture-overview.md).*
