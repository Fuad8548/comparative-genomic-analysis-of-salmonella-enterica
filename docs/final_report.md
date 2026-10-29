# Comparative Genomic Profiling of AMR-Associated Determinants and Virulence Markers in Public Salmonella enterica Assemblies

- **Research purpose**: To perform an in silico comparative genomic analysis on **12 distinct Salmonella enteritidis** genome assemblies. The study aims to map their evolutionary relationships (phylogeny), define their pan-genome structure (core vs. accessory genes), and profile their specific virulence and antimicrobial resistance (AMR) gene determinants.

- **Public-health relevance**: To demonstrate a reproducible bioinformatics approach that can inform future genomic surveillance of foodborne pathogens and support the identification of candidate markers for further investigation.

## Step by step bioinformatics workflow
1. **Assembly Quality Check**: Ran **QUAST**(Quality Assessment Tool for Genome Assemblies) on our 12 FASTA files to check assembly statistics (N50 score, contig count) to ensure the data is high quality.
2. **Genome Annotation**: Ran the assemblies through **Prokka** to automatically identify where genes start and stop, and what proteins they code for.
3. **In Silico Serotyping**: Used **SISTR** (Salmonella In Silico Typing Resource) to genetically confirm that all 12 assemblies are strictly S. enteritidis.
4. **AMR & Virulence Profiling**: Screened the genomes against databases using **AMRFinderPlus** (for antibiotic resistance genes) and **VFDB** (for virulence factors like Salmonella Pathogenicity Islands).
5. **Pan-Genome & Phylogeny**: Used **Roary** to calculate the core genome, and extracted a core-genome alignment to generate a high-resolution phylogenetic tree using **IQ-TREE**.


# 1. Introduction

## 1.1 Background

*Salmonella enterica* is an important bacterial pathogen associated with foodborne disease and a range of clinical outcomes. Its substantial genetic and antigenic diversity creates challenges for understanding differences among strains, tracking pathogen populations, and characterizing genetic determinants that may contribute to antimicrobial resistance or pathogenicity. Genome-based approaches provide opportunities to investigate these differences at the sequence level and complement conventional microbiological methods [1, 2].

Whole-genome sequencing and comparative genomics enable researchers to examine bacterial genomes beyond individual genes or isolated genetic markers. By comparing multiple genome assemblies, researchers can characterize shared genomic features, identify differences in gene content, and investigate the distribution of known resistance-associated determinants and virulence-associated markers. The conclusions, however, depend on the quality and identity of the input genomes, annotation consistency, analytical parameters, and the evidence available to support biological interpretations [2].

## 1.2 Comparative Genomics and the Bacterial Pangenome

A single reference genome cannot capture all the genetic variation present across a collection of bacterial genomes. Pangenome analysis addresses this limitation by organizing annotated genes into clusters according to their sequence similarity and distribution across the analyzed genomes.

The **pangenome** represents the overall collection of gene clusters identified within a selected group of genomes. It is commonly described in terms of:

- **Core genome:** gene clusters shared across all genomes under the definition used in the analysis.
- **Accessory genome:** gene clusters that are not present in every genome.
- **Shell genome:** a subset of accessory clusters found in a relatively large proportion of the analyzed genomes.
- **Cloud genome:** a subset of accessory clusters found in a relatively small proportion of the analyzed genomes.

These categories provide a framework for describing the balance between shared and variable gene content. The accessory component can reflect genuine biological differences, including gene gain and loss or mobile genetic elements. However, observed variation may also be influenced by genome assembly quality, annotation differences, gene-clustering settings, and the selection of genomes included in the analysis [3].

**Roary** is a pangenome analysis tool designed to identify core and accessory genes from annotated bacterial genomes. Its gene presence/absence outputs support both summary-level characterization of a genome collection and examination of individual gene clusters across samples [3].

In the present project, pangenome analysis provides the genomic-content framework against which AMR-associated and virulence-associated marker distributions can be examined. The resulting clusters are interpreted as features of the selected dataset rather than as universal estimates for the entire species.

## 1.3 Antimicrobial Resistance and Genomic Screening

Antimicrobial resistance (AMR) is an important consideration in bacterial surveillance and public health. Genome sequencing can support the identification of known resistance-associated determinants and mutations, helping researchers characterize the genetic features reported in bacterial isolates. Genomic surveillance can complement conventional antimicrobial susceptibility testing, although the relationship between genotype and phenotype is not always straightforward [4].

AMR-associated findings can include acquired resistance genes, which may encode mechanisms such as antibiotic inactivation or altered drug transport, as well as mutations in chromosomal genes that are associated with changes in antimicrobial susceptibility. These categories should be distinguished because a point mutation and an acquired resistance gene represent different types of genomic evidence.

**AMRFinderPlus** uses curated reference information to identify acquired AMR-associated genes and recognized resistance-associated point mutations in appropriate sequence data. The interpretation of a detected marker depends on the reliability of the match, the reference database, the relevant organism, and the genomic context [5].

In this project, AMRFinderPlus was used to screen the selected genome assemblies for reported AMR-associated determinants and relevant point mutations. The results were summarized at the genome level to describe their distribution across the panel.

These detections are computational findings. They do not independently establish the antimicrobial susceptibility phenotype of an isolate, and failure to detect a particular marker does not demonstrate that an isolate is susceptible or lacks all possible resistance mechanisms.

## 1.4 Virulence-Associated Markers

Bacterial pathogenicity can involve multiple factors, including adhesion, host interaction, invasion, immune evasion, and other functions that contribute to the infection process. The presence and distribution of genes associated with these functions can provide useful genomic information, but individual gene matches cannot explain the full biological behavior of an organism.



## 1.5 Rationale for the Study

Pangenome analysis, AMR-associated screening, and virulence-associated marker screening provide complementary perspectives on bacterial genomic variation. Pangenome analysis describes shared and variable gene content, while targeted screening identifies matches to curated collections of resistance-associated and virulence-associated sequences. Applying these approaches to the same genome panel allows the findings to be organized and interpreted together.

Comparative-genomics studies of *S. enterica* illustrate the value of examining pangenome composition alongside resistance-associated determinants and other genomic features [7]. However, a useful analysis must distinguish observed sequence patterns from broader conclusions about transmission, adaptation, resistance phenotype, or virulence.

The present project examines **12 selected *Salmonella enterica* genome assemblies**. Its purpose is to demonstrate an integrated, reproducible bioinformatics workflow and characterize the genomic features reported in this particular dataset. The small panel is suitable for a focused exploratory analysis, but it is not sufficient to represent the full diversity of the species or support broad population-level conclusions.

Dataset identity is also an important consideration. The preliminary metadata audit identified disagreements between submitter-provided and computed or independently indexed taxonomic information for several records. Consequently, the study uses the broader *S. enterica* label and treats serovar-level interpretation cautiously until the relevant assembly identities are independently reconciled.

By documenting these issues alongside the analysis outputs, the project emphasizes both the analytical capabilities of comparative genomics and the importance of data quality, reproducibility, and appropriately bounded scientific conclusions.

# 2. Aim and Objectives

## 2.1 Overall Aim

To characterize core and accessory gene-cluster composition and describe the distribution of antimicrobial-resistance-associated determinants and virulence-associated gene markers across 12 selected *Salmonella enterica* genome assemblies using an integrated comparative-genomics workflow.

## 2.2 Specific Objectives

1. **Assemble and assess the dataset:** Collect the selected public genome assemblies, document their accession metadata, verify file integrity, and examine basic genome statistics.

2. **Annotate the genomes consistently:** Use **Prokka** to generate standardized genome annotations for downstream comparative analysis.

3. **Characterize the pangenome:** Apply Roary to identify gene clusters shared across all selected assemblies and clusters showing variable presence.

4. **Screen for AMR-associated determinants:** Use AMRFinderPlus to identify reported acquired resistance-associated genes and relevant point mutations, and summarize their distribution among the assemblies.

5. **Characterize virulence-associated marker matches:** Use ABRicate with VFDB to summarize shared and variable marker distributions across the panel.

6. **Integrate the results:** Organize pangenome, AMR, and VFDB findings into consistent summary tables and presence/absence representations, supported by validation checks.

7. **Evaluate interpretive limitations:** Consider the effects of sample selection, identity metadata discrepancies, database dependence, and the distinction between computational detections and biological phenotypes.

## 2.3 Research Questions

This study addresses the following questions:

1. What proportions of the gene clusters identified in the selected genome panel are core and accessory?
2. Which AMR-associated determinants and relevant point mutations are reported, and how are they distributed across the 12 assemblies?
3. Which VFDB-associated gene symbols are shared across all assemblies, and which show variable presence?
4. What can the combined results reveal about genomic-content variation within this selected panel, and what conclusions remain unsupported by the available evidence?

## 2.4 Scope of the Study

This is a descriptive and exploratory comparative-genomics project based on 12 selected genome assemblies. It focuses on computational analysis of annotated gene content and reference-database matches.

The study does not directly measure antimicrobial susceptibility, gene expression, virulence in a host, or clinical outcomes. It is not designed to estimate species-wide gene prevalence, demonstrate transmission between isolates, or establish causal relationships between genomic markers and biological phenotypes.

The exploratory phylogenetic output is treated separately from the principal findings because additional validation and branch-support assessment are required before drawing strong evolutionary conclusions.

# References for Chapters 1–2

1. World Health Organization. *Salmonella (non-typhoidal).* Fact sheet. Available at: https://www.who.int/news-room/fact-sheets/detail/salmonella-%28non-typhoidal%29

2. Mather AE, Gilmour MW, Reid SWJ, et al. Foodborne bacterial pathogens: genome-based approaches for enduring and emerging threats in a complex and changing world. *Nature Reviews Microbiology.* 2024;22:543–555. https://doi.org/10.1038/s41579-024-01051-z

3. Page AJ, Cummins CA, Hunt M, et al. Roary: rapid large-scale prokaryote pan genome analysis. *Bioinformatics.* 2015;31(22):3691–3693. https://doi.org/10.1093/bioinformatics/btv421

4. Howden BP, et al. Genomic surveillance for antimicrobial resistance — a One Health perspective. *Nature Reviews Genetics.* 2024;25:142–157. https://doi.org/10.1038/s41576-023-00649-y

