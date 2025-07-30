---
layout: post
tags: [UK Biobank, population genetics, rare variant association, manuscript editing, addressing reviewer comments]
permalink: inherited-blood-cancer-predisposition-through-altered-transcriptional-elongation
---

As part of efforts to validate rare variant associations identified in earlier analyses, I led the replication of gene-based association testing in the expanded UK Biobank (UKB) whole exome sequencing (WES) cohort comprising over 450,000 individuals. This analysis built upon prior findings and significantly increased statistical power. I re-processed and quality-controlled the population-level variant call format (pVCF) data, applying rigorous genotype- and sample-level filters in Hail, and restricting to rare variants (MAF < 1%) with high-confidence deleterious annotations. Variant effect prediction was performed using multiple tools including LOFTEE, ALoFT, and InMeRF, the latter chosen based on its superior performance in classifying pathogenic missense variants (AUROC = 0.83).

Phenotypes for myeloid malignancies were curated using ICD-10/ICD-9 codes, self-reported diagnoses, and cancer histology codes, and then combined into a unified "myeloid megaphenotype" to enhance power. I performed association testing using REGENIE v3.2.5 with a gene-based collapsing framework incorporating both loss-of-function and deleterious missense variants. Covariates included age, sex, ancestry PCs, and technical batch effects. Genes with a minor allele count ≥20 were included, and results were corrected for multiple testing using the Benjamini-Hochberg procedure (FDR < 0.05). These analyses enabled robust replication of key findings and extended the generalizability of rare variant signals across a much larger and more diverse UKB cohort.

[Publication](https://www.cell.com/cell/fulltext/S0092-8674(23)01348-X?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS009286742301348X%3Fshowall%3Dtrue)

