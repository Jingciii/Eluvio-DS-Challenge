# Eluvio-DS-Challenge

Repository for Eluvio Data Science Challenge. The dataset contains 8 fields including 

 time_created | date_created | up_votes | down_votes | title | over_18 | author | category 
 
 among which "down_votes" and "category" are single-value columns so I dropped them. The rest are used for analysis and predicting up_votes given the above information.
 
## Notebook
 
 **ETL.ipynb**
 
 Scripts for data exploration, feature engineering and feature selection.
 
 **Model Development.ipynb**
 
 Scripts to build model for the prediction, as well as hyper-parameter tuning and comparison on different models
 
 **Model Explaination.ipynb**
 
 Scripts to explain the outputs of the developed models
 
 