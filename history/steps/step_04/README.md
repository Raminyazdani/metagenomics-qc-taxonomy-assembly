# Metagenomics Pipeline Analysis

## Tools & Setup

**Bioinformatics Tools:**
- FastQC - Quality control
- MetaPhlAn - Taxonomic profiling  
- MEGAHIT - Genome assembly
- GeneMarkS - Gene prediction
- BLAST - Functional annotation

Installation instructions: See individual stage commands below.

## Data

Input: `data/ERR688365.fastq` (220 MB, stored externally - see LARGE_FILES.md)

## Pipeline Progress

### 1. Quality Control ✓
```bash
fastqc data/ERR688365.fastq -o Results/
```

### 2. Taxonomic Profiling ✓
```bash
metaphlan data/ERR688365.fastq --input_type fastq -o Results/metaphlan_result.tabular
```

### 3. Genome Assembly ✓
```bash
megahit --12 data/ERR688365.fastq -o Results/megahit_output
# Assembled contigs extracted to: Results/megahit_result.fasta
```

**Installation:**
```bash
sudo apt-get install megahit  # or compile from source
```

## Current Results

- FastQC quality report
- MetaPhlAn taxonomic composition  
- MEGAHIT assembled contigs (megahit_result.fasta)

Next: Gene prediction with GeneMarkS
