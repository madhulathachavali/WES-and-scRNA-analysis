# WES-and-scRNA-analysis

1. Whole-Exome Sequencing (WES) Pipeline
This pipeline involves processing raw sequencing data to identify genomic variants.

Step 1: Prepare Tools

bwa (alignment)
Samtools (manipulate alignment files)
GATK (variant calling)
Picard (remove duplicates)
VCFtools or bcftools (variant filtering and manipulation)

Based on the content of GSM4286769_ABZM0327.txt, the file appears to be a gene expression matrix, where:

Rows represent genes (e.g., 1/2-SBSRNA4, 5S_rRNA, etc.).
Columns represent samples (e.g., WZM0165001, WZM0165002, etc.).
