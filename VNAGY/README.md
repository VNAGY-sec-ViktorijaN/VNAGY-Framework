# VNAGY Framework

A modular offline‑first security framework for local behavioral correlation, signal analysis, and deterministic anomaly evaluation.  
VNAGY is a non‑reconstructable, isolated, and concept‑only public repository. Operational logic is private.

## RD — Repository Description

This repository contains the public, non‑operational components of the VNAGY security framework.

It provides:

- structural module layout  
- conceptual architecture  
- non‑reconstructable behavioral models  
- offline‑first design principles  
- coding standards  
- symbolic heuristics  
- module interaction diagrams  
- UI integration structure (Flutter / Kotlin / Tauri)

No operational detection logic, thresholds, weights, heuristics, or executable security algorithms are included.

VNAGY is an active R&D project.  
The public repository serves as a technical showcase, documentation hub, and structural reference.

## RM — Repository Modules

core/
 ├─ C-Pack/          # UI interaction signals
 ├─ L-Pack/          # Log & monitoring events
 ├─ M-Module/        # Central correlation engine (non-operational)
 ├─ P-Pack/          # Data alerts
 ├─ S-Pack/          # Security utilities
 └─ X-Pack/          # Behavioral scoring (concept-only)

behavior-engine/
 ├─ anomaly-subnetting/
 ├─ cpu-behavior-monitor/
 ├─ memory-only-process-detection/
 └─ pattern-detection/

offline-first/
 ├─ local-cache/
 ├─ local-event-bus/
 ├─ local-exporter/
 ├─ local-killing-chain/
 ├─ local-scoring/
 └─ zero-cloud-dependency/

rule-export/
 ├─ adapters/
 ├─ converters/
 ├─ heuristics/
 ├─ siem-integration/
 └─ threat-mapping/

ui/
 ├─ flutter/
 ├─ kotlin/
 └─ tauri/

 
Each module is structural only and does not contain operational logic.

## M‑Module Summary

The M‑Module acts as the central correlation layer:

- validates structural and semantic consistency  
- normalizes heterogeneous signals  
- performs deterministic correlation  
- routes unified outputs to X‑Pack  

Operational logic is not included in the public version.

## License

This project is licensed under:

### VNAGY CC BY‑NC‑ND 4.0 — Code Edition (2026)  
© Viktorija Nađ

#### Allowed:
- reading the code  
- learning and analysis  
- academic reference with attribution

#### Prohibited:
- commercial use  
- code modification  
- redistribution  
- derivative works  
- integration into other projects  
- removal of author markings  
- rebranding  
- operational reconstruction

Full license text is available in the LICENSE ( https://github.com/VNAGY-sec-ViktorijaN/VNAGY-Framework/tree/main/VNAGY/LICENSE ) directory.

## Documentation

Included documentation:

- VNAGY Coding Standard Specification ( https://github.com/VNAGY-sec-ViktorijaN/VNAGY-Framework/blob/main/VNAGY/whitepapers/VNAGY%20Coding%20Standard%20Specification.pdf )
- Offline‑First Architecture ( https://github.com/VNAGY-sec-ViktorijaN/VNAGY-Framework/blob/main/VNAGY/whitepapers/VNAGY%20Secure%E2%80%91First%20Conceptual%20Architecture%20Specification.pdf ) 
- Behavior‑Engine Model  
- STRIDE & MITRE Mapping  
- Conceptual heuristics (non-operational)

All documentation is symbolic and non‑reconstructable.

## Project Status

VNAGY is an active security R&D project.  
The public repository contains conceptual, structural, and non‑operational components only.  
Operational modules are private.


## Education

- **Bachelor of Physics**  
  Josip Juraj Strossmayer University of Osijek, Department of Physics  
  Completed: 2021  
  Academic title: University Bachelor of Physics 
  

- **Master of Physics and Computer Science**  
  Josip Juraj Strossmayer University of Osijek, Department of Physics  
  Completed: 2024  
  Academic title: University Master of Education in Physics and Computer Science  