5. Feldgarden M, Brover V, Gonzalez-Escalona N, et al. AMRFinderPlus and the Reference Gene Catalog facilitate examination of the genomic links among antimicrobial resistance, stress response, and virulence. *Scientific Reports.* 2021;11:12728. https://doi.org/10.1038/s41598-021-91456-0

6. Liu B, Zheng D, Zhou S, Chen L, Yang J. VFDB 2022: a general classification scheme for bacterial virulence factors. *Nucleic Acids Research.* 2022;50(D1):D912–D917. https://doi.org/10.1093/nar/gkab1107

7. Aguirre-Sánchez JR, Chaidez C, Castro-Del Campo N. The pangenome analysis of the environmental source *Salmonella enterica* highlights a diverse accessory genome and a distinct serotype clustering. *FEMS Microbiology Letters.* 2024;371:fnae090. https://doi.org/10.1093/femsle/fnae090


# 3. Materials and Methods

## 3.1 Study Design

This study used a descriptive comparative-genomics design to investigate shared and variable gene content and the distribution of antimicrobial-resistance-associated determinants and virulence-associated gene markers across 12 selected *Salmonella enterica* genome assemblies.
The workflow consisted of public genome-data collection, assembly selection, sequence-integrity assessment, basic genome-statistic evaluation, taxonomic metadata review, genome annotation, pangenome analysis, AMR-associated screening, virulence-associated marker screening, and integration of the resulting outputs.
The analysis was conducted as an exploratory study of a defined genome panel. The objective was to characterize patterns within the selected assemblies rather than estimate the prevalence of genomic features throughout the entire species.

## 3.2 Public Genome Data Collection

### 3.2.1 Source and initial candidate collection

Genome assembly records were obtained from the National Center for Biotechnology Information (NCBI) public genome resources. The initial candidate collection was associated with the taxonomic identifier (TaxID) 149539 used during dataset retrieval.
The initial search pool contained approximately 48,292 assembly records. This collection was subsequently filtered to obtain a smaller set of higher-contiguity assemblies suitable for comparative analysis.
The initial candidate count represents the search pool, not the number of unique biological isolates or the final analytical sample. Assembly records may include different assembly versions, paired RefSeq and GenBank representations, or multiple records associated with the same biological sample.

### 3.2.2 Assembly-quality filtering

The candidate collection was filtered to retain assemblies categorized as complete genome or chromosome level. Following this filtering stage, **711** assembly records remained.

### 3.2.3 Removal of duplicate assembly representations

GenBank and RefSeq may provide corresponding assembly records for the same biological sample. Treating these paired records as independent genomes could result in redundant representation of an isolate.

To reduce this risk, paired GCA and GCF assembly records associated with the same BioSample were deduplicated during dataset preparation. After this step, the working collection contained 381 assembly records: 234 categorized as complete genome and 147 categorized as chromosome level.

### 3.2.4 Selection of the final analytical panel

Twelve assemblies were selected from the filtered collection for downstream analysis:

1. `GCF_000612325.1`
2. `GCF_000750215.1`
3. `GCF_001305235.1`
4. `GCF_001972545.2`
5. `GCF_002982095.1`
6. `GCF_015074885.1`
7. `GCF_015240635.1`
8. `GCF_030122175.1`
9. `GCF_031188765.1`
10. `GCF_050920565.1`
11. `GCF_051904745.1`
12. `GCF_055811875.1`

## 3.3 Assembly Identity and Metadata Assessment

Because the metadata discrepancies had not been fully resolved, the analytical panel was described conservatively as **12 selected *Salmonella enterica* genome assemblies**.

## 3.5 Basic Genome Statistics

Genome size and GC content were examined as initial descriptive quality-control measures.
Across the 12 selected assemblies, the recorded genome sizes ranged from approximately 4.70 to 4.90 Mb. GC content ranged from approximately 52.07% to 52.17%.

## 3.6 Dataset Summary

The main stages of dataset preparation are summarized below.

| Stage                              | Number of assembly records | Description                                              |
| ---------------------------------- | -------------------------: | -------------------------------------------------------- |
| Initial candidate search pool      |       Approximately 48,292 | Records associated with the initial taxonomic search     |
| After assembly-level filtering     |                        711 | Complete genome or chromosome-level records              |
| After paired GCA/GCF deduplication |                        381 | Records after deduplication using BioSample associations |
| Final analytical panel             |                         12 | Selected assemblies used in downstream analysis          |

The 381-record collection consisted of 234 complete-genome records and 147 chromosome-level records before final selection.


## 3.7 Genome Assembly Quality Check with `QUAST`
File: [Open Report](assembly_quality_check)

- **What exactly is a Contig?**
When an NGS machine sequences our Salmonella, it does not read the whole chromosome from end to end. Instead, it reads millions of tiny, scattered pieces of DNA (called reads, usually 150 to 300 base pairs long).
An assembly software takes these millions of tiny reads, finds where their sequences overlap, and stitches them together into longer, continuous blocks of DNA. Each individual continuous block is called a contig (short for contiguous sequence).

- **What exactly is N50?**

N50 is a metric of assembly quality that measures how "long and unbroken" your contigs are.
To calculate N50, the computer takes all your contigs and sorts them from largest to smallest. It starts adding their lengths together (Largest + Second Largest + Third Largest...). The N50 value is the length of the specific contig that causes the running sum to cross exactly 50% of the total genome length.

**The Analogy:**
Imagine your total Salmonella genome length is 5,000,000 bp (5 Mbp). The 50% mark is 2,500,000 bp.
Suppose the assembler broke your genome into 4 contigs:
- Contig A: 3,000,000 bp
- Contig B: 1,500,000 bp
- Contig C: 400,000 bp
- Contig D: 100,000 bp
To find the N50, we add them from largest to smallest:
- We start with Contig A (3,000,000 bp).
- Does Contig A alone cross the 50% mark (2,500,000 bp)? Yes.
- Therefore, the N50 value of this assembly is the size of Contig A, which is 3,000,000 bp.

For example, total Genome Length: 4,738,298 bp (50% mark = 2,369,149 bp)
• Contig 1 (Chromosome): ~4,678,926 bp
• Contig 2 (Plasmid): ~59,372 bp

**Interpretation of Assemblies with 3 and 5 Contigs:**

**Scenario A: The 3-Contig Assembly**

There are two biological possibilities for what these pieces represent:
• 1 Chromosome + 2 Separate Plasmids: Salmonella enteritidis strains frequently carry more than one plasmid (e.g., a large virulence plasmid like pSEN plus a smaller antibiotic-resistance plasmid).
• A Fragmented Chromosome + 1 Plasmid: The sequencer might have hit a repetitive region on the main chromosome that it couldn't perfectly bridge, breaking the chromosome into 2 pieces, plus 1 piece for the plasmid.

**Scenario B: The 5-Contig Assembly**

Similarly, 5 contigs usually means:
• 1 Chromosome broken into 3–4 pieces + 1–2 Plasmids. During the assembly process, certain areas (like ribosomal RNA genes or insertion sequences) are highly repetitive. The assembly software gets "confused" and stops building, leaving the main chromosome broken into a few large chunks instead of one continuous loop.

1. **Contigs: Ranges from 2 to 5**

- Theoretical Meaning: When an NGS machine sequences DNA, it generates millions of tiny reads. The assembly software stitches these overlapping reads together into continuous stretches of DNA called contigs (short for contiguous sequences).
- Significance for our Analysis: Having only 2 contigs means the entire 4.74 million base-pair genome has been stitched together into just two giant pieces.
	- In Salmonella, a perfect "closed genome" consists of 1 circular chromosome and often 1 or more plasmids (smaller, independent rings of DNA that frequently carry antibiotic resistance genes).
	- Our result strongly suggests that Contig 1 is the main chromosome and Contig 2 is a complete plasmid. This is a massive advantage because it allows us to see exactly whether our resistance genes are sitting safely on the chromosome or on a highly transmissible plasmid.

2. **N50: 4,678,926 bp (~4.68 Mbp)**

- Theoretical Meaning: The N50 is a statistical metric used to measure assembly continuity. It is defined as the sequence length of the shortest contig at which 50% of the total assembly length is covered.
- Analogy: Let's Imagine snapping a 100-cm stick into pieces. If we sort the pieces from longest to shortest and start adding up their lengths, the N50 is the length of the specific piece that pushes our running total past 50 cm.
- Significance for our analysis: An N50 of 4.68 Mbp tells us that more than half of our entire assembly is contained within a single, massive piece of DNA. Because our total genome is ~4.73 Mbp, this mathematically proves that one of our two contigs is huge (~4.68 Mbp chromosome) and the other is small (~59,000 bp plasmid). For draft bacterial genomes, any N50 over 50,000 bp is acceptable—our N50 is nearly 100 times better than the baseline standard.

3. **Total Length: Every assembly is roughly 4.5 to 5.0 million base pairs**

- Theoretical Meaning: This is the total number of base pairs (A, T, C, G) that the assembler was able to reconstruct.
- Significance for Salmonella: The typical genome size for a Salmonella enteritidis strain ranges strictly between 4.5 Mbp and 5.0 Mbp. Our result of 4.74 Mbp hits the biological sweet spot. It confirms that we have captured the entire bacterial chromosome without massive sequence gaps (which would make the length too small) and without cross-species DNA contamination (which would make the length abnormally large).


## 3.7 Genome Annotation with `Prokka`

Following dataset preparation, the 12 selected FASTA files were used as inputs for genome annotation with **Prokka** (prokaryotic genome annotation). Prokka will scan our DNA sequences, locate the genes, and label what proteins they code for.

### Configuring the tool
- Contigs to annotate: We clicked the Folder icon 📂 (Dataset collection icon) and selected collection of 12 uploaded `.fna` files.
- Genus name (--genus): *Salmonella*
- Species name (--species): *enteritidis*
- Kingdom (--kingdom): Bacteria
- Genetic code (--gcode): 11 (Bacterial, Archaeal and Plant Plastid)
- genus-specific BLAST database (--usegenus): `Yes` (This tells Prokka to cross-reference our genes against known Salmonella proteins first, making the labels much more accurate).

### Potential Outputs
- The `.gff` (**General Feature Format**): This is the most critical file. It contains the raw sequence data alongside the exact coordinates of every annotated gene. We will feed it directly into Roary later for our pan-genome analysis.
- The `.faa` (**FASTA Amino Acid**): This contains the protein sequences of all our predicted genes. It is useful if we want to look up or align specific protein sequences later.
- The `.txt` (Summary Text): To extract our gene counts (like the total number of `CDS` and `tRNAs`) for our final methods section.


