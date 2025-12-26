# Git History Reconstruction: Metagenomics QC-Taxonomy-Assembly Pipeline

This document describes a realistic development history for the Metagenomics QC-Taxonomy-Assembly Pipeline, reconstructing how this project would have evolved from initial setup to its current portfolio-ready state.

## Development Timeline

### Step 01: Initial Repository Setup
**Commit Message:** `Initial commit: repository structure and basic documentation`

**Files Created:**
- `README.md` - Basic project description
- `.gitignore` - Ignore large data files and temp files
- `LARGE_FILES.md` - Document external data storage approach

**Rationale:** Every project starts with initialization. Set up the repository with basic documentation explaining the project scope and how to handle large sequencing data files that can't be stored in Git.

**Date Context:** Early in project - just created the repository

---

### Step 02: Add Quality Control Results
**Commit Message:** `Add FastQC quality control results`

**Files Created:**
- `Results/FastQC_on_data_1__Webpage.zip` - FastQC HTML report
- Updated `README.md` - Add QC section and FastQC installation instructions

**Rationale:** First pipeline stage - quality control. After obtaining the metagenomic sequencing data (ERR688365.fastq), ran FastQC to assess read quality. This is always the first step in any sequencing analysis workflow.

**Date Context:** After data acquisition, first analysis step

---

### Step 03: Add Taxonomic Profiling Results  
**Commit Message:** `Add MetaPhlAn taxonomic profiling results`

**Files Created:**
- `Results/metaphlan_result.tabular` - Taxonomic composition (tabular format)
- `Results/metaphlan.xlsx` - Taxonomic composition (Excel format for easier viewing)
- Updated `README.md` - Add taxonomic profiling section and MetaPhlAn instructions

**Rationale:** Second pipeline stage - determine what organisms are present. MetaPhlAn identifies microbial taxa and their relative abundances using marker genes. Essential for understanding community composition before assembly.

**Date Context:** After QC passed, proceeding with analysis

---

### Step 04: Add Assembly Results
**Commit Message:** `Add MEGAHIT assembly results`

**Files Created:**
- `Results/megahit_result.fasta` - Assembled contigs
- Updated `README.md` - Add assembly section and MEGAHIT instructions

**Rationale:** Third pipeline stage - de novo assembly. MEGAHIT reconstructs longer genomic sequences (contigs) from short sequencing reads. Critical for downstream gene prediction and annotation.

**Date Context:** After taxonomic profiling, now reconstructing genomes

---

### Step 05: Add Gene Prediction Results
**Commit Message:** `Add GeneMarkS gene prediction results`

**Files Created:**
- `Results/gmhmmp.20240724.053709.682348.gmhmmp.out.txt` - GeneMarkS raw output
- `Results/gmhmmp.20240724.053709.682348.gmhmmp.out.fnn.txt` - Predicted genes (nucleotide sequences)
- `Results/gmhmmp.20240724.053709.682348.gmhmmp.out.faa.txt` - Predicted proteins (amino acid sequences)
- Updated `README.md` - Add gene prediction section and GeneMarkS instructions

**Rationale:** Fourth pipeline stage - identify genes. GeneMarkS predicts protein-coding genes from assembled contigs. The timestamped filenames reflect the actual output format from GeneMarkS runs.

**Date Context:** After assembly, identifying coding sequences

---

### Step 06: Add BLASTX Functional Annotation Setup
**Commit Message:** `Prepare sequences for functional annotation`

**Files Created:**
- `Results/blastx_inputs.fasta` - Selected sequences for BLAST analysis
- Updated `README.md` - Add BLAST preparation notes

**Rationale:** Preparation for functional annotation. Selected representative predicted genes to query against protein databases. Not all genes need to be BLASTed due to computational cost.

**Date Context:** Preparing for functional annotation stage

---

### Step 07: Add BLAST Annotation Results
**Commit Message:** `Add BLAST functional annotation results`

