# Reanalysis of public WES data SRR4088561 for RAG1-associated severe combined immunodeficiency using Galaxy

This repository contains organized output files from an educational-diagnostic reanalysis of public WES data **SRR4088561** performed in Galaxy. The analysis focused on genes associated with severe combined immunodeficiency (**SCID**) and on the **RAG1 c.2308G>A, p.E770K / p.Glu770Lys** variant.

## Main result

| Parameter | Result |
|---|---|
| Gene | RAG1 |
| Position | chr11:36575612 |
| REF/ALT | G>A |
| cDNA | c.2308G>A |
| Protein | p.E770K / p.Glu770Lys |
| Effect | missense_variant |
| Genotype | 1/1 |
| DP / AD | DP=2; AD=0,2 |
| Transcript | NM_000448.3 / ENST00000299440.6 |
| rsID | rs768260595 |
| SIFT | deleterious_low_confidence(0.01) |
| PolyPhen | probably_damaging(0.991) |

**Interpretation note:** the local coverage of the RAG1 p.E770K position is very low. This result should be treated as an educational reproduction of a reported/targeted variant and **not** as a clinically validated diagnostic finding.

## Repository structure

```text
docs/                 final report and data availability notes
metadata/             Zenodo metadata, file manifest and citation information
workflow/             Galaxy workflow summary
qc/                   quality-control reports
annotation/           SnpEff and VEP annotation summaries
results/tables/       result tables
results/depth/        local coverage/depth files for the RAG1 variant position
supplementary/        additional supporting tables
```

## Key files

- `docs/final_report_EN.md` — final English report.
- `results/tables/13_RAG1_p.E770K_final_VEP_annotated.tsv` — final RAG1 variant table with VEP annotation.
- `results/depth/14_DEPTH_RAG1_p.E770K_single_position.txt` — local depth at the RAG1 variant position.
- `results/tables/12_PANEL_SCID_HIGH_MODERATE_DP10_nonREF.tsv` — SCID-panel variants after quality filtering.
- `results/tables/12_PANEL_SCID_gene_counts.tsv` — counts of variant entries per gene after filtering.
- `annotation/15_VEP_summary.txt` — VEP run summary.
- `qc/alignment/07_ALIGN_final_sorted_dedup_flagstat.txt` — alignment summary statistics.

## Input data

Raw input data are not stored in this repository. They should be downloaded directly from NCBI SRA:

```text
SRR4088561
```

## Limitations

- Low local coverage of the RAG1 p.E770K position: DP=2.
- No parental data.
- No Sanger/MLPA or other laboratory validation.
- CNV analysis was not performed.
- This is an educational/portfolio-oriented analysis, not a clinical diagnostic report.

## License

Recommended license for reports, tables and metadata: **CC BY 4.0**.
