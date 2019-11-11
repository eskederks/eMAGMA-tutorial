**PART 2** 
# eMAGMA GENE-SET ANALYSIS**

In this step we use the output of the gene-based analysis for the Amygdala, to test what modules within a co-expression network are more highly associated with MDD risk.  The test is carried out using the gene-sets function in MAGMA.

The co-expression network files are provided in the folder network_files.zip  
    https://github.com/AngelaMinaVargas/eMAGMA-tutorial/blob/master/network_files.zip

Details of the assembly of the co-expression networks are given in Gerrin et al., 2019a. Each co-expression network is subdivided into “modules” of highly correlated genes. Each co-expression network file has 2 columns: the modules are represented in the first column and are labelled as a colour; this is just a tag to identify the module or group during the analysis. The second column correspond to the genes ID. 

If you haven’t yet, unzip the networks.zip file and run the analysis with code below:

    ./magma --gene-results Amygdala_emagma.genes.raw 
    --set-annot network_files/Brain_Amygdala_entrez_gtex_v7_normalised.txt col=2,1 
    --out Amygdala_emagma 

The log file [Amygdala_emagma.log] shows that 24 gene-set (modules) were read from the input file, of these, 23 gene-sets contain genes defined in the genotype data (containing a total of 1188 unique genes). 

The results of the gene-set analysis are presented in the gsa.out file [Amygdala_emagma.gsa.out ]. This file shows that the smallest P-value=0.03703 is for the module: white, formed by 16 genes. Below is an example of how the file looks. 
    
    # MEAN_SAMPLE_SIZE = 64134
    # TOTAL_GENES = 1258
    # TEST_DIRECTION = one-sided, positive (set), two-sided (covar)
    # CONDITIONED_INTERNAL = gene size, gene density, sample size, inverse mac, log(gene size), log(gene density), log(sample size), 
    VARIABLE            TYPE  NGENES         BETA     BETA_STD           SE            P
    black                SET      55    0.0073145    0.0014962      0.13874      0.47898
    skyblue3             SET       3     -0.64108    -0.031281      0.57506      0.86742
    turquoise            SET     280     0.071266     0.029657     0.067712      0.14639
    white                SET      16      0.45136     0.050599      0.25247      0.03703



 
After correcting for multiple testing, if significant genes are found, MAGMA generates a genes.sets.out file, with results for the significant sets. Modules in the Amygdala network are not significant.  Gerrin et al.,2009a, present an example of post-analysis when significant modules are detected. 

The user is invited to follow the steps in this tutorial to analyse their own data and make use of the annotation files and network files provided here.  We encourage the user to explore the potential that these resources have, to find functional relationships and to mine GWAS summary data.
