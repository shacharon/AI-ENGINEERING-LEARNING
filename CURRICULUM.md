# CURRICULUM — AI-ENGINEERING-LEARNING

**Status: APPROVED by the learner on 2026-10-16** (9 modules, 35 lessons, 9 reviews). Lesson 01 is prepared (files only) and is **not started**; it starts when the learner says "start lesson 01".
**Rules for this file:** it is the contract. It changes only with the learner's explicit approval, and every change is logged in the Change log. It contains no lesson content, hints or solutions; lesson material is produced by the mentor (see MENTOR.md).

## Purpose and how this differs from the Agentic AI course
Practical **AI engineering and senior interview preparation**: decisions, numbers, trade-offs, failure analysis and evaluation for LLM, RAG and production systems. It is framework-free and does not teach agents, tool loops, LangChain, LangGraph, MCP or multi-agent patterns.

Overlap with existing courses (verified by reading the files; pointers only, nothing is copied):
| Topic here | Related existing material | What this course adds |
|---|---|---|
| M1 LLM foundations | `ai-agentic-lecture` lessons 01–09 (tokens, context, sampling, pricing, models, prompts, structured output) | Decision and interview angle: task fit, cost estimation, testing consequences; no tokenizer or sampler implementation |
| M2–M3 Embeddings, vector search | `ai-agentic-lecture` lessons 05, 29; `CLAUDE-AI-AGENTIC-BASIC/src/rag2-chunking-embeddings`, `rag3-vector-search` | Model choice and versioning, drift, recall/latency trade-offs, index operations and isolation |
| M4 RAG | `ai-agentic-lecture` lessons 28, 30; `CLAUDE-AI-AGENTIC-BASIC/src/rag1`–`rag5` | Failure taxonomy and diagnosis, grounding policy, interview defence; no agentic RAG |
| M5–M6 Retrieval and LLM evals | `ai-agentic-lecture` lessons 30, 33–35; `CLAUDE-AI-AGENTIC-BASIC/src/pe2-evaluations` | Metric choice (recall@k, MRR, nDCG), eval-set design, judge calibration, regression gates; no LangSmith or trajectory evals |
| M7 Security | `ai-agentic-lecture` lessons 36–38; `CLAUDE-AI-AGENTIC-BASIC/src/pe3-security` | RAG-specific threats and per-user retrieval access; no agent or MCP authorization |
| M8 Observability | `ai-agentic-lecture` lesson 35; `CLAUDE-AI-AGENTIC-BASIC/src/pe1-observability` | Privacy-aware logging and end-to-end debugging of one bad answer |
| M9 Cost and production | `ai-agentic-lecture` lessons 40–42; `CLAUDE-AI-AGENTIC-BASIC/src/pe4-reliability`, `pe5-production-readiness` | Cost modelling and the full banking architecture defence |
`agentic-ai-academy` (legacy candidate) also lists similar topics and is not used. Learners do **not** need to have completed the other courses; this one is self-contained.

## Lesson kinds and tiers
| Kind | What happens |
|---|---|
| **discussion** | A fictional banking scenario, one question at a time, written or chat answers, rubric review (MENTOR.md section 8) |
| **code** | A small offline TypeScript exercise with Vitest specs on fake data (lessons 16, 18, 21, 30 only). Tooling is created at the first code lesson (16) after a separate approval; no model API calls ever |

| Tier | The mentor supplies | The learner supplies |
|---|---|---|
| **A Guided** | Answer structure and a worked mini-example of the method on a different problem | Content for each heading |
| **B Constrained** | Requirements and constraints only | Structure, numbers, design |
| **C Open** | One-paragraph business problem | Clarifying questions, then everything |

Every lesson: theory, a scenario, one question at a time with progressive hints on request, a rubric review, one senior interview question with at most two follow-ups. Pacing is mastery-based: no deadlines.

## Study order
**M1 → M2 → M3 → M4 → M5 → M6 → M7 → M8 → M9 → lessons 34, 35.** Within a module, lessons in order, then its review (R1–R9). Ids are stable keys.

