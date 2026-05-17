# Raport końcowy

## Reanaliza publicznych danych WES SRR4088561 w kierunku wariantu RAG1 związanego z ciężkim złożonym niedoborem odporności

### 1. Cel analizy

Celem analizy była bioinformatyczna reanaliza publicznych danych WES oznaczonych jako **SRR4088561**, wykonana w środowisku Galaxy, z ukierunkowaniem na warianty w genach związanych z ciężkim złożonym niedoborem odporności (**SCID, severe combined immunodeficiency**). Szczególną uwagę poświęcono genowi **RAG1** oraz wariantowi **c.2308G>A, p.E770K / p.Glu770Lys**.

Analiza miała charakter edukacyjno-diagnostyczny i została wykonana jako modelowy workflow WES obejmujący kontrolę jakości, trimming, mapowanie do genomu referencyjnego, przygotowanie pliku BAM, wariantowanie, adnotację funkcjonalną oraz filtrowanie wariantów w panelu genów SCID.

### 2. Materiał

Materiałem wejściowym były sparowane odczyty WES pobrane z publicznego zbioru danych **SRR4088561**. Dane zostały analizowane jako odczyty paired-end. Po imporcie do Galaxy wykonano kontrolę jakości, oczyszczanie odczytów, mapowanie do genomu referencyjnego **GRCh38/hg38**, a następnie analizę wariantów germinalnych typu SNV/indel.

### 3. Metody

Surowe odczyty oceniono za pomocą narzędzi FastQC/Falco oraz MultiQC. Następnie wykonano trimming adapterów i końców niskiej jakości przy użyciu **Cutadapt 5.2**. Zastosowano adaptery Illumina dla odczytów paired-end, próg jakości Q20, usuwanie nukleotydów N oraz minimalną długość odczytu 20 bp. Cutadapt przetworzył **47 950 176 par odczytów**; po filtracji zachowano **47 825 731 par**, czyli **99,7%** danych wejściowych. Adaptery wykryto w 1,6% odczytów R1 i 2,9% odczytów R2.

Oczyszczone odczyty zmapowano do genomu referencyjnego **GRCh38/hg38** przy użyciu **BWA-MEM2**. Następnie plik BAM posortowano po współrzędnych genomowych oraz oznaczono duplikaty przy użyciu MarkDuplicates. W końcowym BAM uzyskano **95 863 850 odczytów łącznie**, z czego **94 519 298 odczytów było zmapowanych**, co odpowiada **98,60%**. Odsetek prawidłowo sparowanych odczytów wyniósł **98,24%**.

Warianty SNV/indel wykryto przy użyciu **FreeBayes**. Uzyskany plik VCF adnotowano narzędziem **SnpEff**, a następnie przekształcono do tabeli za pomocą **SnpSift Extract Fields**. Dodatkową adnotację wykonano za pomocą **VEP 115.2** z cache **Homo sapiens hg38 V106**. VEP przetworzył **2 934 639 wariantów**, z czego **1 750 747** zostało oznaczonych jako warianty istniejące w bazach, a **1 183 892** jako potencjalnie nowe względem użytych zasobów.

### 4. Wyniki

#### 4.1. Wariant główny

| Parametr | Wynik |
|---|---|
| Gen | RAG1 |
| Chromosom / pozycja | chr11:36575612 |
| REF/ALT | G>A |
| cDNA | c.2308G>A |
| Białko | p.E770K / p.Glu770Lys |
| Efekt | missense_variant |
| Impact | MODERATE |
| Genotyp | 1/1 |
| DP | 2 |
| AD | 0,2 |
| Transkrypt Ensembl | ENST00000299440.6 |
| RefSeq / MANE Select | NM_000448.3 |
| rsID | rs768260595 |
| SIFT | deleterious_low_confidence(0.01) |
| PolyPhen | probably_damaging(0.991) |

Wariant **RAG1 c.2308G>A, p.E770K** został wykryty jako wariant homozygotyczny alternatywny (**GT=1/1**) i został opisany przez VEP na transkrypcie **MANE Select NM_000448.3 / ENST00000299440.6**. Predykcje in silico sugerują możliwy wpływ funkcjonalny wariantu: **SIFT: deleterious_low_confidence(0.01)** oraz **PolyPhen: probably_damaging(0.991)**.

#### 4.2. Pokrycie pozycji wariantu

Najważniejszym ograniczeniem wyniku jest bardzo niskie lokalne pokrycie pozycji wariantu. W tabeli wariantu FreeBayes/SnpEff/VEP uzyskano:

```text
DP = 2
AD = 0,2
```

