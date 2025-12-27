# Metagenomics Pipeline Analysis

**Project Type:** University Project  
**Primary Stack:** Bioinformatics Tools

## Description

This is a metagenomics analysis project using various bioinformatics tools and pipelines. The project involves processing metagenomic sequencing data, performing taxonomic classification with MetaPhlAn, genome assembly with MEGAHIT, gene prediction with GeneMarkS, and functional annotation using BLAST.

## Tech Stack

- FastQC (quality control)
- MetaPhlAn (taxonomic profiling)
- MEGAHIT (genome assembly)
- GeneMarkS (gene prediction)
- BLAST / BLASTX (functional annotation)
- Python (for data processing)
- Shell scripts (pipeline automation)

## Folder Structure

```
metagenomics/
├── data/
│   └── ERR688365.fastq           # Input sequencing data
├── Results/                       # Analysis results
│   ├── FastQC_on_data_1__Webpage.zip
│   ├── metaphlan.xlsx             # MetaPhlAn taxonomic results
│   ├── metaphlan_result.tabular
│   ├── megahit_result.fasta       # Assembled contigs
│   ├── gmhmmp.*.faa.txt          # Predicted proteins
│   ├── gmhmmp.*.fnn.txt          # Predicted genes (nucleotides)
│   ├── blast_result.txt           # BLAST annotation results
│   ├── blast_result.json
│   ├── blastx_results.txt
│   └── blastx_inputs.fasta
├── report.docx                    # Project report
└── README.md                      # This file
```

## Setup / Installation

### Install Required Tools

1. **FastQC**:
```bash
# Ubuntu/Debian
sudo apt-get install fastqc

# macOS
brew install fastqc
```

2. **MetaPhlAn**:
```bash
pip install metaphlan
```

3. **MEGAHIT**:
```bash
# Ubuntu/Debian
sudo apt-get install megahit

# From source
git clone https://github.com/voutcn/megahit.git
cd megahit && make
```

4. **GeneMarkS**:
- Download from http://exon.gatech.edu/GeneMark/
- Requires free academic license

5. **BLAST+**:
```bash
# Ubuntu/Debian
sudo apt-get install ncbi-blast+

# macOS
brew install blast
```

## How to Run

The pipeline can be run step by step:

1. **Quality Control**:
```bash
cd metagenomics
fastqc data/ERR688365.fastq -o Results/
```

2. **Taxonomic Profiling**:
```bash
metaphlan data/ERR688365.fastq --input_type fastq -o Results/metaphlan_result.tabular
```

3. **Assembly**:
```bash
megahit --12 data/ERR688365.fastq -o Results/megahit_output
```

4. **Gene Prediction**:
```bash
gmhmmp -m MetaGeneMark_v1.mod Results/megahit_result.fasta -o Results/gmhmmp.out.txt
```

5. **Functional Annotation**:
```bash
blastx -query Results/blastx_inputs.fasta -db nr -out Results/blastx_results.txt -outfmt 6
```

## Inputs/Outputs

**Inputs:**
- `data/ERR688365.fastq` - Metagenomic sequencing reads in FASTQ format

**Outputs:**
- `Results/FastQC_on_data_1__Webpage.zip` - Quality control report
- `Results/metaphlan.xlsx` - Taxonomic composition
- `Results/megahit_result.fasta` - Assembled contigs
- `Results/gmhmmp.*.faa.txt` - Predicted protein sequences
- `Results/gmhmmp.*.fnn.txt` - Predicted gene sequences
- `Results/blast_result.txt` - Functional annotations
- `report.docx` - Comprehensive project report

## Notes

- This is a complete metagenomics analysis pipeline
- Tools should be installed and available in PATH
- BLAST searches can be time-consuming and may require remote database access
- All file paths are relative to the project directory
- Large result files are already generated in the Results/ directory
- MetaPhlAn requires database download on first run

## Troubleshooting

- If tools are not found, ensure they are installed and in PATH: `which fastqc`
- For MetaPhlAn database issues: `metaphlan --install`
- BLAST may require downloading databases: `update_blastdb.pl nr`
- If memory issues occur during assembly, reduce the dataset size or increase available RAM
- For GeneMarkS license issues, obtain a free academic license from the GeneMark website