## Syllabus (9 modules, 35 lessons, 9 reviews)
Columns: prerequisites · scenario (fictional bank, never real data) · challenge · interview question · tier · kind.

### M1 — LLM Foundations (engineering view)
| # | Topic | Prereq | Scenario | Challenge | Interview question | Tier | Kind |
|---|---|---|---|---|---|---|---|
| 01 | When an LLM is the right tool: task fit and failure modes | none | Cedar Bank customer assistant: which tasks go to an LLM | Classify banking tasks as LLM, grounded LLM, deterministic or human, with error cost and fallback | "When would you not use an LLM?" | A | discussion |
| 02 | Per-request cost and latency: tokens, context and budgets in practice | 01 | Budgeting a fee-explanation call at 1M requests a month | Estimate cost and p95 latency; find the dominant driver | "How do you estimate the cost of an LLM feature before building it?" | A | discussion |
| 03 | Nondeterminism, sampling and reproducibility | 01 | Two compliance drafts differ between runs | Decide settings and tests for a feature that must be repeatable | "Why isn't temperature 0 fully deterministic, and what does that do to your tests?" | B | discussion |
| 04 | Structured outputs and output contracts | 01 | Extracting dispute details into a fixed schema | Design the contract, validation, bounded repair and refusal path | "How do you make LLM output safe to feed into a system?" | B | discussion |
| 05 | Model selection and routing trade-offs | 02, 04 | Three workloads, three models | Choose a model per workload using quality, cost, latency and data rules | "API model or open-weight: how do you decide?" | B | discussion |
| **R1** | **Review:** mixed scenario on LLM Foundations (engineering view) (tier C) + five rapid-fire questions | 01–05 | | | | C | discussion |

### M2 — Embeddings
| # | Topic | Prereq | Scenario | Challenge | Interview question | Tier | Kind |
|---|---|---|---|---|---|---|---|
| 06 | What embeddings represent and how similarity behaves | 01 | Matching customer questions to known topics | Predict which pairs are neighbours and which are not, and why | "What does an embedding capture, and what does it miss?" | A | discussion |
| 07 | Choosing and versioning an embedding model | 06 | Switching embedding models in a live system | Plan evaluation, versioning and re-indexing | "How do you change an embedding model without breaking search?" | B | discussion |
| 08 | Embedding limits: domain, language, drift and dimension trade-offs | 06, 07 | Mixed English and Hebrew banking text | Diagnose a poor-retrieval case and pick a fix | "Why would a good embedding model do badly on your data?" | B | discussion |
| **R2** | **Review:** mixed scenario on Embeddings (tier C) + five rapid-fire questions | 06–08 | | | | C | discussion |

### M3 — Vector search
| # | Topic | Prereq | Scenario | Challenge | Interview question | Tier | Kind |
|---|---|---|---|---|---|---|---|
| 09 | Nearest-neighbour search: exact vs approximate, recall vs latency | 06 | Searching 50 million passages | Pick exact or approximate search and defend the recall target | "What does approximate search trade away?" | A | discussion |
| 10 | Filters, hybrid keyword + vector search and reranking | 09 | Queries with account numbers and product names | Design retrieval for exact terms and meaning together | "Why isn't vector search enough on its own?" | B | discussion |
| 11 | Operating an index: updates, deletes, multi-tenancy and sizing | 09, 10 | Policy documents change daily; customers must not see each other's data | Plan updates, deletion and isolation, and estimate size | "How do you keep a vector index correct and private?" | B | discussion |
| **R3** | **Review:** mixed scenario on Vector search (tier C) + five rapid-fire questions | 09–11 | | | | C | discussion |

