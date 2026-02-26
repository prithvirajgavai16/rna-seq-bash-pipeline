# RNA-seq Alignment Pipeline (Bash-based)

A simple, interactive RNA-seq analysis pipeline written in Bash for quality control, read trimming, and genome alignment.

This pipeline is designed for educational purposes and small-scale RNA-seq projects. It allows users to execute FastQC, Trimmomatic, and HISAT2 interactively from the command line. The pipeline allows users to provide custom Trimmomatic and HISAT2 commands, offering full flexibility in parameter selection. Both single-end and paired-end sequencing data are supported.
---

## Features

- Interactive command-line workflow
- Optional quality control using FastQC
- Optional read trimming using Trimmomatic
- Alignment using HISAT2
- BAM file generation using samtools
- Execution time tracking
- Flexible command execution via user input

---

## Dependencies

The following tools must be installed:

- FastQC
- Trimmomatic (Java-based)
- HISAT2
- samtools
- Java (>= 8)
- Bash (Linux environment)

Example installation on Ubuntu:

```bash
sudo apt update
sudo apt install fastqc hisat2 samtools trimmomatic default-jre
```

---

##  Project Structure

```
RNA_seq_pipeline/
│
├── script/
│   └── rna_seq_pipeline.sh
│
├── Data/               # Input FASTQ files
├── Results/            # Output files (FastQC, BAM, etc.)
│
└── README.md
```

---

## Usage

1. Make the script executable:

```bash
chmod +x script/rna_seq_pipeline.sh
```

2. Run the pipeline:

```bash
./script/rna_seq_pipeline.sh
```

3. Follow interactive prompts:
   - Enter working directory
   - Provide FASTQ file path
   - Choose which steps to run
   - Enter full commands for Trimmomatic and HISAT2 when prompted

---

## Example Commands

### Example Trimmomatic (Single-End)

```bash
java -jar /usr/share/java/trimmomatic-0.39.jar SE \
-threads 8 \
input.fastq \
output_trimmed.fastq \
ILLUMINACLIP:/usr/share/trimmomatic/TruSeq3-SE.fa:2:30:10 \
LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36
```

### Example HISAT2 Alignment

```bash
hisat2 -q --rna-strandness R \
-x /path/to/grch38_index \
-U output_trimmed.fastq \
| samtools sort -o aligned_reads.bam
```

---

##  Security Note

This pipeline uses `eval` to execute user-provided commands.  
Only use in trusted environments. Avoid running unverified commands.

---

##  Tested Environment

- Ubuntu 22.04 LTS
- Bash 5+
- Java 11+

---

## Future Improvements

- Add logging support
- Add argument-based CLI (non-interactive mode)
- Add featureCounts or StringTie
- Add MultiQC reporting
- Convert to Snakemake or Nextflow workflow

---

##  License

This project is licensed under the MIT License.

---

##  Author

Prithviraj
Bioinformatics / Computational Biology  
Year: 2026
