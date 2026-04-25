---
theme: default
title: Multi-Agent Coordination for Construction AI
author: Data-Driven Construction (DDC)
colorSchema: light
aspectRatio: 16/9
transition: slide-left
fonts:
  sans: Arial, sans-serif
  serif: Arial, serif
  mono: Fira Code, monospace
themeConfig:
  primary: '#0070F2'
drawings:
  enabled: false
exportFilename: MultiAgent_Construction_Patterns
---

# Multi-Agent Coordination Patterns
## for Data-Driven Construction Automation

<div class="absolute bottom-10 left-14">
  <div style="color: #354A5F; font-weight: 600;">Based on: Anthropic Coordination Guidelines · DDC Skills Framework · Boiko (2025)</div>
  <div class="text-sm mt-1" style="color: #687078;">Construction AI Agent Swarm — Phase 5 Target Architecture</div>
</div>

---
layout: default
---

# Agenda

<div class="grid grid-cols-2 gap-8 mt-8">
  <div class="flex gap-4">
    <div class="text-4xl font-bold" style="color: #0070F2;">01</div>
    <div>
      <div class="font-semibold">The Construction Data Problem</div>
      <div class="text-sm" style="color: #687078;">Why construction lags behind other industries</div>
    </div>
  </div>
  <div class="flex gap-4">
    <div class="text-4xl font-bold" style="color: #0070F2;">02</div>
    <div>
      <div class="font-semibold">Five Coordination Patterns</div>
      <div class="text-sm" style="color: #687078;">Definitions, selection criteria, trade-offs</div>
    </div>
  </div>
  <div class="flex gap-4">
    <div class="text-4xl font-bold" style="color: #0070F2;">03</div>
    <div>
      <div class="font-semibold">Construction Applications</div>
      <div class="text-sm" style="color: #687078;">Cost estimation, schedules, BIM, documents</div>
    </div>
  </div>
  <div class="flex gap-4">
    <div class="text-4xl font-bold" style="color: #0070F2;">04</div>
    <div>
      <div class="font-semibold">DDC Agent Swarm Architecture</div>
      <div class="text-sm" style="color: #687078;">Recommended production system design</div>
    </div>
  </div>
</div>

---
layout: two-cols
---

# Construction's Data Problem

- **Last of 19 industries** in IT spending
- Banks decide in **minutes** — data only
- Agriculture decides in **hours** — data + experience
- Construction decides in **days** — opinion
- BIM and PMIS offer **highest ROI** potential
- Adoption remains **critically low**

<div class="mt-6 p-3 rounded-lg" style="background-color: #001944;">
  <div style="color: #89D1FF; font-size: 0.9em;">"The digital future of construction is not just about new technologies — it is fundamentally rethinking data handling and business models."</div>
  <div class="text-sm mt-2" style="color: #687078;">— Boiko, DDC Book (2025)</div>
</div>

::right::

<div class="h-full flex flex-col justify-center pl-8 gap-4">
  <div class="p-4 rounded-lg" style="background-color: #D1EFFF;">
    <div class="font-semibold" style="color: #0070F2;">Banking</div>
    <div class="text-sm" style="color: #354A5F;">Decisions in minutes — 100% data-driven</div>
  </div>
  <div class="p-4 rounded-lg" style="background-color: #D1EFFF;">
    <div class="font-semibold" style="color: #049F9A;">Agriculture</div>
    <div class="text-sm" style="color: #354A5F;">Decisions in hours — data + experience</div>
  </div>
  <div class="p-4 rounded-lg" style="background-color: #FFA0A0;">
    <div class="font-semibold" style="color: #AA0808;">Construction</div>
    <div class="text-sm" style="color: #354A5F;">Decisions in days — opinion-based</div>
  </div>
</div>

---
layout: default
---

# The DDC Framework: BIM + AI + Multi-Agent

