# eMAGMA-TUTORIAL
Supplementary Methods

In this tutorial  xxxx
we use the GWAS summary statistics from a GWAS in Major Depression Disoreders(MDD), publically available in the Psychiatric Genomic Consortium(PGC) website
For further details on xxxx please read Gerring 2019 add link!

Preliminary Steps:
Set a working directory and download the version of that suits your OS, for this tutorial use Linux 64bits.

        -mkdir [depression_test2]
        -wget https://ctg.cncr.nl/software/MAGMA/prog/magma_v1.07b.zip
(for all files download you could use curl i,e
        -curl https://ctg.cncr.nl/software/MAGMA/prog/magma_v1.07b.zip)

Get Auxiliary files: Gene locations build 38 & reference data Europeans

        -wget https://ctg.cncr.nl/software/MAGMA/aux_files/NCBI38.zip



        -wget https://ctg.cncr.nl/software/MAGMA/ref_data/g1000_eur.zip


 Now that we have MAGMA and the auxiliar files, we will start for doing a
annotation


Using MAGMA: do a Gene association analysis to generate a list of genes that are associated with the trait of interest, in this case is MDD.

        Data files:
                GWAS summary = MDD2018_ex23andMe from PGC web site: https://www.med.unc.edu/pgc/results-and-downloads/mdd/
                Gene location file: a file for protein-coding genes, in the same build that the imput data= 37(hg19)( gene location files for build 36, 37, & 38 are availabl from MAGMA website

        #?.1 Annotation step=Map the SNPs to genes  Anotation Step

        ./magma --annotate --snp-loc [depression_test2/]
        --gene-loc NCBI38.gene.loc
        --out depression_test1/depression1
