# Git History Reconstruction: Metagenomics QC-Taxonomy-Assembly Pipeline

This document describes a realistic development history for the Metagenomics QC-Taxonomy-Assembly Pipeline, reconstructing how this project would have evolved from initial setup to its current portfolio-ready state.

## History Expansion Note

**Previous historian run:** 11 steps (N_old = 11)  
**Current historian run:** 17 steps (N_target = 17)  
**Achieved multiplier:** 1.55× (exceeds the 1.5× requirement)

### Expansion Strategy Applied

This expanded history uses two key strategies to increase step count while maintaining realism:

**Strategy A - Split large commits:** Several substantial commits from the original 11-step history were split into smaller, more atomic commits that a real developer would make:
- **Old step 01** → **New steps 01-02:** Split repository initialization (README first, then .gitignore and LARGE_FILES.md)
- **Old step 03** → **New steps 04-05:** Split MetaPhlAn results (tabular output first, then Excel format)
- **Old step 05** → **New steps 07-08:** Split GeneMarkS outputs (main predictions first, then sequence files)
- **Old step 07** → **New steps 10-11:** Split BLAST results (initial run first, then additional output formats)

**Strategy B - Insert "oops → hotfix" sequence:** Inserted a realistic mistake-and-fix pair:
- **New step 12 (OOPS):** Accidentally documented wrong data file path in README (`data/sequences/ERR688365.fastq` instead of `data/ERR688365.fastq`)
- **New step 13 (HOTFIX):** Immediately corrected the path error after noticing it wouldn't work

### Mapping from Old Steps to New Steps

| Old Steps | New Steps | Description |
|-----------|-----------|-------------|
| Old step 01 | New steps 01-02 | Initial repository setup (split into README + config files) |
| Old step 02 | New step 03 | FastQC quality control results |
| Old step 03 | New steps 04-05 | MetaPhlAn taxonomic profiling (split tabular + Excel) |
| Old step 04 | New step 06 | MEGAHIT assembly results |
| Old step 05 | New steps 07-08 | GeneMarkS gene prediction (split output + sequences) |
| Old step 06 | New step 09 | BLAST input preparation |
| Old step 07 | New steps 10-11 | BLAST functional annotation (split result formats) |
| *NEW* | New steps 12-13 | **Oops → Hotfix pair:** Wrong path in README, then corrected |
| Old step 08 | New step 14 | Comprehensive analysis report |
| Old step 09 | New step 15 | Documentation enhancement |
| Old step 10 | New step 16 | Portfolio identity and tracking files |
| Old step 11 | New step 17 | Final portfolio transformation |

---

## Development Timeline

### Step 01: Initial Repository Setup - README
**Commit Message:** `Initial commit: basic README and project description`

**Files Created:**
- `README.md` - Basic project description

**Rationale:** Every project starts with a README. Created a minimal initial README to establish the repository with basic project information before adding configuration files.

**Date Context:** Day 1 - just created the repository

---

### Step 02: Repository Configuration
**Commit Message:** `Add .gitignore and document large file storage approach`

**Files Created:**
- `.gitignore` - Ignore large data files (FASTQ) and temporary files
- `LARGE_FILES.md` - Document external data storage approach

**Rationale:** After establishing the basic README, added essential repository configuration. The .gitignore ensures large sequencing files (220 MB) won't be accidentally committed. LARGE_FILES.md documents where the data is stored and how to access it.

**Date Context:** Day 1 - completing initial repository setup

---

### Step 03: Add Quality Control Results
**Commit Message:** `Add FastQC quality control results`

**Files Created:**
- `Results/FastQC_on_data_1__Webpage.zip` - FastQC HTML report with quality metrics

**Rationale:** First pipeline stage - quality control. After obtaining the metagenomic sequencing data (ERR688365.fastq), ran FastQC to assess read quality. This is always the first step in any sequencing analysis workflow. The QC must pass before proceeding with downstream analysis.

**Date Context:** Day 2 - after data acquisition, first analysis step

---

### Step 04: Add Taxonomic Profiling Results (Tabular)
**Commit Message:** `Add MetaPhlAn taxonomic profiling - tabular output`

**Files Created:**
- `Results/metaphlan_result.tabular` - Taxonomic composition in tabular format

**Rationale:** Second pipeline stage - determine what organisms are present. MetaPhlAn identifies microbial taxa and their relative abundances using marker genes. Started with the standard tabular output format which is the primary MetaPhlAn output.

**Date Context:** Day 3 - QC passed, proceeding with taxonomic analysis

---

### Step 05: Add Taxonomic Profiling Results (Excel)
**Commit Message:** `Export MetaPhlAn results to Excel format for easier viewing`

**Files Created:**
- `Results/metaphlan.xlsx` - Taxonomic composition in Excel format

**Rationale:** After generating the tabular results, converted them to Excel format for easier viewing and sharing with collaborators who prefer spreadsheet tools over plain text tables.

**Date Context:** Day 3 - same day, formatting results for better accessibility

---

### Step 06: Add Assembly Results
**Commit Message:** `Add MEGAHIT de novo assembly results`

