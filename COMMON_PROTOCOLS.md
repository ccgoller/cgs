---
layout: default
title: Common Protocols
nav_order: 4
permalink: /protocols
---
# 🔬 Common Protocols

> Standard operating procedures (SOPs) used in the Gordy–Goller teaching labs.  
> Always confirm with your instructor/mentor if a protocol has been modified for your specific experiment.

{% include download_links.html markdown_url="/downloads/common-protocols.md" pdf_url="/downloads/common-protocols.pdf" %}

---

## Table of Contents

1. [Aseptic Technique](#1-aseptic-technique)
2. [Preparing Liquid Media](#2-preparing-liquid-media)
3. [Preparing Agar Plates](#3-preparing-agar-plates)
4. [Bacterial Transformation (Heat Shock)](#4-bacterial-transformation-heat-shock)
5. [PCR Amplification](#5-pcr-amplification)
6. [Agarose Gel Electrophoresis](#6-agarose-gel-electrophoresis-using-e-gel-system)
7. [Restriction Enzyme Digest](#7-restriction-enzyme-digest)
8. [Gram Staining](#8-gram-staining)
9. [Serial Dilution and Plate Counting](#9-serial-dilution-and-plate-counting)
10. [Micropipette Calibration and Usage](#10-micropipette-calibration-and-usage)

---

## 1. Aseptic Technique

**Purpose:** Prevent contamination of cultures and reagents.

**Materials:** 70% ethanol, sterile loops/pipettes.

**Procedure:**
1. Wipe bench with 70% ethanol; allow to dry.
2. Activate biosafety cabinet (if available).
3. Keep all media containers open for the minimum time necessary.
4. Never set down lids — hold them or place upside down on a clean surface.
5. Dispose of used loops and pipettes in appropriate waste immediately.

---

## 2. Preparing Liquid Media

**Example:** LB broth (1 L)

| Reagent | Amount |
|---|---|
| Tryptone | 10 g |
| Yeast extract | 5 g |
| NaCl | 10 g |
| dH₂O | to 1 L |

> [!IMPORTANT]
> We often use pre-mixed powders that have agar for plates or without it for broth. Please get help from one of your peers before autoclaving. 

1. Combine ingredients in a 2 L flask. Please note that we often use premixed media: all components in a single powder.
2. Stir to dissolve.
3. Autoclave at 121°C, 15 psi, 20 min (liquid cycle).
4. Allow to cool to ~55°C before adding heat-sensitive supplements.
5. Store at 4 °C for up to 4 weeks.

---

## 3. Preparing Agar Plates

1. Prepare LB broth as above; add **15 g agar** per liter before autoclaving.
2. After autoclaving, cool in a 55 °C water bath until the flask is comfortable to hold.
3. Add any antibiotics or supplements at this stage (see supplement table below).
4. Pour ~25 mL per 100-mm plate in a laminar-flow hood. If available and using the correct flask, use the KEIO plate pourer.
5. Allow to solidify at room temperature (~20 min), then invert and store at 4 °C.

**Common Antibiotics (stock → working concentration):**

| Antibiotic | Stock | Working | Solvent |
|---|---|---|---|
| Ampicillin | 100 mg/mL | 100 µg/mL | dH₂O (sterile) |
| Kanamycin | 50 mg/mL | 50 µg/mL | dH₂O (sterile) |
| Chloramphenicol | 25 mg/mL | 25 µg/mL | 100% ethanol |

---

## 4. Bacterial Transformation (Heat Shock)

**Materials:** Chemically competent *Escherichia coli*, plasmid DNA, SOC medium, LB+antibiotic plates.

1. Thaw competent cells on ice (10 min).
2. Add 1–5 ng plasmid DNA to 50 µL cells; flick gently to mix — **do not pipette**.
3. Incubate on ice for 30 min.
4. Heat shock at **42 °C for exactly 45 s** in a water bath.
5. Return to ice for 2 min.
6. Add 950 µL room-temperature SOC medium.
7. Incubate at 37 °C, 200 rpm, for 1 h (recovery).
8. Plate 100–200 µL on selective plates; spread with sterile beads or a spreader.
9. Incubate plates inverted at 37 °C overnight.

---

## 5. PCR Amplification

**Typical 25 µL reaction:**

| Component | Volume |
|---|---|
| 2× Master Mix | 12.5 µL |
| Forward primer (10 µM) | 1.0 µL |
| Reverse primer (10 µM) | 1.0 µL |
| Template DNA | 1.0 µL |
| Nuclease-free H₂O | 9.5 µL |

**Cycling conditions (adjust annealing Tm as directed):**

| Step | Temp | Time | Cycles |
|---|---|---|---|
| Initial denaturation | 95 °C | 3 min | 1× |
| Denaturation | 95 °C | 30 s | 30× |
| Annealing | *Tm − 5 °C* | 30 s | 30× |
| Extension | 72 °C | 1 min/kb | 30× |
| Final extension | 72 °C | 5 min | 1× |
| Hold | 4 °C | ∞ | — |

---

## 6. Agarose Gel Electrophoresis using E-Gel System

Review the [E-Gel video](https://youtu.be/6_TtIGAm45w).
[![Watch the video](https://youtube.com)](https://youtu.be/6_TtIGAm45w)


1. Prepare E-Gel system by obtaining an E-Gel base and appropriate E-Gel.
2. Place E-Gel in the base until it clicks.
3. Load 5-20 µL ladder + x µL loading dye) for a total of 20 µL per well.
3. Load 5-20 µL sample buffer + 5 µL sample (mixed with 6× loading dye) per well.
6. Run at **100 V for 30–45 min** in 1× TAE.
7. Image on UV transilluminator — **wear a UV-blocking face shield**.

---

## 7. Restriction Enzyme Digest

**Typical 20 µL reaction:**

| Component | Volume |
|---|---|
| CutSmart Buffer (10×) | 2 µL |
| DNA (~1 µg) | variable |
| Enzyme 1 (20 U/µL) | 1 µL |
| Enzyme 2 (if double digest) | 1 µL |
| Nuclease-free H₂O | to 20 µL |

1. Assemble on ice; add enzyme last.
2. Incubate at **37 °C for 1 h** (or as recommended by manufacturer).
3. Heat-inactivate at **65 °C for 20 min** (check enzyme datasheet — not all enzymes are inactivatable).
4. Analyse by gel electrophoresis.

---

## 8. Gram Staining

1. Prepare a thin bacterial smear on a clean slide; air dry, then heat-fix.
2. Flood with **crystal violet** — 1 min; rinse gently with water.
3. Flood with **Gram's iodine** — 1 min; rinse gently with water.
4. **Decolourise** with 95% ethanol — 10–15 s; rinse immediately with water. *(This step is critical — do not over-decolourise.)*
5. Flood with **safranin** — 1 min; rinse gently with water.
6. Blot dry (do not wipe); observe under 100× oil-immersion lens.

**Expected results:**

| Result | Interpretation |
|---|---|
| Purple/violet cells | Gram-positive |
| Pink/red cells | Gram-negative |

---

## 9. Serial Dilution and Plate Counting

1. Label tubes 10⁻¹ through 10⁻⁶ (or as needed).
2. Add 900 µL sterile diluent (PBS or saline) to each tube.
3. Transfer 100 µL of original culture → 10⁻¹ tube; vortex.
4. Transfer 100 µL from 10⁻¹ → 10⁻² tube; repeat to desired dilution. **Change pipette tips between every transfer.**
5. Plate 100 µL of appropriate dilutions (aim for 30–300 CFU/plate).
6. Incubate inverted at appropriate temperature overnight.
7. Count colonies; calculate CFU/mL: `CFU/mL = colonies ÷ (dilution factor × volume plated in mL)`.

---

## 10. Micropipette Calibration and Usage

**Calibration (gravimetric method):**
1. Set pipette to target volume; weigh a tared tube on analytical balance.
2. Dispense 10 replicate aliquots of dH₂O into tube; record weight.
3. Accuracy: measured volume should be within ±1% of target (at 20 °C, 1 µL water ≈ 1 mg).

**Usage tips:**
- Always use the correct pipette for your volume range:
  - P2: 0.2–2 µL | P10: 1–10 µL | P20: 2–20 µL | P200: 20–200 µL | P1000: 100–1000 µL
- Pre-wet tips with the sample before final aspiration when working with viscous solutions.
- Hold pipette vertically during aspiration; avoid air bubbles.

---

*Return to [Hub Home](/cgs/)*
