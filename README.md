# portfolio
Phil Bell's Data Science Portfolio


[**Project 1: Using NN, RF and Logistic Regression to predict the 2020 Presidential election**](https://github.com/pfvbell/president)

![](/images/Graph_of_Predictors.png)

Four sets of models were used to predict the 2020 Presidential election results.

![](/images/rf_preds_map_2.png)

![](/images/strike_rate_map.jpg)

[See full Github Repo](https://github.com/pfvbell/president)



[**Project : What are the most common global education indicators (using SQL)**](https://www.kaggle.com/philipbell/sql-world-bank)
Educational Research is relatively [new](http://https://tannerlectures.utah.edu/Allen%20manuscript.pdf) as a field distinct from other social sciences, such as economics and psychology. 

The World Bank International Education database provides a landscape view of both indicators of educational achievement, and also the types of studies conducted. Mining the information on this large dataset therefore provides useful insights into the way in which measurement of educational achievement may itself impact the nature of the education (akin to what Physicists call the 'observer effect'.

Add graph of change in spending over time.

Sub-questions included the average spending as a percentage of GDP for all countries, as well as how the amount of data gathered differs by year.

Add Image of output (as graph).

[**Project: Covid data scraper](https://github.com/pfvbell/covid_data_scraper)
Scraping and Analysing Covid data

Up-to-date covid data was scraped from https://usafacts.org/visualizations/coronavirus-covid-19-spread-map/state. This was then analysed in order to find the highest number of deaths per county and the highest death rate.

After merging voting and demographic data with the scraped data, this was then used to analyse how covid death rates were related to other demographic details of an area. I expected to find a relationship between density and voters for Clinton or Trump. Indeed, there did seem to be a potential relationship since the average density value for a county with a high proportion of Clinton voters was much higher than a county with a high density of Trump voters. I also found a potential link between counties with a high proportion of people with cancer and counties with a high proportion of people voting Trump. Indeed, when I used the interquartile ranges of the describe tables from the counties with a high proportion voting Trump I was able to use those to create new subsets of the data and thereby see that these counties, conversely, had low levels of unemployed.
