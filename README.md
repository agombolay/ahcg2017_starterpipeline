# Applied Human Computational Genomics 2017

Author: Alli Gombolay  
About: 3rd year PhD student,Bioinformatics  
Hobbies: Learning new programming languages!

## GitHub
* [Fork a repository](https://help.github.com/articles/fork-a-repo/)
  * A fork is a copy of a repository

## Markdown Syntax
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

## Mission Statement
To create robust and validated computational pipelines to detect cancer before symptoms become apparent.

## Liquid Biopsy Companies
* [GRAIL](https://grail.com/science/)
* **Liquid biopsy**:  
In contrast to solid biopsies, liquid biopsies is a non-invasive method to detect the presence of small fragments of tumor DNA, known as circulating tumor DNA (ctDNA). ctDNA originates from somatic mutations that occur in the tumor over the course of an individual's life unlike germline mutations that are present in all cells.

## Applied Human Computational Genomics Pipeline
**Purpose**: Call variants in genomic data to detect somatic changes within the pool of circulating nucleic acids

### Requirements
1. [Python3, Version 3.6.2](https://www.python.org/downloads/)
2. Variant calling tools: [GATK, Version 3.8.0](https://software.broadinstitute.org/gatk/download/)
3. Reference-based read aligner: [Bowtie2, Version 2.3.2](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml)
4. Read trimming based on quality: [Trimmomatic, Version 0.36](http://www.usadellab.org/cms/?page=trimmomatic)
5. Manipulation of genomic data files: [Picard tools, Version 2.11.0](http://broadinstitute.github.io/picard/)