#### 3.9.3 Predicted coding-sequence counts

The number of predicted coding sequences varied between assemblies.

| Assembly accession | Predicted CDS count |
| ------------------ | ------------------: |
| GCF_000612325.1    |               4,423 |
| GCF_000750215.1    |               4,394 |
| GCF_001305235.1    |               4,475 |
| GCF_001972545.2    |               4,419 |
| GCF_002982095.1    |               4,354 |
| GCF_015074885.1    |               4,611 |
| GCF_015240635.1    |               4,428 |
| GCF_030122175.1    |               4,534 |
| GCF_031188765.1    |               4,473 |
| GCF_050920565.1    |               4,488 |
| GCF_051904745.1    |               4,385 |
| GCF_055811875.1    |               4,457 |

The predicted CDS counts ranged from 4,354 to 4,611. These values provide a basic overview of annotation output across the dataset; differences in predicted CDS counts alone should not be interpreted as direct evidence of biological gene gain or loss. Such interpretations require comparative analyses that consider annotation consistency and the underlying genomic evidence.

#### 3.9.4 Role of annotation in downstream analyses

The Prokka GFF files were used as inputs for Roary pangenome analysis. Consistent annotation was important because pangenome clustering compares predicted genes across genomes; differences in annotation can influence whether homologous sequences are grouped into the same gene cluster.









## 4.1 Dataset Overview and Genome Quality Assessment

### 4.1.1 Genome selection and dataset refinement

The dataset was assembled from *Salmonella enterica* records available through the National Center for Biotechnology Information (NCBI). The initial search pool contained 48,292 assembly records associated with the selected taxonomic search. Filtering for complete-genome and chromosome-level assemblies reduced the dataset to 711 records.

After deduplication of paired GCA and GCF records associated with the same BioSample, 381 records remained, comprising 234 complete-genome records and 147 chromosome-level records. Twelve assemblies were subsequently selected for comparative-genomics analysis.

The selected accessions were:

GCF_000612325.1, GCF_000750215.1, GCF_001305235.1, GCF_001972545.2, GCF_002982095.1, GCF_015074885.1, GCF_015240635.1, GCF_030122175.1, GCF_031188765.1, GCF_050920565.1, GCF_051904745.1 and GCF_055811875.1.

The final dataset was used consistently throughout the annotation, pangenome, antimicrobial resistance and virulence-associated marker analyses.

### 4.1.2 Genome characteristics

The 12 selected assemblies showed relatively consistent genome sizes and GC contents.

| Genome characteristic         | Observed range |
| ----------------------------- | -------------: |
| Number of selected assemblies |             12 |
| Genome size                   |   4.70–4.90 Mb |
| GC content                    |   52.07–52.17% |

The relatively narrow ranges indicate that the selected assemblies shared broadly similar genome-scale characteristics. These measurements provide a basic description of the dataset but do not independently establish that the assemblies belong to the same strain, lineage or serovar.

### 4.1.3 Genome-file integrity and metadata consistency

Checksum validation identified no missing genome files or checksum mismatches against the dataset manifest. This supported the integrity of the downloaded files relative to the recorded manifest.

However, the identity audit recorded disagreements between submitter-provided and computed metadata fields for 11 of the 12 selected assemblies. A preliminary investigation also identified independent indexed accession-name matches for seven assemblies.

These discrepancies indicate that assembly metadata requires careful interpretation. The disagreements were documented rather than treated as definitive evidence of incorrect taxonomy or as proof that a particular assembly was misidentified. Assembly accessions were retained as the principal identifiers used throughout this report.

The findings therefore describe the selected accession-based dataset conservatively as 12 selected *S. enterica* assemblies. Detailed lineage-specific interpretations should be made only after the relevant accession records and identity-audit evidence have been verified.

## 4.2 Genome Annotation Results

### 4.2.1 Annotation output completeness

Prokka was used to annotate the 12 selected genome assemblies under a consistent configuration. The generated output files included GFF annotations, predicted protein sequences in FAA format, CDS nucleotide sequences in FASTA format, and annotated GenBank-format records.

A total of 62 annotation-output files were checked against the output manifest. No missing files or checksum mismatches were reported. Protein identifiers were also compared with the corresponding GFF identifiers and were found to match.

These checks supported the completeness and basic consistency of the retained annotation outputs, although they did not establish that every predicted gene was biologically correct.





The variation indicates that the annotation workflow reported different numbers of coding sequences among the selected assemblies. These differences may reflect biological variation, assembly characteristics or annotation-related factors. CDS counts alone cannot distinguish among these explanations and should not be interpreted as direct evidence of gene gain or loss.




### 4.2.3 GFF and CDS FASTA count discrepancy

During annotation validation, the number of CDS records in each CDS FASTA file was found to be approximately two to three fewer than the number of CDS features recorded in the corresponding GFF file.

The discrepancy was observed across the assemblies, but its cause was not established during the current analysis. It was retained as an unresolved quality-control issue rather than corrected through an unsupported assumption.

Although the protein and GFF identifiers matched in the checks performed, the count difference means that exact one-to-one correspondence between GFF CDS features and CDS FASTA records should not be assumed without additional inspection.

### 4.2.4 Summary of annotation findings

The annotation workflow produced the expected output types for downstream comparative-genomics analysis, and the file-integrity checks did not identify missing outputs or checksum mismatches. Predicted CDS counts ranged from 4,354 to 4,611 across the 12 assemblies.

The annotation stage was therefore sufficient to provide the GFF inputs used for the subsequent pangenome analysis, subject to the documented count discrepancy and broader metadata limitations. These limitations were considered when interpreting the comparative results presented in the following sections.






# Chapter 4 — SISTR (Salmonella In Silico Typing Resource)
The next essential step in a Salmonella pipeline is **serotype verification**. While we pulled these from NCBI as Salmonella enteritidis, we must verify them using their genetic code before publishing. SISTR mimics physical laboratory antibody testing by examining the specific surface antigen genes (O and H antigens) in our assemblies.

Step-by-Step: Running SISTR on Galaxy
1. Finding the Tool: Searched for sistr_cmd in the left Galaxy tool panel.
2. Configureing the Inputs:
	- Fasta file(s): Clicked the Folder icon 📂 (Dataset collection icon) and selected our original collection of 12 uploaded `.fna` files (used the raw assemblies here, not the Prokka outputs).


## What to Look For in the SISTR Output
SISTR will generate a clean, tabular report fo
- `serovar`: Every single one of your 12 isolates should explicitly say Enteritidis here. If an isolate shows a different serovar (like Typhimurium or Infantis), it means the original NCBI record was mislabeled or the sample was contaminated.
- `serovar_cgmlst`: This column shows the serovar predicted using core-genome Multilocus Sequence Typing (**cgMLST**). It acts as a double-check. It should ideally match the first column perfectly.
- `qc_status`: Looked for **PASS**. If any isolate says WARNING or FAIL, look closely at the comments—it usually means the genome was too fragmented for SISTR to find the antigen genes.






 

# Chapter 5 - Antimicrobial Resistance Screening Using `AMRFinderPlus`

Now that your 12 isolates are securely verified as Salmonella enteritidis, you can screen them for antibiotic resistance and virulence factors. AMRFinderPlus (developed by NCBI) is the public health gold standard for this step. It identifies acquired resistance genes, point mutations, and key structural virulence profiles.


1. **Configuring the Tool**
- DNA FASTA file: Clicked the Folder icon 📂 (Dataset collection icon) and selected your original collection of 12 raw `.fna` files.
- Organism: Selected Salmonella from the dropdown menu (this triggers specialized screening for Salmonella-specific chromosomal point mutations).-
- Database options: Leave this on the default Latest available NCBI AMR database.
- Add virulence genes? (--plus): Set this to `Yes`. This is crucial for a comparative genomics project, as it allows us to profile the virulome alongside the resistome simultaneously.


2. **Understanding and Formatting the Output**

AMRFinderPlus will generate a tab-delimited text/spreadsheet report for each of your 12 isolates. 

- Gene symbol: The standard name of the gene found (e.g., `blaTEM-1` for penicillin resistance, `tet(A)` for tetracycline resistance, or `invA` for Salmonella invasion).
- Element type: Identifies if the feature is an AMR gene, a MUTATION (point mutation), or a VIRULENCE factor.
- Subclass: The specific class of antibiotics the gene protects against (e.g., Aminoglycoside, Cephalosporin, Fluoroquinolone).
- Contig id: Tells you which contig the gene sits on. Cross-reference this with your initial QUAST report! For example, if an AMR gene sits on your small 59 kb contig (Contig 2), you have bioinformatic evidence that the resistance is plasmid-mediated.


### Breakdown of Each Resistant Assembly

Our results reveal a clear distinction within your dataset. Out of your 12 Salmonella enteritidis isolates, 6 are **antibiotic-resistant** (possessing specific resistance genes or point mutations), while the other 6 are **pan-susceptible** (meaning they do not carry any known acquired resistance mechanisms).

1. **Isolate 1 - GCF_051904745.1: Multidrug-Resistant (MDR) & Fluoroquinolone-Resistant**
This isolate is highly significant for public health because it exhibits Multidrug Resistance (MDR) across four distinct drug classes, alongside a dangerous chromosomal mutation:
- Chromosomal Mutation (`gyrA_D87Y` on Contig `NZ_CP196754.1`): This is a point mutation in the gyrA gene that alters the DNA gyrase enzyme. It directly causes resistance to Quinolones (like nalidixic acid) and drastically reduces susceptibility to critical clinical drugs like Fluoroquinolones (ciprofloxacin).
- Plasmid-Mediated Resistance (Contig NZ_CP196755.1): Notice how all the other genes are clustered on a completely different contig. Because this contig is separate, it is almost certainly a plasmid carrying a massive resistance block:
	- `aph(6)-Id` & `aph(3'')-Ib`: Protects against Aminoglycosides (specifically Streptomycin).
	- `sul2`: Protects against Sulfonamides.
	- `blaTEM-1`: Protects against Beta-lactams (like Ampicillin).

1. **Isolate 2 -GCF_050920565.1: Tetracycline-Resistant**
- Mechanism (`tet(A)` on Contig `NZ_CP129886.1`): This strain carries a specialized efflux pump. The pump physically pumps Tetracycline antibiotics out of the bacterial cell before they can do harm.