<div class="grid grid-cols-3 gap-6 mt-6">
  <div class="p-5 rounded-xl" style="background-color: #D1EFFF; border-top: 4px solid #0070F2;">
    <div class="text-xl font-bold" style="color: #0070F2;">BIM = Database</div>
    <div class="text-sm mt-3" style="color: #354A5F;">IFC files expose structured volumes, areas, materials via ifcopenshell — no 3D viewer required</div>
  </div>
  <div class="p-5 rounded-xl" style="background-color: #D1EFFF; border-top: 4px solid #049F9A;">
    <div class="text-xl font-bold" style="color: #049F9A;">55,719 CWICR Items</div>
    <div class="text-sm mt-3" style="color: #354A5F;">Standardized work item database in 9 languages — semantic search via Qdrant vector DB</div>
  </div>
  <div class="p-5 rounded-xl" style="background-color: #D1EFFF; border-top: 4px solid #F58B00;">
    <div class="text-xl font-bold" style="color: #F58B00;">Phase 5 Goal</div>
    <div class="text-sm mt-3" style="color: #354A5F;">Construction AI Agent Swarm: PLANNER · ESTIMATOR · SCHEDULER · VALIDATOR · REPORTER</div>
  </div>
</div>

<div class="mt-6 p-3 rounded-lg" style="background-color: #EAECEE;">
  <strong style="color: #354A5F;">Gartner 2025:</strong>
  <span style="color: #354A5F;"> Multi-agent system inquiries surged 1,445% from Q1 2024 to Q2 2025. 40% of enterprise applications will embed AI agents by end of 2026.</span>
</div>

---
layout: center
class: text-center
---

<div class="text-6xl font-bold" style="color: #0070F2;">
Five Coordination Patterns
</div>
<div class="text-xl mt-4" style="color: #687078;">
Selecting the right architecture for each construction task
</div>

---
layout: default
---

# The Five Patterns at a Glance

| Pattern | Primary Strength | Construction Application |
|---------|-----------------|--------------------------|
| **Generator-Verifier** | Quality-critical output, explicit criteria | Cost estimate validation, BIM IDS compliance |
| **Orchestrator-Subagent** | Clear decomposition, parallel subtasks | IFC → cost estimate pipeline |
| **Agent Teams** | Long-running specialist context | Multi-package estimating, multi-building |
| **Message Bus** | Event-driven, extensible ecosystem | RFI processing, document routing |
| **Shared-State** | Collaborative knowledge accumulation | Project knowledge base, benchmarks |

<div class="mt-4 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <strong style="color: #0070F2;">Production recommendation:</strong>
  <span style="color: #354A5F;"> Combine Orchestrator-Subagent + Shared-State + Generator-Verifier — not a single pattern</span>
</div>

---
layout: two-cols
---

# Pattern 1: Generator-Verifier

**Best for:** Quality-critical outputs with explicit criteria

- Generator agent produces initial output
- Verifier checks against defined criteria
- Failure returns structured feedback to generator
- Loop continues until criteria are satisfied

<div class="mt-4 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <div class="font-semibold" style="color: #0070F2;">Construction use cases</div>
  <div class="text-sm" style="color: #354A5F;">Cost estimate validation · BIM IDS compliance · Schedule logic checks</div>
</div>
<div class="mt-3 p-3 rounded-lg" style="background-color: #FFA0A0;">
  <div class="text-sm font-semibold" style="color: #AA0808;">Key risk: early victory problem</div>
  <div class="text-sm" style="color: #354A5F;">Vague criteria produce rubber-stamp approval — be explicit</div>
</div>

::right::

<div class="flex items-center justify-center h-full">

```mermaid {scale: 0.75}
flowchart TB
    G[Generator Agent\nproduces estimate] --> V[Verifier Agent\nexplicit criteria]
    V -->|Pass| Out([Validated\nOutput])
    V -->|Fail + feedback| G
```

</div>

