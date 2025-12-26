# Metagenomics Pipeline Analysis

## Pipeline Progress

### Completed Stages ✓
1. Quality Control (FastQC)
2. Taxonomic Profiling (MetaPhlAn)
3. Genome Assembly (MEGAHIT)
4. Gene Prediction (GeneMarkS)

### 5. Functional Annotation - Preparation
Selected representative predicted genes for BLAST analysis:
- Created `Results/blastx_inputs.fasta` with query sequences

Due to computational cost, not all predicted genes are queried against BLAST databases. Representative sequences selected based on length and uniqueness.

## Next Steps

Run BLASTX to assign functional annotations:
```bash
blastx -query Results/blastx_inputs.fasta -db nr -out Results/blastx_results.txt -outfmt 6
```

Note: BLAST searches can be time-consuming. Consider using remote BLAST (-remote flag) or local database.
