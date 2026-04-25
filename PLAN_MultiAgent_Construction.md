## Multi-Agent Construction Automation — Architecture Plan

**Based on:** DDC Book (Artem Boiko, 2nd Ed.), Anthropic Multi-Agent Patterns, MCP Production Patterns, DDC Skills Collection, Improvement Roadmap

---

## Goal

Design an agentic system in Claude Code that automates four core construction workflows — Cost Estimation, Schedule Optimization, Document Processing, BIM Data Analysis — using the optimal multi-agent coordination pattern for each, with native Czech language support and open-source tooling.

---

## Findings Summary

### Source 1: Five Multi-Agent Coordination Patterns (Anthropic)

| Pattern | Mechanism | Best When | Weakness |
|---|---|---|---|
| Generator-verifier | Generate → verify → loop | Quality-critical, explicit criteria | Verifier needs clear rubric |
| Orchestrator-subagent | Lead delegates bounded subtasks | Clear decomposition, minimal interdependence | Info bottleneck at orchestrator |
| Agent teams | Persistent workers, shared queue | Parallel, independent, long-running | Workers can't share intermediate findings |
| Message bus | Publish/subscribe events | Event-driven, growing ecosystem | Hard to trace/debug cascades |
| Shared-state | Agents read/write shared store | Collaborative, findings build on each other | Duplicate work, reactive loops |

### Source 2: When Multi-Agent Beats Single-Agent (Anthropic)

Three conditions justify multi-agent overhead:
1. **Context pollution** — subtask generates >1000 tokens irrelevant to main task
2. **Parallelization** — independent facets benefit from simultaneous exploration
3. **Specialization** — 15+ tools, conflicting personas, or deep domain context

**Key principle:** Context-centric decomposition (divide by what context each agent needs, not by work type).

### Source 3: MCP Production Patterns (Anthropic)

- Group tools around **intent**, not endpoints (fewer calls, better agent accuracy)
- **Tool search** cuts context by 85% (load tool definitions on demand)
- **Programmatic tool calling** reduces tokens by 37% (filter in code, not LLM)
- **Skills + MCP = domain specialist** — Skills teach HOW, MCP provides WHAT
- Remote MCP servers for cloud agents; standardized OAuth auth

### Source 4: DDC Book — Data Types in Construction

| Type | Examples | Processing | Agent Implication |
|---|---|---|---|
| Structured | Excel, ERP, CSV, P6 | SQL, pandas | Direct parsing, low AI cost |
| Semi-structured | IFC, JSON, XML, BCF | ifcopenshell, parsers | Schema-aware extraction |
| Unstructured | PDF, photos, emails, scans | OCR, LLM, pdfplumber | High AI cost, verification needed |
| Geometric | CAD/BIM 3D models | ifcopenshell, speckle | Specialized subagent required |

### Source 5: DDC Book — Construction Uberization Concept

The book's core thesis (Part 10): construction is transitioning from opinion-based to data-based decisions. The "uberization" model replaces human-factor bottlenecks (cost estimation = days, schedule = opinions) with automated data pipelines. Multi-agent AI is the execution layer for this vision.

### Source 6: Czech Language Challenge

Czech morphology makes regex search impossible for construction documents:
- 7 grammatical cases × 3 genders × 2 numbers = hundreds of word forms
- "betonová zeď" → betonové zdi, betonovou zdí, betonových zdí, betonovou zeď...
- Construction terminology compounds the problem (composite nouns, abbreviations)
- **Solution:** Vector/semantic search (embeddings ignore morphology) + LLM understanding

### Source 7: CWICR Database

55,719 standardized work items in 9 languages → the backbone of cost estimation. Must be searchable via vector DB (Qdrant) with multilingual embeddings to handle Czech morphological variants.

---

## Pattern-to-Task Mapping

### 1. Cost Estimation → Orchestrator-Subagent + Generator-Verifier

**Why Orchestrator-Subagent:**
- Clear decomposition: IFC parsing → quantity extraction → CWICR matching → rate lookup → markup → total
- Each subtask is bounded, produces clear output
- Orchestrator synthesizes final estimate from subagent results

**Why Generator-Verifier overlay:**
- Cost estimates are quality-critical (DDC Book Part 5: errors compound exponentially)
- Verifier checks: quantities match IFC model, rates match CWICR, markups within policy bounds
- Explicit rubric possible: ±5% tolerance, all elements accounted for, no duplicates

**Subagent Breakdown:**
```
Orchestrator (receives: "Estimate project from IFC model")
├── Subagent 1: IFC Parser          → ifcopenshell → element list + quantities
├── Subagent 2: CWICR Matcher       → vector search (Qdrant) → matched work items
├── Subagent 3: Rate Calculator      → unit costs × quantities + markups
├── Subagent 4: Validator (G-V)      → cross-check totals, flag anomalies
└── Orchestrator synthesizes         → structured Excel/JSON estimate
```

