# PART 2

#In this part of the tutorial we will use the eMAGMA aproach to generate a list of genes which xxxxx(function is associated with MDDxxxx). Similar to PART 1 of the tutorial we will use MAGMA for the association anlysis. Basically the steps to follow are the same that in PART 1 of the tutorial but instead of doing a SNP to gene annotation follow by gene-level analysis, we will do a SNP to tissue-specific gene annotation and a tissue-specific gene-level analysis.

This step uses the annotation files provided genes.annot, to illustrate the proceedings we will use only the annotation files for brain tissue. With your own data you can make use all the annotation files that are provided are your own convenience.

    unzip Brain_annot_genes.zip
 
 **eMAGMA Gene-based association: SNP to tissue specific genes**

    for file in Brain/*genes.annot; do 
    ./magma --bfile g1000_eur 
    --gene-annot $file 
    --pval MDD2018_excluding23andMe_short.txt N=307,354 
    --gene-settings adap-permp=10000 
    --out $file_MDD_emagma; done
    
somthing about the ouput: 


**eMAGMA Gene-set Analysis: tissue to funcion or other way around check the wording!!!! :)

for file1 in MDD/*_normalised.txt; do 
  for file2 in MDD/*genes.raw do
 ./magma --gene-results "$file2" --set-annot "$file1" col=2,1 --out geneset$file1; done
 
 
