# VNAGY — Policies & Directives  
**Offline‑First Security Engineering**  
**Minimal • Deterministic • Explicit**

---

## Purpose
This directory contains all normative documents governing system‑wide constraints, module interaction rules, offline‑first requirements, symbolic behavior limits, heuristic scoring boundaries, and non‑operational formats within the VNAGY framework.

All documents in this section are binding, non‑algorithmic, and non‑reconstructable, following VNAGY licensing and structural standards.

---

## Document Types

### 1. Policies (POL)
Policies define localized mandatory rules for specific VNAGY subsystems.

Included policies:
- VNAGY‑AIP‑001 — AI Isolation Policy  
- VNAGY‑MIP‑002 — Modular Interaction Policy  
- VNAGY‑BEC‑001 — Behavior Engine Constraints  
- VNAGY‑HSM‑001 — Heuristic Scoring Model  
- VNAGY‑KCF‑001 — Killing Chain Format  

Policies apply to:
- module behavior  
- symbolic interaction  
- deterministic state boundaries  
- non‑operational constraints  

Policies do not define algorithms, thresholds, or operational logic.

---

### 2. Directives (DIR)
Directives define system‑wide mandatory conditions that apply to the entire VNAGY architecture.

Included directives:
- VNAGY‑OFD‑001 — Offline‑First Directive  

Directives apply to:
- global system behavior  
- offline‑valid operation  
- deterministic execution  
- non‑network dependency  

Directives override policies when scope overlaps.

---

## Structure
All documents follow the VNAGY normative format:

- Policy/Directive Identifier  
- Directive/Policy Statement  
- MUST rules  
- MUST NOT rules  
- MAY rules  
- Interaction/System Boundaries  
- Enforcement Notes  
- Non‑Operational Clause  
- Licensing Reference  

No document contains:
- operational logic  
- dynamic thresholds  
- algorithms  
- reconstructable behavior  
- implementation details  

---

## Licensing
All documents in this directory are licensed under:

**VNAGY CC BY‑NC 4.0 Extended License**  
and  
**VNAGY Minimal License (PSDL-1.3)** (for short normative documents)

Usage restrictions include:
- No reconstruction  
- No operational derivation  
- No commercial deployment  
- No algorithmic extraction  

© Viktorija Nađ — All Rights Reserved

---

## Compliance
Modules, components, or subsystems failing to comply with any policy or directive in this directory are not eligible for VNAGY integration and must be excluded from system‑level operation.