---
layout: two-cols
---

# Pattern 2: Orchestrator-Subagent

**Best for:** Multi-step tasks with clear decomposition

- Orchestrator decomposes and delegates tasks
- Subagents work in isolated context windows
- Each returns distilled, compact findings
- Orchestrator synthesizes final output

<div class="mt-4 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <div class="font-semibold" style="color: #0070F2;">Construction use cases</div>
  <div class="text-sm" style="color: #354A5F;">IFC → cost estimation · BIM analysis · Complex document processing</div>
</div>
<div class="mt-3 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <div class="text-sm font-semibold" style="color: #0070F2;">Key benefit: context protection</div>
  <div class="text-sm" style="color: #354A5F;">5,000+ token IFC data never enters the Rate Calculator context</div>
</div>

::right::

<div class="flex items-center justify-center h-full">

```mermaid {scale: 0.75}
flowchart TB
    Orch[Orchestrator] --> A[Subagent A]
    Orch --> B[Subagent B]
    Orch --> C[Subagent C]
    A -->|distilled result| Orch
    B -->|distilled result| Orch
    C -->|distilled result| Orch
    Orch --> Out([Synthesized\nOutput])
```

</div>

---
layout: two-cols
---

# Pattern 3: Agent Teams

**Best for:** Parallel long-running specialist analyses

- Coordinator assigns work from a shared queue
- Worker agents persist across many assignments
- Workers accumulate deep domain context
- Best for independent, partitioned workloads

<div class="mt-4 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <div class="font-semibold" style="color: #0070F2;">Construction use cases</div>
  <div class="text-sm" style="color: #354A5F;">Multi-package estimating · Multi-building scheduling · Trade-specific analysis</div>
</div>
<div class="mt-3 p-3 rounded-lg" style="background-color: #FFD23D;">
  <div class="text-sm font-semibold" style="color: #9A5B00;">Key requirement: independence</div>
  <div class="text-sm" style="color: #354A5F;">Teammates cannot share context directly — partition by trade or zone</div>
</div>

::right::

<div class="flex items-center justify-center h-full">

```mermaid {scale: 0.75}
flowchart TB
    Coord[Coordinator] --> T1[ESTIMATOR\nPackage A]
    Coord --> T2[ESTIMATOR\nPackage B]
    Coord --> T3[ESTIMATOR\nPackage C]
    T1 -->|result| Coord
    T2 -->|result| Coord
    T3 -->|result| Coord
    Coord --> Out([Consolidated\nEstimate])
    style Coord fill:#0070F2,color:#fff
```

</div>

---
layout: two-cols
---

# Pattern 4: Message Bus

**Best for:** Event-driven, growing agent ecosystems

- Agents publish to topics and subscribe to events
- Router delivers matching messages automatically
- New agents added without rewiring existing ones
- Every event logged with timestamp and agent ID

<div class="mt-4 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <div class="font-semibold" style="color: #0070F2;">Construction use cases</div>
  <div class="text-sm" style="color: #354A5F;">RFI processing · Change order tracking · Document routing · Submittal review</div>
</div>
<div class="mt-3 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <div class="text-sm font-semibold" style="color: #0070F2;">Key benefit: extensibility</div>
  <div class="text-sm" style="color: #354A5F;">New document types → new subscriber agents, no rewiring</div>
</div>

::right::

<div class="flex items-center justify-center h-full">

```mermaid {scale: 0.70}
flowchart TB
    Email[Email Monitor] --> Bus[Message Bus\nn8n]
    Bus --> DC[Document\nClassifier]
    DC --> Bus
    Bus --> RP[RFI Parser]
    RP --> Bus
    Bus --> BQ[BIM Query\nAgent]
    style Bus fill:#0070F2,color:#fff
```

</div>

---
layout: two-cols
---

# Pattern 5: Shared-State

**Best for:** Collaborative knowledge accumulation

