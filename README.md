# eMAGMA-TUTORIAL

This tutorial is a step by step guide on how to use eMAGMA, an approach to conducting eQTL informed gene-based tests by assigning SNPs to tissue-specific eGenes as presented in Gerring et al., 2019a, Gerring et al., 2019b. Here we provide the scripts and files to use the eMAGMA methodology which generates a list of disease-associated eGenes using genome-wide summary statistics. In this tutorial, we will show how to apply eMAGMA using GWAS summary statistics of Major Depression Disorder (MDD) as example data; these summary statistics are publicly available from the Psychiatric Genomic Consortium (PGC) website.

The tutorial is divided into two parts. Part 1 conducts eMAGMA gene-based analysis, this analysis integrates SNP-gene associations from an eQTL reference dataset with GWAS summary statistics. We generated annotation files in which SNPs are assigned to genes based on their association with gene expression.   The SNP-gene associations are tissue specific; hence we can estimate what genes are more highly associated with a disease at the tissue level. Part 2 conducts eMAGMA gene-set analysis, testing for the enrichment of association in co-expression networks. The aim of this analysis is to identify modules (sets of highly correlated genes) that are highly associated with disease risk. Tissue-specific annotation files and co-expression network files (for 48 tissues) are shared as part of this tutorial.   Explanation of the methods and resources used in this tutorial are provided in the publication accompanying this tutorial, Gerring et al., 2009a.


**Requirements** 

This tutorial is executable in Unix, it is assumed that users are familiar with the Unix environment and command line. You can type or copy paste the commands or re-structure them as you wish. This is a hands-on tutorial with minimum theoretical explanations. It is essential that the user reads through the publications that accompany the tutorial (Gerring et al. 2019a, Gerring et al., 2019b) as they provide the theoretical background for the analyses. Knowledge of GWAS and GWA-summary analysis is required. We have previously generated a tutorial on the execution of GWAS analysis through another Github  repository https://github.com/MareesAT/GWA_tutorial (Marees et al., 2018).

*************************************



**Setting Up**


Start by creating an eMAGMA folder with all the files we will use throughout the tutorial.
       
       cd /path/to-yourworking folder
        mkdir eMAGMA
        cd eMAGMA
        
The analysis is done using MAGMA v1.07b (de Leeuw, Neale, Heskes, & Posthuma, 2016). MAGMA and auxiliary files can be downloaded from the program website: https://ctg.cncr.nl/software/magma. Two auxiliary files are required: a file with gene locations for protein-coding genes from NCBI and a genome reference file. For this tutorial we use build 37(hg19) that matches the build of the summary data (MDD2018_excluding23andMe) and the reference file for the European population. Gene location files for build 36, 37, & 38 are available from the MAGMA website. You can use wget o curl to import the files directly into your directory, for example:



*MAGMA*
    
    wget https:// https://ctg.cncr.nl/software/MAGMA/prog/magma_v1.07b_static.zip

*Auxiliary files for 37(hg19)*
        
    wget https://ctg.cncr.nl/software/MAGMA/aux_files/NCBI37.3.zip

*Reference data*
    
    wget https://ctg.cncr.nl/software/MAGMA/ref_data/g1000_eur.zip

*GWAS summary = MDD2018_ex23andMe from PGC web site*
        
     https://www.med.unc.edu/pgc/results-and-downloads/
        
        

Notice: If you are using your own data, make sure to download the auxiliary files that correspond to the genome build of your data.

This tutorial provides gene annotation and co-expression networks for 48 tissues, including 13 brain tissues and whole blood. At the end of the tutorial you will be able to apply the eMAGMA approach to your own data using these files.



****************************************************
**LIST OF FILES SHARED WITH THIS TUTORIAL:**



**eMAGMA Annotation files for 48 tissues:**

**Batch1.annotation:**
*Brain_Amygdala.genes.annot, Brain_Hippocampus.genes.annot, Brain_Anterior_cingulate_cortex_BA24.genes.annot, Brain_Hypothalamus.genes.annot, Brain_Caudate_basal_ganglia.genes.annot, Brain_Nucleus_accumbens_basal_ganglia.genes.annot
Brain_Cerebellar_Hemisphere.genes.annot, Brain_Putamen_basal_ganglia.genes.annot, Brain_Cerebellum.genes.annot                     Brain_Spinal_cord_cervical_c-1.genes.annot, Brain_Cortex.genes.annot, Brain_Substantia_nigra.genes.annot, Brain_Frontal_Cortex_BA9.genes.annot.*

 **Batch2.annotation:**
*Adipose_Subcutaneous.genes.annot, Artery_Aorta.genes.annot, Breast_Mammary_Tissue.genes.annot, Adipose_Visceral_Omentum.genes.annot, Artery_Coronary.genes.annot, Adrenal_Gland.genes.annot, Artery_Tibial.genes.annot.*


 **Batch3.annotation:**
*Cells_EBV-transformed_lymphocytes.genes.annot, Esophagus_Gastroesophageal_Junction.genes.annot, Cells_Transformed_fibroblasts.genes.annot, Esophagus_Mucosa.genes.annot, Colon_Sigmoid.genes.annot, Esophagus_Muscularis.genes.annot
Colon_Transverse.genes.annot.*


 **Batch4.annotation:**
*Heart_Atrial_Appendage.genes.annot, Liver.genes.annot, Minor_Salivary_Gland.genes.annot, Nerve_Tibial.genes.annot, Heart_Left_Ventricle.genes.annot, Lung.genes.annot, Muscle_Skeletal.genes.annot.*

 **Batch5.annotation:**
