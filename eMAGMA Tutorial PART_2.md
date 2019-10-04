# PART 2

#In this part of the tutorial we will use the eMAGMA aproach to generate a list of genes which xxxxx(function is associated with MDDxxxx). Similar to PART 1 of the tutorial we will use MAGMA for the association anlysis. Basically the steps to follow are the same that in PART 1 of the tutorial but instead of doing a SNP to gene annotation follow by gene-level analysis, we will do a SNP to tissue-specific gene annotation and a tissue-specific gene-level analysis.


 
 **eMAGMA GENE-BASED ASSOCIATION: SNP TO TISSUE SPECIFIC GENES**

#Here we assign MDD risk SNPs to genes tissue-specific SNP-gene association from GTEx, this is adding eQTL informattion to assigne SNP to genes based on their association with gene expression. We use P-values from MDD, the european reference. the torial provides five batches of tissue-specific SNP-gene files: Batch_1,Batch_2, Batch_3, Whole blood and Brain). For practical reasons in the tutorial we will use only the annotation files for brain tissue, there are xx annotation files [Brain_genes.annot].  With your own data you can make use of all provided files at your own convenience.
 
    Mkdir Brain
    wget -P /Brain/ https://github.com/AngelaMinaVargas/eMAGMA-tutorial/blob/master/Brain_annot_genes.zip
    
    for file in Brain/*genes.annot; do 
    ./magma --bfile g1000_eur 
    --gene-annot $file 
    --pval MDD2018_excluding23andMe_short.txt N=307,354 
    --gene-settings adap-permp=10000 
    --out $file_MDD_emagma; done
    
Similar to the steps in tutorial 1, the above code outputs a genes.raw file and a genes.out file but in this case we have on file for each of the brain tissues. That is 20 genes.raw and xx genes.out files.


**eMAGMA Gene-set Analysis: tissue to funcion or other way around check the wording!!!! :)

for file1 in MDD/*_normalised.txt; do 
  for file2 in MDD/*genes.raw do
 ./magma --gene-results "$file2" --set-annot "$file1" col=2,1 --out geneset$file1; done
 
 
