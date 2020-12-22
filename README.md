# portfolio
Phil Bell's Data Science Portfolio


# Project 1: Using NN, RF and Logistic Regression to predict the 2020 Presidential election
[Full Github](https://github.com/pfvbell/president)

## Predicting the 2020 Presidential Elections

Modelling US presidential elections, in particular, is especially difficult due to the lack of example elections, as there have only been 58 presidential elections in the history of the US. This problem is exacerbated by the unique circumstances surrounding the 2020 election, largely due to the implications of the COVID-19 pandemic. Though only three incumbent presidents have lost in the last 100 years, President Trump is facing growing scrutiny for his response (or lack thereof) to the pandemic and its impact on the economy and the welfare of American citizens, and Joe Biden has maintained a consistent lead over incumbent President Trump in opinion polls before the election [1]. The widespread usage of mail-in ballots will also change the voter turnout and voter demographic, further influencing the result of the election.

The Democrats are favored to win the House, as they gained 41 seats in the 2018 midterm election and hold a strong majority of seats. The Senate vote, however, is much closer, as the Republicans currently hold a 53-45 majority, with 23 Republican seats, compared to 12 Democratic seats, up for reelection—this election, the Democratic party has the potential to win the House, Senate, and the Presidency [2].

These political, social, and economic consequences make the task of predicting the results all the more important. Not only is some level of certainty in the likely outcome important for calming business and markets in the wake of the COVID-19 pandemic, it is also important for restoring Americans’ confidence in democracy and the democratic process.

In order to select the best model four sets of models were trained and the best one was selected based on the validation accuracy ('dev in the figures').


![](https://github.com/pfvbell/president/blob/main/Graph%20of%20Predictors.png)


Data Description
The FiveThirtyEight database was used to get the raw data for all polls conducted from 1980 to 2020 [3]. Some of the polling data from early elections (including 1980 and 1984) was missing and was imputed using a linear regression model based on previous polling results. The US Election Project, from the University of Florida, was used for voter turnout data and demographic data from the electorate, including voting age population and prison population [4]. Election results for each election since 1980, by state, were downloaded from the MIT Election Data Science Lab [5]. The 2020 election results were scraped from the New York Times [6]. The data from the 10 elections from 1980-2016 was split into a training set with 410 observations and a validation set with 100 observations. The test set, with 2020 data, contained 51 observations (all 50 states and Washington, D.C.). The response variable was whether the Democrats had won that state (0=Republican, 1=Democrat). 

Here we see the results from the 2012 election:


![](https://github.com/pfvbell/president/blob/main/2012_results_map.png)

### EDA
The best predictor, from a t-test analysis, was polls_outcome, which indicated the party favored to win in state-wide opinion polls. However, there was uncertainty associated with polls_outcome. 


![](https://github.com/pfvbell/president/blob/main/2020_polls_dist.png)


From the distribution of 2020 polls (above) we can see that some states are more likely to be polled than others. For example, Arizona and Florida were polled more in 2020 than other states, compared to states such as West Virginia and Wyoming. It seems that states where Democrats and Republicans are closer have more polls taken. This makes sense because there is likely to be a greater premium on predicting these swing states. However, in order to gain a baseline model polls were initially averaged for each year and each state. To introduce further information about the accuracy of the polls into the model, we added a new variable, “polls_strike_rate”, which represented the proportion of previous elections (since 1980) that had been correctly predicted by polls for that state. 

Feature selection was based on the train and validation accuracies for different combinations of predictors. The final Logistic Regression Model (resularised with Lasso) used all predictors. Indeed, interactions were added to the predictors, initially through interacting the top predictors, and latterly through iterative observation of their effect on model accuracy scores. This was done because it seemed likely that interactions between variables would be important. Firstly, from the pariplot we included we could say that, for example, non-citizen variable seems to be associated with vep, and non-citizen and prison population. Secondly, it was understood that ‘polls_strike_rate’ clearly could interact with ‘polls_margin’ and ‘polls_outcome’ because information about the previous success of the polls in a particular state (‘polls_strike_rate’), when combined with ‘polls_outcome’, could have more predictive power.

Here we see the percentage of correct poll outcomes for each state from 1980-2016 (i.e. polls_strike_rate variable for the 2016 election)


![](https://github.com/pfvbell/president/blob/main/strike_rate_map.jpg)


Above we can see that polls in some states, such as Florida and North Carolina, Wisconsin, Pennsylvania and Michigan have been less predictive of the outcome of the election compared to polls in other states.

### Model Selection
The accuracy of four sets of models (logistic regression, KNN, random forest and neural networks) was calculated on the training set and the evaluation set. (See appendix 3)

First a logistic regression model was fit. This was the baseline model using one predictor, resulting in a validation accuracy score of 81% and training accuracy score of 85%. A logistic regression model using all predictors resulted in a lower training score (80%) and the same validation score (81%). The relatively low accuracy scores suggested that there may be overfitting taking place, and therefore a regularised model was fit. A regularised logistic regression model (using Lasso) was more accurate (92% validation accuracy) than a logistic regression model with all the predictors, but unregularised. Indeed, from the coefficients it is clear that 12  coefficients were sent to 0 by the lasso regularisation, which suggests that the unregularised model may be overfitting and therefore was increasing bias at the expense of variance. 

Since Lasso had succeeded in simplifying the model, and in doing so improved the accuracy from the unregularised model, Logistic Regression with PCA might also improve the accuracy of the initial baseline logistic regression model by simplifying it. A logistic Regression model using 2 principal components resulted in a validation accuracy of 84% while a logistic regression model using 15 principal components resulted in a validation accuracy of 88%. Though the PCA models performed better than baseline Logistic Regression they did not surpass the Lasso Logistic Regression validation score. Next an optimised KNN was trained. The best K was found to be k=5. However, the validation scores were not as high as they were for the regularised logistic regression or PCA logistic regression.

Here we see the first PCs plotting against eachother:


![](https://github.com/pfvbell/president/blob/main/PCA_division.png)


We can also see the amount of predictor variation that each PC cumulatively explains:

![](https://github.com/pfvbell/president/blob/main/PCA%20Variance.png)


From the relatively higher performance of the Lasso compared to the unregularized logistic regression we know that preventing overfitting is important to increasing performance. 

### Results and Conclusions

![](https://github.com/pfvbell/president/blob/main/Graph%20of%20Predictors.png)


Based on these accuracies Lasso Logistic Regression model was chosen, as its validation  accuracy (91%) was higher than the Random Forest or Neural Network validation scores, even though its training accuracy was not as high as the random Forest training accuracy. The final model chosen was therefore the Lasso model with a final accuracy on the test set of 92.2%.

Lasso Logistic Regression Probabilities of prediction of Republican or Democrat for each state:
![](https://github.com/pfvbell/president/blob/main/lasso_preds_map_2.png)

Random Forest Probabilities of prediction of Republican or Democrat for each state:
![](https://github.com/pfvbell/president/blob/main/rf_preds_map_2.png)

It is useful to note that the logistic lasso model and neural network models were less secure in their predictions compared to the random forest model. Therefore, the random forest model is more likely to vary when applied to different sets of data. This makes the model overly flexible, which is another reason why lasso logistic regression is preferable as the final model.

### Limitations
There were systematic inaccuracies with 2020 polling data that were not captured with previous polls. In 2016 the major inaccuracy was caused by undersampling of non-college voters. This sampling error was corrected by most polling organisations in 2020 [7]. However, there are clearly other errors in the 2020 data that have not yet been unearthed. One theory is that those who refuse phone surveys are more likely to be anti-establishment, and therefore polling reflects this.

It is not clear that there is a trend of polling errors between elections on a geographical level. Indeed, the polls predicted some states very closely (for example Minnesota) and some very poorly, such as Florida in 2020. It is not yet clear why this is the case.

Due to the inherent uncertainty in using polling data to predict election results in future this project could be improved by more succinctly visualising and communicating the prediction uncertainties. In future it may be necessary to move beyond the dichotomy between so-called ‘fundamentals models’ (using demographic and economic data) and polling data, and triangulate both these approaches using new methods, such as sentiment analysis and social network graph analysis.

### References
FiveThirtyEight Election Forecast, 2020. https://projects.fivethirtyeight.com/2020-election-forecast/. Accessed November 3, 2020.
Wikipedia contributors. (2020, December 12). 2020 United States elections. In Wikipedia, The Free Encyclopedia. Retrieved December 13, 2020, from https://en.wikipedia.org/w/index.php?title=2020_United_States_elections&oldid=993755354
FiveThirtyEight Polling Database, 2020. https://projects.fivethirtyeight.com/polls/. Accessed November 3, 2020.
McDonald, Michael P. 2020. "Voter Turnout." United States Elections Project. Accessed November 3, 2020, from http://www.electproject.org/home/voter-turnout/voter-turnout-data
MIT Election Data and Science Lab, 2017, "U.S. President 1976–2016", https://doi.org/10.7910/DVN/42MVDX, Harvard Dataverse, V5, UNF:6:Mw0hOUHAijKPTVRAe5jJvg==
“2020 Live Election Results”, New York Times, https://github.com/favstats/USElection2020-NYT-Results/blob/master/data/2020-11-07%2014-15-14/results_president.csv. Accessed November 7, 2020.
Hatley, N. and Kennedy, C. ‘A Resource for State Preelection Polling’, 2020, Pew Research Centre.
MIT Election Data and Science Lab, 2017, "U.S. Senate 1976–2018", https://doi.org/10.7910/DVN/PEJ5QU, Harvard Dataverse, V4, UNF:6:WzSZLQX8O9Nk6RKWwkjx9g==
Wikipedia contributors. (2020, December 13). 2020 United States Senate elections. In Wikipedia, The Free Encyclopedia. Retrieved November 18, 2020, from https://en.wikipedia.org/w/index.php?title=2020_United_States_Senate_elections&oldid=993938893
U.S. Bureau of Economic Analysis, 2019, “Annual State Personal Income and Employment.” Accessed November 18, 2020, from https://apps.bea.gov/regional/docs/DataAvailability.cfm
U.S. Bureau of Economic Analysis, 2019, “Annual Gross Domestic Product by State.” Accessed November 18, 2020, from https://apps.bea.gov/regional/docs/DataAvailability.cfm
U.S. Bureau of Labor Statistics, 2020, “Local Area Unemployment Statistics.” Accessed November 18, 2020, from https://beta.bls.gov/dataQuery/find?fq=survey:%5Bla%5D&s=popularity:D
Steven Manson, Jonathan Schroeder, David Van Riper, Tracy Kugler, and Steven Ruggles. IPUMS National Historical Geographic Information System: Version 15.0. Minneapolis, MN: IPUMS. 2020. http://doi.org/10.18128/D050.V15.0
U.S. Census Bureau. “American Community Survey 1-Year Data (2005-2019).” The United States Census Bureau, www.census.gov/data/developers/data-sets/acs-1year.html. Accessed October 15, 2020.
Wikipedia contributors. (2020, December 13). List of former United States senators. In Wikipedia, The Free Encyclopedia. Retrieved November 18, 2020, from https://en.wikipedia.org/w/index.php?title=List_of_former_United_States_senators&oldid=993991258
Wikipedia contributors. (2020, December 7). List of current United States senators. In Wikipedia, The Free Encyclopedia. Retrieved November 18, 2020, from https://en.wikipedia.org/w/index.php?title=List_of_current_United_States_senators&oldid=992916830
Berwick, R. “An Idiot’s guide to Support vector machines (SVMs).” MIT 6.034, November 10, 2011, MIT. PDF.
MIT Election Data and Science Lab, 2017, "U.S. House 1976–2018", https://doi.org/10.7910/DVN/IG0UN2, Harvard Dataverse, V8, UNF:6:p05gglERZ/Fe5LP4RarxeA==
Wikipedia contributors. (2020, December 13). 2020 United States House of Representatives elections. In Wikipedia, The Free Encyclopedia. Retrieved 00:12, December 14, 2020, from https://en.wikipedia.org/w/index.php?title=2020_United_States_House_of_Representatives_elections&oldid=993939371
Lichtman, Allan. “The Keys to the White House: Forecast for 2020 · 2.4.” Harvard Data Science Review, PubPub, 27 Oct. 2020, hdsr.mitpress.mit.edu/pub/xhgpcyoa/release/2. 


# Project 2: Kannada MNIST Kaggle submission
[Full Github](https://github.com/pfvbell/kannada_neuralnetwork_kaggle)

This entry was placed 252 in the kaggle competition with a final test accuracy of 91.8%. Validation Accuracy was 95.8% and train accuracy was 99.7%.
Images of kannada digits were classified as '0' or '1' using a regularised feed-forward neural network (including L2 and dropout). 2000 epochs were used, with a batch size of 32.

![](https://github.com/pfvbell/kannada_neuralnetwork_kaggle/blob/main/one.png) ![](https://github.com/pfvbell/kannada_neuralnetwork_kaggle/blob/main/zero.png)

I took a sequential approach, changing one hyperparameter at a time and seeing if changing that hyperparameter improved the model. If it did improve the model then I kept the change and tried a different adaptation. However, I took a logical order through the various hyperparameter options. I started by adjusting Adam. I realised that you must start with small numbers (coefficients) for L2 regulaization and increase them. Small numbers mean less penalisation in this instance. However, using too high values for the coefficients resulted in the penalisation reducing the ability for the model to train on the data and therefore resulted in lower scores. Therefore I used a value in between these extremes. My validation score is much higher than the test score on kaggle which may suggest that there is a lot of noise in the data and the model is fitting to that noise. Therefore, data augmentation would be useful in this instance.

Below is the accuracy (left) and loss (right).
![](https://github.com/pfvbell/kannada_neuralnetwork_kaggle/blob/main/Accuracy%20and%20Loss.png)


# Project: Exploring Neural Network interpretability through predicting flight delay
[Full Github](https://github.com/pfvbell/Flights_ANN/blob/main/README.md)

### Modeling
This project mainly aims to explore the uncertainty in feedforward neural networks. First an artificial neural network was fit. This was an overfit artificial neural network, as can be seen below. The aim was not to fit a very accurate model, but rather to explore the predictions made and the certainty with which they were made. 

![](https://github.com/pfvbell/Flights_ANN/blob/main/train_val_loss.png)

### Interpretability step 1: Exploring feature importance
Then a logistic regression proxy model was trained using the predictions from the original artificial neural network. This allowed interpretation of the major predictors for flight delay and I found that the departure hour of the flight was the most important predictor (using sklearn's 'permutation importance' function on the proxy model.)

![](https://github.com/pfvbell/Flights_ANN/blob/main/feature_importance.png)

Through plotting the probability of delay against departure hour we see that the probability of delay increases as the scheduled departure hour increases. However, it seems to plateau and then decrease as the scheduled departure hour reaches later into the day. This makes sense because we would expect to see delays accruing during the day. However, it should be noted that the probability of delay changes a relatively small amount overall.

![](https://github.com/pfvbell/Flights_ANN/blob/main/Delay%20Probability.png)

I then plotted the predicted probabilities of delay against the main predictors identified in the permutation importance.

![](https://github.com/pfvbell/Flights_ANN/blob/main/dist_departure_hour.png)

It seems that departure hour is more important than flight count. Overall there seem to be lower probabilities of delay at lower levels of flight count. However, high flight counts are less associated with high delay probabilities later in the day. Indeed, high flight count seems to begin after 5am, which is not surprising. There is a correlation between Scheduled departure hour and scheduled arrival hour, and when both scheduled departure hour and scheduled arrival hour are high the probability of delay seems also to be high. When scheduled departure time and scheduled arrival time are around midnight to 1am there seems to be a higher probability of delay. Indeed, the probability of delay seems to be less closely associated with distance. However, there does seem to be some interaction between distance and scheduled departure hour. There seems to be a trend of long-haul flights departing earlier in the day being more likely to see delays as compared to later in the day.

### Interpretability step 2: Exploring and visualising uncertainty
Eight predictors were then bootstrapped to viusalise the variation accross bootstraps.

![](https://github.com/pfvbell/Flights_ANN/blob/main/variation.png)

It seems that there is a large probability distribution for both classes. This suggests that we cannot be too certain about our predictions for either class. Indeed, the confidence intervals are wide, which suggests that we cannot be confident that the predictions for either class are in a narrow range. Only two of the probability distributions have confidence intervals that do not reach over the threshold (0.5) into the opposite class to the true class.

# Interpretability step 3: Building an abstain bagging model
To further measure the uncertainty of the model we build a model which abstains from making predictions when it is uncertain. The Posterior Probability Ratio (the proportion of predictions which cross the 0.5 boundary).

![](https://github.com/pfvbell/Flights_ANN/blob/main/accuracy%20vs%20ppr.png)

The test accuracy increases as the PPR decreases, apart from an outlier result at PPR=0.2. However, it seems that there is only a very close association between test accuracy and PPR at very low PPR values. This suggests that the PPR threshold for this abstain model may need to be much lower than 0.5 if it is to be highley predictive. Depending on the level of test accuracy needed, it may have to be as low as 0.05. However, this may mean that very few observations could be used. Overall it is clear that many of the bagged predictions are not predicted with high confidence. Indeed, as the PPR decreases the proportion of test observations not abstained also increases. This relationship is close to linear.


# Project : What are the most common global education indicators? (using SQL)
[Full Project](https://www.kaggle.com/philipbell/sql-world-bank)

Educational Research is relatively [new](http://https://tannerlectures.utah.edu/Allen%20manuscript.pdf) as a field distinct from other social sciences, such as economics and psychology. 

The World Bank International Education database provides a landscape view of both indicators of educational achievement, and also the types of studies conducted. Mining the information on this large dataset therefore provides useful insights into the way in which measurement of educational achievement may itself impact the nature of the education (akin to what Physicists call the 'observer effect'.

Add graph of change in spending over time.

Sub-questions included the average spending as a percentage of GDP for all countries, as well as how the amount of data gathered differs by year.

Add Image of output (as graph).

# Project: Covid data scraper
[Full Github](https://github.com/pfvbell/covid_data_scraper)
Scraping and Analysing Covid data

Up-to-date covid data was scraped from https://usafacts.org/visualizations/coronavirus-covid-19-spread-map/state. This was then analysed in order to find the highest number of deaths per county and the highest death rate.

After merging voting and demographic data with the scraped data, this was then used to analyse how covid death rates were related to other demographic details of an area. I expected to find a relationship between density and voters for Clinton or Trump. Indeed, there did seem to be a potential relationship since the average density value for a county with a high proportion of Clinton voters was much higher than a county with a high density of Trump voters. I also found a potential link between counties with a high proportion of people with cancer and counties with a high proportion of people voting Trump. Indeed, when I used the interquartile ranges of the describe tables from the counties with a high proportion voting Trump I was able to use those to create new subsets of the data and thereby see that these counties, conversely, had low levels of unemployed.

