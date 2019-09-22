# eMAGMA-TUTORIAL

#This tutorial is a step by step guide on how to use eMAGMA, an approach to assign SNPs to tissue specific genes as presented in xxref(which reference to use new one ?) or Gerring 2019 add link!

#We provide the scripts to apply the eMAGMA approach and generate a list of individual genes risk genes and gene-co-expression networks using genome-wide summary statistics. 
In this tutorial we use the GWAS summary statistics from a GWAS in Major Depression Disoreders(MDD), publically available in the Psychiatric Genomic Consortium(PGC) website. We provide an example with MDD, but you can use the scripts with your own data. 
The tutorial is divided in two parts: **Part 1 Runs MAGMA** to assign SNPs to the nearest genes (gene-base analysis) and then run a gene-set analysis of proximity to estimate what set of genes are more highly associated with MDD. **Part 2 runs eMAGMA** using summary statistics and eQTl data from GTex (SNP to tissue specific annotation) data to run a gene-base analysis then combined with a gene Co-expression network to assign SNPs to tissue specific genes and estimate what tissue specific genes are more highly associated with MDD.

Tissue specific annotation files and Co-expression network files are freely provided with this tutorial. Explanation of the methods and resources used in this tutorial are provided in the publication accompanying this tutorial. *Ref

**FILES and SOFTWARE TO DOWNLOAD

#The analysis is done using MAGMA v1.07b (ref) MAGMA and auxiliary files can be download from the program website: https://ctg.cncr.nl/software/magma.
#Two auxiliary files are required: a file with gene locations for protein-coding genes from NCBI and a genome reference file. For this tutorial we use build 37(hg19) that matches the build of the summary data (MDD2018_excluding23andMe) and reference file for European population. Gene location files for build 36, 37, & 38 are available from MAGMA website.

#You can use wget o curl to import the files directly into your directory example:

#MAGMA: 
        
        wget https:// https://ctg.cncr.nl/software/MAGMA/prog/magma_v1.07b_static.zip

#Auxiliary files for 37(hg19): 
        
        wget https://ctg.cncr.nl/software/MAGMA/aux_files/NCBI37.3.zip

#reference data 
        
        wget https://ctg.cncr.nl/software/MAGMA/ref_data/g1000_eur.zip

#GWAS summary = MDD2018_ex23andMe from PGC web site: https://www.med.unc.edu/pgc/results-and-downloads/mdd/

**Notice: If you are using your own data, make sure to download the auxiliary files that correspond to the genome build of your data.

You also need the folling files: 
**eMAGMA Annotation files 
***eMAGMA network files https://github.com/AngelaMinaVargas/eMAGMA-tutorial/blob/master/network_files.zip 





Using MAGMA: do a Gene association analysis to generate a list of genes that are associated with the trait of interest, in this case is MDD.

Data files:
 

        #?.1 Annotation step=Map the SNPs to genes  Anotation Step

        ./magma --annotate --snp-loc [depression_test2/]
        --gene-loc NCBI38.gene.loc
        --out depression_test1/depression1
