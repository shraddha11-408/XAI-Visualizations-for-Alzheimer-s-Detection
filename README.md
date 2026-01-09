# XAI-Visualizations-for-Alzheimers
Here, we build a CNN model for the classification of MRI scans into different stages of Alzheimer's. We then explain this classification by incorporating interpretability in the model through an XAI algorithm called SHAP

This repository contains the implementation of SCR-NetX, a VGG-16 convolutional neural network developed for four-class Alzheimer’s disease classification using brain MRI scans. The main goal of this work is not only to achieve good classification performance, but also to make the model’s decisions interpretable and clinically meaningful using explainable AI techniques.


The code in this repository supports the work presented in the paper:

*“SHAP-Based Explainability for Local and Global Insights in Alzheimer’s Detection”*
Engineering, Technology & Applied Science Research (ETASR), 2026

## About the Model

SCR-NetX is the name given to a modified version of the standard VGG-16 architecture. 

Key modifications include:-

i) Using 128×128 MRI images as input

ii) Replacing the original fully connected layers with Global Average Pooling

iii) Adding Batch Normalization to improve training stability

iv) Using a compact set of dense layers before the final classification layer

## Focus on Interpretability

The main focus of this project is interpretability rather than only improving accuracy. Deep learning models are often treated as black boxes, which limits their use in medical settings. To address this, SHAP (SHapley Additive exPlanations) is used to explain the model’s predictions.
<img width="602" height="422" alt="image" src="https://github.com/user-attachments/assets/cf9ae59e-f001-4877-94ae-c205510c6292" />


Two levels of interpretability are explored:

### Local Interpretability

Local explanations help understand why the model made a specific prediction for a single MRI scan.

- SHAP values are computed at the pixel level  
- Pixels are grouped using SLIC superpixel segmentation  
- Heatmaps are generated to highlight important brain regions for each prediction  

These explanations are demonstrated using multiple example MRI scans from each class.

### Global Interpretability

Global explanations help understand how the model behaves across multiple samples.

- SHAP values are aggregated across MRI scans  
- A fixed grid-based segmentation is used to ensure consistency across images  
- This allows comparison of region importance at the dataset level  

Together, these two approaches provide both patient-specific and population-level insights.

## Repository Structure

```text
├── Model_parameters/
│   └── Contains model configuration and parameter-related files
│
├── ModelTraining_and_XAI_Analysis/
│   ├── FINAL_Kaggle_VGG16_Training.ipynb
│   ├── Training_and_Validation_Loss_Graphs.ipynb
│   ├── Global_Interpretability.ipynb
│   ├── Grid_Based_Segmentation.ipynb
│   ├── SLIC_Segmentation.ipynb
│   ├── NonDemented_5samples.ipynb
│   ├── VeryMild_5samples.ipynb
│   ├── MildlyDemented_5samples.ipynb
│   └── ModeratelyDemented_5samples.ipynb
│
└── README.md

```
All files are provided as Jupyter notebooks and are compatible with Google Colab.

## Model Training

Model training is performed in the notebook:

- **FINAL_Kaggle_VGG16_Training.ipynb**

**Dataset**
- Alzheimer MRI Preprocessed Dataset (Mendeley Data)
- Total MRI scans: **6,400**

**Preprocessing and Augmentation**
- Image resizing
- Random rotation
- Zoom augmentation
- Horizontal and vertical flips
- Contrast adjustment

**Training Strategy**
- Class imbalance handled using **class weights**
- Evaluation metrics used:
  - Accuracy
  - AUC
  - Precision
  - Recall
  - Loss

The trained SCR-NetX model achieves **91.74% accuracy on the test set**.


## Running the Code

All notebooks can be run independently. However, a typical execution order is:

1. **FINAL_Kaggle_VGG16_Training.ipynb**  
2. **SLIC_Segmentation.ipynb**  
3. **Grid_Based_Segmentation.ipynb**  
4. **Global_Interpretability.ipynb**  
5. Class-specific sample notebooks

All experiments were designed to run directly in **Google Colab**, with no additional setup required.


## Results Summary

The proposed **SCR-NetX** model achieves competitive classification performance while maintaining strong interpretability:

- Test accuracy: **91.74%**
- High AUC with balanced precision and recall
- SHAP-based explanations consistently highlight clinically meaningful brain regions
- Background and corner regions receive near-zero importance, supporting the reliability of the explanations





