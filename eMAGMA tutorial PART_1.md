# PART 1

The tutorial assumes that the eMAGMA files and the program (MAGMA) and auxiliary files are all in the same directory. If your files are in different directories you must add the directory path to the command line. 

    cd /path/to-yourworking folder/eMAGMA


Unzip the program folders and the data file magma_v1.07b.zip, NCBI37.3.zip and MDD2018_excluding23andMe (downland this file from the PGC website)
    
    unzip *file.zip 


To run the gen-based association we need the P-values from the MDD GWAS summary statistics. Run the following code to extract SNP ID, chromosome, base pair position, and p-value information from the GWAS summary statistics, into a new txt file.

    awk '{print $2,$1,$3,$11}' MDD2018_excluding23andMe > MDD2018_excluding23andMe_short.txt


The three first columns of the input summary data must be in the order: SNP ID, chromosome and base pair position, the program (MAGMA) ignores other columns. 




**************************************************************************************************


**eMAGMA GENE-BASED ASSOCIATION: SNP TO TISSUE SPECIFIC GENES**


The analysis requires raw genotype data from an appropriate reference sample to model the LD structure. For this purpose, we use the genome reference file for European population [g1000_eur]. This analysis also requires of an annotation file that links SNPs to genes based on physical proximity. Since we would link SNPs to genes based on eQTL regulation, we use annotation files for which we have previously assign SNPs to target genes. These annotation files were generated based on significant (FDR<0.05) SNP-gene associations in GTEx, there are 48 files corresponding to 48 different tissues (see Gering 2009, for further details). The annotation files are provided in the directories Batch1, Batch2, Batch3 and Batch4. Below is the list of files in each directory:

For practical reasons, we will use only the annotation files for the Amygdala, which is in the directory Batch1. In Batch1, there are 13 annotation files with the tissue name as prefix and the suffix genes.annot. To download Batch1 (Brain tissue data) into a directory named Brain do:

    mkdir Brain 
    cd Brain 
    
    wget Btch1 to add link!!!
    unzip Batch1.zip
    cd ..

Make sure you are back to the eMAGMA folder, to run the association do:

    ./magma --bfile g1000_eur 
    --gene-annot Brain/Amygdalaxxx" 
    --pval MDD2018_excluding23andMe_short.txt ncol=[N_COL]
    --gene-settings adap-permp=10000 
    --out emagma      
     

The above command directs the analysis to be perform in each file on the Brain directory that has the suffix genes.annot. Pvalues are extracted from the MDD GWAS summary data [MDD2018_excluding23andMe_short.txt]. The effective number of samples is in column xxx total. Multiple testing is done using 10,000 adaptive permutations (--adap-permp=10,000). 

The analysis outputs a genes.raw xxxx file and a genes.out xxxx file for each of the input.  Brain_Spinal_cord_cervical_c-1.genes.annot_emagma.genes.raw. 

Below is an example of the a genes.out file, it has information on gene ID, position, the number of SNPs mapped to the gene and the pvalue of the association and the pvalue of the permutation. 

    GENE       CHR      START       STOP  NSNPS  NPARAM       N        ZSTAT            P        PERMP  NPERM
    441869       1    1353800    1356824     23       4  307354     -0.35438      0.63847        0.639   1000
    219293       1    1378152    1405538     56       4  307354      0.44829      0.32697        0.267   1000
    83858        1    1407139    1444852     85       6  307354     -0.68153      0.75223        0.782   1000


The program also generates a log file, example :Brain_Spinal_cord_cervical_c-1.genes.annot_emagma.log. The log file has summary information of the run, i.e. error if any, how many genes were read and how many genes have a valid SNP assigned.

Following the example with the Amygdalaxxxx, an inspection of the log file shows that xxx1600 gene definitions were read from the annotation file and xxx1541 genes have a valid SNPs in genotype data.


To Extract a list of genes significant assocaited genes, after correcting for multiple testing (Bonferroni correction=0.05/number of genes tested) do:

    awk '{if ($9<=8.86839E-06) print $0 }' "xxxx" > top_gene-based_emagma.txt; done
    

The above code created a file top_gene-based_emagma.txt that has a list of significant associated genes. There are xxx80 associations listed in the file

An inspection of the file indicates:

    The highest association is shown by the gene ID 4277  
    the gene is located in chromosome  6:31462054-31478901
    The gene is mapped by xxx SNPS       
    Pvalue  of assocaition 1.7524e-12      
    tissue: eMAGMA/Brain_Cerebellar_Hemisphere.genes.annot_emagma_genebased_short.genes.out neeed to fix !!!


Notice that some genes may have multiple entries given that a gene can be found in multiple tissues. To know how many genes are significant without including repetitions do: 

    awk '!a[$1]++' top_genes.txt |wc -l 

There are xxx unique genes.

We have identified xxx significant brain tissue-specific associations with MDD, this associations represent xxx unique genes. The gene-based analysis also generated a raw file for each tissue, this file would be the input for the second part of the tutorial.