### M4 — RAG
| # | Topic | Prereq | Scenario | Challenge | Interview question | Tier | Kind |
|---|---|---|---|---|---|---|---|
| 12 | RAG architecture and a failure taxonomy | 10 | "Why can't I raise my limit?" answered from policies | Locate each possible failure along the pipeline | "Walk me through where a RAG answer can go wrong." | A | discussion |
| 13 | Chunking and context assembly | 12 | Long policy PDFs with tables | Choose chunk size, overlap and metadata, with a test plan | "How do you pick a chunking strategy?" | B | discussion |
| 14 | Grounding, citations and abstention | 12 | The answer must be supported or the assistant must decline | Define when to answer, cite and refuse | "How do you stop a RAG system from making things up?" | B | discussion |
| 15 | Query rewriting and multi-step retrieval | 13, 14 | Follow-up questions that depend on earlier turns | Design rewriting and when a second retrieval is justified | "When is a more complex retrieval pipeline worth it?" | C | discussion |
| **R4** | **Review:** mixed scenario on RAG (tier C) + five rapid-fire questions | 12–15 | | | | C | discussion |

### M5 — Retrieval evaluation
| # | Topic | Prereq | Scenario | Challenge | Interview question | Tier | Kind |
|---|---|---|---|---|---|---|---|
| 16 | Gold sets and retrieval metrics: recall@k, precision, MRR, nDCG | 12 | Measuring whether the right policy is retrieved | Build a small gold set and compute the metrics | "How do you measure retrieval quality?" | B | code |
| 17 | Diagnosing retrieval failures | 16 | Retrieval recall dropped after a content update | Find the cause from the metrics and examples | "Retrieval got worse after a release: how do you investigate?" | C | discussion |
| 18 | Evaluating changes to chunking, embeddings and reranking | 16, 17 | Comparing two pipeline versions fairly | Run an A/B comparison and decide with evidence | "How do you know a retrieval change is an improvement?" | C | code |
| **R5** | **Review:** mixed scenario on Retrieval evaluation (tier C) + five rapid-fire questions | 16–18 | | | | C | discussion |

### M6 — LLM evals
| # | Topic | Prereq | Scenario | Challenge | Interview question | Tier | Kind |
|---|---|---|---|---|---|---|---|
| 19 | Eval set design and rubrics | 04 | Defining "a good answer" for a banking assistant | Write rubric, cases, edge cases and ownership | "How do you build an eval set for a new feature?" | A | discussion |
| 20 | LLM-as-judge: bias, calibration and agreement with humans | 19 | A judge that prefers long answers | Design a judge and test its reliability | "When can you trust an LLM judge?" | B | discussion |
| 21 | Regression gates: offline vs online evaluation | 19, 20 | Blocking a bad prompt change before release | Define gate thresholds and what blocks a release | "How do you stop a prompt change from regressing quality?" | B | code |
| 22 | Groundedness, faithfulness and human review loops | 14, 20 | Sampling production answers for review | Design the review loop and sampling plan | "How do you evaluate answers in production?" | C | discussion |
| **R6** | **Review:** mixed scenario on LLM evals (tier C) + five rapid-fire questions | 19–22 | | | | C | discussion |

### M7 — Security
| # | Topic | Prereq | Scenario | Challenge | Interview question | Tier | Kind |
|---|---|---|---|---|---|---|---|
| 23 | Threat model for LLM applications | 12 | Mapping risks for the assistant | List assets, attackers, entry points and impact | "What are the main security risks of an LLM app?" | A | discussion |
| 24 | Prompt injection: direct, indirect and through retrieved content | 23, 12 | A document in the index contains hostile instructions | Design layered defences and be honest about residual risk | "Can prompt injection be fully prevented?" | B | discussion |
| 25 | PII, data leakage and per-user access control in retrieval | 11, 23 | One customer's data must never reach another | Enforce access at retrieval time and prove it | "How do you do authorization in RAG?" | B | discussion |
| 26 | Guardrails, red-teaming and incident handling | 24, 25 | A jailbreak found in production | Design guardrails, a red-team plan and a response | "How would you red-team an LLM feature?" | C | discussion |
| **R7** | **Review:** mixed scenario on Security (tier C) + five rapid-fire questions | 23–26 | | | | C | discussion |

