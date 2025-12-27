# Metagenomics Pipeline Analysis

## Pipeline Progress

### 1. Quality Control ✓
FastQC quality assessment completed.

### 2. Taxonomic Profiling ✓  
MetaPhlAn taxonomic composition analysis completed.

### 3. Genome Assembly ✓
MEGAHIT de novo assembly completed.

### 4. Gene Prediction ✓
```bash
gmhmmp -m MetaGeneMark_v1.mod Results/megahit_result.fasta -o Results/gmhmmp.out.txt
```

**Outputs:**
- `gmhmmp.20240724.053709.682348.gmhmmp.out.txt` - GeneMarkS predictions
- `gmhmmp.20240724.053709.682348.gmhmmp.out.fnn.txt` - Gene sequences (nucleotides)
- `gmhmmp.20240724.053709.682348.gmhmmp.out.faa.txt` - Protein sequences (amino acids)

**Installation:**
GeneMarkS requires free academic license from http://exon.gatech.edu/GeneMark/

## Results Summary

- Quality control: FastQC report
- Taxonomy: MetaPhlAn results (tabular + Excel)
- Assembly: MEGAHIT contigs
- Genes: Predicted coding sequences and proteins

Next: Functional annotation with BLAST