**Files Created:**
- `Results/blastx_results.txt` - BLASTX results (tabular format)
- `Results/blast_result.txt` - Alternative BLAST output
- `Results/blast_result.json` - BLAST results in JSON format
- `Results/results.out` - Summary output
- Updated `README.md` - Add functional annotation section and BLAST instructions

**Rationale:** Fifth pipeline stage - functional annotation. BLAST searches identify protein homologs and assign functions to predicted genes. Multiple output formats for different downstream analyses.

**Date Context:** Final analysis stage completed

---

### Step 08: Add Comprehensive Analysis Report
**Commit Message:** `Add comprehensive analysis report`

**Files Created:**
- `report.docx` - Detailed project report with methods, results, and interpretation
- `~$report.docx` - Word temporary file (auto-generated)

**Rationale:** Document the complete analysis workflow, results, and biological findings in a formal report. The Word temp file is typical when editing .docx files.

**Date Context:** After all analyses complete, documenting findings

---

### Step 09: Documentation Enhancement
**Commit Message:** `Enhance README with complete pipeline documentation`

**Files Modified:**
- `README.md` - Comprehensive update with all pipeline stages, troubleshooting, and reproducibility notes

**Rationale:** After completing all analysis stages, enhanced documentation to be comprehensive and useful for others wanting to reproduce or understand the workflow.

**Date Context:** Polishing documentation after pipeline completion

---

### Step 10: Portfolio Preparation - Professional Identity
**Commit Message:** `Add professional project identity and tracking files`

**Files Created:**
- `project_identity.md` - Professional project framing
- `report.md` - Portfolio readiness tracking report  
- `suggestion.txt` - Issue tracking ledger
- `suggestions_done.txt` - Change tracking ledger

**Rationale:** Preparing repository for portfolio use. Establish professional project identity and create systematic tracking for portfolio-readiness transformation.

**Date Context:** Transitioning from research project to portfolio piece

---

### Step 11: Portfolio Transformation - Final State
**Commit Message:** `Portfolio ready: remove academic traces, professional documentation`

**Files Modified:**
- `README.md` - Complete professional overhaul:
  - Removed "University Project" label
  - Professional active voice and framing
  - Enhanced with system requirements, prerequisites, citations
  - Reorganized into portfolio-appropriate sections
  - Clarified pre-generated results nature
- `report.md` - Complete portfolio readiness tracking
- `suggestion.txt` - All issues documented and marked APPLIED
- `suggestions_done.txt` - All changes logged with before/after snippets

**Rationale:** Final portfolio transformation. Removed all academic traces and reframed as professional bioinformatics project suitable for portfolio display. Maintained scientific accuracy while improving presentation.

**Date Context:** Final portfolio preparation - current state

---

## Development Narrative

This metagenomics pipeline project followed a natural bioinformatics workflow progression:

1. **Setup Phase (Step 01):** Established repository and documented approach for handling large sequencing files
2. **Quality Control (Step 02):** Assessed sequencing data quality - the essential first step
3. **Taxonomic Profiling (Step 03):** Identified community composition using marker-gene approach
4. **Assembly (Step 04):** Reconstructed longer genomic sequences from short reads
5. **Gene Prediction (Step 05):** Identified protein-coding genes from assembled sequences
6. **Functional Annotation (Steps 06-07):** Assigned biological functions through homology search
7. **Documentation (Steps 08-09):** Comprehensive reporting and workflow documentation
8. **Portfolio Transformation (Steps 10-11):** Professional reframing for career portfolio

Each step represents a logical progression in metagenomic data analysis, with results stored incrementally as each stage completed. The final transformation to portfolio-ready state maintains all scientific content while removing academic context markers.

## Snapshot Verification Notes

- All snapshots exclude the `history/` directory itself (to avoid recursion)
- Step 11 (final snapshot) matches the current repository working tree exactly
- Binary files (FASTQ data) are documented but not included due to size (220 MB)
- All result files are preserved exactly as generated by the bioinformatics tools
- Timestamps in filenames (e.g., GeneMarkS outputs) are preserved for authenticity