### M8 — Observability
| # | Topic | Prereq | Scenario | Challenge | Interview question | Tier | Kind |
|---|---|---|---|---|---|---|---|
| 27 | What to log and trace for LLM applications, with privacy | 12 | Debugging a wrong answer without storing customer secrets | Decide what is recorded, redacted and retained | "What do you log for an LLM request?" | A | discussion |
| 28 | Metrics, drift detection and feedback loops | 27, 22 | Quality drifts after a provider model update | Choose signals, alerts and sampling | "How do you detect quality drift?" | B | discussion |
| 29 | Debugging a bad answer end to end | 27, 17 | A complaint: the assistant quoted an old fee | Trace the cause across retrieval, prompt, model and data | "Walk me through debugging one bad answer." | C | discussion |
| **R8** | **Review:** mixed scenario on Observability (tier C) + five rapid-fire questions | 27–29 | | | | C | discussion |

### M9 — Cost and production AI architecture
| # | Topic | Prereq | Scenario | Challenge | Interview question | Tier | Kind |
|---|---|---|---|---|---|---|---|
| 30 | Cost modelling, caching and batching | 02 | Cutting monthly spend by 40% without hurting quality | Build a cost model and rank the levers | "How would you cut LLM cost by 40%?" | B | code |
| 31 | Latency, streaming, reliability, fallbacks and rate limits | 02, 05 | Provider outage during peak | Design timeouts, retries, fallbacks and degradation | "What happens when the model provider is down?" | B | discussion |
| 32 | Release and change management: prompts, models, indexes, rollback and governance | 21, 28 | Rolling out a new model version safely | Plan versioning, canary and rollback with audit needs | "How do you ship a model or prompt change safely?" | C | discussion |
| 33 | End-to-end architecture for a banking AI assistant | M1–M8 | The full design with numbers | Produce and defend a complete architecture | "Design a grounded AI assistant for a bank." | C | discussion |
| **R9** | **Review:** mixed scenario on Cost and production AI architecture (tier C) + five rapid-fire questions | 30–33 | | | | C | discussion |

### Capstone — senior interview rounds
| # | Topic | Prereq | Scenario | Challenge | Interview question | Tier | Kind |
|---|---|---|---|---|---|---|---|
| 34 | Mock senior interview: design round (unseen AI system) | gates M1–M9 | A problem chosen by the mentor | Timed design with follow-ups | Scored with the rubric in MENTOR.md | C | discussion |
| 35 | Mock senior interview: evaluation, security and incident round | 34 | Eval plan, threat model and a live incident | Timed rapid case rounds | Scored with the rubric in MENTOR.md | C | discussion |

## Gates
A module gate needs every lesson `passed` or `passed-with-help` and its review without a *Missing* on the module's critical dimensions, plus the learner's explicit approval. Skips or reorders need approval and a change-log entry.

## Coverage check (requested topics → lessons)
| Topic | Lessons |
|---|---|
| LLM Foundations | 01–05, R1 |
| Embeddings | 06–08, R2 |
| Vector Search | 09–11, R3 |
| RAG | 12–15, R4 |
| Retrieval Evaluation | 16–18, R5 |
| LLM Evals | 19–22, R6 |
| Security | 23–26, R7 |
| Observability | 27–29, R8 |
| Cost and Production AI Architecture | 30–33, R9 |
| Senior interview rounds | 34–35 |

Out of scope: agents and tool loops, MCP, LangChain/LangGraph/LangSmith, fine-tuning and training, multimodal models, calling real model APIs or vector databases.

## Decisions
1. Syllabus (35 lessons, 9 reviews): approved 2026-10-16.
2. Code lessons (16, 18, 21, 30) use offline TypeScript + Vitest, set up only when lesson 16 is reached, after a separate approval: still to be confirmed at that point.
3. Overlap approach (self-contained course, pointers only): accepted with the syllabus approval.

## Change log
| Date | Change | Approved by |
|---|---|---|
| 2026-10-16 | File created as a draft; Lesson 01 prepared ahead (files only) at the owner's request | not yet approved |
| 2026-10-16 | Status set to approved; no content change | learner ("yes") |
