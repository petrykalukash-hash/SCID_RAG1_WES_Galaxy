# Final report

## Reanalysis of public WES data SRR4088561 for RAG1-associated severe combined immunodeficiency using Galaxy

### 1. Aim

The aim of this analysis was to perform an educational-diagnostic bioinformatic reanalysis of public WES data **SRR4088561** in Galaxy, focusing on genes associated with severe combined immunodeficiency (**SCID**) and, in particular, on the **RAG1 c.2308G>A, p.E770K / p.Glu770Lys** variant.

The analysis was designed as a model WES workflow including read quality control, adapter trimming, reference alignment, BAM preparation, variant calling, functional annotation and targeted filtering of a SCID gene panel.

### 2. Material

The input material consisted of paired-end WES reads from the public dataset **SRR4088561**. The reads were processed in Galaxy and aligned to the **GRCh38/hg38** reference genome. Germline SNV/indel variant analysis was then performed.

### 3. Methods

Raw reads were assessed using FastQC/Falco and MultiQC. Adapter and low-quality ends were trimmed using **Cutadapt 5.2** with paired-end Illumina adapters, Q20 quality trimming, trimming of ambiguous `N` bases and a minimum read length of 20 bp. Cutadapt processed **47,950,176 read pairs** and retained **47,825,731 read pairs**, corresponding to **99.7%** of the input pairs. Adapter sequence was detected in 1.6% of R1 reads and 2.9% of R2 reads.

Trimmed reads were aligned to **GRCh38/hg38** using **BWA-MEM2**. The BAM file was coordinate-sorted and duplicates were marked with MarkDuplicates. BAM quality control showed **95,863,850 total reads**, of which **94,519,298 were mapped**, corresponding to **98.60%**. Properly paired reads accounted for **98.24%**.

SNV/indel variants were called using **FreeBayes**. The resulting VCF was annotated with **SnpEff** and converted to a tabular format with **SnpSift Extract Fields**. Additional annotation was performed with **VEP 115.2** using the **Homo sapiens hg38 V106** cache. VEP processed **2,934,639 variants**, including **1,750,747 known variants** and **1,183,892 variants not matched to known entries in the used resources**.

### 4. Results

#### 4.1. Main RAG1 variant

| Parameter | Result |
|---|---|
| Gene | RAG1 |
| Chromosome / position | chr11:36575612 |
| REF/ALT | G>A |
| cDNA | c.2308G>A |
| Protein | p.E770K / p.Glu770Lys |
| Effect | missense_variant |
| Impact | MODERATE |
| Genotype | 1/1 |
| DP | 2 |
| AD | 0,2 |
| Ensembl transcript | ENST00000299440.6 |
| RefSeq / MANE Select | NM_000448.3 |
| rsID | rs768260595 |
| SIFT | deleterious_low_confidence(0.01) |
| PolyPhen | probably_damaging(0.991) |

The **RAG1 c.2308G>A, p.E770K** variant was detected as a homozygous alternate variant (**GT=1/1**) and was annotated by VEP on the **MANE Select transcript NM_000448.3 / ENST00000299440.6**. In silico predictions suggest a possible functional impact: **SIFT: deleterious_low_confidence(0.01)** and **PolyPhen: probably_damaging(0.991)**.

#### 4.2. Local coverage

The main technical limitation of the finding is the very low local coverage of the variant position. In the FreeBayes/SnpEff/VEP-derived table, the variant had:

```text
DP = 2
AD = 0,2
```

Additional Samtools depth checks were performed for `chr11:36575612` and for the surrounding region `chr11:36575550-36575680`. These checks confirmed that the local coverage around the target variant was low. Therefore, although the variant was reproduced bioinformatically, its technical confidence is limited by the low number of supporting reads.

#### 4.3. SCID gene-panel analysis

The analysis was also restricted to a SCID-associated gene panel. After applying a quality-oriented filter:

```text
HIGH/MODERATE impact
DP ≥ 10
GT != 0/0
```

variant entries were retained in several SCID-panel genes. This table should be interpreted as a supporting result, because some entries may correspond to multiple transcript annotations of the same variant rather than independent clinical variants.

The target **RAG1 p.E770K** variant does not pass the DP≥10 filter because its local coverage is DP=2. It is therefore reported separately as a biologically expected/targeted variant with limited technical support in this run.

### 5. Interpretation

The **RAG1 c.2308G>A, p.E770K / p.Glu770Lys** variant is consistent with the aim of the analysis and was detected in WES data SRR4088561. **RAG1** is involved in V(D)J recombination, which is essential for normal T- and B-cell development. Loss or impairment of RAG1/RAG2 function can cause severe combined immunodeficiency, including T−B−NK+ SCID phenotypes.

In this analysis, the variant was called as **homozygous alternate**, which is consistent with an autosomal recessive disease model for RAG1-related disease. The variant is a missense change and was predicted by in silico tools to be potentially damaging.

However, the most important limitation is the very low local coverage (**DP=2; AD=0,2**). In a standard diagnostic setting, this level of coverage would not be sufficient to confirm the variant independently. The result should therefore be interpreted as an **educational reproduction of a reported/targeted variant**, not as a clinically validated diagnostic call.

### 6. Conclusion

The Galaxy-based WES reanalysis of SRR4088561 reproduced the **RAG1 c.2308G>A, p.E770K / p.Glu770Lys** variant, which is biologically consistent with RAG1-associated SCID. The variant was detected as a homozygous missense variant and annotated on the **MANE Select NM_000448.3** transcript, with in silico predictions suggesting a possible functional effect.

Due to very low local coverage (**DP=2**), the result requires cautious interpretation. As a portfolio project, this analysis demonstrates a complete WES workflow from read QC to variant calling, annotation and targeted gene-panel filtering. It should not be presented as a clinically validated diagnostic report.

### 7. Limitations

- Low local coverage of the RAG1 p.E770K variant: DP=2.
- No parental data were available.
- No Sanger, MLPA or other laboratory validation was performed.
- No full clinical dataset was available.
- CNV analysis was not performed.
- SCID-panel variants passing DP≥10 require further manual interpretation.

### 8. Key output files

- `results/tables/13_RAG1_p.E770K_final_VEP_annotated.tsv`
- `results/tables/12_PANEL_SCID_HIGH_MODERATE_DP10_nonREF.tsv`
- `results/tables/12_PANEL_SCID_gene_counts.tsv`
- `results/depth/14_DEPTH_RAG1_p.E770K_single_position.txt`
- `results/depth/14_DEPTH_RAG1_p.E770K_region_chr11_36575550_36575680.txt`
- `annotation/15_VEP_summary.txt`
- `qc/trimmed/03_TRIM_Cutadapt_report.txt`
- `qc/alignment/07_ALIGN_final_sorted_dedup_flagstat.txt`
