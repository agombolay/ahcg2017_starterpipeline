# Applied Human Computational Genomics 2017

Author: Alli Gombolay  
About: 3rd year PhD student,Bioinformatics  
Hobbies: Learning new programming languages!

## Mission Statement
To create an affordable non-invasive preventive medical test to detect cancer before symptoms become apparent

Our project involves exome sequencing with 200-250X coverage. The DNA will be derived from nanovesicles to yield high molecular DNA. The most updated version of the computational pipeline (version 1.0.5) can be found at this [link]( https://github.com/agombolay/ahcg2017_starterpipeline/blob/master/ahcg_pipeline.py).

## Applied Human Computational Genomics Pipeline
**Purpose**: Call variants in genomic data to detect somatic changes within the pool of circulating nucleic acids

### Requirements
1. [Python3, Version 3.6.2](https://www.python.org/downloads/)
2. [R language, Version 3.3.2](https://cran.cnr.berkeley.edu/)
3. Read quality trimming: [Trimmomatic, Version 0.36](http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.36.zip)
4. Reference-based read aligner: [Bowtie2, Version 2.3.2](https://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.3.2/bowtie2-2.3.2-legacy-linux-x86_64.zip/download)
5. Process SAM/BAM alignment files: [Samtools, Version 1.6](https://downloads.sourceforge.net/project/samtools/samtools/1.6/samtools-1.6.tar.bz2?r=https%3A%2F%2Fsourceforge.net%2Fprojects%2Fsamtools%2F&ts=1510018121&use_mirror=phoenixnap)
6. Detect variants with HaplotypeCaller: [GATK, Version 3.8.0](https://software.broadinstitute.org/gatk/download/)
7. Manipulate genomic data files: [Picard tools, Version 2.11.0](http://broadinstitute.github.io/picard/)
8. Detect copy-number changes: [Control-FREEC, Version 11.0](https://github.com/BoevaLab/FREEC/archive/v11.0.tar.gz)

### Reference genome
* Download human reference genome (GRCh38) from [Illumina iGenomes](https://support.illumina.com/sequencing/sequencing_software/igenome.html)

```
#Create FASTA index file
samtools faidx reference.fa
```

```
#Create FASTA dictionary file
#Note: Version 1.8 of Java is required to run Picard
java -jar picard.jar CreateSequenceDictionary R=reference O=dictionary
```

### Data Acquisition
* [SRA (Short Read Archive) Toolkit: NCBI's toolkit to convert SRA files to Fastq](https://www.ncbi.nlm.nih.gov/sra/docs/toolkitsoft/)

#### Test Dataset 1
* [SRR948994, NCI-H2126 20](https://www.ncbi.nlm.nih.gov/sra/SRX332536[accn])
* [Frampton et al, Nat Biotech 2013](http://www.nature.com/nbt/journal/v31/n11/full/nbt.2696.html?foxtrotcallback=true)

#### Test Dataset 2
* [SRR3502999, 1day-1-CTR15](https://www.ncbi.nlm.nih.gov/sra/SRR3502999/)
* [Newman et al, Nat Biotech 2016](https://www.nature.com/nbt/journal/v34/n5/abs/nbt.3520.html)

### Command to run pipeline
python ahcg_pipeline.py -i /path/to/FASTQ1 /path/to/FASTQ2 -o /path/to/output -p /path/to/picard.jar \  
-g /path/to/GenomeAnalysisTK.jar -b /path/to/bowtie2 -w /path/to/genome.bt2 -r /path/to/genome.fa \  
-d /path/to/genome.vcf -t /path/to/trimmomatic-0.36.jar -a /path/to/adapters.fa -o /path/to/output \  
-s /path/to/guardant360.refGene_hg38.genes.bed

### Features of pipeline
* Filters variants by quality and depth
* Calculates median and max coverage  

### Per base sequencing coverage of genome
```
samtools depth -r CHR1:1000-2000 input.bam > output.bed
```

### Obtain exon coordinates using UCSC genome browser
* [Step-by-step instructions to download list of exon coordinates](https://github.com/agombolay/ahcg2017_starterpipeline/blob/master/transcript08.pdf)

### Filter variants by quality and depth of sequencing coverage
* [GATK SelectVariants to filter VCF files by QUAL >= 30 && DP >= 25](http://snpeff.sourceforge.net/SnpSift.html)

```
java -jar GenomeAnalysisTK.jar -R FASTA -T SelectVariants -V input.vcf -o output.vcf -select "QUAL >= 30 && DP >= 25"
```
