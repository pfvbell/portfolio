# portfolio
I am currently a Fulbright Scholar at Harvard University studying the intersection of politics, education policy and data science.

# **Project 1: Using NN, RF and Logistic Regression to predict the 2020 Presidential election**
[Full Github](https://github.com/pfvbell/president)

## Predicting the 2020 Presidential Elections

I used logistic regression, Random Forest, KNN and neural networks to predict the 2020 Presidential election. Data was scraped from the US census API. Polling, turnout and voter data from 1980 was engineered to build uncertainty into the predictions. See the Github notebook for details on data cleaning, feature selection, model selection and uncertainty visualisation. A final test accuracy of 92.2% was seen on the Lasso Logistic Regression model, and the Random Forest Model saw a final test accuracy of 96%.

![](/images/lasso_preds_map_2.png)

# **Project 2: Kannada MNIST Kaggle submission**
[Full Github](/images/kannada_neuralnetwork_kaggle)

This entry was placed 252 in the kaggle competition with a final test accuracy of 91.8%. Validation Accuracy was 95.8% and train accuracy was 99.7%.
Images of kannada digits were classified as '0' or '1' using a regularised feed-forward neural network (including L2 and dropout). 2000 epochs were used, with a batch size of 32.

![](/images/one.png) ![](/images/zero.png)

I took a sequential approach, changing one hyperparameter at a time and seeing if changing that hyperparameter improved the model. If it did improve the model then I kept the change and tried a different adaptation. However, I took a logical order through the various hyperparameter options. I started by adjusting Adam. I realised that you must start with small numbers (coefficients) for L2 regulaization and increase them. Small numbers mean less penalisation in this instance. However, using too high values for the coefficients resulted in the penalisation reducing the ability for the model to train on the data and therefore resulted in lower scores. Therefore I used a value in between these extremes. My validation score is much higher than the test score on kaggle which may suggest that there is a lot of noise in the data and the model is fitting to that noise. Therefore, data augmentation would be useful in this instance.

Below is the accuracy (left) and loss (right).
![](/images/Accuracy%20and%20Loss.png)


# Project: Exploring Neural Network interpretability through predicting flight delay
[Full Github](https://github.com/pfvbell/Flights_ANN/blob/main/README.md)

### Modeling
This project mainly aims to explore the uncertainty in feedforward neural networks. First an artificial neural network was fit. This was an overfit artificial neural network, as can be seen below. The aim was not to fit a very accurate model, but rather to explore the predictions made and the certainty with which they were made. 

![](/images/train_val_loss.png)

### Interpretability step 1: Exploring feature importance
Then a logistic regression proxy model was trained using the predictions from the original artificial neural network. This allowed interpretation of the major predictors for flight delay and I found that the departure hour of the flight was the most important predictor (using sklearn's 'permutation importance' function on the proxy model.)

![](/images/feature_importance.png)

Through plotting the probability of delay against departure hour we see that the probability of delay increases as the scheduled departure hour increases. However, it seems to plateau and then decrease as the scheduled departure hour reaches later into the day. This makes sense because we would expect to see delays accruing during the day. However, it should be noted that the probability of delay changes a relatively small amount overall.

![](/images/Delay%20Probability.png)

I then plotted the predicted probabilities of delay against the main predictors identified in the permutation importance.

![](/images/dist_departure_hour.png)

It seems that departure hour is more important than flight count. Overall there seem to be lower probabilities of delay at lower levels of flight count. However, high flight counts are less associated with high delay probabilities later in the day. Indeed, high flight count seems to begin after 5am, which is not surprising. There is a correlation between Scheduled departure hour and scheduled arrival hour, and when both scheduled departure hour and scheduled arrival hour are high the probability of delay seems also to be high. When scheduled departure time and scheduled arrival time are around midnight to 1am there seems to be a higher probability of delay. Indeed, the probability of delay seems to be less closely associated with distance. However, there does seem to be some interaction between distance and scheduled departure hour. There seems to be a trend of long-haul flights departing earlier in the day being more likely to see delays as compared to later in the day.

### Interpretability step 2: Exploring and visualising uncertainty
Eight predictors were then bootstrapped to viusalise the variation accross bootstraps.

![](/images/variation.png)

It seems that there is a large probability distribution for both classes. This suggests that we cannot be too certain about our predictions for either class. Indeed, the confidence intervals are wide, which suggests that we cannot be confident that the predictions for either class are in a narrow range. Only two of the probability distributions have confidence intervals that do not reach over the threshold (0.5) into the opposite class to the true class.

# Interpretability step 3: Building an abstain bagging model
To further measure the uncertainty of the model we build a model which abstains from making predictions when it is uncertain. The Posterior Probability Ratio (the proportion of predictions which cross the 0.5 boundary).

![](/images/accuracy%20vs%20ppr.png)

The test accuracy increases as the PPR decreases, apart from an outlier result at PPR=0.2. However, it seems that there is only a very close association between test accuracy and PPR at very low PPR values. This suggests that the PPR threshold for this abstain model may need to be much lower than 0.5 if it is to be highley predictive. Depending on the level of test accuracy needed, it may have to be as low as 0.05. However, this may mean that very few observations could be used. Overall it is clear that many of the bagged predictions are not predicted with high confidence. Indeed, as the PPR decreases the proportion of test observations not abstained also increases. This relationship is close to linear.


# **Project 3: What are the most common global education indicators? (using SQL)**
[Full Project](https://www.kaggle.com/philipbell/sql-world-bank)

Educational Research is relatively [new](http://https://tannerlectures.utah.edu/Allen%20manuscript.pdf) as a field distinct from other social sciences, such as economics and psychology. 

The World Bank International Education database provides a landscape view of both indicators of educational achievement, and also the types of studies conducted. Mining the information on this large dataset therefore provides useful insights into the way in which measurement of educational achievement may itself impact the nature of the education (akin to what Physicists call the 'observer effect'.

Add graph of change in spending over time.

Sub-questions included the average spending as a percentage of GDP for all countries, as well as how the amount of data gathered differs by year.

Add Image of output (as graph).

# **Project 4: Covid data scraper**
[Full Github](https://github.com/pfvbell/covid_data_scraper)

## Scraping and Analysing Covid data

Up-to-date covid data was scraped from https://usafacts.org/visualizations/coronavirus-covid-19-spread-map/state. This was then analysed in order to find the highest number of deaths per county and the highest death rate.

After merging voting and demographic data with the scraped data, this was then used to analyse how covid death rates were related to other demographic details of an area. I expected to find a relationship between density and voters for Clinton or Trump. Indeed, there did seem to be a potential relationship since the average density value for a county with a high proportion of Clinton voters was much higher than a county with a high density of Trump voters. I also found a potential link between counties with a high proportion of people with cancer and counties with a high proportion of people voting Trump. Indeed, when I used the interquartile ranges of the describe tables from the counties with a high proportion voting Trump I was able to use those to create new subsets of the data and thereby see that these counties, conversely, had low levels of unemployed.