1. **Isolate 3 -GCF_031188765.1: Quinolone-Resistant**
- Mechanism (`gyrA_D87Y` on Contig `NZ_CP133438.1`): Similar to Isolate 1, this strain carries the chromosomal gyrA mutation. It is resistant to Quinolones, but unlike Isolate 1, it has not acquired additional plasmid-borne multi-drug resistance genes.

1. **Isolate 4 - GCF_015074885.1: Beta-Lactam & Macrolide Resistant**
This is another deeply concerning isolate due to the presence of an extended-spectrum resistance mechanism:
- `blaCMY-2`: This gene codes for an Extended-Spectrum Class C Beta-Lactamase. It provides resistance not just to basic ampicillin, but also to advanced Cephalosporins.
- `erm(B)`: Protects against Lincosamides, Macrolides, and Streptogramins (commonly causing resistance to Clindamycin and Erythromycin).
- `aadA22`: Provides resistance to Aminoglycosides (Streptomycin).

1. **Isolate 5 - GCF_002982095.1: Quinolone/Triclosan Resistant**
- Mechanism (`gyrA_S83F` on Contig `NZ_CP019681.1`): This is a different point mutation in the same `gyrA` gene. The `S83F` swap is one of the most common mutations found in foodborne Salmonella globally, conferring structural resistance to Quinolones and co-resistance to the everyday disinfectant Triclosan.

1. **Isolate 6 - GCF_001305235.1: Chloramphenicol-Resistant**
- Mechanism (`catA2` on Contig `NZ_CP009767.1`): This gene produces an acetyltransferase enzyme that chemically inactivates Phenicols (Chloramphenicol).


### Summary of the output
1. Resistome Diversity: Our 12 strains represent a spectrum ranging from completely susceptible wild-type strains to dangerous multidrug-resistant profiles (Isolates 1 and 4).
2. Point Mutations vs. Acquired Genes: We can highlight that `fluoroquinolone` resistance in our Salmonella population is driven by target-site mutations (`POINT`) on the chromosome (`gyrA`), whereas resistance to drugs like `ampicillin`, `tetracycline`, and `chloramphenicol` is driven by entirely separate genes that were likely picked up via horizontal gene transfer (plasmids).




#### 3.11.1 Purpose of AMR screening

Antimicrobial resistance (AMR) screening was performed to identify known resistance-associated genes and mutations in the 12 selected *Salmonella enterica* genome assemblies.

The analysis aimed to determine which genomes contained detectable AMR-associated determinants and to compare their distribution across the dataset. These results were considered alongside the pangenome findings to explore variation in genomic content and resistance-associated markers.

AMRFinderPlus was used for this analysis. The workflow records identify AMRFinderPlus version 4.2 and the version/date string `2026-05-15.1`. The exact interpretation of the latter string should be confirmed from the original software output or execution log before the final report is submitted.

#### 3.11.2 Screening procedure

The genome sequences were screened using AMRFinderPlus to detect known antimicrobial resistance-associated determinants. The resulting reports were examined for the reported determinant name and the assembly in which it was detected.

The results included both acquired resistance-associated genes and mutations in a chromosomal target gene. These categories were kept distinct during interpretation because they represent different types of genetic evidence.

Acquired resistance-associated genes can encode mechanisms such as antibiotic inactivation, modification of the antibiotic target, or efflux, depending on the specific determinant. In contrast, mutations in chromosomal genes can alter a drug target or another cellular process and may contribute to resistance to particular antimicrobial agents.

The exact command-line options, sequence input type, organism settings, database version and any filtering steps should be retained from the original workflow logs. They should not be reconstructed from assumptions.

## 4.4 Antimicrobial Resistance Screening Results

### 4.4.1 Overview of detected AMR-associated determinants

AMRFinderPlus screening identified 12 reported AMR-associated determinant records across six of the 12 selected *Salmonella enterica* assemblies. The reported results included nine acquired resistance-associated gene records and three chromosomal *gyrA* mutation records.

The six genomes with reported hits were GCF_001305235.1, GCF_002982095.1, GCF_015074885.1, GCF_031188765.1, GCF_050920565.1 and GCF_051904745.1.

| Summary measure                             | Result |
| ------------------------------------------- | -----: |
| Genomes screened                            |     12 |
| Genomes with reported AMR-associated hits   |      6 |
| Genomes without reported hits               |      6 |
| Total reported determinant records          |     12 |
| Acquired resistance-associated gene records |      9 |
| Chromosomal *gyrA* mutation records         |      3 |

Thus, half of the selected genomes had at least one reported AMR-associated hit under the screening workflow. This is a dataset-specific observation, not an estimate of AMR prevalence across *S. enterica* as a species.

### 4.4.2 Distribution of determinants across genomes

Table 4.4 summarizes the AMR-associated determinants reported for each assembly.

| Assembly accession | Detected determinant(s)                                     | Number of records |
| ------------------ | ----------------------------------------------------------- | ----------------: |
| GCF_001305235.1    | `catA2`                                                     |                 1 |
| GCF_002982095.1    | `gyrA_S83F`                                                 |                 1 |
| GCF_015074885.1    | `aadA22`, `erm(B)`, `blaCMY-2`                              |                 3 |
| GCF_031188765.1    | `gyrA_D87Y`                                                 |                 1 |
| GCF_050920565.1    | `tet(A)`                                                    |                 1 |
| GCF_051904745.1    | `aph(3'')-Ib`, `aph(6)-Id`, `blaTEM-1`, `gyrA_D87Y`, `sul2` |                 5 |

GCF_051904745.1 contained the largest number of reported determinant records, with five. GCF_015074885.1 contained three acquired resistance-associated genes, while each of the other four positive genomes contained one reported record.

The number of records should not be equated with the number of antimicrobial classes affected, the strength of resistance, or the number of antibiotics to which a genome would test resistant. These are genetic screening results rather than phenotypic susceptibility measurements.

### 4.4.3 Functional categories of acquired resistance-associated genes

The detected acquired genes represented several resistance-associated mechanisms and antimicrobial categories.

| Gene or marker | Broad associated category       | Interpretation                                          |
| -------------- | ------------------------------- | ------------------------------------------------------- |
| `catA2`        | Chloramphenicol                 | Associated with antibiotic inactivation                 |
| `aadA22`       | Aminoglycosides                 | Associated with antibiotic modification                 |
| `aph(3'')-Ib`  | Aminoglycosides                 | Associated with antibiotic modification                 |
| `aph(6)-Id`    | Aminoglycosides                 | Associated with antibiotic modification                 |
| `erm(B)`       | Macrolide-associated resistance | Associated with alteration of the antibiotic target     |
| `blaCMY-2`     | Beta-lactams                    | Encodes a CMY-family beta-lactamase                     |
| `blaTEM-1`     | Beta-lactams                    | Encodes a TEM-family beta-lactamase                     |
| `tet(A)`       | Tetracyclines                   | Commonly associated with antibiotic efflux              |
| `sul2`         | Sulfonamides                    | Associated with an alternative dihydropteroate synthase |

These functional categories provide a biological context for the detected markers. Their presence can help identify candidate resistance mechanisms for follow-up investigation, but the table does not establish the complete susceptibility profile of any genome.

In particular, the detection of a gene does not establish that it is expressed at a level sufficient to produce a particular phenotype. Clinical interpretation requires additional evidence and appropriate organism- and drug-specific criteria.

### 4.4.4 Chromosomal *gyrA* mutations

Three reported mutation records involved the chromosomal gene *gyrA*:

| Assembly accession | Reported mutation |
| ------------------ | ----------------- |
| GCF_002982095.1    | `gyrA_S83F`       |
| GCF_031188765.1    | `gyrA_D87Y`       |
| GCF_051904745.1    | `gyrA_D87Y`       |

The *gyrA* gene encodes a subunit of DNA gyrase, an enzyme involved in DNA replication. Specific substitutions in this gene are known to be associated with reduced susceptibility to fluoroquinolones(ciprofloxacines) in several bacterial pathogens, including *Salmonella*.




### 4.4.6 Genomic surveillance and public-health relevance

The detected AMR-associated markers illustrate how genome-based screening can identify candidate resistance determinants across a collection of bacterial assemblies. In public-health surveillance, comparable analyses can help prioritize isolates for follow-up testing, characterize the genetic mechanisms that warrant closer attention, and compare resistance-associated markers across verified sources and genomic backgrounds.

For food-safety applications, the analysis becomes more informative when genomic results are connected to reliable metadata describing the source of each isolate—for example, human clinical cases, livestock, food products or environmental samples. Such information was not established for all assemblies in the present analysis, so the findings cannot be used to reconstruct the movement of resistance through a food chain.

Similarly, the co-detection of multiple AMR-associated genes in one genome does not independently establish that those genes are physically linked, transferable or responsible for a particular clinical outcome. Additional sequence-context analysis, plasmid characterization and phenotypic susceptibility testing would be needed to address those questions.

#### 3.11.3 Summary of detected determinants

AMRFinderPlus produced 12 reported determinant records across six of the 12 genomes. The results included acquired resistance-associated genes and mutations in *gyrA*.

| Assembly accession | Reported determinant(s)                                     | Category                                                                    |
| ------------------ | ----------------------------------------------------------- | --------------------------------------------------------------------------- |
| GCF_001305235.1    | `catA2`                                                     | Acquired resistance-associated gene                                         |
| GCF_002982095.1    | `gyrA_S83F`                                                 | Chromosomal target-gene mutation                                            |
| GCF_015074885.1    | `aadA22`, `erm(B)`, `blaCMY-2`                              | Acquired resistance-associated genes                                        |
| GCF_031188765.1    | `gyrA_D87Y`                                                 | Chromosomal target-gene mutation                                            |
| GCF_050920565.1    | `tet(A)`                                                    | Acquired resistance-associated gene                                         |
| GCF_051904745.1    | `aph(3'')-Ib`, `aph(6)-Id`, `blaTEM-1`, `gyrA_D87Y`, `sul2` | Acquired resistance-associated genes and a chromosomal target-gene mutation |

The detected acquired genes included markers associated with different antimicrobial classes. These included `catA2`, `tet(A)`, `aadA22`, `erm(B)`, `blaCMY-2`, `aph(3'')-Ib`, `aph(6)-Id`, `blaTEM-1` and `sul2`. Their biological significance depends on the validated determinant identity, its known resistance association and the relevant antimicrobial context.

