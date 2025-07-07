# Tensor Completion for Cancer Differential Expression Analysis

The application of tensor completion techniques to human RNA-seq data from lung cancer samples. 
The goal is to recover missing gene expression values in a biologically meaningful way by leveraging multi-dimensional structures in the data.

### Background

RNA-seq data is often sparse and noisy, with missing values arising from technical variation or dropout. Traditional matrix-based imputation methods flatten complex biological structure. This project instead reformats expression data as a **3D tensor (gene × sample × condition)** to preserve patterns across conditions and genes.

We implement and compare two tensor decomposition methods for imputing missing values:

- **CP-ALS (CANDECOMP/PARAFAC)**  
- **Tucker Decomposition**

Both are evaluated using synthetic missingness masks applied to a curated lung cancer RNA-seq dataset from The Cancer Genome Atlas (TCGA).

### Methods

- Data filtered to include genes with adequate expression.
- Expression values were log-transformed and reshaped into 3D tensors.
- Missing values were simulated using random NaN masks.
- Tensor completion was performed using TensorLy implementations of:
  - CP decomposition with Alternating Least Squares (ALS)
  - Tucker decomposition with ALS
- RMSE and visual plots used for evaluation.

### Results

- **CP-ALS** achieved RMSE < 1 across missingness levels (0–80%) and preserved biologically realistic expression ranges.
- **Tucker-ALS** smoothed out expression values, often underfitting and reverting to dataset mean.
- CP-ALS demonstrated better trade-off between expressiveness and error minimization.

### Limitations

- Memory constraints prevented full transcriptome-wide tensor completion (~60K genes).
- Low-abundance genes were often ignored by completion algorithms due to optimization on global error.
- Completed values require additional biological interpretation post hoc.

### Future Work

- Integration with **redescription mining tools** like SIREN for pathway-level analysis.
- Applying structured or condition-aware missingness.
- Scaling the approach with sparse tensor libraries or GPU acceleration.
