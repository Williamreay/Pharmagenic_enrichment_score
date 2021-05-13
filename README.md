# Pharmagenic_enrichment_score
 Scripts to priortise gene-sets which could be used to calculate pharmagenic enrichment scores and sample scripts to calculate the scores using LD clumping and thresholding: see PMID: 31964963 and 33720009 for further details  
 
William Reay (william.reay@uon.edu.au)
 
## Overview

This repository contains scripts which will facilitate the following:
  i) Identification of candidate pathways targeted by known drugs which could        be used to construct pharmagenic enrichment scores
  ii) Filtering GWAS summary statistics such that variants specific to that          pathway are extracted
  iii) Generating pharmagenic enrichment scores using variants mapped to the          pathway of interest via LD clumping and thresholding
  
## Specifc usage

1. Define candidate druggable pathways enriched with common variant associations - PES_pathway_identification_v1.07.py

GWAS summary statistics are subjected to gene-set association with MAGMA (v1.07 and above) at four P value thresholds (P < 0.005, 0.05, 0.5, and 1) using PES_pathway_identification_v1.07.py. The MAGMA executable file (which can be obtained from https://ctg.cncr.nl/software/magma) must be in the same directory as this script. The specific commond line flags for this script can be viewed using the help flag. We provide a set of canonical and hallmark pathways from MSigDB that overlap with at least one druggable gene (Tclin, TCRD v 6.1.0) as described in Reay et al (PMID: 31964963 and 33720009).

Multiple testing-correction can be applied via FDR to the output of this script, which performs gene-set association at each threshold using the PES_candidate_gene_set_multiple_testing_correction.R script which combines the files and automatically excludes sets with less than 5 overlapping genes at that threshold.

2. Filter GWAS summary statistics for the variants mapped to the pathway of interest - Filter_pathway_variants.py

Using the Filter_pathway_variants.py script, users can input a gene location file (CHR, START, END, and STRAND) to extract the SNPs mapped to genes in that pathway using strand-sensitive upstream and downstream boundaries of the genic coordinates to capture regulatory variation.

3. Profile pharmagenic enrichment scores in individual genotype data using filtered summary statistics - PES_profile_generation.py

This script is a wrapper for the PRSice2 polygenic scoring package (https://www.prsice.info/) - this allows users to input their filtered summary statistics for the pathway they wish to generate a PES for and output a score after LD clumping and thresholding at a desired P value. This script currently only supports traditional plink binaries (.bed, .bim, .fam), however, this will be expanded to .bgen in future. By default this will calculate a PES averaged by the number of non-missing alleles per invidual, as is default in PRSice2. 

  
