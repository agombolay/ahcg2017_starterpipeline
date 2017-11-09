## What is liquid biopsy?  
In contrast to a solid biopsy, a liquid biopsy is a non-invasive method that detects the presence of circulating tumor DNA (ctDNA). ctDNA originates from somatic mutations that occur in the tumor over the course of an individual's life unlike germline mutations that are present in all cells. [GRAIL](https://grail.com/science/) and [Guardant Health](http://www.guardanthealth.com/) are two healthcare companies that harness the power of next-generation sequencing and liquid biopsies to detect cancer before symptoms arise.

## Variant Calling Pipelines
* [MuSE](http://bioinformatics.mdanderson.org/main/MuSE), [LoFreq](http://csb5.github.io/lofreq/), [VarScan](http://varscan.sourceforge.net/), [MuTect2](https://software.broadinstitute.org/gatk/documentation/tooldocs/current/org_broadinstitute_gatk_tools_walkers_cancer_m2_MuTect2.php), [SomaticSniper](http://gmt.genome.wustl.edu/packages/somatic-sniper/), and [GDC DNA-Seq](https://docs.gdc.cancer.gov/Data/Bioinformatics_Pipelines/DNA_Seq_Variant_Calling_Pipeline/)

## [Sequencing Coverage Calculator](http://support.illumina.com/downloads/sequencing_coverage_calculator.html)
* Calculate coverage needed to accurately detect somatic mutations
* Liquid biopsies require a much higher level of coverage than solid biopsies
  * We need orders of magnitude higher than standard 900-1100X coverage
  
## Types of alterations in liquid biopsies
1. **Epigenetic modifications**: Bisulfite sequencing to detect methylation
2. **Single nucleotide variants (SNV's)**: Variation in nucleotide that can be present in somatic cells
3. **Copy number alterations (CNA's)**: Changes in copy number of genes present in somatic tissue