- No central coordinator — agents act autonomously
- All agents read and write to persistent store
- Write domains partitioned to prevent conflicts
- Termination: convergence signal from Validator

<div class="mt-4 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <div class="font-semibold" style="color: #0070F2;">Construction use cases</div>
  <div class="text-sm" style="color: #354A5F;">Project knowledge base · Historical cost database · Cross-session institutional memory</div>
</div>
<div class="mt-3 p-3 rounded-lg" style="background-color: #FFD23D;">
  <div class="text-sm font-semibold" style="color: #9A5B00;">Key risk: reactive loops</div>
  <div class="text-sm" style="color: #354A5F;">Each agent must write only to its designated domain</div>
</div>

::right::

<div class="flex items-center justify-center h-full">

```mermaid {scale: 0.68}
flowchart LR
    A[CPM Agent] --> CP[critical_path]
    B[Resource Agent] --> RA[resource_alloc]
    C[4D Agent] --> SC[spatial_conflicts]
    D[Duration Agent] --> PR[predictions]
    CP --> V[Validator]
    RA --> V
    SC --> V
    PR --> V
```

</div>

---
layout: two-cols
---

# Pattern Selection Guide

**Choose based on task characteristics:**

- Explicit quality criteria → **Generator-Verifier**
- Event-driven, growing ecosystem → **Message Bus**
- Long-running parallel specialists → **Agent Teams**
- Knowledge accumulation across agents → **Shared-State**
- Multi-step decomposition → **Orchestrator-Subagent**

<div class="mt-4 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <div class="font-semibold" style="color: #0070F2;">Production systems combine patterns</div>
  <div class="text-sm" style="color: #354A5F;">Primary: Orchestrator-Subagent + Shared-State knowledge layer + Generator-Verifier quality gate</div>
</div>

::right::

<div class="flex items-center justify-center h-full">

```mermaid {scale: 0.65}
flowchart LR
    A[Construction Task] --> GV[Generator-Verifier\nExplicit quality criteria]
    A --> MB[Message Bus\nEvent-driven workflow]
    A --> AT[Agent Teams\nLong-running specialists]
    A --> SS[Shared-State\nKnowledge accumulation]
    A --> OS[Orchestrator-Subagent\nDecomposable tasks]
```

</div>

---
layout: center
class: text-center
---

<div class="text-6xl font-bold" style="color: #0070F2;">
Construction Applications
</div>
<div class="text-xl mt-4" style="color: #687078;">
Deep dives: Cost Estimation · Scheduling · Documents · BIM
</div>

---
layout: default
---

# Recommended Hybrid Architecture

<div class="grid grid-cols-3 gap-6 mt-6">
  <div class="p-5 rounded-xl" style="background-color: #D1EFFF; border-left: 5px solid #0070F2;">
    <div class="font-bold text-lg" style="color: #0070F2;">Orchestrator-Subagent</div>
    <div class="text-sm mt-2" style="color: #354A5F;">Primary workflow: decomposes tasks, dispatches specialized subagents, synthesizes outputs</div>
    <div class="text-xs mt-3" style="color: #687078;">IFC Parser · CWICR Matcher · Rate Calculator · Document Processor</div>
  </div>
  <div class="p-5 rounded-xl" style="background-color: #D1EFFF; border-left: 5px solid #049F9A;">
    <div class="font-bold text-lg" style="color: #049F9A;">Shared-State</div>
    <div class="text-sm mt-2" style="color: #354A5F;">Persistent knowledge layer: Qdrant + PostgreSQL accumulate institutional project knowledge across sessions</div>
    <div class="text-xs mt-3" style="color: #687078;">CWICR embeddings · Historical estimates · Document extracts</div>
  </div>
  <div class="p-5 rounded-xl" style="background-color: #D1EFFF; border-left: 5px solid #F58B00;">
    <div class="font-bold text-lg" style="color: #F58B00;">Generator-Verifier</div>
    <div class="text-sm mt-2" style="color: #354A5F;">Quality gate at every output: explicit criteria prevent false positives from reaching users</div>
    <div class="text-xs mt-3" style="color: #687078;">Estimate validation · Schedule verification · BIM compliance</div>
  </div>
