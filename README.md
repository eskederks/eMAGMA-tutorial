# eMAGMA-TUTORIAL

#This tutorial is a step by step guide on how to use eMAGMA, an approach to conducting eQTL informed gene-based tests by assigning SNPs to tissue-specific eGenes as presented in Gerrin et al., 2019ab. Here we provide the scripts and files to apply the eMAGMA approach which generates a list of disease-associated eGenes using genome-wide summary statistics. In this tutorial, we apply eMAGMA to GWAS summary statistics of Major Depression Disorder (MDD); these summary statistics are publicly available from the Psychiatric Genomic Consortium (PGC) website.

The tutorial is divided in two parts. Part 1 Runs eMAGMA gene-based analysis of proximity, this analysis integrates a SNP-gene association from GTEx to a GWAS summary data. SNPs (from the summary data) are assigned to genes based on their association with gene expression. The SNP-gene association from GTEx is a tissue specific annotation, hence we can estimate what genes are more highly associated with MDD at the tissue level. Part 2 runs eMAGMA gene-set it test the enrichment of association in co-expression networks. The aim is to identify modules (sets defined by highly correlated genes) that are highly associated with MDD risk.
Tissue-specific annotation files and Co-expression network files are freely provided with this tutorial. Explanation of the methods and resources used in this tutorial are provided in the publication accompanying this tutorial, Gerrin et al., 2009b


**Requirements** 

This tutorial is executable in Unix, it is assumed that users are familiar with the Unix environment and command line. You can type or copy paste the commands or re-structure them as you wish. This is a hands-on tutorial with minimum theoretical explanations. It is essential that the user reads through the publications that accompanies the tutorial (Gerring et al. 2019ab) as they provide the theoretical background for the analyses. Knowledge of GWAS and GWA-summary analysis is necessary. Maree’s repository https://github.com/MareesAT/GWA_tutorial offers a detailed guide on GWAS analysis.


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
        
        https://www.med.unc.edu/pgc/results-and-downloads/mdd/
        
        

Notice: If you are using your own data, make sure to download the auxiliary files that correspond to the genome build of your data.
This tutorial freely provides files for gene annotation and co-expression networks for 48 tissues. At the end of the tutorial you will be able to apply the eMAGMA approach to your own data using these files.



Notice: If you are using your own data, make sure to download the auxiliary files that correspond to the genome build of your data.





**eMAGMA Annotation files**

   *Batch1.annotation
   
   
       Brain_Amygdala.genes.annot                        Brain_Cortex.genes.annot                                                              Brain_Putamen_basal_ganglia.genes.annot
       Brain_Anterior_cingulate_cortex_BA24.genes.annot  Brain_Frontal_Cortex_BA9.genes.annot                                        
       Brain_Spinal_cord_cervical_c-1.genes.annot
       Brain_Caudate_basal_ganglia.genes.annot           Brain_Hippocampus.genes.annot                          
       Brain_Substantia_nigra.genes.annot
       Brain_Cerebellar_Hemisphere.genes.annot           Brain_Hypothalamus.genes.annot
       Brain_Cerebellum.genes.annot                      Brain_Nucleus_accumbens_basal_ganglia.genes.annot

   *Batch2.annotation*
   
   *Batch3.annotation*
   
   *Batch4.annotation*
   
   *Batch5.annotation*
 
 


**eMAGMA Co-expression network files**


   *network_files.zip*


**eMAGMA tutorial-Amygdala output file**


*************************************

Now that you have all the necessary files go to Part 1 to begin with the analysis.



