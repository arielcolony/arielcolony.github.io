# Experiment 02: What the Colony Found — PGK1 and the Glycolytic-Immune Interface

*Engineering log — May 20, 2026*

[← Back to ARIEL Colony](index)

---

## Background

In [Experiment 01](experiment-01-cancer), we fed 30 PubMed abstracts on tumor 
microenvironment metabolism into a colony of 3 LÉNY digital organisms and detected 
10 topological anomalies. The nearest domain concept was `microenvironment` — 
consistent across all 10 events.

This experiment scales to 100 abstracts and introduces two pipeline improvements:
TF-IDF weighted domain decoding (S156) and author-name filtering (S157). These 
changes remove hash-lucky noise tokens and surface biologically meaningful signals.

---

## What We Did

100 PubMed abstracts, tumor microenvironment metabolism, 2022-2026.  
Colony: 3 LÉNY agents, d=1,000, 10,000 ticks without respawning.  
Pipeline: TF-IDF weighted codebook + author-name stop-list.

---

## What the Colony Found

**77 topological anomalies** — 34 loop births, 43 loop deaths.  
Tick range: 2,100–9,500. Phase_time ≈ 1,389.

### The Signal

| Concept | Frequency | Biological relevance |
|---------|-----------|---------------------|
| levels | 77/77 | expression/metabolic levels — methodological |
| **pgk1** | **69/77** | **Phosphoglycerate Kinase 1 — direct glycolysis** |
| **effector** | **66/77** | **Effector T-cells — TME immune axis** |
| viability | 61/77 | Cell viability — therapeutic endpoint |
| medicine | 46/77 | Therapy context |
| regulation | 33/77 | Gene regulation |

---

## Two Axes

The colony did not find one signal. It found two — and they point at the same 
intersection.

**Axis 1 — Glycolysis:** `pgk1` (Phosphoglycerate Kinase 1) is a key enzyme in 
the Warburg pathway. Tumor cells upregulate glycolysis even in the presence of 
oxygen. PGK1 sits in the middle of this pathway and has been implicated in 
hypoxia response, metabolic reprogramming, and drug resistance. 69 of 77 
topological loops in the colony's conceptual space showed PGK1 as the nearest 
domain anchor.

**Axis 2 — Immune suppression:** `effector` refers to effector T-cells — the 
immune cells that tumors suppress to evade destruction. 66 of 77 anomalies 
showed effector T-cell concepts as secondary anchors.

---

## The White Space

These two axes are individually well-studied. The intersection is not.

**How does tumor glycolysis suppress effector T-cell function?**

The metabolic competition hypothesis exists in the literature: tumor cells 
consume glucose and produce lactate, starving T-cells of the fuel they need 
to kill. But the mechanistic link through PGK1 specifically — how PGK1 
activity modulates the tumor-immune metabolic interface — is structurally 
underexplored.

The colony found this intersection not by reading about it. It found it by 
detecting where the geometry of 100 abstracts becomes topologically unstable — 
where loops form and dissolve repeatedly around the same conceptual region.

---

## Comparison: 30 vs 100 Abstracts

| Metric | 30-abs (Exp 01) | 100-abs (Exp 02) |
|--------|-----------------|------------------|
| Anomalies | 10 | 77 |
| Top signal | microenvironment | pgk1 + effector |
| Interpretability | 0.061–0.088 | 0.160–0.260 |
| Pipeline | word-bundle | TF-IDF weighted |

The 3.5× improvement in interpretability score confirms that TF-IDF weighting 
surfaces biologically meaningful tokens over hash-lucky noise.

The signal shift from `microenvironment` (general) to `pgk1 + effector` 
(mechanistically specific) suggests that larger corpora allow the colony to 
resolve finer-grained conceptual structure.

---

## What This Is Not

This is not a discovery. PGK1 is known. Effector T-cell suppression is known.  
The intersection has been noted in the literature.

What is not known — and what the colony's topological instability may be 
pointing at — is the specific mechanistic pathway through which PGK1 activity 
shapes the effector T-cell microenvironment. This is a structural white space: 
the concepts are present, the connection is implied, but the loop is not closed 
in the literature.

Whether this white space is scientifically valuable requires expert evaluation.  
We are not making that claim. We are making the observation.

---

## What Comes Next

- Domain expert blind evaluation: is the PGK1-effector intersection a real 
  research gap or a known pathway we missed?
- Prostate cancer TME corpus: does the same glycolytic-immune intersection 
  appear in a different cancer type?
- Cross-domain run: cancer metabolism + mathematical TDA — Colony Logos synthesis
- Longer standby runs: 50+ generations with domain injection

---

*Published: May 20, 2026*  
*System: LÉNY–ARIEL v5.1 — S157 pipeline*  
[← Back to ARIEL Colony](index.md)