</div>

<div class="mt-6 p-3 rounded-lg" style="background-color: #001944;">
  <span style="color: #89D1FF; font-weight: 600;">Anthropic:</span>
  <span style="color: #D1EFFF;"> "A common hybrid uses orchestrator-subagent for the overall workflow with shared state for a collaboration-heavy subtask."</span>
</div>

---
layout: two-cols
---

# Cost Estimation Pipeline
## 16 hours → 2 hours (87% faster)

- **Stage 1:** IFC Parser extracts element inventory
- **Stage 2:** CWICR Matcher — Qdrant semantic search
- **Stage 3:** Rate Calculator — PostgreSQL unit rates
- **Stage 4:** Validator — statistical range checks
- **Stage 5:** Orchestrator synthesizes final report

<div class="mt-4 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <div class="font-semibold" style="color: #0070F2;">Context isolation benefit</div>
  <div class="text-sm" style="color: #354A5F;">5,000+ token IFC element data never enters the Rate Calculator context — clean subagent boundaries</div>
</div>

::right::

<div class="flex items-center justify-center h-full">

```mermaid {scale: 0.75}
flowchart TB
    A[IFC File] --> B[IFC Parser]
    B --> C[CWICR Matcher]
    C --> D[Rate Calculator]
    D --> E[Validator]
    E --> F[Cost Estimate Report]
```

</div>

---
layout: two-cols
---

# Schedule Optimization
## Agent Teams + Shared-State

- **CPM Agent** writes critical path activities
- **Resource Agent** reads CPM, writes leveled durations
- **4D Simulation** reads both, writes spatial conflicts
- **Duration Agent** writes ML-predicted durations
- **Validator** monitors all sections — signals convergence

<div class="mt-4 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <div class="font-semibold" style="color: #0070F2;">Write domain partitioning</div>
  <div class="text-sm" style="color: #354A5F;">Each agent writes only to its section — prevents reactive loops. polars: 7-10x faster than pandas for large activity networks.</div>
</div>

::right::

<div class="flex items-center justify-center h-full">

```mermaid {scale: 0.62}
flowchart LR
    CPM[CPM Analyst] --> CP[critical_path]
    RLA[Resource Agent] --> RA[resource_alloc]
    Sim[4D Simulation] --> SC[spatial_conflicts]
    DPA[Duration Agent] --> PR[predictions]
    CP --> Val[Validator]
    RA --> Val
    SC --> Val
    PR --> Val
    Val --> Out([Optimized\nSchedule])
```

</div>

---
layout: two-cols
---

# RFI Document Processing
## Message Bus Pipeline

- **Email Monitor** publishes `documents.incoming`
- **Classifier** routes to `documents.rfi`
- **RFI Parser** extracts question and drawing refs
- **BIM Query** looks up elements via MCP4IFC
- **Response Drafter** generates draft answer
- **Approval Router** routes to engineer queue

<div class="mt-4 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <div class="font-semibold" style="color: #0070F2;">Extensibility</div>
  <div class="text-sm" style="color: #354A5F;">Add submittal or change order agents by subscribing to new topics — no rewiring of existing agents</div>
</div>

::right::

<div class="flex items-center justify-center h-full">

```mermaid {scale: 0.62}
flowchart TB
    Email[Email Monitor] --> Bus[Message Bus\nn8n]
    Bus --> DC[Document\nClassifier]
    DC --> Bus
    Bus --> RP[RFI Parser]
    RP --> Bus
    Bus --> BQ[BIM Query\nMCP4IFC]
    BQ --> Bus
    Bus --> RD[Response\nDrafter]
    RD --> Bus
    Bus --> AR[Approval\nRouter]
    AR --> EQ[Engineer\nQueue]
    style Bus fill:#0070F2,color:#fff
```