**Confidence: 9/10** — This is textbook orchestrator-subagent territory.

### 2. Schedule Optimization → Agent Teams + Shared-State

**Why Agent Teams:**
- Schedule optimization decomposes into persistent, parallel workers:
  - CPM analysis agent (accumulates context about critical path)
  - Resource leveling agent (needs sustained view of resource pools)
  - Duration prediction agent (ML model, needs historical data context)
- Each agent builds domain familiarity over multi-step analysis

**Why Shared-State overlay:**
- Agents' findings ARE interdependent: CPM changes affect resources, resource constraints affect durations
- Shared schedule state (Gantt data in shared store) lets agents build on each other
- Termination condition: no agent produces new findings for 2 cycles

**Agent Architecture:**
```
Coordinator (receives: "Optimize schedule for 18-month office build")
├── Team Worker 1: CPM Analyzer      → reads schedule, identifies critical path
│                                       writes findings to shared store
├── Team Worker 2: Resource Optimizer → reads CPM findings + resource data
│                                       writes resource conflicts to shared store
├── Team Worker 3: Duration Predictor → reads historical data + current schedule
│                                       writes predicted durations to shared store
└── Coordinator: convergence check    → merges findings, produces optimized schedule
```

**Confidence: 7/10** — More complex than orchestrator-subagent; justified when projects have 100+ activities.

### 3. Document Processing → Message Bus + Generator-Verifier

**Why Message Bus:**
- Documents arrive as EVENTS (new RFI uploaded, submittal received, specification updated)
- Different document types need different agents (PDF parser ≠ Excel parser ≠ photo analyzer)
- Agent ecosystem GROWS: new document types added without rewiring
- Pipeline: Triage → Parse → Extract → Classify → Store → Notify

**Why Generator-Verifier overlay:**
- Extracted data from unstructured docs needs verification (OCR errors, misclassified fields)
- Verifier checks against schema: all required fields present, values in valid ranges
- Critical for Czech: LLM extraction must be verified for morphological accuracy

**Event Flow:**
```
[Document arrives] → Message Bus
├── Topic: "pdf.rfi"      → RFI Parser Agent     → extracted fields → Verifier → Store
├── Topic: "xlsx.estimate" → Excel Parser Agent   → structured data  → Verifier → Store
├── Topic: "image.site"   → Photo Analyzer Agent  → tags + metadata  → Verifier → Store
├── Topic: "pdf.contract"  → Contract Parser Agent → clauses + terms  → Verifier → Store
└── Topic: "ifc.model"    → BIM Triage Agent      → routes to BIM pipeline
```

**Confidence: 8/10** — Message bus excels here because document types are open-ended and event-driven.

### 4. BIM Data Analysis → Orchestrator-Subagent (Primary Pattern)

**Why Orchestrator-Subagent:**
- BIM analysis has CLEAR task decomposition with bounded subtasks
- IFC model is the single input; each analysis dimension is independent
- Subagents return structured results; orchestrator merges

**Detailed Step-by-Step Example:**
```
Orchestrator receives: "Analyze IFC model for cost estimation and compliance"

Step 1: Orchestrator reads IFC file metadata (size, schema version, element count)
Step 2: Dispatches parallel subagents:

├── Subagent A: Quantity Extractor
│   Tools: ifcopenshell
│   Task: Extract all IfcBuildingElement quantities (NetVolume, NetArea, Length)
│   Output: JSON {element_id, type, quantities{}, properties{}}
│
├── Subagent B: CWICR Classifier
│   Tools: Qdrant vector search, CWICR embeddings
│   Task: Match each element to CWICR work item code
│   Input: Element descriptions from Subagent A
│   Output: JSON {element_id, cwicr_code, description, unit, confidence}
│   NOTE: Handles Czech morphology via semantic search (not regex)
│
├── Subagent C: Compliance Checker
│   Tools: IDS validator, rule engine
│   Task: Validate model against Information Delivery Specification
│   Output: {passed: bool, violations: [{element, rule, severity}]}
│
├── Subagent D: Clash Detector
│   Tools: ifcopenshell spatial queries
│   Task: Detect geometric intersections between elements
│   Output: {clashes: [{element_a, element_b, type, location}]}

Step 3: Orchestrator waits for all subagents
Step 4: Orchestrator synthesizes:
  - Merges quantities + CWICR codes → cost estimate line items
  - Appends compliance report
  - Appends clash report
  - Generates summary with confidence scores

Step 5: Generator-Verifier loop:
  - Verifier checks: all elements classified, no missing quantities,
    costs within historical range, compliance violations addressed
  - If rejected: specific feedback → Orchestrator fixes → re-verify
```

