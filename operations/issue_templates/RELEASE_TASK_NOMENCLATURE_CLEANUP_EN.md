# Issue Template: Mandatory Nomenclature & License Standardization

**Suggested Title:** `chore: NΞØ Standard - Enforce 'Smart' Nomenclature & License (Deprecate 'Forge')`

## 🚨 Required Normative Change

As per official decision on **2026-01-24**, the `FORGE` nomenclature has been officially **deprecated** and replaced by **SMART** across the entire ecosystem. Additionally, we must ensure all repositories have a clear **LICENSE** file and a **LEGAL_STATUS.md** reference.

This repository must be audited and updated immediately for compliance.

### 📄 Official Reference
Consult the normative document: `docs/auditoria/NOMENCLATURA_OFICIAL.md` and `docs/core/LEGAL_STATUS.md`.

---

## 📋 Verification Checklist

### 1. Code & File naming
-[ ] Replace `ForgeToken` with `NeoToken` or `SmartToken`.
-[ ] Replace `ForgeFactory` with `NeoSmartFactory` or `NeoJettonFactory`.
-[ ] Rename any files containing `forge` in the filename.
-[ ] Audit variable and function names (`forgeCore`, `initForge`, etc.).

### 2. Configuration & Metadata
-[ ] `package.json`: Verify `name` and dependencies (use `@neosmart/*` scope).
-[ ] `README.md`: Remove references to "Neural Forge" or "Forge Factory".
-[ ] Source Code Comments: Update internal documentation and TODOs.

### 3. Licensing & Legal (CRITICAL)
-[ ] Ensure `LICENSE` file exists in the root (MIT for code).
-[ ] Ensure `LICENSE-DOCS.md` exists if there is significant documentation (CC BY 4.0).
-[ ] Add reference to the official authorship proof (January 22, 2026).

### 4. Branding
-[ ] Project Name: **NΞØ Smart Token Factory**.
-[ ] CLI: **`nsf`** (instead of `neo-smart-factory` or `forge`).

---

## 🚫 Forbidden Terms (Search & Destroy)

Run `grep -ri "forge" .` and eliminate occurrences of:
-`forge-core`
-`forge-ui`
-`forge-cli`
-`Neural Forge`

> **Note:** If historical mentions exist in CHANGELOG or ARCHIVE files, add a warning note at the top stating the terminology is obsolete, but **do not alter historical records** unless strictly necessary for core functionality.

---

**Priority**: Maximum 🔴  
**Assignee**: Tech Lead / Maintainer