</div>

---
layout: two-cols
---

# BIM Analysis Orchestration
## Five-Subagent Pipeline

- **Subagent 1:** IFC Parser — spatial boundary filter
- **Subagent 2:** Element Classifier — OmniClass/UniClass
- **Subagent 3:** CWICR Matcher — top-5 similarity search
- **Subagent 4:** Rate Calculator — regional PostgreSQL rates
- **Subagent 5:** Validator — range checks + completeness

<div class="mt-4 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <div class="font-semibold" style="color: #0070F2;">Provenance chain</div>
  <div class="text-sm" style="color: #354A5F;">Every estimate line traced to its IFC element — impossible in manual estimating. Full audit trail for dispute resolution.</div>
</div>

::right::

<div class="h-full flex items-center justify-center">
  <div class="space-y-1 w-full px-4">
    <div class="p-2 rounded-lg" style="background-color: #D1EFFF; border-left: 4px solid #0070F2;">
      <div class="text-sm font-semibold" style="color: #0070F2;">1. IFC Parser</div>
      <div class="text-xs" style="color: #687078;">ifcopenshell · spatial boundary filter</div>
    </div>
    <div class="text-center text-xs" style="color: #687078;">↓</div>
    <div class="p-2 rounded-lg" style="background-color: #D1EFFF; border-left: 4px solid #0070F2;">
      <div class="text-sm font-semibold" style="color: #0070F2;">2. Element Classifier</div>
      <div class="text-xs" style="color: #687078;">OmniClass · UniClass · trade grouping</div>
    </div>
    <div class="text-center text-xs" style="color: #687078;">↓</div>
    <div class="p-2 rounded-lg" style="background-color: #D1EFFF; border-left: 4px solid #0070F2;">
      <div class="text-sm font-semibold" style="color: #0070F2;">3. CWICR Matcher</div>
      <div class="text-xs" style="color: #687078;">multilingual embeddings · Qdrant top-5</div>
    </div>
    <div class="text-center text-xs" style="color: #687078;">↓</div>
    <div class="p-2 rounded-lg" style="background-color: #D1EFFF; border-left: 4px solid #0070F2;">
      <div class="text-sm font-semibold" style="color: #0070F2;">4. Rate Calculator</div>
      <div class="text-xs" style="color: #687078;">regional PostgreSQL unit rates</div>
    </div>
    <div class="text-center text-xs" style="color: #687078;">↓</div>
    <div class="p-2 rounded-lg" style="background-color: #FFD23D; border-left: 4px solid #F58B00;">
      <div class="text-sm font-semibold" style="color: #9A5B00;">5. Validator</div>
      <div class="text-xs" style="color: #687078;">range + completeness checks · fail loops back</div>
    </div>
    <div class="text-center text-xs" style="color: #687078;">↓</div>
    <div class="p-2 rounded-lg" style="background-color: #001944;">
      <div class="text-sm font-semibold" style="color: #89D1FF;">Estimate Report with Provenance Chain</div>
    </div>
  </div>
</div>

---
layout: center
class: text-center
---

<div class="text-6xl font-bold" style="color: #0070F2;">
Technical Infrastructure
</div>
<div class="text-xl mt-4" style="color: #687078;">
MCP Integration · Czech NLP · Open-Source Stack
</div>

---
layout: two-cols
---

# Czech Language Challenge
## Morphological Complexity

- **7 grammatical cases** — one concept, 5+ surface forms
- "betonová zeď" → genitive, dative, instrumental, plural forms
- Standard regex misses **4 of 5** occurrences
- Construction CWICR covers **9 languages**