**Confidence: 9/10** — This is the showcase example for the research report.

---

## Recommended Hybrid Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                 CONSTRUCTION AI AGENT SYSTEM                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │              SHARED KNOWLEDGE BASE                       │    │
│  │  (Vector DB: Qdrant — CWICR + project history)          │    │
│  │  (Document Store: project files, specs, contracts)       │    │
│  │  Pattern: SHARED-STATE for cross-workflow knowledge      │    │
│  └──────────────────────┬──────────────────────────────────┘    │
│                          │                                       │
│  ┌───────────┬───────────┼───────────┬───────────────┐          │
│  │           │           │           │               │          │
│  ▼           ▼           ▼           ▼               ▼          │
│ COST EST.  SCHEDULE   DOCUMENT    BIM ANALYSIS   REPORTING     │
│ Orch+GV    Teams+SS   MsgBus+GV   Orch+GV        Orch         │
│                                                                  │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │              MCP INTEGRATION LAYER                       │    │
│  │  qdrant-mcp │ speckle-mcp │ n8n-mcp │ postgres-mcp     │    │
│  │  ifc-server  │ google-drive │ github  │ telegram         │    │
│  └─────────────────────────────────────────────────────────┘    │
│                                                                  │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │              DDC SKILLS LAYER                            │    │
│  │  ifc-to-excel │ semantic-search-cwicr │ pdf-construction │    │
│  │  estimate-builder │ bim-validation │ cost-prediction     │    │
│  └─────────────────────────────────────────────────────────┘    │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Pattern Selection Decision Tree

```
Is the task event-driven with open-ended document types?
├── YES → Message Bus (+ Generator-Verifier for extraction quality)
└── NO
    Does the task decompose into clear, bounded subtasks?
    ├── YES → Orchestrator-Subagent (+ Generator-Verifier for critical outputs)
    └── NO
        Do workers need sustained context and build on each other?
        ├── YES → Agent Teams + Shared-State
        └── NO → Single agent (most tasks don't need multi-agent)
```

---

## Czech Language Strategy

### Problem
Czech morphology creates combinatorial explosion for text search:
- Noun "zeď" (wall): zeď, zdi, zdí, zeď, zdí, zdi, zdech, zdmi (8 forms)
- Adjective "betonový" (concrete): 42+ forms across gender/case/number
- Construction compound: "železobetonová nosná stěna" → hundreds of combinations

### Solution: Three-Layer Approach

1. **Vector Embeddings (Primary):** Multilingual sentence-transformers encode meaning, not form. "betonová zeď" and "betonových zdí" map to same semantic neighborhood.

2. **LLM Lemmatization (Pre-processing):** Before indexing any Czech construction document, LLM normalizes text to base forms. Stored alongside original for search.

3. **CWICR Multilingual Index:** The 55,719 CWICR items already exist in 9 languages including Czech. Vector index over Czech descriptions enables fuzzy semantic matching regardless of morphological form.

**Tool Stack:**
- Embeddings: `sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2`
- Vector DB: Qdrant (supports multilingual, fast ANN search)
- Lemmatizer: MorphoDiTa (Czech-specific) or LLM-based
- Search: Hybrid — vector similarity + BM25 on lemmatized text

---

## Open-Source Tool Stack

| Task | Tool | Role | Maturity |
|---|---|---|---|
| BIM/IFC parsing | ifcopenshell | Extract geometry, properties, quantities from IFC | Production |
| Vector search | Qdrant | CWICR semantic search, document embeddings | Production |
| PDF extraction | pdfplumber + marker | Table extraction, layout-aware parsing | Production |
| Multi-format docs | unstructured.io / docling | PDF, DOCX, XLSX, images → structured | Production |
| BIM data exchange | Speckle | Real-time BIM model sharing, versioning | Production |
| Workflow orchestration | n8n | Event triggers, ETL pipelines, notifications | Production |
| Data processing | pandas / polars | Tabular data manipulation, aggregation | Production |
| ML predictions | scikit-learn | Cost/duration prediction models | Production |
| OCR | Tesseract + EasyOCR | Scanned document text extraction | Production |
| Schedule analysis | Python-CPM libraries | Critical path computation | Emerging |

---

## MCP Server Architecture

