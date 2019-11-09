# PART 

# 2eMAGMA GENE-SET ANALYSIS 

In this step we use the output of the gene-based analysis for the Amygdala, to test what modules within a co-expression network are more highly associated with MDD risk.  The test is carried out using the gene-sets function in MAGMA.

The co-expression network files are provided in the folder network_files.zip  
    https://github.com/AngelaMinaVargas/eMAGMA-tutorial/blob/master/network_files.zip

Details of the assembly of the co-expression networks are given in Gerrin et al., 2019a. Each co-expression network is subdivided into “modules” of highly correlated genes. Each co-expression network file has 2 columns: the modules are represented in the first column and are labelled as a colour; this is just a tag to identify the module or group during the analysis. The second column correspond to the genes ID. 

If you haven’t yet, unzip the networks.zip file and run the analysis with code below:

    ./magma --gene-results Amygdala_emagma.genes.raw 
    --set-annot network_files/Brain_Amygdala_entrez_gtex_v7_normalised.txt col=2,1 
    --out Amygdala_emagma 


The results of the gene-set association analysis are presented in the gsa.out file [Amygdala_emagma.gsa.out ]. 
    
    # MEAN_SAMPLE_SIZE = 64134
    # TOTAL_GENES = 1258
    # TEST_DIRECTION = one-sided, positive (set), two-sided (covar)
    # CONDITIONED_INTERNAL = gene size, gene density, sample size, inverse mac, log(gene size), log(gene density), log(sample size),   
    log(inverse mac)
    VARIABLE            TYPE  NGENES         BETA     BETA_STD           SE            P
    black                SET      55    0.0073145    0.0014962      0.13874      0.47898
    blue                 SET     141     -0.05808     -0.01833     0.086617      0.74868
