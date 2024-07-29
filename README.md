
# Table of Contents
<!-- TOC -->

- [Table of Contents](#table-of-contents)
    - [Business Understanding](#business-understanding)
        - [The business objective](#the-business-objective)
    - [Data Understanding](#data-understanding)
        - [Data Description](#data-description)
        - [EDA](#eda)
    - [Data Preparation](#data-preparation)
    - [Modeling](#modeling)
        - [Models](#models)
        - [Models evaluation metrics](#models-evaluation-metrics)
    - [Evaluation](#evaluation)
        - [Evaluation of models with the default data](#evaluation-of-models-with-the-default-data)
        - [Comparison of models trained with default data and PCA](#comparison-of-models-trained-with-default-data-and-pca)
        - [Comparison of models trained with default data and 46 features selected by RFE](#comparison-of-models-trained-with-default-data-and-46-features-selected-by-rfe)
        - [The best model and the best dataset](#the-best-model-and-the-best-dataset)
        - [Feature importance](#feature-importance)
    - [Executive summary](#executive-summary)
    - [Next steps](#next-steps)

<!-- /TOC -->

This README file provides a summary of findings for a Capstone project: A machine learning model for phishing websites detection.

The accompanying Jupyter notebook can be [found here](https://github.com/epakhomov/capstone/blob/main/scr/DataSet1_3.ipynb). 

<img src="/images/07.png" alt="Fig.1" class="center" style="width:600px;height:600;">

## Business Understanding

Despite the fact that phishing is an ancient and a very straightforward attack, phishing attacks accounted for 36% of all US data breaches in 2023. 94% of firms are hit by phishing attacks in 2023. A lot of companies and organizations still perform phishing simulation exercises with employees today. Therefore, there is a need to create an engine that would correctly identify phishing (malicious) url as such and vice versa. 

### The business objective 


There are **two business** objectives for this project:  
1. The first objective is to build a machine learning model what would correctly classify an url into two classes: a) normal url b) phishing url. An url can belong to only one class.   
2. The model should be relatively light so it could be deployed locally on target machines as well. 

The model would be available for security vendors who would like to add or improve phishing detecting capabilities.

The training data can be [found here](https://github.com/epakhomov/capstone/tree/main/data/dataset_full.csv).

## Data Understanding

### Data Description

Data was acquired through the publicly available lists of phishing and legitimate websites by Grega Vrbančič and others, from which the features presented in the datasets were extracted by the authors. They published the details of data collection [here](https://www.sciencedirect.com/science/article/pii/S2352340920313202) and published the datasets on Github [here](https://github.com/GregaVrbancic/Phishing-Dataset).

The entire dataset was divided into the following sections:
- Dataset attributes based on URL
- Dataset attributes based on Domain URL
- Dataset attributes based on URL directory
- Dataset attributes based on URL file name
- Dataset attributes based on URL parameters
- Dataset attributes based on resolving URL and external services

This division can be illustrated with Figure 1.

<img src="/images/url.jpg" alt="Fig.1" class="center" style="width:600px;height:auto;">
    
### EDA

Due to the nature of the data and the business problem, there isn't much EDA that can be performed for this dataset. There are no business value in understanding relationships between number of question marks and number of backslashes in the data, for example. I'm providing this assessment as a certified (CISSP) domain expert with 10+ experience in cybersecurity. 

With that said, it's clear that all 112 features are not required to build a model. As in a car, for example, not all car features and mechanisms have any impact on the maximum speed. Not all features of an url have any impact on the url being malicious or not.

It turns out that the domain section has near zero mean variance which might indicate its less importance as can be seen on Figure 2.

<img src="/images/01.png" alt="Fig.2" class="center" style="width:800px;height:auto;">

## Data Preparation

The original data is relatively clean. It doesn't contain categorical variables and doesn't contain missing values, so minimum data preparation was required.

## Modeling

As we discussed above, one of the business objective is to reduce the original dataset while not sacrificing the accuracy of the model.

The dataset was reduced using the following techniques:  
- Principal Component Analysis  
- Recursive feature elimination  
- VarianceThreshold selector

Resulting dataset was used in the modeling as well as the original dataset.

### Models

The following models were used:  

- Logistic regression  
- Decision tree  
- KNN classifier  
- Random Forest  
- XGBoost  

### Models evaluation metrics

For this problem, a false positive will be observed when a model labels a normal url as malicious. A false negative will be observed when a model labels a malicious url as normal. False negatives are more dangerous as a user will trust a malicious site. Therefore, we will be using the recall score.

## Evaluation

### Evaluation of models with the default data

As you can see from the image, all models performed well, above 0.9 for both recall and ROC AUC scores. Random Forest and XGBoost performed best of all and got very close scores.

<img src="/images/02.png" alt="Fig.3" class="center" style="width:800px;height:auto;">

### Comparison of models trained with default data and PCA

Most of the models scored worse with the PCA components as compared with default data:

<img src="/images/03.png" alt="Fig.3" class="center" style="width:600px;height:auto;">

### Comparison of models trained with default data and 46 features selected by RFE

Surprisingly, all models except for KNN, performed better than the models trained with the default data (97 features)

<img src="/images/04.png" alt="Fig.3" class="center" style="width:600px;height:auto;">

### The best model and the best dataset

Overall, all models performed roughly the same across all datasets except for KNN which showed a stronger sensitivity to a number of selected features. 

Random Forest and XGBoost were the top models that produced the best scores on a dataset with 46 features selected by RFE.

<img src="/images/05.png" alt="Fig.3" class="center" style="width:800px;height:auto;">

### Feature importance

SHAP values were used to calculated feature importance. The following plot depicts feature importance for class 1 (is phishing):

<img src="/images/06.png" alt="Fig.3" class="center" style="width:800px;height:auto;">

Let's discuss top three features:  
 
- length_url (total number of characters in an url) is the feature that has the most prediction impact on the target. It has both negative and positive impact. From the shap plot, we can say that the longer url, the more chances that it is phishing which intuitevely makes sense as well.  
- time_domain_activation (Domain activation time in days). Phishing domains have shorter activation times which can be seen on the plot as well: lower values negatively impact prediction of class 1 (is phishing).  
- directory_length (total number of characters of a directory in an url) typically is correlated with the lenght of url so not surprisingly we see similar behavior of this feature.


## Executive summary

Phishing attacks, despite being a simple form of cyberattack, remain a significant threat, accounting for 36% of all US data breaches in 2023. With 94% of firms affected, there's a clear need for effective tools to identify phishing URLs. This project aims to develop a machine learning model that can accurately distinguish between normal and phishing URLs, and is lightweight enough for local deployment.

Business Objectives:

- Accurate Classification: Develop a model to classify URLs as either normal or phishing with high accuracy.  
- Deployment Readiness: Ensure the model is light enough for local deployment on various machines.  

To achieve the objectives, we applied different techniques of data reduction, and utilized a number of machine learning models.

All models performed well, achieving various scores above 0.9. Random Forest and XGBoost were the top performers, especially with a reduced dataset of 46 features.

Key features influencing the model included: URL length, domain activation time, and directory length, with longer URLs and shorter domain activation times being strong indicators of phishing URL.

## Next steps
- Applying neural network models  
- Creating a prototype to test the model  
- Deploy model in a testing environment  
- Expanding scope of the research to include identification of malicious API endpoints, not just URLs
