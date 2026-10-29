# Comparative Genomics of Selected *Salmonella enterica* Assemblies

## Project Overview

This project investigates core and accessory genome variation, antimicrobial resistance (AMR)-associated determinants, and virulence-associated gene distributions across 12 selected *Salmonella enterica* genome assemblies.

The analysis integrates genome annotation, pangenome analysis, AMR determinant screening, and virulence-associated gene screening to explore genomic similarities and differences among the selected assemblies.

**Project type:** Comparative genomics and bioinformatics  
**Organism:** *Salmonella enterica*  
**Genome assemblies:** 12 selected assemblies  
**Primary tools:** Prokka, Roary, AMRFinderPlus, ABRicate, VFDB, and IQ-TREE (exploratory phylogenetic analysis)

## Research Questions

1. How much of the analyzed gene repertoire is shared across all 12 assemblies, and how much is accessory?
2. Which AMR-associated determinants are detected, and how are they distributed among the assemblies?
3. Which virulence-associated gene markers are shared or variable across the selected genomes?
4. How can these findings be interpreted alongside differences in genome content?

## Workflow

1. **Genome selection and quality checks:** Selected 12 genome assemblies and checked assembly metadata, sequence files, checksums, genome size, and GC content.
2. **Genome annotation:** Annotated the assemblies using **Prokka** with consistent settings.
3. **Pangenome analysis:** Used **Roary** to identify core and accessory gene clusters.
4. **AMR screening:** Used **AMRFinderPlus** to identify reported resistance-associated determinants and relevant point mutations.
5. **Virulence-associated gene screening:** Used **ABRicate** with the **VFDB** database to identify matching gene markers.
6. **Integration and quality checks:** Organized the output into presence matrices, hit-level tables, summary statistics, and documentation.
7. **Exploratory phylogenetic analysis:** Generated a core-genome alignment and exploratory **IQ-TREE** output; this analysis should be treated as preliminary unless its support and reproducibility are further validated.


                  [12 uploaded .fna FASTA files]
                                │
                                ▼
         ┌──────────────────────┴──────────────────────┐
         ▼                                             ▼
  1. Quality Assessment                         2. Genomic Annotation
  Tool: [QUAST]                                 Tool: [Prokka]
  Outputs: Contig length, N50,                  Outputs: GenBank (`.gbk`) & 
  and genome completeness stats                 GFF3 files for all 12 strains
         │                                             │
         ▼                                             ▼
  3. Serotype Verification                      4. Resistome & Virulome
  Tool: [SISTR]                                 Tool: [AMRFinderPlus] / [ResFinder]
  Outputs: Genotypic verification               Outputs: Spreadsheets of antimicrobial
  of Salmonella enteritidis                     resistance and virulence genes
                                                       │
                                                       ▼
                                                5. Pan-Genome Analysis
                                                Tool: [Roary] (Uses Prokka's `GFF3` outputs)
                                                Outputs: Core genome alignment & 
                                                gene presence/absence matrix
                                                       │
                                                       ▼
                                                6. Phylogenetic Tree
                                                Tool: [IQ-TREE] or [FastTree]
                                                Outputs: Newick (`.nwk`) tree file

## Key Findings

### Pangenome

Roary identified **4,916 gene clusters**, including **4,237 core clusters** present in all 12 assemblies and **679 accessory clusters**.

The accessory clusters comprised 357 shell clusters and 322 cloud clusters under the thresholds used for this analysis.

### Antimicrobial Resistance

AMRFinderPlus reported AMR-associated determinants or relevant mutations in six of the 12 assemblies. Reported findings included *tet(A)*, *blaTEM-1*, *blaCMY-2*, *sul2*, aminoglycoside-associated determinants, and *gyrA* substitutions.

These are computational detections, not antimicrobial susceptibility test results. The absence of a reported hit does not establish that an assembly is susceptible or free of resistance determinants.

### Virulence-Associated Markers

VFDB screening produced 1,951 reported hits representing 165 distinct gene symbols. Of these symbols, 154 were detected in all 12 assemblies, while 11 showed variable presence.

These results describe sequence matches to database markers. They do not establish gene expression, functional activity, or virulence in a host.

## Repository Structure

- `data/metadata/` — assembly identity audit and reproducibility records.
- `data/raw/` — instructions concerning raw input data and their provenance.
- `results/pangenome/` — Roary pangenome outputs and summaries.
- `results/amr/` — AMR presence matrix and hit-level records.
- `results/vfdb/` — virulence-associated marker summaries and presence matrices.
- `results/figures/` — figures generated from the analyzed results, where available.
- `results/` — integrated summaries and validation records, where available.
- `docs/` — consolidated report, identity reconciliation note, and methods checklist.
- `scripts/` — scripts or instructions for processing and validating results.
- `workflows/` — workflow descriptions and tool configuration notes.

## Important Limitations

- The dataset contains only 12 selected assemblies and is not necessarily representative of the species as a whole.
- Assembly identity and metadata discrepancies require careful reconciliation. Conclusions about serovar or lineage should not be made until the relevant metadata are independently verified.
- Gene presence does not establish gene expression or phenotype.
- AMR screening results do not replace laboratory antimicrobial susceptibility testing.
- VFDB matches indicate similarity to database-associated markers, not demonstrated pathogenicity.
- The exploratory phylogenetic output should not be used for strong evolutionary conclusions without additional validation and adequate branch-support reporting.
- Results depend on the versions, databases, parameters, and thresholds used in the analyses.

## Reproducibility

The repository retains selected analysis outputs and documentation. Consult `docs/METHODS_REPRODUCIBILITY_CHECKLIST.md` for recorded software settings, database details, input provenance, and outstanding reproducibility gaps.

Raw genome assemblies are not necessarily included in this repository. Their accessions and retrieval instructions should be documented so that the inputs can be obtained again.

## Intended Use

This project is an academic bioinformatics portfolio project demonstrating comparative genome analysis, gene presence/absence analysis, resistance-associated determinant screening, and interpretation of database-derived results.

It is not intended for clinical diagnosis or treatment decisions.

## Author

**AL FUAD**  
Bioinformatics | Comparative Genomics | Molecular Biology
