# Maker Portfolio—Systems, Failure, and Publication Infrastructure

This repository is a **maker portfolio proxy** containing inspectable artifacts from two independent systems I built:

1. **PALADIN** — a research framework for error-resilient tool-using AI agents  
2. **FTR** — a youth advocacy news site with a focus on the backend and creation platform.

The purpose of this repository is **inspection, not execution parity**.  
It exposes the **control logic, invariants, and design decisions** behind each system without requiring large-scale compute or production infrastructure.

---

## Project 1: PALADIN—Error-Resilient Tool-Using Agents

PALADIN is a research framework for evaluating how language-model agents recover from execution-time tool failures.

Most benchmarks collapse failure and recovery into a single outcome. PALADIN instead treats execution-time failure as a **first-class learning and evaluation signal** and then teaches models to recover from such failures.

### What the PALADIN artifacts demonstrate

The `Paladin Demos/` directory contains **offline, deterministic proxies** of the PALADIN framework that make the system’s structure inspectable:

- Explicit detection of execution-time tool failures  
- Data annotation to highlight recovery as a core signal not implicit reasoning  
- Reuse of recovery trajectories instead of brute-force retries  

These files preserve the **decision structure** of the full system:

failure → diagnosis → strategy shift → continuation or termination.

### What is intentionally omitted

By design, this repository does **not** include:

- Trained or fine-tuned language models  
- Full production code (withheld due to ongoing research use)
- Large-scale evaluation infrastructure  
- Internal data-generation pipelines  

The code shown here mirrors the rules used in the full research system, but is stripped down to make **control flow and recovery logic legible**.

### PALADIN dataset

The failure–recovery dataset generated using this framework is publicly available here:

https://huggingface.co/datasets/E-k-O/PaladinDataSet

### Related publication

Vuddanti, Shah, et al.  
**PALADIN: Self-Correcting Language Model Agents to Cure Tool-Failure Cases**  

arXiv: https://arxiv.org/abs/2509.25238

Accepted for presentation at the AAAI 2026 conference (Oral).

---

## Project 2: FTR—Youth Advocacy News Platform

FTR is a **youth-led advocacy news site** where multiple editors collaborate on image-heavy articles addressing social and civic issues.

The core engineering challenge was not visual polish, but adjusting to observed failures in collaborative publishing workflows to appeal to both authors and readers.

### What the FTR artifacts demonstrate

The FTR code excerpts included here show:

- A **publication-aware article editor** where authors write directly in the layout readers see  
- Context-aware formatting controls that disappear when not needed  
- Inline image handling with **durable, publish-safe storage guarantees**  
- A backend architecture that shifts **authority from application code to the database**  
- Declarative enforcement of permissions and invariants (via Supabase Row Level Security)  

The system was shaped by real failures encountered during collaboration, including broken media persistence, fragile permissions, and correctness depending on developer discipline rather than system guarantees.

### Full FTR codebase

This repository contains only representative artifacts intended to show architectural decisions.

The **complete FTR website**, including frontend, backend, schema, and deployment logic, is available here:

https://github.com/BasicHooman/website-ftr

---

## Repository Structure

```
├── FTR Code/
│ └── Representative frontend and backend excerpts
├── Paladin Demos/
│ ├── annotate_clean.py
│ ├── annotate_recovery.py
│ ├── simulation_with_paladin_error_match.py
│ └── toolscan_taxonomy_map.json
├── README.md
└── LICENSE
```
---

## How to read this repository

If you are skimming:

1. Start with `simulation_with_paladin_error_match.py` to see PALADIN’s end-to-end control flow  
2. Read `annotate_recovery.py` to understand how recovery behavior is formalized  
3. Skim the FTR excerpts to see how correctness and invariants are enforced in a real publishing system  
