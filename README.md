# Applied Human Computational Genomics 2017

Author: Alli Gombolay  
About: 3rd year PhD student,Bioinformatics  
Hobbies: Learning new programming languages!

Acknowledgements: Dr. Fredrik Vannberg and Cai Huang

## Mission Statement
To create an affordable non-invasive preventive blood test to detect cancer before symptoms become apparent

## Applied Human Computational Genomics Pipeline
The goal of this pipeline is to detect and evaluate somatic variants that might be indicative of early stage cancer.   
This pipeline was created by the 2017 AHCG class under the supervision of Dr. Fredrik Vannberg at Georgia Tech.

* **Input of pipeline**: Exome sequencing data; **Output of pipeline**: VCF file of variants

* The most current version of the pipeline (version 1.0.8) can be downloaded from this [link]( https://github.com/agombolay/ahcg2017_starterpipeline/blob/master/ahcg_pipeline.py).

* **Note**: A virtual box with required software is accessible at ssh vannberglab@localhost -p 10022

### How to run pipeline
```
ahcg_pipeline_v1.0.1.py -c config_file.txt
```
Note: Version 1.8 of Java is required to run Picard

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

## Configuration file
### `[tools]` section

| Option        | Description                                                     |
|---------------|-----------------------------------------------------------------|
| `gatk`        | Path to GATK jar file                                           |
| `freec`       | Path to Control-FREEC                                           |
| `picard`      | Path to Picard Tools jar file                                   |
| `bowtie2`     | Path to Bowtie2 executable                                      |
| `samtools`    | Path to Samtools executable                                     |
| `makegraph`   | Path to `makeGraph.R` script                                    |
| `trimmomatic` | Path to Trimmomatic jar file                                    |  

### `[data]` section

| Option       | Description                                                      |
|--------------|------------------------------------------------------------------|
| `index`      | Path to Bowtie2 indices                                          |
| `outputdir`  | Path to the output directory                                     |
| `reference`  | Path to the reference genome fasta file                          |
| `inputfiles` | List of paired-end read files (comma sparated)                   |
| `dbsnp`      | Path to dbSNP vcf file of known variants for GATK                |
| `geneset`    | Path to BED of genes for which to calculate coverage metrics     |
| `adapters`   | Path to FASTA containing sequencing adapters for Trimmomatic     |
| `chrfiles`   | Path to directory with chromosome FASTA files for Control-FREEC  |
| `chrlenfile` | Path to files containing lengths of chromosomes for Control-FREEC|

## Reference genome
* Download reference genome from [Illumina iGenomes](https://support.illumina.com/sequencing/sequencing_software/igenome.html)
  * Species: *Homo sapiens*, Source: NCBI, Build: GRCh38
  * FASTA (.fa) and FASTA index reference files (.fai) are required
  * Sequence dictionary of FASTA is required (create using Picard)

## Build directory structure
```
mkdir -p data/reads data/reference data/adapters output 
```

## Test Dataset
* [SRR1654210 (tumor exome data)](https://www.ncbi.nlm.nih.gov/sra/?term=SRR1654210)
* [SRR1654222 (germline exome data)](https://www.ncbi.nlm.nih.gov/sra/SRR1654222/)

## Exon coordinates
* [Step-by-step instructions to download list of exon coordinates](https://github.com/agombolay/ahcg2017_starterpipeline/blob/master/transcript08.pdf)