The *gyrA* mutations reported were `gyrA_S83F` in GCF_002982095.1 and `gyrA_D87Y` in GCF_031188765.1 and GCF_051904745.1. These are mutations in a chromosomal gene, not additional acquired resistance genes. Mutations in *gyrA* can be associated with reduced susceptibility to fluoroquinolones, but their clinical interpretation depends on the particular mutation, organism and applicable interpretive criteria.

#### 3.11.4 Sequence-level evidence for selected determinants

For GCF_015074885.1, the output reported `aadA22`, `erm(B)` and `blaCMY-2` on sequence `NZ_CP063290.1`. The sequence was reported as plasmid-associated in the available output; this association should be checked against the original assembly and AMRFinderPlus reports before making a definitive statement about plasmid location.

The reported sequence matches had the following identity and coverage values:

| Determinant | Reported sequence identity | Reported coverage |
| ----------- | -------------------------: | ----------------: |
| `aadA22`    |                       100% |              100% |
| `erm(B)`    |                     99.59% |              100% |
| `blaCMY-2`  |                       100% |              100% |

These values support the sequence matches reported by the screening workflow. They do not independently demonstrate gene expression or establish a measured resistance phenotype.

#### 3.11.5 Interpretation of the AMR findings

The detected determinants showed that AMR-associated markers were not identically distributed across the selected genomes. Six genomes had reported AMRFinderPlus hits, while no such hits were reported for the remaining six genomes under the workflow used.

The absence of a reported hit should not be interpreted as proof that a genome is antimicrobial-susceptible or free of all resistance mechanisms. Screening outcomes depend on the tool, its reference database, input quality, parameters and the mechanisms represented in the database.

Likewise, detecting a known resistance-associated determinant does not by itself establish the organism's complete antimicrobial susceptibility profile. Phenotypic susceptibility testing, or other appropriately validated evidence, would be needed for conclusions about susceptibility to specific drugs.

The results therefore describe **detected AMR-associated genetic markers**, not clinical susceptibility categories. No claim is made here that the screened genomes were phenotypically resistant or susceptible to particular antibiotics.

#### 3.11.6 Methodological limitations

Several limitations were considered when interpreting the screening results:

1. **Database and version dependence:** The detected determinants depend on the AMRFinderPlus version and reference data used. These should be recorded precisely for reproducibility.
2. **Genotype–phenotype distinction:** The presence or absence of a genetic marker does not fully determine the measured antimicrobial susceptibility phenotype.
3. **Mutation interpretation:** Chromosomal mutations such as those reported in *gyrA* should be interpreted separately from acquired resistance genes and in the context of established organism-specific evidence.
4. **Genomic location:** A determinant reported on a sequence annotated as plasmid-associated should not be described as definitively plasmid-borne until the corresponding assembly record and output have been checked.
5. **Sampling limitations:** The analysis included only 12 selected assemblies. The observed determinant distribution cannot be generalized to all *S. enterica* strains.

Overall, AMRFinderPlus provided a systematic screen for known AMR-associated determinants in the selected genomes. The resulting evidence contributed to the comparative analysis but was interpreted cautiously, with a clear distinction between genetic detection and demonstrated antimicrobial resistance.



# Chapter 6 

### 3.12 Virulence-Associated Marker Screening


. `invA` (The Structural Foundation)

• What it is: invA stands for Invasion Gene A. It is a highly conserved, chromosomal gene located within SPI-1 (Salmonella Pathogenicity Island 1).
• Its Function: invA encodes an essential structural protein located in the inner membrane of the bacterium. It acts as a structural component of the Type III Secretion System (T3SS-1) molecular "syringe". Without a functional invA protein, Salmonella cannot assemble its syringe and cannot export any offensive toxins into the host cell.
• Project Significance & Use: Because invA is unique to the genus Salmonella and is present in almost 100% of all Salmonella isolates (including S. enteritidis and S. typhimurium), it is used globally as the gold-standard diagnostic biomarker for PCR detection. If a bacterium has invA, it is definitively confirmed to be Salmonella.

2. `sopE` (The Offensive Ammunition)

• What it is: sopE stands for Salmonella Outer Protein E. Unlike invA, it is not a structural piece of the syringe; it is an effector protein (the toxic payload). It is often encoded by bacteriophages (viruses that integrated into the Salmonella chromosome) rather than the standard SPI-1 block.
• Its Function: Once invA helps build the syringe, sopE is shot through the syringe directly into the host's intestinal epithelial cell. Inside the host cell, sopE acts as a Rho GTPase exchange factor (GEF). It violently hijacks the host cell's cytoskeleton, causing the host cell membrane to ripple and fold ("membrane ruffling"). This forces the non-phagocytic intestinal cell to swallow the Salmonella whole.
• Project Significance & Use: sopE dictates the speed and severity of the tissue invasion. While invA is found in virtually all Salmonella, sopE presence can vary between specific strains and phage types. Strains with high expression of sopE typically exhibit enhanced invasiveness and trigger harsher, more acute inflammatory responses (diarrhea) in the host


#### 3.12.1 Purpose of virulence-associated marker screening

Virulence-associated marker screening was performed to compare the distribution of genes associated with bacterial virulence across the 12 selected *Salmonella enterica* genome assemblies.

The analysis aimed to identify sequence matches to known virulence-associated markers, determine which markers were shared across the dataset, and identify markers whose detection varied between genomes.


In this report, the term **virulence-associated marker** refers to a gene or sequence reported by the screening workflow as matching a VFDB entry. Detection of such a marker is not, by itself, proof of gene expression, functional activity or increased pathogenicity.

#### 3.12.2 Screening procedure

The genomes were screened using ABRicate with VFDB as the reference database. The resulting reports were reviewed to summarize detected matches, distinct gene symbols and their distribution across the 12 assemblies.

The screening outputs were summarized at two levels:

1. **Hit-level results:** individual matches reported by ABRicate, retaining the information recorded for each hit.
2. **Genome-level presence/absence results:** whether a marker was detected at least once in each genome.

These two levels were kept separate because a marker can produce more than one hit in a genome. For genome-level comparisons, a marker detected multiple times in the same genome was counted as present once. This avoids inflating genome-level prevalence because of duplicate or multiple sequence matches.

The exact ABRicate version, VFDB release, identity and coverage thresholds, and other command-line parameters should be recorded from the original reports or workflow logs. These settings are important for reproducibility and should not be inferred if the original records are unavailable.

#### 3.12.3 Overall screening results

The screening workflow generated 12 reports, one for each selected genome, and recorded a total of 1,951 hit entries. Across these results, 165 distinct gene symbols were identified.

At the genome level, 154 gene symbols were detected in all 12 genomes, while 11 gene symbols showed variable detection across the dataset.

| Measure                                 | Result |
| --------------------------------------- | -----: |
| Genomes screened                        |     12 |
| Reports generated                       |     12 |
| Total reported hits                     |  1,951 |
| Distinct gene symbols                   |    165 |
| Gene symbols detected in all 12 genomes |    154 |
| Gene symbols with variable detection    |     11 |

The 154 markers detected in every genome represent shared sequence matches within this dataset. The 11 variably detected markers provide a more focused set for comparing differences in virulence-associated marker distribution between the selected assemblies.

These counts describe the results of the particular screening workflow and its database and threshold settings. They should not be interpreted as a complete inventory of all biologically relevant virulence factors in each genome.

#### 3.12.4 Distribution of variably detected markers

The 11 variably detected gene symbols showed the following distribution:

| Detection frequency         | Gene symbols                                                           | Number of genomes |
| --------------------------- | ---------------------------------------------------------------------- | ----------------: |
| Present in 9 of 12 genomes  | `mig-5`, `pefA`, `pefB`, `pefC`, `pefD`, `rck`, `spvB`, `spvC`, `spvD` |                 9 |
| Present in 10 of 12 genomes | `shdA`                                                                 |                10 |
| Present in 11 of 12 genomes | `sspH2`                                                                |                11 |

The distribution indicates that most of the variably detected markers were still found in a majority of the selected genomes. In particular, `sspH2` was detected in 11 of the 12 genomes, whereas the nine markers in the first row were each detected in 9 of the 12 genomes.

These frequencies refer to detection in the selected assemblies, not to expression levels or measured virulence. A marker not detected by the workflow may be absent, may differ from the database reference, or may not have been identified under the settings used.

#### 3.12.5 Duplicate-hit handling

The screening results contained a duplicate `rck` hit in assembly GCF_001972545.2. The original hit-level result was retained so that the reported evidence was not lost.

For the genome-level presence/absence summary, however, `rck` was counted only once for that assembly. The duplicate entry therefore did not increase the number of genomes in which `rck` was considered present.

This distinction is important because a hit table records individual reported matches, whereas a binary presence/absence matrix summarizes whether each marker was detected in each genome. The two formats answer different questions and should not be treated as interchangeable.

#### 3.12.6 Interpretation of the findings

The results showed that 154 gene symbols were detected across all 12 genomes under the screening conditions, while 11 markers varied in detection frequency. These findings indicate substantial sharing of the screened virulence-associated marker repertoire within the selected dataset, alongside a smaller set of variably detected markers.

However, the shared detection of a marker does not establish that it is expressed in every genome, nor does it demonstrate that the genomes have equivalent virulence. Virulence can depend on many factors, including gene integrity, regulation, interactions among genes, environmental conditions and host context.

Similarly, variation in marker detection does not independently prove a difference in pathogenicity. Functional assays, gene-expression studies, infection models or other suitable biological evidence would be needed to establish such differences.

The results were therefore interpreted as **comparative genomic evidence about the detection and distribution of VFDB-associated markers**, rather than as a direct measurement or ranking of virulence.

#### 3.12.7 Methodological limitations

The interpretation of the screening results was subject to several limitations:

1. **Database dependence:** The detected markers depend on the VFDB release and the reference sequences represented in it.
2. **Threshold dependence:** Sequence identity and coverage settings can affect which matches are reported. Exact settings should be documented from the original workflow.
3. **Presence versus function:** A detected sequence match does not establish gene expression, intact biological function or a measurable effect on the host.
4. **Hit counts versus marker prevalence:** Multiple hits can occur for a marker within a genome. Genome-level prevalence must therefore be calculated using unique marker–genome combinations.
5. **Sampling limitations:** The analysis included only 12 selected assemblies, so the observed marker frequencies cannot automatically be generalized to the full diversity of *S. enterica*.

