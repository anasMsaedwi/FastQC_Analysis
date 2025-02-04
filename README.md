# FastQC_Analysis
📝 Description: This repository provides scripts and documentation for FastQC, a quality control tool for high-throughput sequencing data. It includes installation instructions, usage examples, automation scripts, and troubleshooting tips to help analyze and interpret sequencing quality.


# 🧬 FastQC_Analysis: Quality Control for High-Throughput Sequencing Data  

This repository provides scripts and documentation for **FastQC**, a quality control tool for high-throughput sequencing data. It includes installation instructions, usage examples, automation scripts, and troubleshooting tips to help analyze and interpret sequencing quality.  

---

## 🚀 Installation  

### 🔹 Install FastQC on Linux/macOS  
```bash
# Install via Conda (recommended)
conda install -c bioconda fastqc

# OR download and install manually
wget https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.12.1.zip
unzip fastqc_v0.12.1.zip
chmod +x FastQC/fastqc
export PATH=$PWD/FastQC:$PATH  # Add FastQC to PATH
```

### 🔹 Install FastQC on Windows  
- Download from [FastQC Official Website](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/).  
- Run using **Git Bash, WSL, or a Linux Subsystem**.  

---

## 📊 Running FastQC  

### 🔹 Run FastQC on a Single File  
```bash
fastqc sample.fastq.gz
```

### 🔹 Run FastQC on Multiple Files  
```bash
fastqc *.fastq.gz
```

### 🔹 Specify an Output Directory  
```bash
fastqc sample.fastq.gz -o fastqc_results/
```

---

## 📈 Interpreting FastQC Reports  

FastQC generates an **HTML report** with key metrics:  

| **Module** | **Description** | **What to Check** |
|------------|---------------|------------------|
| **Per Base Sequence Quality** | Boxplots of quality scores | Should be high (>30) |
| **Per Sequence Quality Scores** | Distribution of mean scores per read | Should be normally distributed |
| **Per Base Sequence Content** | GC content across positions | Should be relatively stable |
| **Per Base N Content** | Proportion of ambiguous bases (N) | Should be low (near 0%) |
| **Sequence Duplication Levels** | % of duplicate reads | High duplication may indicate bias |
| **Overrepresented Sequences** | Repetitive sequences present | May indicate adapter contamination |
| **K-mer Content** | Overrepresented k-mers | Can indicate technical bias |

---

## 🔄 Automating FastQC with a Bash Script  

```bash
#!/bin/bash
mkdir -p fastqc_results
for file in *.fastq.gz; do
    fastqc "$file" -o fastqc_results/
done
echo "FastQC analysis completed!"
```

Save as `run_fastqc.sh`, then:  
```bash
chmod +x run_fastqc.sh
./run_fastqc.sh
```

---

## 📦 Extracting FastQC Data  

To extract and check summary statistics:  
```bash
unzip fastqc_results/sample_fastqc.zip -d fastqc_results/
cat fastqc_results/sample_fastqc/summary.txt
```

---

## 🛠 Troubleshooting  

| **Issue** | **Solution** |
|-----------|-------------|
| `command not found: fastqc` | Ensure FastQC is installed and in `PATH` |
| `Error: No .fastq.gz files found!` | Check filenames and file paths |
| `Low per-base quality` | Trim low-quality reads using `Trimmomatic` or `Cutadapt` |
| `High sequence duplication` | Check for **PCR bias** or **over-sequencing** |

---

## ✂ Trimming Reads with Trimmomatic  

```bash
trimmomatic PE -phred33 input_R1.fastq.gz input_R2.fastq.gz \
output_R1_trimmed.fastq.gz output_R1_unpaired.fastq.gz \
output_R2_trimmed.fastq.gz output_R2_unpaired.fastq.gz \
ILLUMINACLIP:adapters.fa:2:30:10 SLIDINGWINDOW:4:20 MINLEN:36
```

Rerun FastQC after trimming.

---

## 🔗 Useful Links  
- 📜 **[FastQC Documentation](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)**  
- 📘 **[FastQC on Bioconda](https://anaconda.org/bioconda/fastqc)**  
- 🛠 **[Trimmomatic for Read Trimming](http://www.usadellab.org/cms/?page=trimmomatic)**  

---

🚀 **Now you're ready to analyze sequencing quality with FastQC!**  
