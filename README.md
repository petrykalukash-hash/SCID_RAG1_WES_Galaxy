# Reanaliza publicznych danych WES SRR4088561 w kierunku wariantu RAG1 związanego z SCID

Repozytorium zawiera uporządkowane pliki wynikowe z edukacyjno-diagnostycznej reanalizy danych WES **SRR4088561** wykonanej w Galaxy. Analiza była ukierunkowana na geny związane z ciężkim złożonym niedoborem odporności (**SCID**) oraz na wariant **RAG1 c.2308G>A, p.E770K / p.Glu770Lys**.

## Najważniejszy wynik

W danych wykryto wariant:

| Parametr | Wynik |
|---|---|
| Gen | RAG1 |
| Pozycja | chr11:36575612 |
| REF/ALT | G>A |
| cDNA | c.2308G>A |
| Białko | p.E770K / p.Glu770Lys |
| Efekt | missense_variant |
| Genotyp | 1/1 |
| DP / AD | DP=2; AD=0,2 |
| Transkrypt | NM_000448.3 / ENST00000299440.6 |
| rsID | rs768260595 |
| SIFT | deleterious_low_confidence(0.01) |
| PolyPhen | probably_damaging(0.991) |

**Uwaga interpretacyjna:** wariant jest zgodny z celem analizy, ale lokalne pokrycie pozycji jest bardzo niskie, dlatego wynik należy traktować jako edukacyjne odtworzenie wariantu publikacyjnego, a nie klinicznie zwalidowany wynik diagnostyczny.

## Struktura repozytorium

```text
docs/                 raport końcowy i opis metod
metadata/             metadane Zenodo, manifest plików, cytowanie
workflow/             opis workflow Galaxy
qc/                   raporty kontroli jakości
annotation/           raporty adnotacji SnpEff i VEP
results/tables/       tabele wynikowe
results/depth/        pokrycie pozycji wariantu RAG1
supplementary/        dodatkowe tabele pomocnicze
```

## Główne pliki wynikowe

- `docs/final_report_PL.md` — raport końcowy.
- `results/tables/13_RAG1_p.E770K_final_VEP_annotated.tsv` — końcowa tabela wariantu RAG1 z adnotacją VEP.
- `results/depth/14_DEPTH_RAG1_p.E770K_single_position.txt` — lokalne pokrycie pozycji wariantu.
- `results/tables/12_PANEL_SCID_HIGH_MODERATE_DP10_nonREF.tsv` — warianty panelu SCID po filtrze jakościowym.
- `results/tables/12_PANEL_SCID_gene_counts.tsv` — liczba wpisów wariantowych na gen po filtracji.
- `annotation/15_VEP_summary.txt` — podsumowanie działania VEP.
- `qc/alignment/07_ALIGN_final_sorted_dedup_flagstat.txt` — podstawowe statystyki mapowania BAM.

## Dane wejściowe

Dane wejściowe nie są przechowywane w repozytorium GitHub. Należy je pobrać z NCBI SRA:

```text
SRR4088561
```

## Ograniczenia

- Niskie pokrycie wariantu RAG1 p.E770K: DP=2.
- Brak danych rodzicielskich.
- Brak walidacji Sanger/MLPA.
- Analiza CNV nie została wykonana.
- Raport ma charakter edukacyjno-diagnostyczny, nie kliniczny.

## Licencja

Zalecana licencja dla raportu, tabel i metadanych: **CC BY 4.0**.  
Workflow i drobne skrypty/opisy można traktować jako materiały otwarte zgodnie z opisem w pliku `LICENSE`.
