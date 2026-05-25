# Experiment 04: 48-Sample Prostate CRPC — Three Therapeutic Axes

*Engineering log — arielcolony.github.io — May 2026*

## What We Did

We ran the scaffold-free ARIEL pipeline (Experiment 03 cleanup) on
**GSE278936** — Kiviaho et al. 2024 prostate cancer Visium scRNA-seq
spanning four disease stages:

| Stage  | Samples | Cells aggregated |
|--------|--------:|-----------------:|
| BPH    | 4       | 5,809            |
| TRNA   | 17      | 23,493           |
| NEADT  | 22      | 32,676           |
| CRPC   | 5       | 5,914            |
| **total** | **48**  | **~71,000**      |

Common HVG ∪ DE: **746 genes** shared across all 48 samples (re-processed
without per-sample HVG filtering so the cross-stage intersection survives —
earlier processing left only 2 common genes; the fix raised it to 13,101
candidates, then the master-matrix HVG selection picked 500 and a
pseudobulk BPH-vs-CRPC differential layer added 300 more for a union of
746 unique genes — the union recovers stromal/CAF signals that the variance
filter alone misses). MI×spatial RAF built from the data, per-gene FHRR
centroids per stage, cosine+amplitude hybrid distance NEADT → CRPC,
stage-progression analyzer over the four-stage axis.

No KEGG. No sheaf. No topological assumption.

## What Happened

The pipeline returned 30 progression genes (`min_correlation ≥ 0.6` against
the canonical patterns), and **all 30 matched `IMMUNE_COLLAPSE`** — the
monotone-rise pattern (`0.1 → 0.2 → 0.5 → 0.8 → 1.0` across BPH/TRNA/NEADT/
CRPC). No gene fit `RESISTANCE_LOCK` or `STROMAL_LOCK` strongly enough.

The 30 split into **four functional clusters** — what we are calling the
tumor's "operating system":

### Layer 1 — Mitotic apparatus

```
CDCA5     corr 0.782    cohesin
TPX2      corr 0.780    spindle assembly
CIT       corr 0.802    citron kinase
CENPF     corr 0.771    centromere protein F
CENPE     corr 0.736    kinetochore motor
CENPK     corr 0.678    centromere protein K
STMN1     corr 0.744    stathmin / microtubule
NCAPD3    corr (in FHRR-diff)  condensin
BIRC5     corr 0.805    survivin / anti-apoptotic IAP
```

Cell-cycle infrastructure scaling monotonically toward CRPC. Not
proliferation rate — *machinery for proliferation*.

### Layer 2 — DNA replication / repair

```
RRM2      corr 0.779    ribonucleotide reductase
POLE2     corr 0.677    DNA polymerase ε subunit
HELLS     corr 0.674    helicase / chromatin remodeler
BRCA1     corr 0.685    homologous recombination
```

The replication-licensing and HR layer. BRCA1 here is the punch line — it
opens the door to synthetic-lethality therapy.

### Layer 3 — Notch / Neuroendocrine transdifferentiation

```
HES6      corr 0.835    Notch downstream, NE differentiation
HEY1      (in FHRR diff Δ=2.13)
UCHL1     (in FHRR diff Δ=1.20)    classic NE-CRPC marker
SLITRK6   corr 0.671    neural receptor
SHH       (in FHRR diff Δ=5.99)    Sonic Hedgehog / lineage plasticity
```

The CRPC-NE subtype signature. This is the lineage-plasticity escape from
AR-axis therapy.

### Layer 4 — Immune-IFN axis

```
IFI27     corr 0.831    IFN-α inducible
IGHG2     corr 0.740    immunoglobulin
ADA       corr 0.733    adenosine deaminase
MIR210HG  corr 0.885    hypoxia-induced lncRNA
MMP11     corr 0.891    matrix metalloproteinase
SLC16A3   corr 0.692    MCT4 lactate exporter (Warburg)
PKP3      corr 0.901    plakophilin-3 / cell adhesion
```

