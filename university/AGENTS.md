# AGENTS.md

## Repository Overview & Role

This repository contains Machine Learning lab assignments and implementations for the Bachelor of Science in Artificial Intelligence (BSAI) program.

When converting lab documentation, assignments, or Colab exports into Jupyter Notebook files (`.ipynb`), agents must generate **valid, parseable Jupyter JSON (`nbformat: 4.5`)** without summarization, omission, or truncation.

---

## Non-Negotiable Directives

1. **Zero Truncation / No Summarization:**

- Never replace code, tables, or theory blocks with placeholders, comments (e.g., `# ... rest of code`), or summarized bullet points.
- All tasks, intermediate print statements, visual plots, classification reports, and written analytical answers from the source material must be rendered in full.

2. **Pure JSON Output for Notebooks:**

- When asked for a notebook conversion, provide the output in pure `.ipynb` JSON formatting enclosed in a single JSON block.
- All cell source lines must be correctly JSON-escaped (handling raw quotes `\"`, backslashes `\\`, and explicit line breaks `\n`).

3. **Syntax & Bug Correction:**

- Detect and silently fix syntax errors or logic glitches present in raw source manuals (e.g., accidental syntax errors like `.value_counts()` on strings, unmatched brackets, or deprecated scikit-learn parameters) while preserving the exact intended behavior and results.

---

## Notebook Architecture & Schema Specification

All converted notebooks must adhere to the Jupyter Notebook v4.5 specification:

```json
{
  "cells": [],
  "metadata": {
    "kernelspec": {
      "display_name": "Python 3",
      "language": "python",
      "name": "python3"
    },
    "language_info": {
      "name": "python",
      "version": "3"
    }
  },
  "nbformat": 4,
  "nbformat_minor": 5
}
```

Each cell object must follow this format:

- **Markdown Cell:**

```json
{
  "cell_type": "markdown",
  "id": "unique_string_id",
  "metadata": {},
  "source": ["# Header\n", "Prose description..."]
}
```

- **Code Cell:**

```json
{
  "cell_type": "code",
  "execution_count": null,
  "id": "unique_string_id",
  "metadata": {},
  "outputs": [],
  "source": ["import numpy as np\n", "print('Code here')"]
}
```

---

## Standard Structural Blueprint

Every generated notebook must follow this sequential section layout:

### 1. Student Identity Cell (Top-Level Markdown)

Must precede all academic content:

```markdown
### Student Information

- **Name:** Muhammad Ahmad
- **Roll No:** 34801
- **Subject:** Machine Learning
- **Class:** BS - AI (Semester-05)

---
```

### 2. Lab Header & Metadata Table

Include the title, lab number, topic, component summary table, and basis note.

### 3. Prerequisites & Asset Setup Cell

Specify data file requirements and relative paths:

```markdown
### Prerequisites & Asset Setup

- **Required File:** `<dataset_name>.csv`
- **Repository Path:** Located under `Lab-<XX>/assets/<dataset_name>.csv` (or `./assets/<dataset_name>.csv`). Ensure this CSV is placed in the notebook's working directory or modify `pd.read_csv()` accordingly.
```

### 4. Interleaved Theory and Code Sections

- Split theory, mathematical definitions, and reference distribution tables into individual **Markdown** cells.
- Place executable code blocks into standalone **Code** cells matching standard logical steps (Data Ingestion $\rightarrow$ Preprocessing $\rightarrow$ Baseline Training $\rightarrow$ Cross-Validation $\rightarrow$ Tuning $\rightarrow$ Final Evaluation).
- Do not clump the entire script into a single monolithic code cell; split by section (e.g., 3.1 Imports, 3.2 Loading, 3.3 Target creation).

### 5. Task & Interpretation Cells

Whenever a manual poses conceptual questions, tasks, or metrics interpretation (e.g., confusion matrix analysis, precision/recall trade-offs, baseline comparisons):

- Format them into a dedicated Markdown cell immediately following the relevant code cell.
- Format answers with explicit bold numbering, mathematical formulas in standard LaTeX (`$inline$` or `$$display$$`), and clear rationale.

---

## Verification & QA Check

Before completing a notebook generation, agents must internally verify:

- [ ] Top-level JSON keys exist: `cells`, `metadata`, `nbformat`, `nbformat_minor`.
- [ ] No trailing commas invalidating JSON syntax.
- [ ] All code strings inside `"source": [...]` have proper comma separation between array items.
- [ ] All single-quote and double-quote balance inside Python scripts is preserved.
- [ ] Student info block contains: Muhammad Ahmad | Roll No: 34801 | Machine Learning | BS - AI (Semester-05).
- [ ] Asset paths are clearly documented in the prerequisites section.
