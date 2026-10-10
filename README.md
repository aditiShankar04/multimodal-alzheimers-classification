# Multimodal Alzheimer's Disease Classification

A machine learning project investigating whether combining clinical variables with MRI-derived features improves Alzheimer's disease classification compared with using either data modality independently.

This project was developed as part of my QBIO 465 capstone project.

## Project Overview

Alzheimer's disease classification can draw on multiple types of patient information, including clinical characteristics and neuroimaging. This project explores whether integrating these data sources provides better predictive performance than using either source independently.

Three machine learning approaches were developed and compared:

1. **Clinical-only model:** Logistic regression using demographic and clinical variables.
2. **MRI-only model:** Convolutional neural network (CNN) trained on 2D MRI slices.
3. **Multimodal model:** Multilayer perceptron (MLP) combining clinical variables with MRI feature embeddings extracted by the CNN.

The models were evaluated using accuracy, precision, recall, F1-score, and ROC AUC.

## Dataset

Data were derived from the **Open Access Series of Imaging Studies (OASIS-1)**.

The clinical features used in the analysis included:

- Age
- Sex
- Education
- Normalized whole brain volume (nWBV)

Clinical Dementia Rating (CDR) was converted into a binary classification target:

- **CDR = 0:** Non-demented
- **CDR > 0:** Demented

MRI data consisted of preprocessed 2D MRI slices associated with OASIS subjects. After preprocessing and matching subjects with available clinical and MRI data, 200 subjects were included in the final analysis.

> The datasets are not included in this repository. Please refer to the official OASIS resources for information about data access and usage.

## Methods

### 1. Clinical-Only Model

A logistic regression classifier was trained using standardized clinical and demographic variables. This model served as a baseline for evaluating the predictive value of structured clinical information.

### 2. MRI-Only Model

A convolutional neural network was trained on MRI slices to learn imaging-based representations associated with dementia status.

Five MRI slices were selected per patient and resized to 128 × 128 pixels. Predictions across slices were aggregated to generate patient-level classifications.

### 3. Multimodal Model

The multimodal model combined the two data sources.

MRI feature embeddings were extracted from an intermediate layer of the trained CNN and aggregated at the patient level. These imaging features were then combined with standardized clinical variables and used as input to a multilayer perceptron classifier.

## Results

| Model | Accuracy | Dementia Recall | F1 Score | ROC AUC |
| --- | ---: | ---: | ---: | ---: |
| Clinical-only | 0.75 | 0.50 | 0.62 | 0.79 |
| MRI-only | 0.40 | 1.00 | 0.57 | 0.44 |
| Multimodal | 0.60 | 0.75 | 0.60 | 0.74 |

The **clinical-only model achieved the highest overall accuracy and ROC AUC**, demonstrating the predictive value of structured clinical variables.

The **MRI-only CNN performed poorly and showed evidence of overfitting**, highlighting the challenges of training deep learning models on relatively small medical imaging datasets.

The **multimodal model improved dementia recall from 0.50 to 0.75 compared with the clinical-only model**. Although it did not achieve the highest overall accuracy, it provided more balanced performance and greater sensitivity to dementia cases.

These results suggest that MRI-derived features may provide complementary information when combined with clinical variables, while also demonstrating that increased model complexity does not necessarily lead to better overall performance.

## Technologies Used

- Python
- TensorFlow / Keras
- scikit-learn
- pandas
- NumPy
- Matplotlib
- Convolutional Neural Networks (CNN)
- Logistic Regression
- Multilayer Perceptrons (MLP)

## Repository Contents

- [`multimodal_alzheimers_classification.ipynb`](multimodal_alzheimers_classification.ipynb) — Complete data preprocessing, exploratory analysis, model development, evaluation, and comparison
- `project_report.pdf` — Full capstone project report
- `research_proposal.pdf` — Original research proposal

## Limitations

Several limitations affected model performance:

- The final matched dataset contained a relatively small number of subjects.
- The MRI model used a limited number of 2D slices rather than complete 3D brain volumes.
- Moderate class imbalance was present in the dataset.
- The MRI-only CNN showed evidence of overfitting and limited generalization.

## Future Work

Potential extensions of this project include:

- Training on larger patient cohorts
- Using complete 3D MRI volumes
- Incorporating longitudinal patient data
- Exploring transfer learning for MRI feature extraction
- Evaluating more advanced multimodal architectures
- Improving strategies for handling class imbalance

## Author

**Aditi Shankar**