Immune-microenvironment + Warburg coupling. The IFN signature plus the
lactate-shuttling enzyme is consistent with hypoxia-driven immune
exclusion.

## Top-3 Therapeutic Targets

The clinical ranker (FHRR-differential → progression-pattern →
druggability) returned:

| Rank | Gene  | Pattern         | Drug         | Mechanism                       | Clinical status      |
|-----:|-------|-----------------|--------------|---------------------------------|----------------------|
| 1    | HES6  | IMMUNE_COLLAPSE | DAPT         | γ-secretase / Notch inhibitor   | Experimental NE-CRPC |
| 2    | CENPF | IMMUNE_COLLAPSE | docetaxel    | Anti-mitotic (taxane)           | FDA approved mCRPC   |
| 3    | BRCA1 | IMMUNE_COLLAPSE | olaparib     | PARP inhibitor (synthetic lethality) | FDA approved mCRPC HRR-mut |

Two of the three are FDA-approved standard-of-care. The third (DAPT) is
the experimental Notch-blocker that lines up with the CRPC-NE subtype
identified by Tang et al. (Science 2022). The pipeline is not finding new
drugs — it's finding the *biological axes* the existing drugs already
target, in the right order, from raw single-cell data with no scaffold
hint.

## The Numbers

```
n_samples         : 48 (4 BPH + 17 TRNA + 22 NEADT + 5 CRPC)
n_cells           : 67,892
common HVG ∪ DE   : 746
MI edges          : 13,894 / stage (top 5%)
Kuramoto R        : 0.450 (stable across stages)
Questions/stage   : 9
Progression genes : 30  (corr ≥ 0.6, all IMMUNE_COLLAPSE)
Top-3 ranker      : HES6, CENPF, BRCA1
Top FHRR Δ        : CDCA5 7.23, TPX2 6.84, SHH 5.99, BIRC5 5.44, CENPF 4.86
Robustness        : LOSO 44/48 (91.7%), perm p=0.0196, seed 5/5
```

## What This Is Not

This is not a clinical claim. It is an *unsupervised pattern detection*
result on a public dataset, and three of the top genes already have
approved drugs — which is the whole point: if the method is right, it
should recover what we already know before being trusted on what we
don't. Three out of three recovered.

This is also not a topology paper. Sheaf H¹ does not appear anywhere in
the discovery path. After Experiment 03, we don't use it for biology
claims.

## Caveats

- Single-cohort dataset. Replication on GSE143791 (bone-met TME) is the
  obvious next step before any "CRPC operating system" generalization.
- Spatial coordinates from Visium not yet wired in (the per-spot Jaccard
  on `coords` currently uses synthetic uniform positions — the real
  `tissue_positions.csv` is the S246-next layer).
- The IMMUNE_COLLAPSE-only monotonicity is suspicious — could be a
  selection effect from how the activity matrix is normalized.
  Robustness battery (S247) **completed**: leave-one-sample-out 44/48
  (91.7%), stage-label permutation p = 0.0196, seed variation 5/5
  stable. <b>Verdict: ROBUST.</b>

## What Comes Next

- ✅ **S247 — Robustness battery — DONE**: LOSO 44/48 (91.7%),
  permutation p = 0.0196, seed 5/5. Verdict: ROBUST.
- **GSE143791 replication** (next) — does the four-layer signature
  reproduce in bone-metastasis prostate scRNA-seq?
- **Spatial coords plumbing** (next) — real Visium positions into the
  MI×spatial RAF, not synthetic uniform.

*Three layers known. One layer (Notch-NE) sometimes under-treated. The
operating system is more readable than it looked.*


---
*Published: May 25, 2026*  
*System: LÉNY–ARIEL v8.1 — 1899 tests passing*  
[← Back to ARIEL Colony](index.md)
