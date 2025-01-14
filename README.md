# WES-and-scRNA-analysis

 Whole-Exome Sequencing (WES) Pipeline
This pipeline involves processing raw sequencing data to identify genomic variants.

## Step 1: Setting Up the Environment

### 1.1 Install Necessary Tools
1. **Install SRA Toolkit**:
   - Download the [SRA Toolkit](https://github.com/ncbi/sra-tools/wiki/01.-Downloading-SRA-Toolkit) (version suitable MacOS x86-64 bit architecture)
   - Extract and move to `~/tools`:
     ```bash
     tar -xvf sratoolkit.<version>.mac-arm64.tar.gz
     mv sratoolkit.<version>.mac-arm64 ~/tools/sratoolkit
     ```
   - Add SRA Toolkit to your PATH:
     ```bash
     export PATH=~/tools/sratoolkit/bin:$PATH
     echo 'export PATH=~/tools/sratoolkit/bin:$PATH' >> ~/.zshrc
     source ~/.zshrc
     ```
   - Verify installation:
     ```bash
     prefetch --version
     fastq-dump --version
     ```
2. **Install Alignment and Variant Tools**:
  - Download the [Anaconda](https://www.anaconda.com/download/success)
   Use Conda to install the following tools:
   - `bwa` (alignment)
   - `samtools` (manipulate alignment files)
   - `gatk` (variant calling)
   - `picard` (remove duplicates)
   - `vcftools` or `bcftools` (variant filtering)
     
   ```bash
   conda create -n wes_analysis -c bioconda bwa samtools gatk picard vcftools
   conda activate wes_analysis
   ```

### Step 2. Organize Data and Directories
 ```bash
mkdir -p ~/Desktop/WES_Analysis/{raw_data,processed_data,metadata,scRNA-data}
 ```
## Step 3: Process and Organize scRNA-seq Data

### 3.1 Extract and Process scRNA Files

1. **Extract `.tar` file**:
   ```bash
   tar -xvf GSE144357_RAW.tar -C ~/Desktop/WES_Analysis/scRNA-data
 
2. Decompress .gz files:
   ```bash
   gunzip ~/Desktop/WES_Analysis/scRNA-data/*.gz
   
3. Organize .txt files:
   ```bash
   mkdir -p ~/Desktop/WES_Analysis/scRNA-data/processed
   mv ~/Desktop/WES_Analysis/scRNA-data/*.txt ~/Desktop/WES_Analysis/scRNA-data/processed/
   
###  3.2 Inspect Gene Expression Matrix
- The file GSM4286769_ABZM0327.txt represents a gene expression matrix:
- Rows: Genes (e.g., 1/2-SBSRNA4, 5S_rRNA).
- Columns: Samples (e.g., WZM0165001, WZM0165002).
  preview matrix
  ```bash
  head ~/Desktop/WES_Analysis/scRNA-data/processed/GSM4286769_ABZM0327.txt
  
## Step 4: Download and Convert SRA Files
### 4.1 Download SRA Files
- Download raw sequencing data for SRX7706871:
  ```bash
  prefetch SRX7706871
- The .sra file will be saved to:
  ```bash
  ~/ncbi/public/sra/SRR11060954.sra
### 4.2 Convert .sra to FASTQ
- Convert the .sra file into paired-end FASTQ files:
 ```bash
  fastq-dump --split-files ~/ncbi/public/sra/SRR11060954.sra
```

- Resulting FASTQ files:

- /Users/madhuchavali/Downloads/SRR11060954_1.fastq
- /Users/madhuchavali/Downloads/SRR11060954_2.fastq

- Move these files to raw_data:
```bash
mv ~/Downloads/*.fastq ~/Desktop/WES_Analysis/raw_data/
```



