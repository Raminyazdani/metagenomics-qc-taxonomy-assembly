# Metagenomics QC-Taxonomy-Assembly Pipeline

**End-to-end metagenomic sequencing analysis pipeline with quality control, taxonomic profiling, assembly, and functional annotation**

## Overview

This repository contains the results and documentation of a comprehensive bioinformatics pipeline for analyzing metagenomic sequencing data. The pipeline integrates industry-standard tools to process raw sequencing reads through multiple analysis stages, extracting taxonomic composition, assembled genomes, predicted genes, and functional annotations.

**Key Analysis Stages:**
- Quality control and read assessment (FastQC)
- Taxonomic profiling and community composition (MetaPhlAn)  
- De novo genome assembly (MEGAHIT)
- Gene prediction and protein coding sequence identification (GeneMarkS)
- Functional annotation via homology search (BLAST/BLASTX)

## Tech Stack

**Bioinformatics Tools:**
- **FastQC** - Quality control and read assessment
- **MetaPhlAn** - Taxonomic profiling and abundance estimation
- **MEGAHIT** - De novo metagenome assembly
- **GeneMarkS** - Gene prediction for prokaryotic genomes
- **BLAST/BLASTX** - Functional annotation via sequence homology

**Supporting Technologies:**
- Python (data processing and analysis)
- Shell scripting (pipeline orchestration)

## Repository Structure

This repository contains **pre-generated analysis results** from a complete metagenomics pipeline run:

```
metagenomics-qc-taxonomy-assembly/
├── Results/                         # All pipeline outputs
│   ├── FastQC_on_data_1__Webpage.zip
│   ├── metaphlan.xlsx              # Taxonomic composition (Excel)
│   ├── metaphlan_result.tabular    # Taxonomic composition (tabular)
│   ├── megahit_result.fasta        # Assembled contigs
│   ├── gmhmmp.*.faa.txt           # Predicted protein sequences
│   ├── gmhmmp.*.fnn.txt           # Predicted gene sequences (nucleotides)
│   ├── gmhmmp.*.txt               # GeneMarkS output
│   ├── blast_result.txt            # BLAST annotation results
│   ├── blast_result.json           # BLAST results (JSON format)
│   ├── blastx_results.txt          # BLASTX annotation results
│   └── blastx_inputs.fasta         # Query sequences for BLASTX
├── LARGE_FILES.md                   # External data file documentation
├── report.docx                      # Comprehensive analysis report
└── README.md                        # This file
```

**Note:** The input sequencing data file (`ERR688365.fastq`, 220 MB) is stored externally due to size constraints. See `LARGE_FILES.md` for access details.

## Pipeline Workflow

The analysis follows this sequential workflow:

### 1. Quality Control
```bash
fastqc data/ERR688365.fastq -o Results/
```
Assesses read quality, GC content, sequence duplication, and potential contamination.

### 2. Taxonomic Profiling
```bash
metaphlan data/ERR688365.fastq --input_type fastq -o Results/metaphlan_result.tabular
```
Identifies microbial composition and relative abundance using marker genes.

### 3. Genome Assembly
```bash
megahit --12 data/ERR688365.fastq -o Results/megahit_output
```
Performs de novo assembly to reconstruct longer genomic contigs from short reads.

### 4. Gene Prediction
```bash
gmhmmp -m MetaGeneMark_v1.mod Results/megahit_result.fasta -o Results/gmhmmp.out.txt
```
Identifies open reading frames and predicts protein-coding genes.

### 5. Functional Annotation
```bash
blastx -query Results/blastx_inputs.fasta -db nr -out Results/blastx_results.txt -outfmt 6
```
Assigns functional annotations by comparing predicted sequences against reference databases.

## Reproducibility

To reproduce this analysis with your own metagenomic data:

### Prerequisites

**System Requirements:**
- Linux or macOS (recommended)
- At least 8 GB RAM (16+ GB recommended for assembly)
- 50+ GB disk space for databases and results

**Required Tools:**

1. **FastQC** (v0.11.9+):
```bash
# Ubuntu/Debian
sudo apt-get install fastqc

# macOS
brew install fastqc
```

2. **MetaPhlAn** (v3.0+):
```bash
pip install metaphlan
metaphlan --install  # Download marker gene database (first run)
```

