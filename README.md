# Applied Human Computational Genomics 2017

Author: Alli Gombolay  
About: 3rd year PhD student,Bioinformatics  
Hobbies: Learning new programming languages!

## Mission Statement
To create robust and validated computational pipelines to detect cancer before symptoms become apparent.  
Dr. Vannberg's idea for mission statement: Create a yearly non-invasive preventive test for cancer to save lives

## Liquid Biopsy Companies
* [GRAIL](https://grail.com/science/)
* [Guardant Health](http://www.guardanthealth.com/)

* **What is liquid biopsy?**  
In contrast to solid biopsies, liquid biopsies is a non-invasive method to detect the presence of small fragments of tumor DNA, known as circulating tumor DNA (ctDNA). ctDNA originates from somatic mutations that occur in the tumor over the course of an individual's life unlike germline mutations that are present in all cells.

## Types of alterations in liquid biopsies
1. **Epigenetic modifications**: Bisulfite sequencing to detect methylation
2. **Single nucleotide variants (SNV's)**: Variation in nucleotide that can be present in somatic cells
3. **Copy number alterations (CNA's)**: Changes in copy number of genes present in somatic tissue

## [Illumina Sequencing Coverage Calculator](http://support.illumina.com/downloads/sequencing_coverage_calculator.html)
* Calculate coverage needed to accurately detect somatic mutations
* Liquid biopsies require a much higher level of coverage than solid biopsies
  * We need orders of magnitude higher than standard 900-1100X coverage

## Examples of Variant Calling Pipelines
* [MuSE](http://bioinformatics.mdanderson.org/main/MuSE), [LoFreq](http://csb5.github.io/lofreq/), [VarScan](http://varscan.sourceforge.net/), [MuTect2](https://software.broadinstitute.org/gatk/documentation/tooldocs/current/org_broadinstitute_gatk_tools_walkers_cancer_m2_MuTect2.php), [SomaticSniper](http://gmt.genome.wustl.edu/packages/somatic-sniper/), and [GDC DNA-Seq](https://docs.gdc.cancer.gov/Data/Bioinformatics_Pipelines/DNA_Seq_Variant_Calling_Pipeline/)

## Applied Human Computational Genomics Pipeline
**Purpose**: Call variants in genomic data to detect somatic changes within the pool of circulating nucleic acids

### Requirements
1. [Python3, Version 3.6.2](https://www.python.org/downloads/)
2. Variant calling tools: [GATK, Version 3.8.0](https://software.broadinstitute.org/gatk/download/)
  * [Best practices with GATK's Haplotype Caller](https://software.broadinstitute.org/gatk/best-practices/bp_3step.php?case=GermShortWGS)
3. Reference-based read aligner: [Bowtie2, Version 2.3.2](https://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.3.2/bowtie2-2.3.2-legacy-linux-x86_64.zip/download)
4. Read trimming based on quality: [Trimmomatic, Version 0.36](http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.36.zip)
5. Manipulation of genomic data files: [Picard tools, Version 2.11.0](http://broadinstitute.github.io/picard/)

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
* [Frampton et al, Nat Biotech 2013](http://www.nature.com/nbt/journal/v31/n11/full/nbt.2696.html?foxtrotcallback=true)
* [SRA (Short Read Archive) Toolkit: NCBI's toolkit to convert SRA files to Fastq](https://www.ncbi.nlm.nih.gov/sra/docs/toolkitsoft/)
* [SRR948994, 1 : 4 pool of tumor (NCI-H2126) and matched normal (NCI-H2126 BL) cell line DNA](https://www.ncbi.nlm.nih.gov/sra/SRX332536[accn])

### Install Virtual Box
* [PDF with installation instructions](https://github.com/agombolay/ahcg2017_starterpipeline/blob/master/VM_setup.pdf)

### Command to run pipeline
python ahcg_pipeline.py -i /path/to/FASTQ1 /path/to/FASTQ2 -o /path/to/output -p /path/to/picard.jar  
-g /path/to/GenomeAnalysisTK.jar -b /path/to/bowtie2 -w /path/to/genome.bt2 -r /path/to/genome.fa  
-d /path/to/genome.vcf -t /path/to/trimmomatic-0.36.jar -a /path/to/adapters.fa -o /path/to/output

### Extract regions of interest from BAM file
```
samtools view input.bam "Chr10:18000-45500" > output.bam
```

### Determine sequencing coverage of genome
```
bedtools genomecov -d -ibam input.bam -g genome.bed > output.bed
```

### Obtain exon coordinates using UCSC genome browser
* [Step-by-step instructions to download list of exon coordinates](https://github.com/agombolay/ahcg2017_starterpipeline/blob/master/transcript08.pdf)

### Filter variants by quality, depth of coverage, & type of mutation
* [SnpSift and SnpEff toolbox to filter and manipulate annotated VCF files](http://snpeff.sourceforge.net/SnpSift.html)

## Miscellaneous: Using GitHub
* [Fork a repository](https://help.github.com/articles/fork-a-repo/)
  * A fork is a copy of a repository

* [Reference for Markdown syntax](https://guides.github.com/features/mastering-markdown/)

Examples:
* Header
```
# This is an <h1> tag
## This is an <h2> tag
```
* Emphasis
```
*This text will be italic*
**This text will be bold**
```
* List
```
* Item 1
  * Item 1a
```
