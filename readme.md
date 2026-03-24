# DNA-Binding Protein Classification (DBP-Class)
Project for NUS IT1244 by Team 21 - Angel Bu Tong Mei, Dexter Tan Yi Jia, Lee Jia Hong, Ong Wei Lun

## Description  
A machine learning pipeline to classify DNA-binding proteins (DBPs) from primary amino acid sequences. This project addresses limitations of traditional lab methods by using computational feature extraction and supervised learning (Logistic Regression, SVM, XGBoost) for efficient DBP identification.

**Key Innovation**:  
Hybrid feature engineering combining **188D sequence descriptors** (amino acid composition, physicochemical properties) with **12 structural features** (e.g., molecular weight, instability index), refined via two feature selection methods (Random Forest + RFE or mRMR).

---

## Features  
- **Input**: Protein sequences (FASTA format) with labels (`label_1` = DBP, `label_0` = non-DBP).  
- **Preprocessing**: Filters sequences (100-500 residues, valid amino acids).  
- **Feature Extraction**:  
  - 188D features (Song et al., 2014) + 12 Biopython-derived structural features.  
- **Feature Selection**:  
  - **Method 1**: Random Forest ranking + LinearSVM-RFE (top 60 features).  
  - **Method 2**: mRMR algorithm (mutual information-based).  
- **Models**: Logistic Regression (baseline), SVM (RBF kernel), XGBoost (optimized ensemble).  

---

## How to Run the Project

### Prerequisites
1. Download these files into the same folder:
   - `training.fasta` (labeled protein sequences)
   - `testing.fasta` (validation sequences)  
   - `it1224_final_project.zip` (Jupyter Notebook pipeline)


### Step-by-Step Execution

#### Notebook 1: Models With Feature Selection (Model_Training_With_Selection.ipynb)
```python
1. Preprocessing:
   - Filters sequences (100-500 residues)
   - Removes invalid amino acids
   - Splits labeled data

2. Feature Extraction:
   - Generates 188D features (AA composition + physicochemical properties)
   - Adds 12 Biopython structural features

3. Feature Selection (Optional):
   - Stage 1: Random Forest ranks top 130 features
   - Stage 2: SVM-RFE reduces to final 60 features

4. Trains models using only the 60 selected features:
a. SVM (RBF kernel) with grid search
b. Logistic Regression (L2 penalty)
c. XGBoost (with early stopping)
```

#### Notebook 2: Models Without Selection (Model_Training_Without_Selection.ipynb)
```python
1. Preprocessing:
   - Filters sequences (100-500 residues)
   - Removes invalid amino acids
   - Splits labeled data

2. Feature Extraction:
   - Generates 188D features (AA composition + physicochemical properties)
   - Adds 12 Biopython structural features

3. Trains models using all 200 features:
a. SVM with feature scaling
b. Logistic Regression with regularization
c. XGBoost (same params as Notebook 2 for comparison)
```