<div class="mt-4 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <div class="font-semibold" style="color: #0070F2;">Three-layer solution</div>
  <ul class="text-sm mt-1" style="color: #354A5F; list-style: disc; padding-left: 1rem;">
    <li>MorphoDiTa lemmatization (Charles University UFAL)</li>
    <li>multilingual-e5-large sentence embeddings</li>
    <li>Qdrant vector search — confidence threshold 0.75</li>
  </ul>
</div>

::right::

<div class="flex items-center justify-center h-full">

```mermaid {scale: 0.68}
flowchart TB
    Doc[Czech Construction\nDocument] --> L[MorphoDiTa\nLemmatization]
    L --> E[Sentence Transformer\nmultilingual-e5-large]
    E --> VS[Qdrant Vector Search\ncosine similarity]
    VS --> Match[CWICR Work Item Match\nconfidence threshold 0.75]
    VS --> LLM[Claude Normalization\nfor low confidence items]
    LLM --> Match
```

</div>

---
layout: default
---

# MCP Integration Architecture

<div class="grid grid-cols-3 gap-4 mt-4">
  <div class="p-4 rounded-xl" style="background-color: #001944;">
    <div class="font-bold mb-3" style="color: #89D1FF;">Construction Agents</div>
    <div class="space-y-2 text-sm" style="color: #D1EFFF;">
      <div>Orchestrator (Tool Search)</div>
      <div>IFC Parser Subagent</div>
      <div>CWICR Matcher Subagent</div>
      <div>Rate Calculator Subagent</div>
      <div>Document Processor Subagent</div>
    </div>
  </div>
  <div class="p-4 rounded-xl" style="background-color: #0070F2;">
    <div class="font-bold mb-3 text-white">MCP Server Layer</div>
    <div class="space-y-2 text-sm text-white">
      <div>Qdrant-MCP — search_work_items</div>
      <div>PostgreSQL-MCP — rate tables</div>
      <div>n8n-MCP — workflow triggers</div>
      <div>Speckle-MCP — BIM data exchange</div>
      <div>IFC Server MCP — 50+ BIM tools</div>
    </div>
  </div>
  <div class="p-4 rounded-xl" style="background-color: #D1EFFF;">
    <div class="font-bold mb-3" style="color: #0070F2;">External Data Systems</div>
    <div class="space-y-2 text-sm" style="color: #354A5F;">
      <div>Qdrant DB (CWICR 55K items)</div>
      <div>PostgreSQL (ERP + Rates)</div>
      <div>n8n Workflows (400+ integrations)</div>
      <div>Speckle Hub (BIM Models)</div>
      <div>IFC OpenBIM Server</div>
    </div>
  </div>
</div>

<div class="mt-4 p-3 rounded-lg" style="background-color: #D1EFFF;">
  <strong style="color: #0070F2;">Tool Search:</strong>
  <span style="color: #354A5F;"> Reduces tool-definition tokens by 85% — loads only tools relevant to the current request, preventing context flooding</span>
</div>

---
layout: default
---

# Open-Source Technology Stack

| Category | Primary Tool | Why Choose It |
|----------|-------------|---------------|
| **BIM / IFC Processing** | ifcopenshell + MCP4IFC | 50+ LLM-native BIM tools, no license needed |
| **Vector Search** | Qdrant | 100M+ vectors, rich payload filtering, Rust speed |
| **Document Processing** | Docling (IBM) + pdfplumber | Complex PDF layouts, table extraction |
| **Data Processing** | polars (7-10x faster than pandas) | Columnar, multi-threaded, lazy evaluation |
| **Workflow Automation** | n8n | 400+ integrations, native AI agent nodes |
| **BIM Collaboration** | Speckle | Open-source, no Revit license, ACC integration |
| **ML Predictions** | scikit-learn + Prophet | Duration and KPI time-series forecasting |
| **Czech NLP** | MorphoDiTa + multilingual-e5-large | 500 noun paradigms, state-of-the-art accuracy |

---
layout: default
---