Dodatkowa analiza Samtools depth dla pozycji `chr11:36575612` potwierdziła niskie pokrycie. W praktyce oznacza to, że wariant został odtworzony bioinformatycznie, ale jego pewność techniczna w tej analizie jest ograniczona przez niską liczbę odczytów wspierających.

#### 4.3. Analiza panelu SCID

Po zawężeniu analizy do panelu genów SCID oraz zastosowaniu filtru jakościowego **HIGH/MODERATE impact, DP ≥ 10, GT != 0/0** uzyskano warianty w kilku genach panelu. Zestawienie to należy traktować jako wynik pomocniczy, ponieważ część wpisów może reprezentować różne transkrypty tego samego wariantu, a nie niezależne warianty kliniczne.

Wariant publikacyjny **RAG1 p.E770K** nie spełnia filtru jakościowego DP≥10, ponieważ jego pokrycie wynosiło DP=2. Z tego powodu został on przedstawiony oddzielnie jako wariant zgodny z oczekiwanym wynikiem biologicznym, ale wymagający ostrożnej interpretacji jakościowej.

### 5. Interpretacja

Wariant **RAG1 c.2308G>A, p.E770K / p.Glu770Lys** jest zgodny z założonym celem analizy i został wykryty w danych WES SRR4088561. Gen **RAG1** jest związany z rekombinacją V(D)J, kluczową dla prawidłowego rozwoju limfocytów T i B. Zaburzenia funkcji RAG1/RAG2 mogą prowadzić do fenotypu ciężkiego złożonego niedoboru odporności, szczególnie postaci **T−B−NK+ SCID**.

W analizowanych danych wariant został oznaczony jako **homozygotyczny alternatywny**, co jest zgodne z autosomalnie recesywnym modelem dziedziczenia chorób związanych z RAG1. Dodatkowo wariant ma charakter missense i został oceniony przez predykcje in silico jako potencjalnie uszkadzający.

Jednocześnie najważniejszym ograniczeniem jest bardzo niskie pokrycie pozycji wariantu (**DP=2; AD=0,2**). W standardowej interpretacji diagnostycznej taki poziom pokrycia nie jest wystarczający do samodzielnego potwierdzenia wariantu. Wynik należy więc traktować jako **odtworzenie wariantu publikacyjnego / edukacyjny wynik pipeline’u WES**, a nie jako pełnoprawny, zwalidowany wynik diagnostyczny.

### 6. Wniosek końcowy

W przeprowadzonej analizie WES SRR4088561 w środowisku Galaxy odtworzono wariant **RAG1 c.2308G>A, p.E770K / p.Glu770Lys**, zgodny z celem projektu i biologicznie spójny z fenotypem SCID zależnym od RAG1. Wariant został wykryty jako **homozygotyczny wariant missense** w genie **RAG1**, z adnotacją na transkrypcie **MANE Select NM_000448.3** oraz z predykcjami in silico sugerującymi potencjalny wpływ na funkcję białka.

Ze względu na bardzo niskie lokalne pokrycie pozycji (**DP=2**) wynik wymaga ostrożnej interpretacji. W kontekście portfolio diagnostycznego analiza pokazuje poprawnie zbudowany workflow WES: od kontroli jakości odczytów, przez mapowanie i wariantowanie, po adnotację SnpEff/VEP oraz filtrowanie panelowe. Nie powinna być jednak przedstawiana jako klinicznie zwalidowany raport diagnostyczny.

### 7. Ograniczenia

- Niskie pokrycie wariantu RAG1 p.E770K — DP=2.
- Brak danych rodzicielskich.
- Brak walidacji laboratoryjnej metodą Sanger, MLPA lub inną metodą diagnostyczną.
- Brak pełnych danych klinicznych pacjenta.
- Analiza CNV nie została wykonana.
- Warianty z panelu SCID po filtrze DP≥10 wymagają dalszej, ręcznej interpretacji.

### 8. Pliki wynikowe

Najważniejsze pliki do repozytorium:

- `results/tables/13_RAG1_p.E770K_final_VEP_annotated.tsv`
- `results/tables/12_PANEL_SCID_HIGH_MODERATE_DP10_nonREF.tsv`
- `results/tables/12_PANEL_SCID_gene_counts.tsv`
- `results/depth/14_DEPTH_RAG1_p.E770K_single_position.txt`
- `results/depth/14_DEPTH_RAG1_p.E770K_region_chr11_36575550_36575680.txt`
- `annotation/15_VEP_summary.txt`
- `qc/trimmed/03_TRIM_Cutadapt_report.txt`
- `qc/alignment/07_ALIGN_final_sorted_dedup_flagstat.txt`
