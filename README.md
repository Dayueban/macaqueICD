# macaqueICD
Python, R, and bash scripts used for analysis of rhesus macaque gut microbiomes for ICD.  Except when described otherwise, tools used are all components of the SAMSA2 pipeline [https://github.com/transcript/samsa2](https://github.com/transcript/samsa2) .

### Base pipeline and analysis

*Script used: bash\_scripts/macaque\_master\_script.bash*

**Explanation:** This is the main pipeline script of SAMSA2, set up to run on a cluster for the macaque metatranscriptome files.  The reference databases used are NCBI's RefSeq Bacterial non-redundant database (version 102, released 22 December 2015), and TheSEED Subsystems database (retrieved 18 January 2017).

### Host read analysis

*Script used: bash\_scripts/macaque\_host\_pipeline\_script.bash*

**Explanation:** Macaque host reads were screened out of metatranscriptome later than analysis of bacterial sequences, and thus a simplified pipeline script was created for analysis.  The reference database used is NCBI's RefSeq macaque proteins database (retrieved 4 October 2017).

### Figure generation R scripts

##### Shannon and Simpson diversity graphs

*Script used: R\_scripts/diversity\_stats.R*

    $ Rscript diversity_stats.R -d working_directory/

Diversity was calculated based on the genus counts for annotations against the RefSeq Bacteria database.  The vegan package is used for calculating Shannon and Simpson diversity measures.

##### PCA plot

*Script used: R\_scripts/make\_DESeq\_PCA.R*

    $ Rscript make_DESeq_PCA.R working_directory/ PCAplot_save_name
    
The PCA plot included in the paper was calculated using genus counts for annotations against the RefSeq Bacteria database, comparing the ICD samples to control samples.  

##### Heatmaps

*Script used: R\_scripts/make\_DESeq\_heatmap.R*    
*Script used for host heatmap: R\_scripts/macaque\_host\_heatmap.R*

    $ Rscript make_DESeq_heatmap.R working_directory/ heatmap_save_name

The heatmap in Figure 1 in the paper was caluclated using genus counts for annotations against the RefSeq Bacteria database, comparing each of the samples against others.  Numbers 1-12 indicate the ICD samples, while 13-24 indicate healthy controls.  For Figure 9, the heatmap of immune functions found in host annotations draws on functional annotations against NCBI's list of macaque proteins.  

##### Stacked bar graphs

*Script used: R\_scripts/make\_combined\_graphs\_top10.R

    $ Rscript make_combined_graphs_top10.R -g graph_title -d working_directory -o graph_save_name

For Figure 2, the graph was created using genus counts for annotations against the RefSeq Bacteria database.  Note that the optional "Other" setting in the script was kept, to preserve Other counts in the figure.

##### Subsystems variable-width bar graphs

*Script used: R\_scripts/Subsystems\_DESeq\_graphs.R*

    $ Rscript Subsystems_DESeq_graphs.R -d working_directory/ -L Subsystems_level (1-4) -o graph_save_name

Using scripts included in the SAMSA2 pipeline, the SEED Subsystems annotations were filtered to select only reads that annotated against a *Prevotella* species in RefSeq Bacteria results.  This subset of Subsystems annotations was used for creating a bar graph of the top functions of Prevotella.  Figure 3 features reads mapped to level 1 annotations, the broadest category.

Figure 4 in the paper used the same script listed above, but no filtering was applied to Subsystems annotated reads, so all Subsystems annotated were used to create the barplot.

##### Boxplots

*Script used: R\_scripts/macaque\_pathogen\_boxplots.R*    
*Script used: R\_scripts/mucin\_degraders\_boxplots.R*    
*Script used: R\_scripts/mucin\_enzymes\_boxplot_all.R*

    $ Rscript macaque_pathogen_boxplots.R 
    $ Rscript mucin_degraders_boxplots.R
    $ Rscript mucin_enzymes_boxplot_all.R

These boxplot scripts are not standardized to the same degree as others; they use hard-coded values for initial counts.  For Figure 5, the macaque pathogens, values are derived from genus counts in a normalized counts table generated by DESeq, annotated against NCBI Bacteria.  Similarly, for Figure 6A, mucin degraders counts are derived from normalized counts of genus-level annotations against the NCBI Bacteria database.  For Figure 6B, mucin degrading enzymes counts are derived from normalized counts of functional annotations against the NCBI Bacteria database.

##### Databases used

Warning: these are links to large files (several gigabytes) that may take time to download.  It may be more advisable to download these from the command line using wget or curl.

RefSeq database used: https://bioshare.bioinformatics.ucdavis.edu/bioshare/download/2c8s521xj9907hn/RefSeq_bac.fa

SEED Subsystems database used: https://bioshare.bioinformatics.ucdavis.edu/bioshare/download/2c8s521xj9907hn/subsys_db.fa


