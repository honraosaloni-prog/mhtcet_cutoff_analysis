# MHT-CET Engineering Cutoff Analysis: Are Computer Branches Really Booming?

Analysis of engineering admission cutoffs in Maharashtra (2022–2025), extracted from official government PDFs, testing whether the perceived surge in demand for Computer branches shows up in the admissions data.

**[View the notebook on Google Colab](ADD_YOUR_COLAB_LINK_HERE)**

---

## Question this answers

Computer Science and allied branches are widely believed to be harder to get into than ever. Does the official cutoff data support that — and is the effect specific to Computer branches, or are all engineering branches tightening together?

## Key findings

- **Computer-adjacent branches average 98.76 percentile vs 96.99 for core branches** — a 1.77 percentile-point gap.
- **The gap holds in all 8 college-year combinations measured**, ranging from +0.35 to +2.94 points. It is not driven by a single prestigious institution or one unusual admission cycle.
- **Core branches are also getting harder.** VJTI Civil Engineering rose from 96.93 to 98.47 percentile between 2022 and 2025. The accurate framing is not "only Computer is booming" but "everything is tightening, and Computer stays consistently ahead."
- **Percentile alone misleads.** COEP shows ~95 percentile cutoffs versus ~99.7 at VJTI and PICT despite comparable reputation — a function of larger intake capacity pushing the closing rank deeper into the applicant pool. Closing *rank* tells the story percentile hides: VJTI Computer Engineering closes around rank 259–882, while VJTI Civil closes around 7,600–14,700.

| Branch category | Avg percentile | Observations |
|---|---|---|
| Computer-adjacent (CS / IT / AI&DS) | 98.76 | 18 |
| Core / Traditional (Civil / E&TC) | 96.99 | 8 |

## Data

Source: **DTE Maharashtra State CET Cell** — official CAP Round 1 cutoff documents, published annually at `mahacet.org`. Each file is a 1,300–1,570 page PDF covering every engineering college in the state.

- **Colleges:** VJTI Mumbai, PICT Pune, COEP Pune
- **Branches:** Computer Engineering, Information Technology, AI & Data Science, Civil Engineering, Electronics & Telecommunication
- **Years:** 2022–2025 (CAP Round 1)
- **Category:** GOPENS (General, Open, State-level)
- **Output:** `mhtcet_cutoffs.csv` — 26 rows

## Method

1. **Extraction** — downloaded each year's full PDF and parsed it with `pdfplumber`, splitting the document into per-college sections using a regex on the `<code> - <College Name>` header pattern
2. **Parsing** — within each college block, located branch sections and extracted the rank and percentile pair for the GOPENS category from the cutoff table that follows
3. **Categorisation** — grouped branches into Computer-adjacent vs Core/Traditional to enable a like-for-like comparison
4. **Analysis** — computed the within-college, within-year gap between the two categories, which controls for institutional prestige and year-to-year exam difficulty
5. **Visualization** — matplotlib: category comparison, per-college branch trends, gap-over-time, and a log-scale rank chart

The gap-within-college-and-year approach is the analytically important step. Comparing raw percentiles across colleges would conflate branch demand with institutional reputation; comparing within a single college and admission cycle isolates the branch effect.

## Limitations

- **CAP Round 1 only.** Cutoffs shift in later rounds as seats fill.
- **GOPENS category only.** Reserved-category cutoffs differ substantially and are not covered here.
- **COEP is absent from 2022–23 data**, likely related to its transition to autonomous university status during that period.
- **Three colleges is a sample, not the full state picture.** The finding is consistent across those three, but generalising to all of Maharashtra would require broader extraction.
- Some branch/college combinations returned no match during extraction. Where a college genuinely does not offer a branch (PICT does not offer Mechanical or Civil), the absence is real; a small number of others may reflect parsing gaps rather than true absences.

## Tools

`Python` · `pandas` · `matplotlib` · `pdfplumber` · `regex`

## Files

```
├── colab_mhtcet.py          # single-cell analysis, data embedded
├── extract_cutoffs.py       # PDF download + parsing script
└── mhtcet_cutoffs.csv       # extracted dataset
```

## Reproducing the extraction

```bash
pip install requests pdfplumber
python extract_cutoffs.py
```

Edit `TARGET_COLLEGES` and `TARGET_BRANCHES` in the script to cover different institutions or branches. College names must match the spelling used in the source PDF, which varies slightly between years.

## Graphs
<img width="887" height="537" alt="OP1" src="https://github.com/user-attachments/assets/83aa8b2e-c70e-44da-ba81-26f1bab4303d" />
<img width="1586" height="513" alt="op2" src="https://github.com/user-attachments/assets/270a5fa3-5834-4fa2-8dca-e489eccedcac" />
<img width="887" height="486" alt="op3" src="https://github.com/user-attachments/assets/e9d9df9e-d81a-47ec-add9-3a886bab3c87" />
<img width="987" height="536" alt="op4" src="https://github.com/user-attachments/assets/bab3d9c8-532b-48c0-a2c9-71bff700ec8e" />


