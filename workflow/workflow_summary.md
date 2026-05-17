# Galaxy workflow summary

## Input data

- Public WES run: SRR4088561
- Data type: paired-end WES
- Reference genome: GRCh38/hg38

## Analysis steps

1. Import FASTQ data from SRA.
2. Raw-read quality control: FastQC/Falco + MultiQC.
3. Adapter and quality trimming: Cutadapt 5.2.
   - R1 adapter: AGATCGGAAGAGCACACGTCTGAACTCCAGTCA
   - R2 adapter: AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGT
   - Quality cutoff: Q20
   - Minimum length: 20 bp
   - Trim N: enabled
4. Alignment: BWA-MEM2 against hg38.
5. BAM sorting: SortSam, coordinate sort.
6. Duplicate marking: MarkDuplicates.
7. BAM quality control: Samtools flagstat and QualiMap BamQC.
8. Variant calling: FreeBayes.
9. Variant annotation: SnpEff hg38.
10. Field extraction: SnpSift Extract Fields.
11. SCID gene-panel filtering.
12. Additional annotation: VEP 115.2 using Homo sapiens hg38 V106 cache.
13. Local coverage check for the RAG1 p.E770K position: Samtools depth.

## SCID gene panel

RAG1, RAG2, IL2RG, ADA, JAK3, IL7R, DCLRE1C, LIG4, NHEJ1, AK2, PNP, CD3D, CD3E, CD3G, ZAP70, CORO1A, FOXN1, MALT1, CARD11.

## SCID-panel quality filter

```python
HIGH/MODERATE impact
DP >= 10
GT != "0/0"
```

The RAG1 p.E770K variant was reported separately because it is the target variant, but its local coverage is low (DP=2).