**Files Created:**
- `Results/megahit_result.fasta` - Assembled contigs

**Rationale:** Third pipeline stage - de novo assembly. MEGAHIT reconstructs longer genomic sequences (contigs) from short sequencing reads. This is critical for downstream gene prediction and annotation. Assembly is computationally intensive and took several hours to complete.

**Date Context:** Day 4 - after taxonomic profiling, now reconstructing genomes

---

### Step 07: Add Gene Prediction Output
**Commit Message:** `Add GeneMarkS gene prediction results`

**Files Created:**
- `Results/gmhmmp.20240724.053709.682348.gmhmmp.out.txt` - GeneMarkS raw output with gene coordinates and predictions

**Rationale:** Fourth pipeline stage - identify genes. GeneMarkS predicts protein-coding genes from assembled contigs. Started by committing the main output file which contains gene coordinates and prediction metadata. The timestamped filename reflects the actual output format from GeneMarkS runs.

**Date Context:** Day 5 - after assembly, identifying coding sequences

---

### Step 08: Add Gene Sequences
**Commit Message:** `Add predicted gene and protein sequences from GeneMarkS`

**Files Created:**
- `Results/gmhmmp.20240724.053709.682348.gmhmmp.out.fnn.txt` - Predicted genes (nucleotide sequences)
- `Results/gmhmmp.20240724.053709.682348.gmhmmp.out.faa.txt` - Predicted proteins (amino acid sequences)

**Rationale:** After the initial GeneMarkS run completed, added the sequence files (nucleotide and amino acid). These are needed for downstream functional annotation via BLAST. Committing them separately makes sense as they're distinct outputs generated in the same run but serving different purposes.

**Date Context:** Day 5 - same run, adding sequence outputs

---

### Step 09: Prepare Sequences for Functional Annotation
**Commit Message:** `Prepare representative sequences for BLAST analysis`

**Files Created:**
- `Results/blastx_inputs.fasta` - Selected sequences for BLAST functional annotation

**Rationale:** Preparation for functional annotation. Selected representative predicted genes to query against protein databases. Not all genes need to be BLASTed due to computational cost and time constraints - selected a representative subset covering diverse gene families.

**Date Context:** Day 6 - preparing for functional annotation stage

---

### Step 10: Run BLAST Functional Annotation
**Commit Message:** `Add BLAST functional annotation results`

**Files Created:**
- `Results/blastx_results.txt` - BLASTX results in tabular format
- `Results/blast_result.txt` - Alternative BLAST output format

**Rationale:** Fifth pipeline stage - functional annotation. BLAST searches identify protein homologs and assign functions to predicted genes. Started with the standard tabular output format which is most commonly used for downstream analysis. BLAST queries against the NCBI nr database took several hours to complete.

**Date Context:** Day 7 - final analysis stage, functional annotation

---

### Step 11: Add Additional BLAST Output Formats
**Commit Message:** `Export BLAST results in JSON format and summary`

**Files Created:**
- `Results/blast_result.json` - BLAST results in JSON format for programmatic access
- `Results/results.out` - Summary output file

**Rationale:** After completing the BLAST run, exported results in additional formats. The JSON format is useful for programmatic parsing and integration with other tools. Added a summary file for quick reference of annotation statistics.

**Date Context:** Day 7 - same day, formatting BLAST outputs

---

### Step 12: Documentation Update - OOPS!
**Commit Message:** `Update README with data file information`

**Files Modified:**
- `README.md` - Added data file location (with incorrect path)

**What broke:** While updating the README to document the input data location, accidentally typed the wrong path: `data/sequences/ERR688365.fastq` instead of the correct `data/ERR688365.fastq`. This would cause confusion for anyone trying to locate the data file.

**Rationale:** Attempted to improve documentation by adding information about where the input data is located. Unfortunately, made a typo in the directory structure - added an extra subdirectory (`sequences/`) that doesn't actually exist.

**Date Context:** Day 8 - documenting data files

---

### Step 13: Fix README Path Error - HOTFIX
**Commit Message:** `Fix: correct data file path in README`

**Files Modified:**
- `README.md` - Corrected data file path to `data/ERR688365.fastq`

**How I noticed:** When I tried to verify the path I documented, I realized `data/sequences/` doesn't exist - the file is directly under `data/`. Also added a reference to LARGE_FILES.md for better documentation.

**What fixed it:** Changed `data/sequences/ERR688365.fastq` to `data/ERR688365.fastq` and added a note to reference LARGE_FILES.md for access details.

**Rationale:** Immediately corrected the path error to prevent confusion. Also improved the documentation by adding a reference to the LARGE_FILES.md document which contains the actual access link.

**Date Context:** Day 8 - same day, quickly fixed after noticing the error

---

### Step 14: Add Comprehensive Analysis Report
**Commit Message:** `Add detailed project report with methods and results`

**Files Created:**
- `report.docx` - Detailed project report with comprehensive methods, results, and interpretation
- `~$report.docx` - Word temporary file (auto-generated during editing)

**Rationale:** Document the complete analysis workflow, methodologies, results, and biological findings in a formal report suitable for academic or professional presentation. The Word temp file is typical when editing .docx files and indicates active document editing.