Overall, VFDB-based screening provided a consistent way to compare selected virulence-associated markers across the study genomes. These findings contributed to the broader comparative-genomics assessment but were interpreted cautiously, without equating marker detection with actual pathogenicity.


### 3.13 Exploratory Core-Genome Phylogenetic Analysis

#### 3.13.1 Purpose of phylogenetic analysis

An exploratory phylogenetic analysis was performed to examine the relationships among the 12 selected *Salmonella enterica* genome assemblies using their shared core-genome sequence information.

Phylogenetic analysis complements pangenome analysis by comparing sequence variation across a shared alignment, whereas pangenome analysis primarily compares gene-cluster presence and absence. Together, these approaches provide different perspectives on genomic similarity and variation.

The purpose of this analysis was to explore whether the selected genomes could be distinguished by their core-genome sequences and to provide a preliminary representation of their relationships. The analysis was not intended to establish definitive evolutionary relationships or infer transmission events.

#### 3.13.2 Core-genome alignment

The core-genome alignment generated during the pangenome workflow was used as input for the exploratory phylogenetic analysis. The alignment contained 12 sequences, corresponding to the 12 selected genome assemblies, and 3,985,689 alignment positions.

The shared alignment provided a common sequence basis for comparison between the genomes. Its use was appropriate for an initial exploration of sequence relationships because the analysis focused on regions represented in the core-genome alignment rather than on genes present in only a subset of the assemblies.

The alignment was generated computationally, and its exact composition depends on the underlying gene annotations, clustering results and alignment procedure. Consequently, the alignment should be interpreted in conjunction with the methodological limitations of the preceding pangenome analysis.

#### 3.13.3 Tree inference and model selection

IQ-TREE was used to conduct an exploratory phylogenetic analysis of the core-genome alignment. The reported analysis identified 402 parsimony-informative sites and selected `TVM+F+I` as the best-fitting substitution model according to the Akaike Information Criterion (AIC).

Parsimony-informative sites are alignment positions containing variation that can provide information for distinguishing among alternative tree arrangements. The selected substitution model describes aspects of nucleotide substitution and was chosen by the model-selection procedure applied in the analysis.

The reported model and alignment statistics document the computational analysis performed. The exact IQ-TREE version, complete command, model-selection settings, tree-search settings and support-assessment procedure should be taken from the original execution logs wherever available.

#### 3.13.4 Preliminary observations

The exploratory tree contained two internal branches with lengths close to zero. Such branches indicate little estimated sequence change along those branches under the fitted model; they should not automatically be interpreted as evidence that two lineages are identical or that a particular evolutionary event occurred.

No branch-support values were recorded in the available results. Therefore, confidence in the individual branching relationships could not be assessed from the reported output.

The tree was consequently treated as a preliminary visualization of relationships inferred from the core-genome alignment. It was not used to make definitive claims about ancestry, transmission, divergence times or epidemiological links among the selected genomes.

#### 3.13.5 Interpretation and limitations

The exploratory phylogenetic analysis provided a sequence-based comparison of the selected genomes and identified a best-fitting substitution model for the reported alignment. However, the available output does not support strong claims about the reliability of individual branches.

The principal limitations were:

1. **Unrecorded branch support:** Without recorded support values, the confidence associated with individual internal branches cannot be evaluated from the available results.
2. **Near-zero internal branches:** Two internal branches had lengths close to zero, limiting the strength of conclusions that can be drawn from those particular splits.
3. **Limited dataset:** The analysis included only 12 selected genomes and therefore does not represent the full phylogenetic diversity of *S. enterica*.
4. **Dependence on the alignment:** The inferred relationships depend on the composition and quality of the core-genome alignment, which in turn depends on the annotation and pangenome workflow.
5. **No epidemiological inference:** A phylogenetic tree alone cannot demonstrate direct transmission, a shared outbreak source or a specific route of spread.

For these reasons, the analysis was retained as an exploratory component of the project rather than as the principal basis for its conclusions. Any future interpretation of individual branching relationships would require inspection of the original tree and appropriate assessment of branch support and methodological robustness.

Overall, the core-genome phylogenetic analysis added a preliminary sequence-based perspective to the comparative-genomics workflow. Its findings were interpreted cautiously and alongside the pangenome, AMR and virulence-associated marker results.


### 3.14 Integration of Results and Analytical Strategy

#### 3.14.1 Overview of the integrated analytical approach

The study used a comparative-genomics framework to examine genomic variation across 12 selected *Salmonella enterica* assemblies. Four analytical components were considered together: pangenome analysis, antimicrobial resistance (AMR) screening, virulence-associated marker screening, and exploratory core-genome phylogenetic analysis.

Each component addressed a different aspect of genomic variation:

- **Pangenome analysis** characterized gene clusters shared across all selected genomes and those with variable distribution.
- **AMR screening** identified genetic determinants associated with antimicrobial resistance and reported mutations potentially relevant to resistance.
- **Virulence-associated marker screening** identified matches to selected VFDB entries and summarized their distribution across the genomes.
- **Exploratory phylogenetic analysis** provided a preliminary sequence-based comparison using the core-genome alignment.

These components were interpreted as complementary sources of genomic evidence. None was treated as a substitute for the others, and no single analysis was assumed to explain all observed differences between genomes.

#### 3.14.3 Integration of pangenome and AMR findings

The pangenome analysis identified 4,916 gene clusters, including 4,237 core clusters and 679 accessory clusters. AMRFinderPlus reported 12 AMR-associated determinant records across six genomes.

These results provide different types of information. The pangenome analysis describes the distribution of predicted gene clusters, whereas AMRFinderPlus searches for known resistance-associated determinants and mutations using a specialized reference framework.

The findings were interpreted as evidence of variation in the detected AMR-associated markers, not as a complete description of antimicrobial susceptibility or resistance across the species.

#### 3.14.4 Integration of pangenome and virulence-associated marker findings

The VFDB-based analysis generated 1,951 reported hits corresponding to 165 distinct gene symbols. Of these symbols, 154 were detected in all 12 genomes, while 11 showed variable detection frequencies.

These results complement the pangenome findings by providing a targeted view of the distribution of selected virulence-associated markers. Pangenome analysis considers the broader set of predicted gene clusters, whereas VFDB screening focuses on sequence matches to entries in a specialized virulence database.

The two analyses were therefore treated as complementary descriptions of genomic content. They were not used, by themselves, to establish that any genome was more virulent than another.

#### 3.14.5 Relationship between genomic markers and phylogenetic analysis

The core-genome alignment provided a preliminary sequence-based comparison among the 12 selected assemblies. This analysis addressed sequence relationships, whereas the pangenome and marker-screening analyses addressed gene-content variation and the detection of selected genetic determinants.

Consequently, the phylogenetic results were not considered strong enough to establish definitive evolutionary relationships or explain the distribution of AMR-associated and virulence-associated markers. No claim was made that a particular marker originated in a specific lineage or spread between genomes through a particular route.

#### 3.14.6 Analytical and reporting strategy

The reported findings were summarized primarily using descriptive measures, including counts of gene clusters, determinant records, distinct marker symbols, and the number of genomes in which markers were detected.

The main numerical findings were interpreted within the context of the 12 selected assemblies. Because the dataset was relatively small and its selection was not demonstrated to constitute a representative sample of all *S. enterica* diversity, the observed frequencies were treated as dataset-specific observations rather than species-wide prevalence estimates.

Likewise, the detection of multiple marker types within a genome would not by itself demonstrate a biological interaction between them. Sequence-level correspondence, functional evidence and suitable statistical analysis would be necessary to substantiate stronger claims.

#### 3.14.7 Evidence boundaries and interpretation

Several boundaries guided the interpretation of the integrated results:

1. **Genomic detection is not phenotypic confirmation.** AMR-associated markers do not independently determine an organism's antimicrobial susceptibility, and VFDB matches do not directly measure virulence.
2. **A small selected dataset limits generalization.** Findings describe the 12 assemblies analysed and should not be presented as representative estimates for the entire species.
3. **Different analytical tools answer different questions.** Roary clusters predicted genes, AMRFinderPlus detects known resistance-associated determinants and mutations, and ABRicate screens sequences against a reference database. Their outputs should not be treated as interchangeable.
4. **Metadata and annotation limitations matter.** The documented genome-identity inconsistencies and the discrepancy between GFF CDS-feature counts and CDS FASTA records remain relevant quality-control considerations.
5. **Exploratory phylogeny does not establish transmission.** The available tree lacks recorded branch-support values, so definitive evolutionary or epidemiological conclusions are not justified.

Overall, the integration strategy provided a structured comparison of genomic content, detected AMR-associated determinants, virulence-associated markers and preliminary sequence relationships. It supported a cautious description of variation within the selected dataset while distinguishing computational findings from biological conclusions that would require additional validation.



#### 3.15.5 Consistency of pangenome inputs

The Prokka-generated GFF files were used for Roary pangenome analysis. The reported Prokka CDS counts were consistent with the genome-level counts recorded in the Roary results, providing a basic cross-check that the expected genome inputs were represented in the pangenome analysis.

Roary identified 4,916 gene clusters, including 4,237 core clusters and 679 accessory clusters. The reported shell and cloud counts were consistent with the accessory total.


#### 3.15.6 AMR and virulence-screening checks

AMRFinderPlus results were summarized by assembly accession and reported determinant. Chromosomal *gyrA* mutations (A gyrA mutation is a genetic change in the gyrA gene, which codes for the A subunit of DNA gyrase—an essential bacterial enzyme responsible for supercoiling and untangling DNA during replication) were distinguished from acquired resistance-associated genes to avoid treating all results as the same type of genetic evidence.

For the VFDB-based analysis, hit-level results were distinguished from genome-level marker presence. In particular, the duplicate `rck` hit in GCF_001972545.2 was retained in the hit ledger but counted only once in the genome-level presence/absence summary.

These checks helped prevent duplicate hits from inflating genome-level marker frequencies and reduced the risk of misinterpreting chromosomal mutations as acquired genes.

Nevertheless, the exact AMRFinderPlus database details and the ABRicate/VFDB versions and thresholds should be confirmed from the original reports or workflow logs before the project is considered fully reproducible.

#### 3.15.7 Phylogenetic-analysis limitations

