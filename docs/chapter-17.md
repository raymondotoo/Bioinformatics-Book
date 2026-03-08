# Chapter 17: Integrated Clinical Proteomics: The Full Analytical Pipeline

## 17.1 Overview

This chapter details the comprehensive computational workflow used to identify proteomic signatures of Alzheimer's Disease (AD) by integrating data from the **ADNI** and **ADRC** cohorts. The analysis proceeds sequentially from raw data cleaning to systems-level network analysis (WGCNA), functional enrichment, and machine learning.

## 17.2 Data Preprocessing and Harmonization

**Scripts:** `00_Data_preprocessing.Rmd`, `02a_ADNI_ADRC_harmonized.Rmd`, `02b_PCA_full.Rmd`

The initial phase focused on ensuring data quality and comparability between cohorts.

### Quality Control and Cleaning
Raw proteomic data often contains missing values and technical artifacts.
*   **Missingness Filtering:** Proteins with high missingness (e.g., >20%) across samples were removed to ensure robust downstream analysis.
*   **Sample Filtering:** Samples with incomplete core clinical metadata (Age, Sex, Diagnosis) were excluded.

### Cross-Cohort Harmonization
To integrate the ADNI and ADRC datasets, which may have been processed at different times or sites, we applied harmonization techniques to mitigate batch effects.
*   **Batch Correction:** Statistical methods were used to align the expression distributions of shared proteins between the two cohorts, ensuring that biological signals were preserved while technical differences were minimized.

### Exploratory Data Analysis (PCA)
Principal Component Analysis (PCA) was performed on the harmonized data.
*   **Variance Explained:** We assessed the proportion of variance captured by the top principal components.
*   **Visualization:** PCA plots allowed us to visualize the separation between cohorts before and after harmonization, as well as to identify and remove potential outliers.

## 17.3 Network Construction (WGCNA)

**Script:** `03_WGCNA_running.Rmd`

We employed Weighted Gene Co-expression Network Analysis (WGCNA) to identify clusters (modules) of co-expressed proteins. This systems biology approach moves beyond single-protein analysis to identify functional units.

### Soft Thresholding
A key feature of WGCNA is **soft thresholding**.
*   **Scale-Free Topology:** We analyzed the scale-free topology fit index for various powers ($\beta$).
*   **Power Selection:** We selected the lowest power $\beta$ that resulted in a high scale-free topology fit ($R^2 > 0.85$ or similar), ensuring the network reflects biological reality (few hubs, many peripheral nodes).
*   **Adjacency Matrix:** The correlation matrix was raised to the power $\beta$ ($|correlation|^\beta$) to create a weighted adjacency matrix, suppressing weak correlations and emphasizing strong ones.

### Module Detection
*   **Topological Overlap Matrix (TOM):** The adjacency matrix was converted into a TOM to measure the interconnectedness of proteins.
*   **Hierarchical Clustering:** We performed average linkage hierarchical clustering on the dissimilarity matrix (1-TOM).
*   **Dynamic Tree Cut:** Modules were identified using the dynamic tree cut algorithm, which is capable of detecting nested clusters.

### Eigengene Calculation
For each module, we calculated the **Module Eigengene (ME)**. The ME is the first principal component of the module's expression matrix and serves as a synthetic representative profile for the entire module.

## 17.4 Functional Annotation and Enrichment

**Scripts:** `04_Functional_Analysis.Rmd`, `07a_Functional_Analysis_GSEA.Rmd`, `07b_Functional_Analysis_ORA.Rmd`

To understand the biological significance of the identified modules, we performed enrichment analyses.

### Over-Representation Analysis (ORA)
*   **Method:** We used hypergeometric testing to determine if specific Gene Ontology (GO) terms or KEGG pathways were present in a module more often than expected by chance.
*   **Databases:** GO (Biological Process, Molecular Function, Cellular Component), Reactome, and KEGG.

### Gene Set Enrichment Analysis (GSEA)
*   **Ranked Lists:** Proteins were ranked based on their correlation with clinical traits or module membership.
*   **Enrichment:** We performed GSEA to identify coordinated pathway alterations that might not be detected by ORA alone, as it considers the entire ranked list rather than a fixed threshold.

## 17.5 Module Scoring and Feature Selection

**Script:** `05_Module_Scoring_Selection.Rmd`

We evaluated the predictive power of the identified modules and selected key features for modeling.

*   **Module Scores:** Composite scores were calculated for each module (e.g., average expression or eigengene value) to relate module activity to clinical traits.
*   **Hub Identification:** We calculated **Module Membership (kME)**, which is the correlation between a protein's expression and the module eigengene. Proteins with high kME are considered "hubs" and are likely drivers of the module's biological function.

## 17.6 Machine Learning for Biomarker Discovery

**Script:** `06_ADNI_ADRC_ML.Rmd`

We trained machine learning models to predict AD status and clinical outcomes using the identified proteomic signatures.

### Model: Elastic Net Regularized Regression
We utilized the **Elastic Net** algorithm (`glmnet` package), which combines L1 (Lasso) and L2 (Ridge) penalties. This is particularly effective for omics data where features (proteins) are correlated.

### Workflow
1.  **Data Splitting:** The dataset was split into training (e.g., 70%) and testing (e.g., 30%) sets using `createDataPartition` from the `caret` package to ensure balanced class distributions.
2.  **Feature Scaling:** Features were centered and scaled (Z-score) to ensure equal contribution to the model.
3.  **Cross-Validation:** We performed k-fold cross-validation (e.g., 5-fold) on the training set to optimize the regularization parameter ($\lambda$).
4.  **Performance Evaluation:** The final model was evaluated on the held-out test set using metrics such as **AUC (Area Under the ROC Curve)**, Sensitivity, and Specificity.

```r
# Example: Elastic Net Training with Caret and Glmnet
cv_fit <- cv.glmnet(
  x = as.matrix(X_train),
  y = y_train,
  family = "binomial",
  alpha = 0.5, # Elastic Net mixing parameter
  nfolds = 5
)
best_lambda <- cv_fit$lambda.min
```

## 17.7 Robustness and Sensitivity Analysis

**Script:** `08_Supplementary_analysis_v3.Rmd`

A critical component of this study was validating the findings. We performed rigorous sensitivity analyses to ensure the results were robust and reproducible.

### Module Preservation
We tested whether modules discovered in the ADNI cohort were preserved in the independent ADRC cohort using the `modulePreservation` function from WGCNA. This generates a **Z-summary** statistic; a Z-summary > 10 indicates strong evidence of preservation.

### Adjusted Regression Models
To isolate specific signals (e.g., vascular contributions) from general AD pathology, we ran adjusted regression models controlling for covariates such as Age, Sex, and APOE genotype.

```r
# Example: Running Module Preservation (ADNI as Reference)
multiExpr_Recip <- list(
  ADNI = list(data = expr_ADNI),
  ADRC = list(data = expr_ADRC)
)

pres <- modulePreservation(
  multiExpr_Recip,
  multiColor = multiColor_Recip,
  referenceNetworks = 1,
  nPermutations = 500,
  networkType = "signed",
  randomSeed = 123
)
```

## Summary

This pipeline transforms raw proteomic data into biologically meaningful modules. By following these four steps—Preprocessing, Network Construction, Module Detection, and Trait Correlation—we identify systems-level protein signatures associated with Alzheimer's Disease.