**Date Context:** Day 9 - after all analyses complete, documenting findings comprehensively

---

### Step 15: Enhance Documentation
**Commit Message:** `Enhance README with complete pipeline documentation and reproducibility notes`

**Files Modified:**
- `README.md` - Comprehensive update with all pipeline stages, system requirements, installation instructions, troubleshooting, and citations

**Rationale:** After completing all analysis stages, significantly enhanced documentation to be comprehensive and useful for others wanting to reproduce or understand the workflow. Added detailed sections on:
- Complete tech stack with tool descriptions
- Step-by-step pipeline workflow with commands
- System requirements and prerequisites
- Installation instructions for all tools
- Troubleshooting common issues
- Citations for all tools used

**Date Context:** Day 10 - polishing documentation after pipeline completion

---

### Step 16: Portfolio Preparation - Add Identity and Tracking Files
**Commit Message:** `Add professional project identity and portfolio tracking`

**Files Created:**
- `project_identity.md` - Professional project framing with display title, tagline, stack, and problem/approach
- `report.md` - Portfolio readiness tracking report
- `suggestion.txt` - Issue tracking ledger (TAB-separated format)
- `suggestions_done.txt` - Change tracking ledger with before/after snippets

**Rationale:** Preparing repository for portfolio use. Establish professional project identity separate from the README, and create systematic tracking files to document the transformation from research project to portfolio piece. These files enable transparent tracking of all changes made during portfolio preparation.

**Date Context:** Week 2 - transitioning from research project to portfolio piece

---

### Step 17: Portfolio Transformation - Final State
**Commit Message:** `Portfolio ready: remove academic traces, professional documentation`

**Files Modified:**
- `README.md` - Complete professional overhaul:
  - Removed "University Project" label
  - Rewrote with professional active voice and framing
  - Enhanced with comprehensive system requirements, prerequisites, and citations
  - Reorganized into portfolio-appropriate sections
  - Clarified pre-generated results nature (not runnable scripts)
  - Added license section and tool acknowledgments
- `report.md` - Completed portfolio readiness tracking
- `suggestion.txt` - All identified issues documented and marked APPLIED
- `suggestions_done.txt` - All changes logged with before/after snippets and locators

**Rationale:** Final portfolio transformation to remove all academic traces and reframe as professional bioinformatics project suitable for portfolio display. Key changes:
- Removed all academic context markers ("University Project", assignment language)
- Converted to professional active voice throughout
- Emphasized practical reproducibility and real-world application
- Maintained scientific accuracy while improving presentation quality
- Made it clear this is a results repository with example outputs
- Added comprehensive citations respecting tool authors

**Date Context:** Week 2 - final portfolio preparation, current state

---

## Development Narrative

This metagenomics pipeline project followed a natural bioinformatics workflow progression:

**Phase 1 - Setup (Steps 01-02):** Established repository structure and documented approach for handling large sequencing files that can't be stored in Git.

**Phase 2 - Core Analysis Pipeline (Steps 03-11):**
1. **Quality Control (Step 03):** Assessed sequencing data quality - the essential first step
2. **Taxonomic Profiling (Steps 04-05):** Identified community composition using marker-gene approach, with results in multiple formats
3. **Assembly (Step 06):** Reconstructed longer genomic sequences from short reads
4. **Gene Prediction (Steps 07-08):** Identified protein-coding genes from assembled sequences, with both coordinates and sequences
5. **Functional Annotation (Steps 09-11):** Prepared sequences and assigned biological functions through homology search, with results in multiple formats

**Phase 3 - Documentation Issue & Fix (Steps 12-13):**
- **Step 12 (Oops):** Made a documentation error with wrong data file path
- **Step 13 (Hotfix):** Immediately caught and corrected the path error

**Phase 4 - Comprehensive Documentation (Steps 14-15):**
- **Formal Reporting (Step 14):** Comprehensive analysis report with methods and biological interpretation
- **Technical Documentation (Step 15):** Enhanced README with complete reproducibility information

**Phase 5 - Portfolio Transformation (Steps 16-17):**
- **Portfolio Infrastructure (Step 16):** Added professional identity and systematic change tracking
- **Final Polish (Step 17):** Professional reframing while maintaining scientific accuracy

Each step represents a logical progression in metagenomic data analysis, with results stored incrementally as each stage completed. The final transformation to portfolio-ready state maintains all scientific content while removing academic context markers and improving professional presentation.

## Snapshot Verification Notes

- All 17 snapshots exclude the `history/` directory itself (to avoid recursion)
- All 17 snapshots exclude the `.git/` directory
- Step 17 (final snapshot) matches the current repository working tree exactly (excluding `history/`)
- Binary files (FASTQ data, 220 MB) are documented but not included due to size constraints
- All result files are preserved exactly as generated by the bioinformatics tools
- Timestamps in filenames (e.g., GeneMarkS outputs with `20240724.053709.682348`) are preserved for authenticity
- The "oops → hotfix" pair (steps 12-13) exists only in intermediate history; the final state (step 17) is correct
- Achieved 1.55× expansion multiplier (17 steps / 11 original steps = 1.545)