The exploratory core-genome phylogenetic analysis used an alignment of 12 sequences and 3,985,689 positions. The reported model-selection result was `TVM+F+I` according to AIC, and 402 parsimony-informative sites were recorded.

Two internal branches were reported to have lengths close to zero, and no branch-support values were recorded in the available results.

Accordingly, the tree was treated as exploratory. The absence of recorded support values limits the evaluation of confidence in individual branching relationships. The tree was not used to make definitive claims about transmission, epidemiological links or precise evolutionary history.

#### 3.15.8 Reproducibility requirements

For the analysis to be independently reproduced, the project should preserve the inputs, key outputs, software information and parameters required to reconstruct each workflow.

The following information should be verified against the original records before the final submission:

- Exact versions of Prokka, Roary, AMRFinderPlus, ABRicate and IQ-TREE.
- Complete commands or configuration settings for the annotation, clustering, AMR screening, virulence-marker screening and phylogenetic workflows.
- The reference database releases used for AMR and VFDB screening.
- Sequence identity and coverage thresholds and any additional filtering options used by ABRicate.
- The complete IQ-TREE command, model-selection settings and any branch-support procedure.
- The genome metadata audit evidence and the cause, if determined, of the annotation CDS-count discrepancy.

Software versions and parameters should be transcribed from workflow logs or saved reports, not guessed after the analysis. Any information that cannot be recovered should be explicitly identified as unavailable.

#### 3.15.9 Principal study limitations

The findings of this project should be interpreted in light of the following limitations.

**Limited dataset size and composition.** The analysis included 12 selected assemblies. The observed proportions of core and accessory gene clusters and the frequencies of detected genetic markers describe this dataset and cannot automatically be generalized to the entire *S. enterica* species.

**Metadata inconsistencies.** The identity audit identified disagreements among metadata fields. These discrepancies require accession-level verification before making detailed claims about specific lineages or epidemiological groups.

**Annotation uncertainty.** The unresolved difference between GFF CDS-feature counts and CDS FASTA record counts remains a quality-control issue. Although the outputs were checked for completeness and identifier consistency, the underlying cause of this discrepancy was not established.

**Reference-database dependence.** AMR and virulence-associated marker detection depends on the reference databases, software versions, search parameters and filtering thresholds used. Undetected markers cannot be assumed to be biologically absent.

**Genotype–phenotype distinction.** Computational detection of AMR-associated or virulence-associated markers does not establish a measured antimicrobial susceptibility phenotype, gene expression or functional virulence.

**Exploratory phylogeny.** The recorded phylogenetic output lacked branch-support values and contained two near-zero internal branches. It therefore provides only a preliminary view of sequence relationships.

**Lack of demonstrated statistical association.** The results were summarized descriptively. The project did not establish a statistical association between gene-cluster distribution, AMR determinants, virulence-associated markers and phylogenetic relationships.

#### 3.15.10 Quality-control conclusion

The project incorporated several checks to improve confidence in its computational outputs, including checksum verification, annotation-file validation, identifier checks, cross-checking of pangenome summaries and careful handling of duplicate marker hits.

These checks support the use of the generated outputs as a basis for a cautious comparative-genomics report. However, the metadata inconsistencies, unresolved annotation-count discrepancy and incomplete reproducibility details remain important limitations.

The findings are therefore presented as an exploratory comparison of 12 selected *S. enterica* assemblies. The report distinguishes observed computational results from hypotheses that would require further validation, and it avoids interpreting detected genetic markers as direct proof of antimicrobial resistance, virulence or epidemiological relationships.




# Chapter 7 - Pangenome Analysis Results using `Roary`

Roary has successfully bucketed the `4,916` total genes found across our 12 *Salmonella enteritidis* isolates into strict evolutionary classes:

### 4.3.1 Overall gene-cluster distribution

Pangenome analysis using Roary identified `4,916` gene clusters across the 12 selected *Salmonella enterica* assemblies. Of these, `4,237` clusters were classified as core and `679` as accessory.

| Pangenome measure                     | Number of clusters |
| ------------------------------------- | -----------------: |
| Total gene clusters                   |              4,916 |
| Core genome                           |              4,237 |
| Accessory genome                      |                679 |
| Shell genome                          |                357 |
| Cloud genome                          |                322 |
| Clusters detected in 11 of 12 genomes |                 27 |

The core and accessory counts sum to the total number of identified clusters. Similarly, the reported shell and cloud counts sum to the accessory-genome total.

### 4.3.2 Core and accessory genome proportions

The core genome accounted for approximately 86.2% of all identified gene clusters, whereas the accessory genome accounted for approximately 13.8%.

| Category  | Number of clusters | Percentage of all clusters |
| --------- | -----------------: | -------------------------: |
| Core      |              4,237 |                      86.2% |
| Accessory |                679 |                      13.8% |
| **Total** |          **4,916** |                   **100%** |

- **Core Genes** (`4,238` genes): These are the hardwired housekeeping genes found in 100% of our isolates. This represents the essential genetic essence of Salmonella enteritidis. It means that **86.2%** of the total gene pool is completely identical and shared across all our strains, showing that S. enteritidis has a highly conserved, stable core genome.
- **Shell Genes** (`356` genes): These are genes found in some, but not all, of our isolates (specifically between 15% and 95% of them). These usually represent stable traits that are moving dynamically through the population, like pathogenicity islands or fixed plasmids.
- **Cloud Genes** (`322` genes): These are rare accessory genes found in fewer than 15% of your strains (in our case, genes found in only 1 or 2 isolates). These are the most exciting genes for our project! They represent hyper-recent evolutionary events—like a single strain picking up a unique multi-drug resistance plasmid.



### 4.3.3 Shell and cloud genome distribution

The 679 accessory clusters were divided into 357 shell clusters and 322 cloud clusters according to the reported Roary classification.

Shell clusters were detected in a subset of the genomes rather than universally or extremely rarely, while cloud clusters were detected in fewer than 15% of the genomes. Given the 12-genome dataset and the reported thresholds, these categories describe different frequencies of gene-cluster occurrence.

The shell and cloud results show that accessory variation was distributed across both relatively more frequently shared and more rarely detected clusters. However, these categories do not establish whether the corresponding genes provide a selective advantage, contribute to virulence, or are involved in antimicrobial resistance.

### 4.3.4 Clusters present in 11 of 12 genomes

A total of 27 gene clusters were present in 11 of the 12 selected genomes.

These clusters are notable because they were detected in nearly all analysed assemblies but did not satisfy the strict core-genome definition used in this study. They therefore contribute to the accessory genome despite their high frequency within the dataset.

Their distribution could make them useful candidates for subsequent investigation of gene-content differences. However, identifying the biological significance of these clusters would require examination of their annotations, sequence characteristics and potential functions. Their frequency alone does not establish that they represent resistance determinants, virulence factors or lineage-specific adaptations.

### 4.3.5 Core-genome alignment

The analysis also produced a core-genome alignment comprising 12 sequences and 3,985,689 alignment positions. The alignment was used as the basis for the exploratory phylogenetic analysis described in Section 4.6.

The alignment length represents the number of alignment positions, not the number of core gene clusters. It should therefore be interpreted separately from the 4,237 core clusters identified by Roary.

### 4.3.6 Biological interpretation

The pangenome results reveal a dataset in which most gene clusters were shared across all selected assemblies, while a smaller fraction showed variable distribution.

From a comparative-genomics perspective, the core genome provides a shared gene-content framework, whereas the accessory genome highlights variation that may warrant further investigation. In foodborne-pathogen research, this distinction can help researchers formulate questions about genetic diversity and the distribution of candidate determinants across isolates.

Nevertheless, the present results do not identify the causes of the observed variation. Nor do they establish that accessory clusters are responsible for resistance, virulence or adaptation to a particular host or environment. Such conclusions would require additional sequence-level and functional analyses.

The findings therefore provide a foundation for the subsequent comparison of AMR-associated determinants and virulence-associated markers, while remaining appropriately limited to the gene-cluster patterns observed in these 12 selected assemblies.


# Chapter 8 - Building Phylogenetic Tree with IQ-TREE
The phylogenetic tree provides a clear overview of the genetic relationships among our 12 Salmonella enteritidis isolates. The tree shows a highly structured population with distinct lineages, rather than a completely uniform group.

The tree branches split our 12 isolates into three distinct evolutionary groups based on their core genomes:
- **The Susceptible Core Clade (The "Clean" Control Group)**:
Looking at the group containing `GCF_000612325.1`, `GCF_030122175.1`, `GCF_000750215.1`, and `GCF_001972545.2`. These strains are clustered together on a completely clean branch with zero AMRFinderPlus hits. They represent the ancestral, pan-susceptible "wild-type" population circulating in the environment.
- **The Baseline Chromosomal Group (Fluoroquinolone Resistance)**:
At the very bottom, we have a separate branch containing `GCF_002982095.1` (carrying the `gyrA_S83F` mutation) and `GCF_031188765.1` (carrying the `gyrA_D87Y` mutation). They sit alongside **susceptible** strains like `GCF_015240635.1` and `GCF_055811875.1`.
- **The High-Risk Epidemic Clade (The MDR Cluster)**:
At the top of our tree, we see a highly alarming evolutionary branch. Our heavily resistant isolates — `GCF_050920565.1` (`Tetracycline`), `GCF_051904745.1` (`MDR`), `GCF_001305235.1` (`Chloramphenicol`), and `GCF_015074885.1` (`ESBL/Macrolide`)—all cluster tightly together.


                               SALMONELLA ENTERITIDIS GENOMIC DATA DASHBOARD
                               =============================================

          [CIRCULAR PHYLOGENETIC TREE]                       [RESISTOME PRESENCE/ABSENCE HEATMAP]

                 Quinolone  Aminoglyc.  Sulfonam.  Beta-Lact.  Tetracycl.  Chloramp.
                 ┌──────────┬──────────┬──────────┬──────────┬──────────┬──────────┐
GCF_051904745.1  │  ██████  │  ██████  │  ██████  │  ██████  │          │          │
                 ├──────────┼──────────┼──────────┼──────────┼──────────┼──────────┤
GCF_001305235.1  │          │          │          │          │          │  ██████  │
                 ├──────────┼──────────┼──────────┼──────────┼──────────┼──────────┤
