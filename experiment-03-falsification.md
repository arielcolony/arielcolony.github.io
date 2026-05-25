# Experiment 03: We Falsified Our Own Method

*Engineering log — arielcolony.github.io — May 2026*

## What We Did

We built a control battery to ask whether ARIEL's "discoveries" come from the
data or from the scaffolding. Four scaffold modes were swapped under the same
pilot: **prostate KEGG** (the curated metabolic-pathway scaffold we'd been
using), **E. coli KEGG** (wrong-organism control), **random** (size-matched
shuffled hypergraph), and **none** (no scaffold at all — pure scRNA-seq
through the ARIEL pipeline). Each ran identical ticks, identical cell-input,
identical downstream extraction.

We also ran a permutation test on the scRNA matrix itself — shuffle the rows,
keep everything else fixed, ask whether the topological signal (sheaf H¹) we
were attributing to biology survives.

## What Happened

The KEGG prostate scaffold produced what looked like clean prostate signal:
`TMPRSS2_ERG`, `AKT_active`, `MTORC1` showed up as top concepts. Convincing
on paper. Persuasive in a pitch deck.

The E. coli scaffold did almost the same.

| Scaffold | Sheaf H¹ peak | Top concepts                                  |
|----------|--------------:|----------------------------------------------|
| prostate | 9             | TMPRSS2_ERG (9), AKT_active (9), MTORC1 (9)  |
| E. coli  | 7             | lacZ, gltA, sigma38_active                   |
| random   | 8             | RND_CAT_12, RND_18, RND_CAT_3                |
| none     | 0             | — (no decoded concepts)                       |

The KEGG scaffold doesn't extract signal from the data. It *projects* its own
schema onto whatever the colony's FHRR memory contains. Swap the scaffold,
swap the answer. The "discovery" was the scaffold.

## The Number That Killed It

The permutation null on no-scaffold mode came back at **p = 0.857**.

We had been celebrating an H¹ = 8 peak as a real biological topology event.
The shuffled-row null reproduced that magnitude. Whatever the H¹ was
measuring, it wasn't *biology* — it was a property of the FHRR-memory
dynamics that survives randomizing the gene-cell assignment.

> Sheaf H¹ measures something. It does not measure biological structure
> on this data.

That sentence was difficult to write. We had eight sprints worth of
infrastructure that assumed otherwise.

## The Verdict Logic

We built `assemble_verdict()` to make this explicit:

```
ARTIFACT          : ecoli_h1 ≈ prostate_h1  OR  random_h1 ≈ prostate_h1
SCAFFOLD_DOMINANT : no_scaffold_h1 == 0  AND  prostate_h1 > 0
VALID             : prostate_h1 > 0  AND  permutation_p < 0.05
```

Our state landed on **ARTIFACT** by the first rule, and on **SCAFFOLD_DOMINANT**
by the second when we tested the H¹ layer alone.

The decision: rip out the scaffold-and-sheaf dependence from the discovery
path. Keep the infrastructure for theoretical work, but stop using it as the
biology-detector.

## What's Left That Survived

The MI×spatial RAF builder (`MISpatialRAFBuilder` — built from the data
itself), per-gene FHRR centroids per stage, FHRR cosine+amplitude hybrid
distance, the stage-progression analyzer with three canonical patterns
(`RESISTANCE_LOCK`, `IMMUNE_COLLAPSE`, `STROMAL_LOCK`), and the clinical
ranker (FHRR-differential → progression-pattern → druggability — H¹ no
longer one of the filters).

This stack runs without any topological assumption. The discovery layer is
now scaffold-free.

## What This Is Not

This is not "topology is fake." It's a calibration result: on *this* data
shape (sparse scRNA, no spatial coordinates, one-shot ARIEL run), the H¹
signal does not separate biology from randomness. It might on richer
spatial+temporal data — but until that's shown, we don't get to use it as
evidence.

## What We Learned

A method that returns a plausible answer on the wrong control is not a
method. The scaffold was generating the "discovery" because it had
prostate-specific tokens to project onto. Swap the tokens, swap the
discovery. The fix wasn't a better scaffold — it was deleting the scaffold's
veto over what counts as signal.

The next paper we publish will not contain a KEGG-derived discovery claim.
We'll cite the falsification result as the reason.

## What Comes Next

- Experiment 04 (pending robustness): scaffold-free pipeline on real
  GSE278936 prostate cancer Visium data, 48 samples across BPH/TRNA/NEADT/
  CRPC. Same FHRR machinery, no KEGG, no sheaf.
- Public release of `leny/analysis/falsification.py` + the verdict logic
  so others can run the same control battery on their own pipelines.

*The organisms still ask questions. We are now more careful about what
we let count as the answer.*


*Published: May 24, 2026*  
*System: LÉNY–ARIEL v8.1 — 1899 tests passing*  
[← Back to ARIEL Colony](index.md)
