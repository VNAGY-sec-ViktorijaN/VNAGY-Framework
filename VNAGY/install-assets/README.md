# install-assets/

Internal directory containing VNAGY installation assets for both Linux and Windows environments.  
Used exclusively by collaborators working on installer‑related modules.

All assets in this directory are protected under the **VNAGY CC BY‑NC 4.0 Extended Asset License (2026)**  
by **Viktorija Nađ**.  
The full license text is located in the `LICENSE/` directory.

---

## Structure

install-assets/
├── format/          # canonical format definitions (Linux + Windows)
├── examples/        # reference minimal install assets
└── integration/     # collaborator integration notes


Each section contains platform‑specific subfolders:

install-assets/
├── format/
│   ├── linux/
│   └── windows/
├── examples/
│   ├── linux/
│   └── windows/
└── integration/
├── linux/
└── windows/



---

## Purpose

This directory standardizes all installation‑related assets, including:

- deterministic install log formats  
- minimal reference examples  
- integration guidelines for module developers  
- platform‑specific output rules (Linux & Windows)

These assets ensure consistent behavior across all VNAGY installer components.

---

## License Notice

All files in `install-assets/` — including formats, examples, diagrams, visuals, and log structures —  
are governed by the **VNAGY CC BY‑NC 4.0 Extended Asset License (2026)**.

This license strictly prohibits:

- commercial use  
- removal or alteration of attribution  
- modification or repurposing of VNAGY visual identity  
- derivative works that imitate VNAGY design language  

Refer to the `LICENSE/` directory for the complete license text.