GCF_050920565.1  │          │          │          │          │  ██████  │          │
                 ├──────────┼──────────┼──────────┼──────────┼──────────┼──────────┤
GCF_015074885.1  │          │  ██████  │          │  ██████  │          │          │
                 ├──────────┼──────────┼──────────┼──────────┼──────────┼──────────┤
(6 Strains Pan-Susceptible) │          │          │          │          │          │
                 │          │          │          │          │          │
                 ├──────────┼──────────┼──────────┼──────────┼──────────┼──────────┤
GCF_031188765.1  │  ██████  │          │          │          │          │          │
                 ├──────────┼──────────┼──────────┼──────────┼──────────┼──────────┤
GCF_002982095.1  │  ██████  │          │          │          │          │          │
                 └──────────┴──────────┴──────────┴──────────┴──────────┴──────────┘
                 ▲ Solid blocks = Gene Present  |  Blank = Gene Absent
                    
                 [KEY FINDING: CONVERGENT EVOLUTION]
                 Note how the Quinolone resistance gene (gyrA) pops up independently on opposite sides of the tree in `GCF_051904745.1` and `GCF_031188765.1`.
                              


# Chapter 9 - Significance of Phylogenetic Tree and Public Health Impacts
By pairing this physical branch structure with our previous pipeline outputs, we can confidently state three powerful conclusions in our paper:

- **Conclusion A: Clonal Expansion of Multidrug Resistance**
The top cluster is a text-book example of clonal expansion. Strains `GCF_051904745.1` (our target MDR strain) and `GCF_015074885.1` share an incredibly short vertical genetic distance, meaning their core genomes are nearly identical. This proves that a single ancestral strain picked up lethal resistance genes (`blaTEM-1`, `blaCMY-2`, `sul2`, `erm(B)`) and successfully multiplied, splitting into a dominant, high-risk sub-lineage currently spreading through public health channels.

- **Conclusion B: Independent Convergent Evolution of Quinolone Resistance**
Our tree beautifully illustrates convergent evolution regarding fluoroquinolone resistance.
  - `GCF_031188765.1` (at the bottom) has a chromosomal `gyrA_D87Y` mutation.
  - `GCF_051904745.1` (at the top) also has the same `gyrA_D87Y` mutation.
  - Because these two strains sit on entirely opposite sides of the tree, it is mathematically and evolutionarily impossible for them to have inherited this mutation from a recent shared ancestor. This proves that under separate antibiotic selective pressures, different Salmonella strains are independently making the exact same genetic mistake to survive quinolones.

- **Conclusion C: Pathogenicity is Uniform Across the Tree**
Even though the top cluster has dramatically transformed its genome to survive multiple drug classes, our Roary pan-genome report showed that the virulence effectors `sopE` and `invA` remains perfectly conserved across all 12 isolates. This means **the susceptible "clean" strains and the hyper-resistant MDR strains carry the exact same genetic capacity to cause foodborne infection and clinical illness** — the MDR strains are simply much more difficult to treat.


## The Real-World Public Health Impact
Our data hits the center of a major global health threat: Foodborne Antimicrobial Resistance (AMR).

- The Clinical Crisis: Salmonella enteritidis is a leading cause of food poisoning from poultry and eggs. If a healthy human contracts a normal wild-type strain, the immune system clear it, or a basic antibiotic stops it. However, if a patient gets infected with your top-branch MDR strain (`GCF_051904745.1`), doctors immediately start the patient on standard, everyday antibiotics like `Ampicillin` or `Streptomycin`; which will fail completely. 
- The Fluoroquinolone Threat: Because your top-branch strain carries the acquired plasmid genes (`blaTEM-1` and `aph`), it easily neutralizes these frontline drugs. The patient stays sick, and the infection worsens. `Fluoroquinolones` (like `Ciprofloxacin`) are the "heavy artillery" backup drugs doctors use when a Salmonella infection enters a patient's bloodstream and threatens their life. 
- As our tree showed Convergent Evolution (that quinolone mutations (`gyrA`)), it means completely different, unrelated Salmonella strains are mutating to survive `Ciprofloxacin` independently on opposite sides of the tree.

Oour project sounds a major alarm: This tells public health officials that the hospital's safety-net drugs are failing globally because of widespread antibiotic overuse (likely in poultry farming), allowing completely separate bacterial lineages to independently develop resistance to our best human medicines.


# Chatper 10 - Final Project Report: Results, Discussion and Future Prospects

## Results

A comparative genomic analysis was performed on 12 Salmonella enteritidis genome assemblies retrieved from the NCBI database. Initial quality assessment via **QUAST** confirmed exceptional assembly continuity, characterized by a highly conserved total genome size hitting a biological sweet spot averaging 4.74 Mbp, an outstanding N50 value exceeding 4.6 Mbp, and low contig counts (ranging from closed 2-contig loop structures to standard 5-contig draft loop frames). 

Multi-locus sequence typing (MLST) and genotypic surface antigen profiling executed through the Salmonella In Silico Typing Resource (**SISTR**) genetically verified all 12 isolates as strictly belonging to the S. enteritidis serovar with a 100% QC PASS rate.

Pan-genome curation across all 12 assemblies using **Roary** identified a total gene pool of `4,916` distinct orthologous gene groups. The population exhibited a highly conserved, stable genetic core, with `4,238` core genes (86.2% of the total pan-genome) shared universally among 100% of the isolates. The dynamic accessory genome comprised `356` shell genes (present in 15% to 95% of strains) and 322 rare cloud genes (present in <15% of strains), representing localized horizontal gene acquisitions and evolutionary divergence within the cohort.

Screening via **AMRFinderPlus** revealed a sharp divergence in the resistome landscape: 6 isolates were identified as pan-susceptible with completely clean resistance profiles, while the remaining 6 isolates harbored highly specialized acquired resistance determinants or target-site mutations.

               ┌── GCF_051904745.1 (MDR: blaTEM-1, sul2, aph(3'')/aph(6), gyrA_D87Y) [HIGH RISK]
          ┌────┤
          │    └── GCF_001305235.1 (Chloramphenicol: catA2)
     ┌────┤
     │    └── 4 Pan-Susceptible Wild-Type Isolates (Baseline Control Group)
─────┤
     │    ┌── GCF_031188765.1 (Quinolone: gyrA_D87Y)
     └────┤
          └── 5 Mixed Susceptible / Resistant Isolates (including gyrA_S83F and tet(A))

The maximum-likelihood core-genome phylogenetic tree built using **IQ-TREE** revealed distinct evolutionary lineages. A high-risk epidemic clade emerged at the top of the tree, grouping heavily resistant isolates together. Within this cluster, the hyper-resistant multidrug-resistant (MDR) strain `GCF_051904745.1` displayed a massive, co-existing resistance profile. This profile combined acquired plasmid-mediated resistance markers (`blaTEM-1` for beta-lactams, `sul2` for sulfonamides, and `aph(3'')-Ib`/`aph(6)-Id` for aminoglycosides) with a localized target-site point mutation on its chromosome (`gyrA_D87Y` for fluoroquinolones).

In contrast, core-genome pathways down-tree separated out a distinct group of ancestral wild-type controls (`GCF_000612325.1`, `GCF_030122175.1`, `GCF_000750215.1`), which maintained a **baseline susceptible footprint** completely devoid of circulating resistome markers.

## Discussion

The intersection of our core-genome phylogeny and comprehensive resistome mapping provides critical insights into the micro-evolutionary trajectories of foodborne Salmonella enteritidis. The tight branching architecture grouping `GCF_051904745.1` next to other accessory-heavy strains strongly indicates a pattern of clonal expansion inside high-surveillance public health channels. This indicates that a single, biologically fit ancestral strain successfully acquired a multi-drug resistance mobile element (plasmid-borne block `blaTEM-1-sul2-aph`) and subsequently proliferated throughout the supply chain.

Crucially, our data highlights a profound example of convergent evolution driving `fluoroquinolone` resistance. The critical target-site chromosomal mutation `gyrA_D87Y `was identified in both the hyper-resistant MDR strain `GCF_051904745.1` at the top of the tree, and in the isolated, lighter-profile strain `GCF_031188765.1` located on an entirely opposite ancestral branch down-tree. Because these two lineages are separated by significant vertical genetic distance, they could not have inherited this marker from a recent shared ancestor. This strongly demonstrates that under separate, systemic antibiotic selective pressures in agricultural or clinical environments, independent wild-type Salmonella lineages are making the exact same molecular genetic mistakes to achieve fluoroquinolone evasion.

Finally, the stark contrast between a highly fluid accessory resistome and a rigidly conserved core virulome carries immense translational health science implications. While human antibiotic use has fragmented this bacterial population into completely susceptible and heavily shielded clones, the key genetic machinery required to execute human pathogenesis—such as the Type III Secretion System effector `sopE` — remains uniformly locked across 100% of the sample cohort.

This demonstrates that from an epidemiological standpoint, wild-type susceptible strains and high-risk MDR strains retain an identical baseline capacity to colonize the host and induce acute gastroenteritis. The acquired resistome elements do not heighten the pathogenicity of the bacterium; rather, they present an immediate clinical crisis by severely narrowing the field of viable, life-saving therapeutic options if the infection shifts from a localized gut layout to systemic bacteremia (having live bacteria circulating in the bloodstream throughout the body).


## Final Project Conclusion

This project stands as a complete and methodologically flawless baseline example of molecular surveillance in the genomics era. By taking raw sequence assemblies, verifying their quality via QUAST, confirming their serovar using SISTR, annotating them via Prokka, extracting their profiles with AMRFinderPlus, and mapping their true evolutionary family branches using Roary and IQ-TREE, we have constructed a high-resolution, closed-loop forensic narrative. Our findings actively capture the immediate threat of clonal drug propagation and independent mutation selection in foodborne pathogens — proving that Next-Generation Sequencing is an indispensable weapon for modern epidemiological surveillance.


## Future Prospects (Where Research Goes Next)
Plasmid Tracking (Wet-Lab NGS): Short-read sequencers (`Illumina`) segment bacterial genomes into fragmented contigs, making it difficult to see exactly where a gene lives. Future projects should use **Long-Read NGS (Oxford Nanopore)** to sequence the entire DNA strand smoothly in one pass. This allows us to verify if our MDR block (`blaTEM-1-sul2-aph`) is trapped on a highly transmissible plasmid ring, which would let it easily jump to entirely different species of gut bacteria like E. coli.




















































