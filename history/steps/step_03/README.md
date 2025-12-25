# Metagenomics Pipeline Analysis

## Description

This project performs metagenomic sequencing data analysis using standard bioinformatics tools. The pipeline includes quality control, taxonomic profiling, genome assembly, gene prediction, and functional annotation.

## Tools

- FastQC - Quality control
- MetaPhlAn - Taxonomic profiling
- MEGAHIT - Genome assembly
- GeneMarkS - Gene prediction
- BLAST - Functional annotation

## Data

Input: `data/ERR688365.fastq` (220 MB, stored externally - see LARGE_FILES.md)

## Setup

### FastQC
```bash
sudo apt-get install fastqc  # or: brew install fastqc
```

### MetaPhlAn
```bash
pip install metaphlan
metaphlan --install  # Download marker gene database
```

## Pipeline Stages

### 1. Quality Control ✓
```bash
fastqc data/ERR688365.fastq -o Results/
```
**Output:** `Results/FastQC_on_data_1__Webpage.zip`

### 2. Taxonomic Profiling ✓
```bash
metaphlan data/ERR688365.fastq --input_type fastq -o Results/metaphlan_result.tabular
```
**Outputs:** 
- `Results/metaphlan_result.tabular`
- `Results/metaphlan.xlsx`

## Results

Quality control and taxonomic profiling completed. Assembly stage next.
