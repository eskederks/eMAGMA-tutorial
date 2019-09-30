# PART 2

#IN this part of the turorial we will use the eMAGMA aproach to generate a list of genes which xxxxx(function is assocaited with MDDxxxx).
Similar to PART 1 of the tutorial we will use MAGMA for the association anlysis. Basically the steps to follow are the same thatn in PART 1 of the turorial but instead of doing a SNP to gene annotation we will do a SNP to gene annotation.

This step uses the annotation files provided genes.annot

    unzip xxxxtrait.genes.annot
 
 **eMAGMA Gene-based association: SNP to tissue specific genes**


    for file in annotation_files/*genes.annot; do 
    ./magma --bfile g1000_eur  
    --gene-annot $file 
    --pval MDD/xxxx N=
    --gene-settings adap-permp=10000 
  --out MDD_full_emagma; done **XXX thismaybe need to change to individual files out !!!!!
    
    somthing about the ouput: 



**eMAGMA Gene-set Analysis: tissue to funcion or other way around check the wording!!!! :)

for file1 in MDD/*_normalised.txt; do 
  for file2 in MDD/*genes.raw do
 ./magma --gene-results "$file2" --set-annot "$file1" col=2,1 --out geneset$file1; done; done
 
 
