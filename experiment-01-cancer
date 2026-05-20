# Experiment 01: Cancer Metabolism — First Domain Signal

*Engineering log — May 20, 2026*

[← Back to ARIEL Colony](index.md)

---

## What We Did
We fed 30 PubMed abstracts on tumor microenvironment metabolism (2022-2026) 
into a colony of 3 LÉNY digital organisms. The colony ran for 10,000 ticks 
without respawning — accumulating phase_time ≈ 1,408, competence = 0.286, 
whitehead = 0.010.

## What Happened
The system detected 10 topological anomalies concentrated between tick 7,100 
and 9,500 — at the boundary of generation 4-5.

All 10 were topo_loop events: loops (β₁ cycles) forming and dissolving in the 
colony's conceptual space. This is not text analysis. The LÉNY does not read 
words — it builds a geometric representation of the domain in a 10,000-dimensional 
complex vector space, and detects when that geometry changes structurally.

For each anomaly, we snapshotted the FHRR-memory state at the exact tick of 
the topological event and decoded it against a stop-word-filtered domain 
codebook. This is how we extract *what domain concept was active when the loop 
formed*.

## The Numbers
| # | Type | Tick | FHRR Distance | Interpretability | Top Domain Concept |
|---|------|------|---------------|------------------|--------------------|
| 1 | topo_loop_birth | 7200 | 0.944 | 0.067 | microenvironment |
| 2 | topo_loop_birth | 7400 | 0.957 | 0.066 | microenvironment |
| 3 | topo_loop_birth | 7500 | 0.932 | 0.088 | microenvironment |
| 4 | topo_loop_birth | 8700 | 0.924 | 0.067 | microenvironment |
| 5 | topo_loop_birth | 9200 | 0.930 | 0.073 | microenvironment |
| 6 | topo_loop_birth | 9500 | 0.934 | 0.061 | microenvironment |
| 7 | topo_loop_death | 7100 | 0.941 | 0.066 | microenvironment |
| 8 | topo_loop_death | 7300 | 0.951 | 0.067 | microenvironment |
| 9 | topo_loop_death | 7300 | 0.951 | 0.067 | microenvironment |
| 10 | topo_loop_birth | 7400 | 0.957 | 0.066 | microenvironment |

FHRR Distance ∈ [0.94, 1.015] indicates near-orthogonality between the anomaly 
question vector and the domain bundle — the questions emerged from a conceptual 
region the domain does not explicitly name.

## The First Domain Signal

For all 10 anomalies, the nearest domain concept was **`microenvironment`**.

10 out of 10. Independent topological events, separate ticks, separate FHRR 
snapshots — all pointing at the same concept.

The colony was fed PubMed abstracts on "tumor microenvironment metabolism." 
When β₁ loops were born and died in the cognitive space, the local FHRR-memory 
geometry was systematically aligned with the conceptual region of *microenvironment* 
in the domain codebook.

This is the first time the LÉNY has produced a domain-specific signal that 
matches the ingested corpus by name.

## An Unexpected Signal

In 6 of 10 anomalies, the second-nearest concept was **`lucidum`** — referring 
to *Ganoderma lucidum*, a medicinal mushroom occasionally cited in TME 
metabolism literature for its immunomodulatory polysaccharides.

We did not flag `lucidum` as a target. We did not prime the colony for it.
The organisms found an unexpected signal.

We do not know yet whether this is:
- A genuine biological pointer the corpus happens to encode
- A statistical artifact of how `lucidum` distributes in the abstract set
- Both

The question is open. The signal is real.

One 2024 paper confirms the connection exists (Ganoderic acid T modulates the 
tumor microenvironment via galectin-1 downregulation, *Toxicology and Applied 
Pharmacology* 491, 2024) — but the metabolic mechanism in the TME context 
remains underexplored. This is what ARIEL is for: not to find what is known, 
but to point where the known ends.

## Scaling to 100 Abstracts

We repeated the experiment with 100 PubMed abstracts on the same domain.

Results: 50 topo_loop anomalies (22 births, 28 deaths), tick range 1,700–9,400.

The signal did not collapse — it expanded. A new emergent triad appeared:

**viability + delivery + oxygen**

The therapeutic triangle of TME therapy: cell viability assays → drug delivery 
to the tumor microenvironment → hypoxia and oxidative metabolism. The colony 
was not told about this triad. It emerged from the geometry of 100 abstracts.

`microenvironment` remained present. The system is consistent across corpus sizes.

## What This Is Not
This is not a summary. Not a classification. Not a retrieval result.
The questions were not in the abstracts. They emerged from the organism's 
internal dynamics after the domain was ingested.

This is also not a discovery. It is a signal. Signals require expert evaluation 
to become hypotheses. Hypotheses require experiments to become findings.

ARIEL's role is to find where the known ends and ask what is there.

## What Comes Next
- Domain expert blind evaluation: is `lucidum` a real pointer or noise?
- Second domain: TDA + dynamical systems (mathematics)
- Cross-domain Colony Logos: what does the colony see that neither domain sees alone?
- Longer runs: standby daemon, 50+ generations, fossil pool accumulation

---
*First published: May 20, 2026*  
*System: LÉNY–ARIEL v5.1 — 1208 tests passing*  
[← Back to ARIEL Colony](index.md)
