## Transcriptional regulatory co-expression network (TRN) inference and analysis of regulated target genes (regulons)
This analysis is part of our manuscript:
**Differential expression of starch and sucrose metabolic genes linked to varying biomass yield in Miscanthus hybrids** 
*Jose J De Vega, Ned Peel, Sarah J Purdy, Sarah Hawkins, Iain Donnison, Sarah Dyer, Kerrie Farrar*


## Summary
The TRN inference and regulon enrichment analysis was done with RTN v. 2.10.1 (Fletcher, Castro et al. 2013) and topGO v. 2.38.1 (Alexa and Rahnenfuhrer 2010). 

The code is fully available in an R notebook (RTN_complete.Rmd) in this repository in Github. An online version of the R notebook is [available here](https://jjdevega.github.io/miscanthus_transcriptional_regulatory_coexpression_network/).



## Transcriptional regulatory co-expression network (TRN) inference
The normalise counts from our previous analysis with DESeq2 and the list of known TFs in M. sinensis were provided to the RTN package with default options. RTN uses permutation (1000 permutations, FDR < 0.05) to remove non-significant TF-target associations, and bootstrapping (100 bootstraps, 95% consensus) to remove unstable interactions, before applying the ARACNE algorithm (eps >= 0) for network reconstruction. 

GO term enrichment in regulons with topGO was done using the list of target genes in a given regulon as gene-set instead of the list of DEGs. The overlap between the target genes in each regulon to the lists of DEGs was done by enrichment analysis with Master Regulatory Analysis (MRA) and two tail GSEA. MRA compared the list of DEGs (present/absent) with the members in each regulon. GSEA ranked the genes by expression fold-change and compared with either the activated (positive regulon) and repressed (negative regulon) subsets of each regulon. Both methods are implemented in the RTN package and were run with default options (except minimum regulon size of 5) for each of the tissues in the two studies: low against high NSC content hybrids, or hybrids against parents (heterosis). An igraph object was generated with RTN, exported to a xgmml file and imported into Cytoscape (v. 3.8.2) to plot the Network.


## Regulons' enrichment analysis
We compared the overlap between the target genes in each regulon and the lists of DEGs previously obtained to identify regulons enriched in DE genes. We later verified this analysis using two-tail GSEA including the expression fold-change to rank the genes. On the other hand, we identified the GO terms enriched (FDR <= 0.05) in each regulon to clarify the processes it may be involved. We identified 28 regulons that were (i) enriched with the “carbohydrate metabolism”, “generation of precursor metabolites and energy”, or “secondary metabolism” GO terms; and were also (ii) enriched in DEGs, or where the TF was DE. These 28 regulons contained 806 target genes in total, but only 134 were DE (Suppl. Table S16). 


## Results from our analysis
We annotated 5,045 transcription factors (TFs) in the M. sinensis proteome based on homology with the Plant Transcription Factor Database (Suppl. Table S5) (Jin, Tian et al. 2016).  The set of target genes regulated by a given TF forms a regulon. We inferred the putative regulon of each TF based on co-expression between targets and TFs using the RTN package (Fletcher, Castro et al. 2013). For 4,427 TFs we identified at least one target gene (Suppl. Table S12). The complete TRN included 26,710 genes (nodes) and 57,643 links (edges).

