# Data availability

## Public input data

Input data are publicly available in NCBI SRA:

```text
SRR4088561
```

Raw FASTQ files are not included in this repository. They should be downloaded directly from SRA and processed according to the workflow described in `workflow/workflow_summary.md`.

## Processed data

This repository contains selected processed outputs generated in Galaxy:

- quality-control reports,
- alignment summary statistics,
- SnpEff/VEP annotation summaries,
- SCID-panel filtered tables,
- final RAG1 p.E770K annotation table,
- local depth files for chr11:36575612.

## Large files

Large intermediate files, including raw FASTQ, BAM, BAI and full VCF files, are not recommended for GitHub. If needed, they should be deposited in Zenodo or generated reproducibly from SRR4088561.

The Zenodo package may include an additional full SnpSift-extracted variant table as supplementary material.
