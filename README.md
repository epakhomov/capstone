
# Table of Contents
<!-- TOC -->

- [Table of Contents](#table-of-contents)
    - [Business Understanding](#business-understanding)
        - [The business objective](#the-business-objective)
    - [Data Understanding](#data-understanding)
        - [EDA](#eda)
    - [Data Preparation](#data-preparation)
    - [Modeling](#modeling)
        - [Models evaluation metrics](#models-evaluation-metrics)
    - [Evaluation](#evaluation)

<!-- /TOC -->

This README file provides a summary of findings for a Capstone project: A machine learning model for phishing websites detection.

The accompanying Jupyter notebook can be [found here](https://github.com/epakhomov/capstone/blob/main/scr/DataSet1_3.ipynb). 

## Business Understanding

The objective of this project is to build a machine learning model what would correctly classify an url into two classes: 1) normal url 2) phishing url. An url can belong to only one class. The training data can be [found here](https://github.com/epakhomov/capstone/tree/main/data/dataset_full.csv).


### The business objective 

Despite the fact that phishing is an ancient and a very straightforward attack, phishing attacks accounted for 36% of all US data breaches in 2023. 94% of firms are hit by phishing attacks in 2023. A lot of companies and organizations still perform phishing simulation exercises with employees today. Therefore, there is a need to create an engine that would correctly identify phishing (malicious) url as such and vice versa. 

## Data Understanding

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
It turns out that the domain section has near zero mean variance which might indicate its less importance as can be seen on Figure 2.

<img src="/images/01.png" alt="Fig.2" class="center" style="width:600px;height:auto;">




## Data Preparation

## Modeling

### Models evaluation metrics

For this problem, a false positive will be observed when a model labels a normal url as malicious. A false negative will be observed when a model labels a malicious url as normal. False negatives are more dangerous as a user will trust a malicious site. Therefore, we will be using the recall score.

## Evaluation
