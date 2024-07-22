**A machine learning model for phishing websites detection.**

# Table of Contents
<!-- TOC -->

- [Table of Contents](#table-of-contents)
    - [Introduction](#introduction)
    - [The objective and the data](#the-objective-and-the-data)
        - [The business objective](#the-business-objective)
    - [The methods](#the-methods)
    - [Models evaluation metrics](#models-evaluation-metrics)
    - [Data quality and data preparation highlights](#data-quality-and-data-preparation-highlights)
    - [Models performance with the default parameters.](#models-performance-with-the-default-parameters)
    - [Hyperparameters tuning](#hyperparameters-tuning)
    - [Feature selection](#feature-selection)
    - [Results and discussion](#results-and-discussion)
        - [Precision score interpretation](#precision-score-interpretation)
    - [Next steps](#next-steps)

<!-- /TOC -->

## Introduction

This README file provides a summary of findings for a Capstone project: A machine learning model for phishing websites detection.

The accompanying Jupyter notebook can be [found here](https://github.com/epakhomov/capstone/blob/main/scr/DataSet1_3.ipynb). 

## The objective and the data

The objective of this project is to build a machine learning model what would correctly classify an url into two classes: 1) normal url 2) phishing url. An url can belong to only one class. The training data can be [found here](https://github.com/epakhomov/capstone/tree/main/data/dataset_full.csv).


### The business objective 

Despite the fact that phishing is an ancient and a very straightforward attack, phishing attacks accounted for 36% of all US data breaches in 2023. 94% of firms are hit by phishing attacks in 2023. A lot of companies and organizations still perform phishing simulation exercises with employees today. Therefore, there is a need to create an engine that would correctly identify phishing (malicious) url as such and vice versa. 


## The methods

The methodology for this assignment was based on CRISP_DM framework and included standard ML stages like Business and Data understanding, Data preparation, etc. 

## Models evaluation metrics

For this problem, a false positive will be observed when a model labels a normal url as malicious. A false negative will be observed when a model labels a malicious url as normal. False negatives are more dangerous as a user will trust a malicious site. Therefore, we will be using the recall score.


## Data quality and data preparation highlights

The data had no missing values and no categorical values. Standard scaled was applied.

## Models performance with the default parameters.

The recall scores each model can be found in Table 1.

|  Model  | Train score | Test score|
|---------|-------------|-----------|
| Dummy   | 0.0         | 0.0       |
| Logistic| 0.916	    | 0.917     |    
| KNN     | 0.949       | 0.933     |   
| D. Tree | 1.0         | 0.93      |
| SVM     | 0.93        | 0.929     |

Table 1. The precision score for models with default hyperparameters.

## Hyperparameters tuning

TBD

## Feature selection 

TBD


## Results and discussion

### Precision score interpretation

TBD

## Next steps

TBD