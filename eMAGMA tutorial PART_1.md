# PART 1  
#eMAGMA GENE-BASED ASSOCIATION


*Input data*

The tutorial assumes that the eMAGMA files, the program (MAGMA) and auxiliary files are all in the same directory. If your files are in different directories you must add the directory path to the command line.

    cd /path/yourworking folder/eMAGMA


Unzip the program folders and the data file magma_v1.07b.zip, NCBI37.3.zip and MDD2018_excluding23andMe (download this file from the PGC website).
    
    unzip [filename].zip 


To run the gen-based association we need the P-values from the MDD GWAS summary statistics. Execute the following code to extract: SNP -ID, chromosome, base pair position, and P-value information from the GWAS summary statistics into a new txt file. 
 

    awk '{print $2,$1,$3,$11,$19}' MDD2018_ex23andMe > MDD2018_ex23andMe_emagma.txt
    
Then remove the lines that have missing data. 
    
    awk 'NF==5' MDD2018_ex23andMe_emagma.tx

The first three columns of the input summary data should now be in the order: SNP ID, chromosome and base pair position. 


**************************************************************************************************


**Analysis**


The analysis requires raw genotype data from an appropriate reference sample to model the LD structure. For this purpose, we use the genome reference file for European population [g1000_eur]. This analysis also requires an annotation file that links SNPs to genes based on physical proximity. Since we are linking SNPs to genes based on eQTL information, we use annotation files for which we have previously assigned SNPs to target genes. These annotation files were generated based on significant (FDR<0.05) SNP-gene associations in GTEx, (see Gering 2009b, for further details). The annotation files are provided in the directories Batch1, Batch2, Batch3 and Batch4, Batch5 and Batch6. 

For practical reasons, we will use only the annotation files for the Amygdala, which is in the directory Batch1. In Batch1, there are 13 annotation files with the tissue name as prefix and the suffix genes.annot. To download Batch1 into a directory named Brain do:


    mkdir Brain 
    cd Brain 
    wget https://github.com/AngelaMinaVargas/eMAGMA-tutorial/blob/master/Batch1.annot.zip
    unzip Batch1.zip
    cd ..

Make sure you are back to the eMAGMA folder. To run the association do:

    ./magma --bfile g1000_eur 
    --gene-annot Brain/Brain_Amygdala.genes.annot 
    --pval MDD2018_ex23andMe_emagma2.txt ncol=Neff 
    --gene-settings adap-permp=10000 
    --out Amygdala_emagma      
     

The above command indicates: Brain_Amygdala.genes.annot, is the input file for the analysis,  P-values are extracted from the MDD GWAS summary data [MDD2018_ex23andMe_emagma.txt]. The effective number of samples is in column Neff. Multiple testing is done using 10,000 adaptive permutations (--adap-permp=10,000).

The program also generates a log file [Amygdala_emagma.log]. The log file has summary information of the run, i.e. errors if any, how many genes were read and how many genes have a valid SNP assigned. An inspection of the Amygdala_emagma.log, shows that 1301 genes definitions were read from the annotation file and 1258 genes have valid SNPs in genotype data.

The analysis outputs a genes.raw [Amygdala_emagma.genes.raw] file and a genes.out [Amygdala_emagma.genes.out] file. 
The genes.raw file contains results and correlations of the analysis and it will be used later in PART 2 of the tutorial.

The genes.out files have the result in an easy to read format. Below is an example of the genes.out file, it has information on gene ID, position, the number of SNPs mapped to the gene, the P-value of the association and the P-value of the permutation.

    GENE       CHR      START       STOP  NSNPS  NPARAM      N        ZSTAT            P        PERMP  NPERM
    26155        1     879583     894679      6       2  38689     -0.47386       0.6822        0.692   1000
    54991        1    1017198    1051736     14       1  61363      0.63601      0.26238        0.248   1000



To extract a list of significant associated genes, after correcting for multiple testing (Bonferroni correction=0.05/number of genes tested) do:


    awk '{if ($9<=3.8431e-5) print $0}' Amygdala_emagma.genes.out > Amygdala_signif_genes.txt
    

The above code generates a list [Amygdala_signif_genes.tx] of four significant genes. 

    GENE       CHR      START       STOP  NSNPS  NPARAM      N        ZSTAT            P        PERMP  NPERM
    10463        4   41992516   42089551      1       1  54271       4.1106    1.973e-05       0.0001  10000
    11118        6   26365387   26378548    223       6  68311       5.6024   1.0573e-08       0.0001  10000
    64288        6   28292514   28321972     48       3  66367       4.5078   3.2753e-06       0.0001  10000
    720          6   31949834   31970457    345       9  65285       4.0559   2.4967e-05       0.0002  10000
    
The highest association is shown by the gene ID 11118, P-value=1.0573e-08, this gene is located in Chromosome 6:26365387 -26378548 and is mapped by 223 SNPs.  Two other genes in chromosome 6 and one gene in chromosome 4 are also significant for MDD.

It is done! you have generated a list of eGenes that are expressed in the Amygdala and have a significant assoctiation with MDD. The information generated from this analysis can be used to investigate biological pathways and functions of these genes. 

To take this analysis one step further proceed to Part 2!