*Pancreas.genes.annot, Skin_Not_Sun_Exposed_Suprapubic.genes.annot, Spleen.genes.annot, Pituitary.genes.annot, Skin_Sun_Exposed_Lower_leg.genes.annot, Stomach.genes.annot, Prostate.genes.annot, Small_Intestine_Terminal_Ileum.genes.annot.*

 **Batch6.annotation:**
*Ovary.genes.annot, Testis.genes.annot, Thyroid.genes.annot  Uterus.genes.annot, Vagina.genes.annot, Whole_Blood.genes.annot.*


**eMAGMA Co-expression network files for 48 tissues:**

 **network_files.zip:**
*Adipose_Subcutaneous_entrez_gtex_v7_normalised.txt
Adipose_Visceral_Omentum_entrez_gtex_v7_normalised.txt
Adrenal_Gland_entrez_gtex_v7_normalised.txt
Artery_Aorta_entrez_gtex_v7_normalised.txt
Artery_Coronary_entrez_gtex_v7_normalised.txt
Artery_Tibial_entrez_gtex_v7_normalised.txt
Brain_Amygdala_entrez_gtex_v7_normalised.txt
Brain_Anterior_cingulate_cortex_BA24_entrez_gtex_v7_normalised.txt
Brain_Caudate_basal_ganglia_entrez_gtex_v7_normalised.txt
Brain_Cerebellar_Hemisphere_entrez_gtex_v7_normalised.txt
Brain_Cerebellum_entrez_gtex_v7_normalised.txt
Brain_Cortex_entrez_gtex_v7_normalised.txt
Brain_Frontal_Cortex_BA9_entrez_gtex_v7_normalised.txt
Brain_Hippocampus_entrez_gtex_v7_normalised.txt
Brain_Hypothalamus_entrez_gtex_v7_normalised.txt
Brain_Nucleus_accumbens_basal_ganglia_entrez_gtex_v7_normalised.txt
Brain_Putamen_basal_ganglia_entrez_gtex_v7_normalised.txt
Brain_Spinal_cord_cervical_c-1_entrez_gtex_v7_normalised.txt
Brain_Substantia_nigra_entrez_gtex_v7_normalised.txt
Breast_Mammary_Tissue_entrez_gtex_v7_normalised.txt
Cells_EBV-transformed_lymphocytes_entrez_gtex_v7_normalised.txt
Cells_Transformed_fibroblasts_entrez_gtex_v7_normalised.txt
Colon_Sigmoid_entrez_gtex_v7_normalised.txt
Colon_Transverse_entrez_gtex_v7_normalised.txt
Esophagus_Gastroesophageal_Junction_entrez_gtex_v7_normalised.txt
Esophagus_Mucosa_entrez_gtex_v7_normalised.txt
Esophagus_Muscularis_entrez_gtex_v7_normalised.txt
Heart_Atrial_Appendage_entrez_gtex_v7_normalised.txt
Heart_Left_Ventricle_entrez_gtex_v7_normalised.txt
Liver_entrez_gtex_v7_normalised.txt
Lung_entrez_gtex_v7_normalised.txt
Minor_Salivary_Gland_entrez_gtex_v7_normalised.txt
Muscle_Skeletal_entrez_gtex_v7_normalised.txt
Nerve_Tibial_entrez_gtex_v7_normalised.txt
Ovary_entrez_gtex_v7_normalised.txt
Pancreas_entrez_gtex_v7_normalised.txt
Pituitary_entrez_gtex_v7_normalised.txt
Prostate_entrez_gtex_v7_normalised.txt
Skin_Not_Sun_Exposed_Suprapubic_entrez_gtex_v7_normalised.txt
Skin_Sun_Exposed_Lower_leg_entrez_gtex_v7_normalised.txt
Small_Intestine_Terminal_Ileum_entrez_gtex_v7_normalised.txt
Spleen_entrez_gtex_v7_normalised.txt
Stomach_entrez_gtex_v7_normalised.txt
Testis_entrez_gtex_v7_normalised.txt
Thyroid_entrez_gtex_v7_normalised.txt
Uterus_entrez_gtex_v7_normalised.txt
Vagina_entrez_gtex_v7_normalised.txt
Whole_Blood_entrez_gtex_v7_normalised.txt*



**Tutorial Output files:**

 **Amygdala_outputs:**
 *Amygdala_emagma.genes.out,
Amygdala_emagma.genes.raw,
Amygdala_emagma.gsa.out,
Amygdala_emagma.log,
Amygdala_signif_genes.txt.*

*************************************



**References**

**a** Zachary F Gerring, Angela Mina-Vargas, Nicholas G Martin2, Eric R Gamazon3-5, Eske M Derks. eMAGMA: An eQTL-informed method to identify risk genes using genome-wide association study summary statistics. doi: https://doi.org/10.1101/854315.

**b** Gerring ZF, Gamazon ER, Derks EM, for the Major Depressive Disorder Working Group of the Psychiatric Genomics Consortium (2019) A gene co-expression network-based analysis of multiple brain tissues reveals novel genes and molecular pathways underlying major depression. PLOS Genetics 15(7): e1008245. https://doi.org/10.1371/journal.pgen.1008245

Marees, AT, de Kluiver, H, Stringer, S, et al. A tutorial on conducting genome‐wide association studies: Quality control and statistical analysis. Int J Methods Psychiatr Res. 2018; 27:e1608. https://doi.org/10.1002/mpr.1608

de Leeuw C, Mooij J, Heskes T, Posthuma D (2015): MAGMA: Generalized gene-set analysis of GWAS data. PLoS Comput Biol 11(4): e1004219. doi:10.1371/journal.pcbi.1004219 
