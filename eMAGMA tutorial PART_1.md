# PART 1
**GENE-BASE ANALYSIS WITH MAGMA*

#This tutorial assumes that MAGMA and all the files required for the tutorial are in the same directory. If your files are in different directories you must add the directory path to the command line. To begin set your working directory and unzip the files

    cd /path/to-your folder.

#Unzip the three folders Gene_level_analysis.zip, magma_v1.07b.zip and NCBI37.3.zip
  
    unzip *file.zip 

**Annotation* Map SNPs to genes

#Annotation is preliminary to the gene association analysis, in this step SNPs from the GWAS summary statistics are mapped to genes in the gene location file. For convenience we start by extracting SNP ID, chromosome, and base pair position from the GWAS summary, into a snp-loc file in MAGMA format, we also extracted the p-value information which will be used in a later step.
  
    awk '{print $2,$1,$3,$11}' MDD2018_excluding23andMe > MDD2018_excluding23andMe_short.txt

#Notice that you don’t need to create an additional file, if the summary data is organized with the three first columns matching the order: SNP ID, chromosome and base pair position, MAGMA ignores other columns.

#To run the annotation use the code below, it will generate a genes.annot [MDD_list.genes.annot] file with all SNPs that mapped to a gene and .log file [MDD_list.log] that should be inspected for warning and errors . 

    ./magma --annotate --snp-loc MDD2018_excluding23andMe_short.txt 
      --gene-loc NCBI37.3.gene.loc 
      --out MDD_list
    
**Gene base analysis on snp-pvalue data*

#In this step SNPs are assigned to nearest gene and gene-based statistics are computed based on the sum of SNP-log (10)P-values. 
The analysis requires of raw genotype data, P-value information, sample size of the summary data and the gene annotation file generated in the previous step. For this tutorial the raw genotype data correspond to the 1000 genome reference file for European population [g1000_eur], P-values were extracted from the MDD GWAS summary data prepared in the previous step [MDD2018_excluding23andMe_short.txt]. The total number of samples for the MDD GWAS is N=307,354. Multiple testing is done using 10000 adaptative permutations (--adap-permp=10000). 
The output is a genes.out file and a genes.raw file that would be used in the next step.

    ./magma --bfile g1000_eur  
      --gene-annot MDD_list.genes.annot 
      --pval MDD2018_excluding23andMe_short.txt N=307,354  
      --gene-settings adap-permp=10000 
      --out magma
    
    **Gene-set analysis*