```yaml
mcp_servers:
  # Data Layer
  qdrant-mcp:
    purpose: Vector search for CWICR, document embeddings, semantic queries
    tools: [search_similar, upsert_vectors, create_collection]

  postgres-mcp:
    purpose: Project database, cost history, schedule data
    tools: [query, insert, update]

  # BIM Layer
  speckle-mcp:
    purpose: BIM model versioning, real-time data exchange
    tools: [get_model, get_elements, get_properties]

  ifc-server-mcp:
    purpose: IFC model serving, quantity extraction
    tools: [parse_ifc, get_quantities, validate_ids]

  # Document Layer
  google-drive-mcp:
    purpose: Document storage, file access
    tools: [list_files, read_file, upload_file]

  # Automation Layer
  n8n-mcp:
    purpose: Workflow triggers, ETL pipeline execution
    tools: [trigger_workflow, get_execution, list_workflows]

  # Communication
  telegram-mcp:
    purpose: Team notifications, alerts
    tools: [send_message, send_document]
```

---

## Skill Chaining Examples

### Chain 1: IFC → Cost Estimate (Orchestrator-Subagent)
```
ifc-to-excel → semantic-search-cwicr → estimate-builder → verification-loop
```

### Chain 2: Daily Document Processing (Message Bus)
```
[new PDF arrives] → pdf-construction → data-quality-check → n8n-approval-workflow → notify
```

### Chain 3: Schedule Optimization (Agent Teams)
```
schedule-delay-analyzer ↔ duration-prediction ↔ resource-optimization
     (shared state: project schedule store)
```

### Chain 4: BIM Validation Pipeline (Orchestrator + G-V)
```
ifc-to-excel → bim-validation-pipeline → [if fails] → generator fixes → re-validate
```

---

## Implementation Phases

### Phase 1: Foundation (Weeks 1-2) — Confidence: 9/10
- Deploy Qdrant with CWICR multilingual embeddings
- Implement `ifc-to-excel` and `semantic-search-cwicr` skills
- Build basic Orchestrator-Subagent for BIM → Cost Estimate chain
- Test Czech language semantic search accuracy

### Phase 2: Document Processing (Weeks 3-4) — Confidence: 8/10
- Implement Message Bus for document event routing
- Build PDF, Excel, and image parser agents
- Add Generator-Verifier for extraction quality
- Integrate with n8n for workflow triggers

### Phase 3: Cost Estimation Pipeline (Weeks 5-6) — Confidence: 8/10
- Full Orchestrator-Subagent cost estimation pipeline
- CWICR matching with confidence scoring
- Rate lookup and markup calculation
- Verification loop with tolerance thresholds

### Phase 4: Schedule & Advanced (Weeks 7-8) — Confidence: 6/10
- Agent Teams for schedule optimization
- Shared-State knowledge base across workflows
- ML prediction models (cost, duration)
- Dashboard/reporting agent

---

## Risks and Mitigations

| Risk | Impact | Mitigation |
|---|---|---|
| Czech NLP accuracy <90% | Incorrect cost matches | Hybrid vector + BM25 on lemmatized text; human review loop |
| IFC model size >500MB | Agent timeout/memory | Chunk-based parsing; stream elements via ifcopenshell |
| Multi-agent token cost 3-10x | Budget overrun | Start with orchestrator-subagent only; add patterns when justified |
| CWICR coverage gaps | Missing work items | Fallback to LLM classification with low-confidence flag |
| Agent coordination failures | Stale/conflicting results | Explicit termination conditions; maximum iteration limits |

---

## Unresolved Questions

1. **Qdrant hosting:** Local vs. cloud for CWICR vector DB? (Depends on project scale)
2. **IFC server:** Self-hosted IfcOpenShell service vs. per-request parsing? (Latency vs. complexity)
3. **n8n vs. native Claude Code orchestration:** When to use external workflow engine vs. agent-native coordination?
4. **Czech lemmatizer:** MorphoDiTa (rule-based, fast) vs. LLM-based (flexible, slower)?
5. **Cost prediction ML:** Sufficient historical data available for training? (DDC Book Part 9 suggests yes for large companies)
6. **GovCloud / data residency:** Do Czech construction projects have data residency requirements affecting tool selection?

---

## Success Criteria

| Metric | Target | How to Measure |
|---|---|---|
| Cost estimate accuracy | ±10% vs. manual | Compare 10 projects automated vs. expert |
| Czech search recall | >95% | Test 100 Czech construction queries against CWICR |
| Document processing time | <2 min per doc | Benchmark PDF/Excel pipeline |
| BIM analysis throughput | <5 min per IFC model | Benchmark quantity extraction + classification |
| Agent coordination overhead | <5x single-agent tokens | Monitor token usage per workflow |

---

*Plan based on: DDC Book 2nd Edition (Artem Boiko), Anthropic Multi-Agent Coordination Patterns, Building Multi-Agent Systems, Building Agents with MCP, DDC Improvement Roadmap, DDC Getting Started Guide.*