# DDC Construction Agent Swarm

<div class="flex justify-center">

```mermaid {scale: 0.60}
flowchart TB
    User([User Request]) --> Orch[Main Orchestrator\nOrchestrator-Subagent Pattern]
    Orch --> A[IFC Parser]
    Orch --> B[CWICR Matcher]
    Orch --> C[Rate Calculator]
    Orch --> D[Doc Processor]
    Orch --> E[Schedule Analyzer]
    A --> GV[Validator\nGenerator-Verifier Gate]
    B --> GV
    C --> GV
    D --> GV
    E --> GV
    GV -->|Fail| C
    GV -->|Pass| Orch
    Orch <--> QD[(Qdrant\nShared-State)]
    Orch <--> PG[(PostgreSQL\nShared-State)]
    Orch --> Out([Validated Output])
```

</div>

---
layout: center
class: text-center
---

<div class="text-6xl font-bold" style="color: #0070F2;">
Conclusion
</div>

---
layout: default
---

# Key Takeaways

<div class="grid grid-cols-2 gap-6 mt-6">
  <div class="p-4 rounded-xl" style="background-color: #D1EFFF; border-top: 4px solid #0070F2;">
    <div class="font-bold" style="color: #0070F2;">Five Patterns, Five Problems</div>
    <div class="text-sm mt-2" style="color: #354A5F;">Each pattern solves a distinct construction challenge — choose based on task characteristics, not convention</div>
  </div>
  <div class="p-4 rounded-xl" style="background-color: #D1EFFF; border-top: 4px solid #5DC122;">
    <div class="font-bold" style="color: #256F3A;">87% Time Saving Verified</div>
    <div class="text-sm mt-2" style="color: #354A5F;">Cost estimation: 16 hours → 2 hours via IFC → CWICR Qdrant → PostgreSQL rates pipeline</div>
  </div>
  <div class="p-4 rounded-xl" style="background-color: #D1EFFF; border-top: 4px solid #049F9A;">
    <div class="font-bold" style="color: #049F9A;">Hybrid is the Target State</div>
    <div class="text-sm mt-2" style="color: #354A5F;">Orchestrator-Subagent + Shared-State + Generator-Verifier is the recommended production architecture</div>
  </div>
  <div class="p-4 rounded-xl" style="background-color: #D1EFFF; border-top: 4px solid #F58B00;">
    <div class="font-bold" style="color: #F58B00;">MCP + Skills = Production</div>
    <div class="text-sm mt-2" style="color: #354A5F;">Skills provide procedural knowledge; MCP servers provide tool access — together they reach production construction systems</div>
  </div>
</div>

<div class="mt-5 p-3 rounded-lg text-center" style="background-color: #001944; color: #89D1FF; font-weight: 600;">
  The agentic future of construction is already under construction in the DDC Skills repository
</div>

---
layout: center
class: text-center
---

# Thank You

<div class="mt-6">
  <div class="text-xl font-semibold" style="color: #0070F2;">Data-Driven Construction (DDC)</div>
  <div class="mt-5 space-y-2" style="color: #354A5F;">
    <div><strong>DDC Book (2025)</strong> — Artem Boiko</div>
    <div><strong>DDC Skills Repository</strong> — github.com/datadrivenconstruction</div>
    <div><strong>MCP4IFC Framework</strong> — Open-source BIM tools for LLMs</div>
    <div><strong>Anthropic</strong> — Multi-Agent Patterns Documentation</div>
  </div>
  <div class="mt-8 p-4 rounded-xl inline-block" style="background-color: #D1EFFF;">
    <div class="font-semibold" style="color: #0070F2;">Complete Open-Source Stack</div>
    <div class="text-sm mt-1" style="color: #354A5F;">ifcopenshell · Qdrant · Docling · polars · n8n · Speckle · MorphoDiTa · scikit-learn</div>
  </div>
</div>
