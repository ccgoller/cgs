---
layout: default
title: Electronic Lab Notebook Template
nav_order: 5
permalink: /eln
---
# 📓 Electronic Lab Notebook (ELN) Template

> An ELN is a permanent, dated, and searchable record of your experimental work. It is a cornerstone of scientific reproducibility and professional practice.

---

## Why Keep an ELN?

- Provides a **legal and scientific record** of your work.
- Allows you and others to **reproduce your experiments**.
- Documents your **thought process**, not just your results.
- Required for any research publication or patent application.

---

## Platform Recommendation

We recommend using **Benchling** (free for academics) or your institution's preferred ELN platform. Alternatively, a well-organised **Markdown workflow in a private GitHub repository** is acceptable for CGs lab undergraduate work.

> 💡 Ask your TA which platform your lab section is using before Week 1.

---

## Using GitHub for Your ELN

If you are keeping your ELN in Markdown, start by opening the CGs lab hub repository at [ccgoller/cgs](https://github.com/ccgoller/cgs). This repository contains the shared lab instructions, protocols, and ELN template that you should reference throughout the semester.

Use the CGs repository as your reference source, but keep your personal notebook entries in your own **private** repository or another TA-approved space rather than in this public site repository.

Recommended setup:

1. Sign in to GitHub and open the CGs lab hub repository: `https://github.com/ccgoller/cgs`
2. Create your own private ELN repository for the semester.
3. Create a clear folder structure (for example: `notebooks/`, `data/`, and `images/`).
4. Create one Markdown notebook file in `notebooks/` for each experiment or lab day.
5. Keep experiment-specific files grouped in matching folders when useful (for example: `data/2026-09-02_BacterialTransformation/`).
6. Copy the ELN structure below into each new notebook and complete it in real time during lab.
7. Commit your updates regularly so each entry has a clear dated history.

Suggested file format for individual notebook entries:

```
YYYY-MM-DD_ExperimentTitle.md
```

**Example:** `2026-09-02_BacterialTransformation.md`

You may also keep related files such as gel images, raw data sheets, or analysis outputs in clearly labelled folders alongside each notebook entry.

---

## ELN Entry Structure

Every entry must contain **all six sections** below. Use the template for each experiment.

---

```
========================================================
EXPERIMENT ENTRY
========================================================
Title:      [Brief descriptive title]
Date:       [YYYY-MM-DD]
Researcher: [Your full name]
Lab Group:  [e.g., CGs Undergraduate Research]
Section:    [Your lab section number]
TA:         [TA name]
========================================================

## 1. Objective / Research Question
[State clearly what you are trying to accomplish or answer in ONE to THREE sentences.]

## 2. Background / Hypothesis
[Brief context (2–4 sentences). State your hypothesis in the form:
"If [independent variable] then [expected result] because [reasoning]."]

## 3. Materials
[List all reagents, equipment, and organisms used. Include:
- Reagent name, concentration/lot number if relevant
- Equipment model numbers where applicable
- Organism(s) and source/strain information]

## 4. Methods
[Describe EXACTLY what you did — enough detail for someone else to repeat it.
Reference the SOP if you followed a standard protocol, then note any deviations.
Use numbered steps.

Example:
1. Followed COMMON_PROTOCOLS.md §4 (Bacterial Transformation) with the following changes:
   - Used 2 µL plasmid DNA instead of 1 µL due to low concentration (see Calculation, below).
2. Plated 100 µL on LB+Amp plates.]

## 5. Results
[Record ALL data — even unexpected or "failed" results.

Include:
- Raw data tables
- Observations (colour, turbidity, colony morphology, etc.)
- Gel images or photographs (attach/embed or reference file name)
- Calculations shown step-by-step

Example table:
| Plate | Colonies Counted | Dilution Factor | CFU/mL |
|---|---|---|---|
| 10⁻⁴  | 47 | 1 × 10⁻⁴ | 4.7 × 10⁶ |
| 10⁻⁵  | 5  | 1 × 10⁻⁵ | 5.0 × 10⁶ |]

## 6. Discussion / Interpretation
[Answer these questions in paragraph form:
1. Did your results support or refute your hypothesis? Explain.
2. Were there any anomalies or unexpected observations? What might explain them?
3. What sources of error could have affected your results?
4. What would you change or test next?]

## Signatures / Sign-off
Researcher: ________________________  Date: __________
TA review:  ________________________  Date: __________

========================================================
END OF ENTRY
========================================================
```

---

## ELN Submission Checklist

Before submitting each entry to your TA, confirm:

- ☐ All six sections are present and complete.
- ☐ Entry is dated on the **day the experiment was performed** (not backdated).
- ☐ Raw data is included — not just final calculated values.
- ☐ Deviations from the published protocol are noted.
- ☐ Any images/gels are labelled with your name, date, and lane/sample info.
- ☐ Calculations show all steps and units.
- ☐ No data has been erased — mistakes are crossed out with a single line and initialled.

---

## File Naming Convention

If submitting digital files, use the following format:

```
LastName_FirstName_YYYYMMDD_ExperimentTitle.ext
```

**Example:** `Smith_Jordan_20260902_BacterialTransformation.pdf`

---

## Tips for a High-Quality ELN

| Do | Don't |
|---|---|
| Write in the lab, in real time | Write from memory after the fact |
| Record instrument settings | Assume "I'll remember" |
| Note the lot numbers of reagents | Skip negative or failed results |
| Use ink (or locked digital entries) | Use pencil or white-out |
| Date and sign every page | Leave blanks to fill in later |

---

*Return to [Hub Home](/cgs/)*
