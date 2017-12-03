# Applied Human Computational Genomics 2017

Author: Alli Gombolay  
About: 3rd year PhD student,Bioinformatics  
Hobbies: Learning new programming languages!

Acknowledgements: Dr. Fredrik Vannberg and Cai Huang

## Mission Statement
To create an affordable non-invasive preventive medical test to detect cancer before symptoms become apparent

## Applied Human Computational Genomics Pipeline
The goal of this pipeline is to detect and evaluate somatic variants that might be indicative of early stage cancer.   
This pipeline was created by the 2017 AHCG class under the supervision of Dr. Fredrik Vannberg at Georgia Tech.

**Input of pipeline**: Exome sequencing data; **Output of pipeline**: VCF file of variants

The most current version of the pipeline (version 1.0.8) can be downloaded from this [link]( https://github.com/agombolay/ahcg2017_starterpipeline/blob/master/ahcg_pipeline.py).

**Note**: A virtual box with required software is accessible at ssh vannberglab@localhost -p 10022

### How to run pipeline
```
ahcg_pipeline_v1.0.1.py -c config_file.txt
```

### Main features of pipeline
* Takes configuration file of parameters as input
* Automatic project sample retrieving from SRA website
* Filters variants by quality (QUAL>=30) and depth (DP>=25)
* Calculates median, average, and max coverage of certain genes
* Detects copy number variants (CNVs) and plots summary results

## Requirements
### Programming Languages:
* [Python3, Version 3.6.2](https://www.python.org/downloads/)
* [R language, Version 3.3.2](https://cran.cnr.berkeley.edu/)

### Pre-processing and alignment:
* Read quality trimming: [Trimmomatic, Version 0.36](http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.36.zip)
* Reference-based read aligner: [Bowtie2, Version 2.3.2](https://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.3.2/bowtie2-2.3.2-legacy-linux-x86_64.zip/download)
* Process SAM/BAM alignment files: [Samtools, Version 1.6](https://downloads.sourceforge.net/project/samtools/samtools/1.6/samtools-1.6.tar.bz2?r=https%3A%2F%2Fsourceforge.net%2Fprojects%2Fsamtools%2F&ts=1510018121&use_mirror=phoenixnap)

### Call variants and post-processing:
* Manipulate genomic data files: [Picard tools, Version 2.11.0](http://broadinstitute.github.io/picard/)
* Detect variants with HaplotypeCaller: [GATK, Version 3.8.0](https://software.broadinstitute.org/gatk/download/)

### Analyze and evaluate somatic variants:
* Detect copy-number changes: [Control-FREEC, Version 11.0](https://github.com/BoevaLab/FREEC/archive/v11.0.tar.gz)

## Reference genome
### 1. Download reference genome
* Download reference genome from [Illumina iGenomes](https://support.illumina.com/sequencing/sequencing_software/igenome.html)
  * Species: *Homo sapiens*, Source: NCBI, Build: GRCh38

### 2. Prepare reference for pipeline
```
#Create FASTA index
samtools faidx FASTA

#Create FASTA dictionary file
#Note: Version 1.8 of Java is required to run Picard commands
java -jar picard.jar CreateSequenceDictionary R=FASTA O=dictionary
```

## Data Acquisition

### 1. Test Dataset 1
* [SRR1654210 (tumor exome data)](https://www.ncbi.nlm.nih.gov/sra/?term=SRR1654210)
* [SRR1654222 (germline exome data)](https://www.ncbi.nlm.nih.gov/sra/SRR1654222/)

### 2. Test Dataset 2
* [SRR948994](https://www.ncbi.nlm.nih.gov/sra/SRX332536[accn]); [Frampton et al, Nat Biotech 2013](http://www.nature.com/nbt/journal/v31/n11/full/nbt.2696.html?foxtrotcallback=true)

### 3. Test Dataset 3
* [SRR3502999](https://www.ncbi.nlm.nih.gov/sra/SRR3502999/); [Newman et al, Nat Biotech 2016](https://www.nature.com/nbt/journal/v34/n5/abs/nbt.3520.html)

## Exon coordinates
* [Step-by-step instructions to download list of exon coordinates](https://github.com/agombolay/ahcg2017_starterpipeline/blob/master/transcript08.pdf)
