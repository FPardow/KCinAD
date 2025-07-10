# KCinAD
 Analysis of KC subtypes in healthy and AD skin 

To regenerating the analysis and all figures of the manuscript follow the subsequent steps:
1. Open the R markdown script "KCinAD_0430_publication.Rmd". Most of the analysis was carried out in R using tis code. 
2. Install the R version and packages used for this study using the renv package manager: Install R version 4.4.1. You can use the renv package to "lazy-load" my version of the installed packages. Alternatively, you can manually install the packages yourself. For both, see the code chunk {r install packages, eval = F} from code line 180 - 224 of the R markdown script 
3. Setting up the directories: please specify the directories on your computer where to get the data from and where to save your results to (line 37 - 41)
4. Pre-processing the SVM training dataset GSE147482 (Wang et al. 2019 biopsy scRNA-seq):

   4.1 please download the GSE147482_RAW.tar data file from https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE147482 into the data.dir.
   
   4.2 run the code from line 264 - 912
6. Pre-processing the SVM test dataset GSE153760 (Rojahn et al. 2020 biopsy scRNA-seq):
   
   5.1 please download the GSE153760_RAW.tar data file from https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE153760 into the data.dir.
   
   5.2 run the code from line 927 - 1170
8. Handling the SVM annotation

   6.1 Gene match the Wang and Rojahn and al dataset and export them in the right format for SVM annotation (code lines 1180 - 1244)

   6.2 ***STOPP!*** now switch from R to Jupiter Notebook. DO NOT continue the analysis further or change the rojahn_kcfiltered2 dataset
   
   6.3 Generate the python environment from the provided SVM.yml file. This step only needs to be done when running the script for the first time. /path/to/directory/ needs to be replaced with the path to the directory where your SVM.yaml file is located.

```
conda env create --name SVM --file /path/to/directory/SVM.yml
```

   6.4 Activate the SVM.yml conda environment.
```
conda activate /path/to/directory/SVM
```

   6.5 Navigate to the directory where the CrossVal.ipynb and SVM.ipynb scripts can be found. 
```
cd /path/to/directory
```

  6.6 Open Jupyter notebook (see code below) and then open the scripts here. 
   
```
jupyter notebook 
```

   6.7 Adjust the file paths in the jupyter notebook and the run the chunks of code. (* means the code is busy running)

The script CrossVal.ipynb performs the 5-fold cross-validation and produces Supplemental Figure 1i (Results > CrossVal > Confusion_matrix_SVM.png). 
The script SVM.ipynb trains the SVM annotation model and annotates the Rojahn et al. dataset. The most important output is the SVM_Pred_Labels.csv file in SVMannotation/Results/RojanhBiop where the predicted KC annotations are stored. 

7. Continue in R markdown with the main part of the analysis:
   7.1 load the SVM annotation labels of the keratinocyte subtypes in line 1253

   7.2 continue running the rest of the script to generate the remaining results  





