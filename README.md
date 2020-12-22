**Phil Bell's data science portfolio**

I am currently a Fulbright Scholar at Harvard University studying the intersection of politics, education policy and data science. Email me at pbell@gse.harvard.edu.

# **Project 1: Using NN, RF and Logistic Regression to predict the 2020 Presidential election**
[Full Github](https://github.com/pfvbell/president)

I used logistic regression, Random Forest, KNN and neural networks to predict the 2020 Presidential election. Data was scraped from the US census API. Polling, turnout and voter data from 1980 was engineered to build uncertainty into the predictions. See the [Github notebook](https://github.com/pfvbell/president/blob/main/README.md) for details on data cleaning, feature selection, model selection and uncertainty visualisation. A final test accuracy of 92.2% was seen on the Lasso Logistic Regression model, and the Random Forest Model saw a final test accuracy of 96%.

![](/images/lasso_preds_map_2.png)

# **Project 2: Kannada MNIST Kaggle submission**
[Full Github](https://github.com/pfvbell/kannada_neuralnetwork_kaggle)

![](/images/one.png) ![](/images/zero.png)

This entry was placed 252 in the kaggle competition with a final test accuracy of 92.8%. Validation Accuracy was 95.8% and train accuracy was 99.7%.
Images of kannada digits were classified as '0' or '1' using a regularised feed-forward neural network (including L2 and dropout). 2000 epochs were used, with a batch size of 32. See the [Github Readme](https://github.com/pfvbell/kannada_neuralnetwork_kaggle) for more details of the approach taken.

Below is the accuracy (left) and loss (right).
![](/images/accuracy_and_loss.png)


# **Project 3: Exploring Neural Network interpretability through predicting flight delay**
[Full Github](https://github.com/pfvbell/Flights_ANN/blob/main/README.md)

This project mainly aims to explore interpretatbility and uncertainty in feedforward neural networks. A feedforward neural network was originally fitted. To explore the important features a logistic regression model was trained as a proxy, and permutation importance was performed, as well as other feature analysis. To explore the certainty of the predictions certain data points were bootstrapped to visualise a subsample of uncertainty. Secondly, an 'abstain' model was fit (based on this research: https://openreview.net/forum?id=rJxF73R9tX) which refrained from predicting when certainty levels were below 0.5. For further details [see](https://github.com/pfvbell/Flights_ANN/blob/main/README.md)  the notebook on the github.

![](/images/train_val_loss.png)


# **Project 4: What are the most common global education indicators? (using SQL)**
[Full Project](https://www.kaggle.com/philipbell/sql-world-bank)

Educational Research is relatively [new](http://https://tannerlectures.utah.edu/Allen%20manuscript.pdf) as a field distinct from other social sciences, such as economics and psychology. 

The World Bank International Education database provides a landscape view of both indicators of educational achievement, and also the types of studies conducted. Mining the information on this large dataset therefore provides useful insights into the way in which measurement of educational achievement may itself impact the nature of the education (akin to what Physicists call the 'observer effect'.

Add graph of change in spending over time.

Sub-questions included the average spending as a percentage of GDP for all countries, as well as how the amount of data gathered differs by year.

Add Image of output (as graph).

# **Project 5: Covid data scraper**
[Full Github](https://github.com/pfvbell/covid_data_scraper)

## Scraping and Analysing Covid data

Up-to-date covid data was scraped from https://usafacts.org/visualizations/coronavirus-covid-19-spread-map/state. This was then analysed in order to find the highest number of deaths per county and the highest death rate.

After merging voting and demographic data with the scraped data, this was then used to analyse how covid death rates were related to other demographic details of an area. I expected to find a relationship between density and voters for Clinton or Trump. Indeed, there did seem to be a potential relationship since the average density value for a county with a high proportion of Clinton voters was much higher than a county with a high density of Trump voters. I also found a potential link between counties with a high proportion of people with cancer and counties with a high proportion of people voting Trump. Indeed, when I used the interquartile ranges of the describe tables from the counties with a high proportion voting Trump I was able to use those to create new subsets of the data and thereby see that these counties, conversely, had low levels of unemployed.

