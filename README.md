**Phil Bell's data science portfolio**

I am currently a Fulbright Scholar at Harvard University studying the intersection of politics, education policy and data science. Email me at pbell@gse.harvard.edu.

# **Project 1: Using NN, RF and Logistic Regression to predict the 2020 Presidential election**
[Full Github Description](https://github.com/pfvbell/president/blob/main/README.md)

Packages used: Pandas, Numpy, SKlearn, Keras.

I used logistic regression, Random Forest, KNN and neural networks to predict the 2020 Presidential election. Data was scraped from the US census API. Polling, turnout and voter data from 1980 was engineered to build uncertainty into the predictions. Missing data from early elections was imputed using a linear regression model trained on other complete predictors. See the [Github notebook](https://github.com/pfvbell/president/blob/main/README.md) for details on data cleaning, feature selection, model selection and uncertainty visualisation. A final test accuracy of 92.2% was seen on the Lasso Logistic Regression model, and the Random Forest Model saw a final test accuracy of 96%.

![](/images/lasso_preds_map_2.png)

# **Project 2: Dog search app using NLP and computer vision**
At [Harvard ComputeFest 2021](https://www.computefest.seas.harvard.edu/) I made an app using state-of-the art computer vision and NLP models. Specifically, CNNs and distillation were used to make a feature for uploading an image to find similar-looking dogs. A fine-tuned double-head GPT-2 NLP model was trained with a simulated dog dialogue dataset to make a chat-bot. The app was hosted on AWS. Docker and Kubernetes were used for deployment.

![](/images/woofwoof.png)

# **Project 3: Zambia Higher Education Spatial Analysis (ongoing)**
[Full Github Description](https://github.com/pfvbell/zambia_hmlp/blob/main/README.md)

Packages used: Geopandas, Folium.

As part of the Harvard Ministerial Leadership Programme I am working with the Zambian government to support gender equality in Higher Education. The latitude and longitude of Zambian private and public universities was geocoded and mapped alongside demographic data in order to make inferences that inform policy recommendations.

![](/images/Pop_density_small.png)
![](/images/working_pop_small.png)

# **Project 4: Kannada MNIST Kaggle submission**
[Full Github Description](https://github.com/pfvbell/kannada_neuralnetwork_kaggle/blob/main/README.md)

Packages Used: LIME, Keras.

![](/images/one.png) ![](/images/zero.png)

This entry was placed 252 in the kaggle competition with a final test accuracy of 92.8%. Validation Accuracy was 95.8% and train accuracy was 99.7%.
Images of kannada digits were classified as '0' or '1' using a regularised feed-forward neural network (including L2 and dropout). 2000 epochs were used, with a batch size of 32. See the [Github Readme](https://github.com/pfvbell/kannada_neuralnetwork_kaggle) for more details of the approach taken.

Below is the accuracy (left) and loss (right).
![](/images/accuracy_and_loss.png)


# **Project 5: Exploring Neural Network interpretability through predicting flight delay**
[Full Github Description](https://github.com/pfvbell/Flights_ANN/blob/main/README.md)

This project mainly aims to explore interpretatbility and uncertainty in feedforward neural networks. A feedforward neural network was originally fitted to predict flight delays from 810 predictors. All categorical variables, including airports, were one-hot-encoded. To explore the important features a logistic regression model was trained as a proxy, and permutation importance was performed, as well as other feature analysis. To explore the certainty of the predictions certain data points were bootstrapped to visualise a subsample of uncertainty. Secondly, an 'abstain' model was fit (based on this research: https://openreview.net/forum?id=rJxF73R9tX) which refrained from predicting when certainty levels were below 0.5. For further details [see](https://github.com/pfvbell/Flights_ANN/blob/main/README.md)  the notebook on the github.

![](/images/train_val_loss.png)


# **Project 6: Using PCA with high-demensionality data to predict cancer types**
[Full Github Description](https://github.com/pfvbell/pca/blob/main/README.md)

High dimensionality is one aspect of big data. Using a big data set with over 7000 predictors I built several classification models to distinguish between two related classes of cancer, acute lymphoblastic leukemia (ALL) and acute myeloid leukemia (AML), using gene expression measurements. Each row in the data file corresponds to a tumor tissue sample from a patient with one of the two forms of leukemia. 

Principal Component Analysis was used to decompose the high dimensional data and then visualise high-dimensionality in a low-dimensional image (see below). Cross-validation was used to predict the best number of principal components to train a logisitc regression model, and then the same technique was used to pick the best PC number to train a multi-nomial logistic regression model that predicted the multi-class problem of cancer subtype.

![](/images/Visualising_PCA.png)


Finally, to understand how PCA with logistic regression had made classification decisions the decision boundaries of two models were plotted. See the [full project](https://github.com/pfvbell/pca/blob/main/README.md) for more details. 

![](/images/decision_boundary.png)
![](/images/pca_ridge_quadratic.png)
