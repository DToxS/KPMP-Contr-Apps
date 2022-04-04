README for Running Jens KPMP Codes

==========================================================

Set 1 - Run these R scripts first inside the kpmp-rp-apps Docker container

Run R scripts by using the following commands (order does not matter):

```
Rscript RunBeforeCSharpScript_PostHocPower_singleNucleusCell_analysis.R "Premiere" 2
Rscript RunBeforeCSharpScript_PostHocPower_singleNucleusCell_analysis.R "UCSD" 2
Rscript RunBeforeCSharpScript_calculate_meanExpressionValues_in_integrated_clusterAnalysis.R
```

Comments on the script "RunBeforeCSharpScript_PostHocPower_singleNucleusCell_analysis.R":

"Premiere" and "UCSD" indicate to analyze the single cell or single nucleus RNAseq datasets, respectivly. The number 2 indicates to use two parallel cores for the analysis. This the minium number of cores that can be specified. It can be increased to any number of cores your computer can support. When 2 cores are specified, the script uses about 80-100 GB memory. This number increases with increasing number of cores.  The highest amount of memory will be used after about a third to half of the total runtime. Please test, how many cores your available memory can support.

----------------------------------------------------------

Set 2 - Run c-sharp script inside the kpmp-cs-apps Docker container, after running all scripts in set 1

Go to the directory "\CS-Codes\KPMP_reference_atlas_csharp_code\Executable_script" and run C# script by using the following command:

```
KPMP_reference_kidney_tissue_atlas.exe
```

A progress report will be written as a text-file ("Report.txt") that can be found in the subdirectory "Results".

----------------------------------------------------------

Set 3 - Run these R scripts inside the kpmp-rp-apps Docker container, after running c-sharp script of set 2

Run R scripts by using the following commands (order does not matter):

```
Rscript RunAfterCSharpScript_metabolicEnergyPathways_all.R
Rscript RunAfterCSharpScript_metabolicEnergyPathways_averaged.R
Rscript RunAfterCSharpScript_PostHocPower_visualizeResults.R "Premiere"
Rscript RunAfterCSharpScript_PostHocPower_visualizeResults.R "UCSD"
Rscript RunAfterCSharpScript_sphingomyosin_metabolism.R
Rscript RunAfterCSharpScript_crossOmicsComparison_correlationCoefficients.R
Rscript RunAfterCSharpScript_crossOmicsComparison_hierarchicalClustering.R
```

Note: the last script is time-consuming and needs about 70GB of memory.

----------------------------------------------------------

Set 4 - Run this R scripts in the given order inside the kpmp-rp-apps Docker container (they are independent of the scripts in set 1, 2 and 3)

Run R scripts by using the following commands in the given order:

```
Rscript IndependentOfCsharpScript_no1_Wu_PMID29980650_Single_cell_analysis.R
Rscript IndependentOfCsharpScript_no2_SCP_readCounts_along_nephron.R
```

The second R script needs access to the internet, because it downloads ensembl gene symbol annotations during runtime (using the command 'useDataset' from the 'biomaRt' package). Our results are based on the ensembl annotation downloaded on 2022 March 25.
