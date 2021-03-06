# Credit Card Fraud Detection using LSTM Network

<p align="center">
  <img src="../metadata/gif/creditcard.gif">
</p>

## Overview 
This examples show Credit Card Transaction Fraud Detection.  

The patterns of the non-fraud transactions are learned and captured in order to identify  
the outliers which can be classified as high risk for transaction frauds.

This is accomplished in this example using a simple LSTM Autoencoder.  
Reconstruction error should be low for stereotypical example, whereas outliers should have high reconstruction error.

While fraud detection normally modelled with unlabelled data,  
the availability of labels in this example further ease the process of validation

This example is model with a fairly large amount of data, closing to 300 thousand data points.   
The data set is highly unbalanced with the ratio of 577 (normal) : 1 (fraud), adding complexity to the data modelling.  
In another words, modelling with a model with softmax output layer would propagate bias.

## How to Run
 1. Download CreditCardFraud.zip file from this link https://drive.google.com/file/d/1ye6kjPQzt5VcQUuwLaPsxUqnAli2AoXe/view?usp=sharingv
 2. In App.java, set zipFilePath to your machine absolute path to CreditCardFraud.zip  
    For example  
    `
    File zipFilePath = new File("C:\\Users\\johndoe\\Downloads\\" +  "CreditCardFraud.zip");
    `
 3. Run App.java

## File Structure 
```
credit-card-fraud 
│   
│───src/main/java/com/codenamewei/CreditCardFraud/App.java    
│
│───src/main/java/com/codenamewei/python  
│     └─────DataPreprocessing
│           │   Credit-Card-Data-Cleaning_0.ipynb
│           │   Credit-Card-Data_Splitting_1.ipynb
│   
└    └─────ResultPostProcessing
            │   Credit-Card-Result-Visualization.ipynb
```

**App.java:**
- The main file for modelling. 

**Credit-Card-Data-Cleaning_0.ipynb:**  
- Remove first row of the data(column names) and first column of the data(Time feature).
 
**Credit-Card-Data_Splitting_1.ipynb:**  
- Normalize the total transaction column of the data
- Split data points into feature and labels and store as .csv.

**Credit-Card-Result-Visualization.ipynb:**
- Visualize the results of the testing data and plot recall-precision curve.  

## Originality of Data Sources

Data is retrieved from https://www.kaggle.com/mlg-ulb/creditcardfraud.  
It is of 2 days of transactions data from European cardholders in September 2013. 

Yet this is not the data this example used in modelling directly.

Preprocessing steps below are done to obtain the current CreditCardFraud.zip data for training and testing.    
Yet if you go for CreditCardFraud.zip directly, proceed to **Training and Testing Data** subsection. 

(1) Drop the time column (For modelling with LSTM, time feature is not necessary)  
(2) Drop the row with name of the columns (Time, V1, V2, V3 ...)  
(3) Normalize the total amount transaction column into the range [-1, 1].   
(4) Split each data point into feature(.csv) and label(.csv) and place in separate directories according to the label  
(5) Redistribute the files into training and testing data sets.  

Each data point(.csv) have a file(.csv) with the same name in the *_label.  
For example, train_data_feature/0.csv<-->train_data_label/0.csv

Data cleansed and proprocessed is further segmented into training and testing dataset,  
which is further elaborated in next section. 

### Training and Testing Data
Number of data points for whole dataset:
- Non-Fraud Data: 284315  
- Fraud Data    :   492

The dataset is further partitioned into training and testing dataset.

Number of data points for training dataset:
- Non-Fraud Data : 255 884   
  File Index: [0.csv - 255883.csv]
 
Number of data points for testing dataset:
- Non Fraud Data : 28431  
  File Name Index: [255884.csv - 284314.csv]
- Fraud Data     : 492  
  File Name Index: [284315.csv - 284806.csv]

These dataset is then zipped and stored as CreditCardFraud.zip.

**Data Structure of CreditCardFraud.zip**

Data structure and distribution in CreditCardFraud.zip is elaborated as follows
```
CreditCardFraud.zip
│
└───train_data_feature
│   │   0.csv
│   │   1.csv
│   │   ...
│   │   99999.csv
│   
└───train_data_label
│   │   0.csv
│   │   1.csv
│   │   ...
│   │   99999.csv
│   
└───test_data_feature
│   │   0.csv
│   │   1.csv
│   │   ...
│   │   8489.csv
│   
└───test_data_label
│   │   0.csv
│   │   1.csv
│   │   ...
│   │   8489.csv
```
