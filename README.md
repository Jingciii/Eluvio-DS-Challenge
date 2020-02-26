# Eluvio-DS-Challenge

Repository for Eluvio Data Science Challenge. The dataset contains 8 fields including 

 time_created | date_created | up_votes | down_votes | title | over_18 | author | category 
 
 among which "down_votes" and "category" are single-value columns so I dropped them. The rest are used for analysis and predicting up_votes given the above information.
 
## Notebooks
 
 **ETL.ipynb**
 
 Scripts for data exploration, feature engineering and feature selection.
 
 **Model Development.ipynb**
 
 Scripts to build model for the prediction, as well as hyper-parameter tuning and comparison on different models
 
 **Model Explaination.ipynb**
 
 Scripts to explain the outputs of the developed models
 
 
## Takeaways
 
  - The upvotes for the news have increase tendency as year goes by, so does the number of news in the dataset.  Within each year, there are more news created on weekend than weekdays and average upvotes on weekend are significantly higher than in weekdays. This partten is also found for each day around midday and midnight vs. rest of hours. So I used *whether the news is created on weekend*,  *whether the news is created around midday or midnight*, *year of creation to now* as predictors
  - The number of authors below 18 is 1500 times larger than that of author over 18. There are much more variance within the younger group in terms of upvotes the received. The average upvotes received for authors over 18 is three times larger than that below 18. Seldom authors create news got extremely high upvotes, but intuitively, a author creates a piece of news receiving high upvotes is more likely to create another one getting such high upvotes. So I took the third quartile of the 25% highest upvotes which is 406 and used *whether the author created a news with upvotes larger than 406* and *whether the author is over 18* as predictors
  - Interestingly, the length of news title seems have positive correlation with upvotes it received until the length reaches around 35. This feature also serves as a predictor
  - From topic analysis, this set of news are mostly about international politics. There are latent topics about government, war in Middle East, Nuclear, Russia and China. Details can be seen in `./vis/lda_topic.html`
  - I conducted feature selection on meta feature (time and author related variables) and text feature (vectorization for news title) separately. The feature selection process uses a simple linear regression with the set of features and the upvotes column and keep the features with p-value lower than 0.05. It turns out that all meta features are important for the prediction and around 1300 text features are kept.
  - Three models are used for prediction: *Linear Regression*, *Random Forest* and *XGBoost*. Linear regression has the closest errors on train set and test set. Tree-based models have tendency of overftting if setting the complexity too high. All three models have similar performance on test set, but XGBoost got sightly better RMSE and MAE comparing the rest two
  - In `Model Explaination` I used [shap](https://github.com/slundberg/shap) to explain the output for each model. It turns out that all three models agree that `authors who create news with high upvotes`, `years to now`, `whether it's created on weekend` and `title length` are predictors with largest contribution to the final output. For the text features, words related to countries and regions like `us`, `china`, `syria` have high contribution. Apart from that, words like `snowden`, `drug`, `old` are also important features for the prediction