3. **MEGAHIT** (v1.2.9+):
```bash
# Ubuntu/Debian
sudo apt-get install megahit

# From source
git clone https://github.com/voutcn/megahit.git
cd megahit && make
```

4. **GeneMarkS** (for metagenomes):
- Download from http://exon.gatech.edu/GeneMark/
- Requires free academic license registration
- Install MetaGeneMark model file

5. **BLAST+** (v2.10.0+):
```bash
# Ubuntu/Debian
sudo apt-get install ncbi-blast+

# macOS
brew install blast

# Download nr database (optional, for functional annotation)
update_blastdb.pl nr
```

### Running the Pipeline

1. **Prepare your input data:**
   - Place FASTQ file(s) in a `data/` directory
   - Supported formats: FASTQ, FASTA (compressed or uncompressed)

2. **Execute pipeline stages** (run commands from repository root):
   - Follow the commands in the "Pipeline Workflow" section above
   - Adjust paths and parameters as needed for your dataset

3. **Review outputs:**
   - Quality reports: `Results/FastQC*.html`
   - Taxonomy: `Results/metaphlan_result.tabular`
   - Assembly: `Results/megahit_output/final.contigs.fa`
   - Genes: `Results/gmhmmp.*.faa.txt` and `*.fnn.txt`
   - Annotations: `Results/blastx_results.txt`

## Analysis Results

This repository contains results from analyzing the **ERR688365** metagenomic sample:

**Input Data:**
- Sample ID: ERR688365
- Format: FASTQ (single-end reads)
- Size: 220 MB (stored externally - see `LARGE_FILES.md`)
- Source: Public metagenomic dataset

**Generated Outputs:**

| Output Type | File(s) | Description |
|------------|---------|-------------|
| Quality Control | `FastQC_on_data_1__Webpage.zip` | HTML report with quality metrics |
| Taxonomic Profile | `metaphlan_result.tabular`, `metaphlan.xlsx` | Species-level abundance tables |
| Assembled Contigs | `megahit_result.fasta` | De novo assembled sequences |
| Predicted Genes | `gmhmmp.*.fnn.txt` | Nucleotide sequences of predicted genes |
| Predicted Proteins | `gmhmmp.*.faa.txt` | Amino acid sequences of predicted proteins |
| Functional Annotations | `blast_result.txt`, `blastx_results.txt` | Homology-based function assignments |
| Summary Report | `report.docx` | Comprehensive analysis documentation |

## Key Findings

The analysis revealed:
- Taxonomic composition of the microbial community
- Assembled genomic contigs for genome reconstruction
- Thousands of predicted protein-coding genes
- Functional annotations linking genes to biological processes

For detailed results and interpretation, see `report.docx`.

## Troubleshooting

**MetaPhlAn database not found:**
```bash
metaphlan --install
```

**BLAST database required:**
```bash
# For local BLAST searches
update_blastdb.pl nr
# Or use remote BLAST with: -remote flag
```

**Memory issues during assembly:**
- Reduce input dataset size
- Increase available RAM
- Use MEGAHIT's `--memory` flag to set limits

**GeneMarkS license:**
- Obtain free academic license from http://exon.gatech.edu/GeneMark/
- Place license key (`gm_key`) in home directory

**Tool not found errors:**
- Verify installation: `which <tool_name>`
- Add tool to PATH: `export PATH=$PATH:/path/to/tool`

## Citation & Acknowledgments

If you use this pipeline or results, please cite the respective tools:

- **FastQC**: Andrews, S. (2010). FastQC: A Quality Control Tool for High Throughput Sequence Data
- **MetaPhlAn**: Beghini et al. (2021). Integrating taxonomic, functional, and strain-level profiling of diverse microbial communities with bioBakery 3
- **MEGAHIT**: Li et al. (2015). MEGAHIT: an ultra-fast single-node solution for large and complex metagenomics assembly via succinct de Bruijn graph
- **GeneMarkS**: Besemer et al. (2001). GeneMarkS: a self-training method for prediction of gene starts in microbial genomes
- **BLAST**: Altschul et al. (1997). Gapped BLAST and PSI-BLAST: a new generation of protein database search programs

## License

This project is provided as-is for educational and research purposes. Individual tools retain their respective licenses.

