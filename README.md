
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
        - [Comparison of models train with default data and PCA](#comparison-of-models-train-with-default-data-and-pca)
    - [Executive summary](#executive-summary)
    - [Next steps](#next-steps)

<!-- /TOC -->

This README file provides a summary of findings for a Capstone project: A machine learning model for phishing websites detection.

The accompanying Jupyter notebook can be [found here](https://github.com/epakhomov/capstone/blob/main/scr/DataSet1_3.ipynb). 

## Business Understanding

Despite the fact that phishing is an ancient and a very straightforward attack, phishing attacks accounted for 36% of all US data breaches in 2023. 94% of firms are hit by phishing attacks in 2023. A lot of companies and organizations still perform phishing simulation exercises with employees today. Therefore, there is a need to create an engine that would correctly identify phishing (malicious) url as such and vice versa. 

### The business objective 

There are **two business** objectives for this project:  
1.The first objective is to build a machine learning model what would correctly classify an url into two classes: a) normal url b) phishing url. An url can belong to only one class.   
2.The model should be relatively light so it could be deployed locally on target machines as well. 

The model would be available for security vendors who would like to add or improve phishing detecting capabilities.

The training data can be [found here](https://github.com/epakhomov/capstone/tree/main/data/dataset_full.csv).

## Data Understanding

### Data Description

Data was acquired through the publicly available lists of phishing and legitimate websites by Grega Vrbančič and others, from which the features presented in the datasets were extracted by the authors. They published the details of data collection [here](https://www.sciencedirect.com/science/article/pii/S2352340920313202) and published the datasets on Github [here](https://github.com/GregaVrbancic/Phishing-Dataset).

The entire dataset was devided into the following sections:
- Dataset attributes based on URL
- Dataset attributes based on Domain URL
- Dataset attributes based on URL directory
- Dataset attributes based on URL file name
- Dataset attributes based on URL parameters
- Dataset attributes based on resolving URL and external services

This division can be illustrated with Figure 1.

<img src="/images/url.jpg" alt="Fig.1" class="center" style="width:600px;height:auto;">
    
### EDA

Due to the nature of the data and the business problem, there isn't much EDA that can be performed for this dataset. There are no business value in understanding relationships between number of question marks and number of backslashs in the data, for example. I'm providing this assessment as a certified (CISSP) domain expert with 10+ experience in cybersecurity. 

With that said, it's clear that all 112 features are not required to build a model. As in a car, for example, not all car features and mechanisms have any impact on the maximum speed. Not all features of an url have any impact on the url being malicious or not.

It turns out that the domain section has near zero mean variance which might indicate its less importance as can be seen on Figure 2.

<img src="/images/01.png" alt="Fig.2" class="center" style="width:800px;height:auto;">

## Data Preparation

The original data is relatively clean. It doesn't contain categorical variables and doesn't contain missing values, so minimum data preparation was required.

## Modeling

As we discussed above, one of the business objective is to reduce the original dataset while not sacrificing the accuracy of the model.

The dataset was reduced using the following techniques:  
-Principal Component Analysis  
-Recursive feature elimination  
-VarianceThreshold selector

Resulting dataset was used in the modeling as well as the original dataset.

### Models

The following models were used:  

-Logistic regression  
-Decision tree  
-KNN classifier  
-Random Forest  
-XGBoost  

### Models evaluation metrics

For this problem, a false positive will be observed when a model labels a normal url as malicious. A false negative will be observed when a model labels a malicious url as normal. False negatives are more dangerous as a user will trust a malicious site. Therefore, we will be using the recall score.

## Evaluation

### Evaluation of models with the default data

As you can see from the image, all models performed well, above 0.9 for both recall and ROC AUC scores. Random Forest and XGBoost performed best of all and got very close scores.

<img src="/images/02.png" alt="Fig.3" class="center" style="width:800px;height:auto;">

### Comparison of models train with default data and PCA

Most of the model scored worse with the PCA components as compared with default data:

<img src="/images/03.png" alt="Fig.3" class="center" style="width:600px;height:auto;">

## Executive summary

## Next steps
