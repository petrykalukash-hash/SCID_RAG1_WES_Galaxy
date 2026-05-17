# Opis workflow Galaxy

## Dane wejściowe

- Publiczne dane WES: SRR4088561
- Typ danych: paired-end WES
- Genom referencyjny: GRCh38/hg38

## Etapy analizy

1. Import FASTQ z SRA.
2. Kontrola jakości surowych odczytów: FastQC/Falco + MultiQC.
3. Trimming: Cutadapt 5.2.
   - Adapter R1: AGATCGGAAGAGCACACGTCTGAACTCCAGTCA
   - Adapter R2: AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGT
   - Quality cutoff: Q20
   - Minimalna długość: 20 bp
   - Trim N: yes
4. Mapowanie: BWA-MEM2 do hg38.
5. Sortowanie BAM: SortSam, coordinate sort.
6. Oznaczanie duplikatów: MarkDuplicates.
7. QC BAM: Samtools flagstat / QualiMap BamQC.
8. Variant calling: FreeBayes.
9. Adnotacja: SnpEff hg38.
10. Ekstrakcja pól: SnpSift Extract Fields.
11. Filtrowanie panelu SCID.
12. Dodatkowa adnotacja: VEP 115.2, cache Homo sapiens hg38 V106.
13. Walidacja bioinformatyczna pozycji RAG1 p.E770K: Samtools depth.

## Panel genów SCID

RAG1, RAG2, IL2RG, ADA, JAK3, IL7R, DCLRE1C, LIG4, NHEJ1, AK2, PNP, CD3D, CD3E, CD3G, ZAP70, CORO1A, FOXN1, MALT1, CARD11.

## Filtr jakościowy panelu SCID

```python
HIGH/MODERATE impact
DP >= 10
GT != "0/0"
```

Wariant RAG1 p.E770K został omówiony osobno, ponieważ jest wariantem docelowym, ale ma niskie pokrycie DP=2.
