---
title: "Inside the Random Forest Black-Box"
date: 2019-11-08
tags: [ensemble learning, tree-based model, hyperparameters, ml]
---

<figure>
   <img src="https://images.unsplash.com/photo-1441974231531-c6227db76b6e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1051&q=80">
    <figcaption><a href="https://unsplash.com/wallpapers/nature/forest/"></a><span style = "font-family: times, serif; font-size:12pt; font-style:italic; color: #B6B3B2; text-align: center;">Source: Unsplash</span> </figcaption>
</figure>


Random Forest is a *non-parametric supervised learning algorithm* which belongs to the category of *ensemble learning algorithms*, meaning it makes prediction by combining the results from many models (i.e. individual decision trees).<br><br>The main idea behind the ensemble learning is that combining individual weak predictions together leads to more robust overall prediction.<br>
{: style="text-align: justify;"}

## How Random Forest are built
{: style="text-align: center;"}

The individual decision trees built by the Random Forest algorithm are constructed independently using the <span style="color:red">bagging technique</span> (where bagging stands for *Bootstrap Aggregating*).<br>
{: style="text-align: justify;"}

Through bagging, the Random Forest algorithm randomly samples training data points when building trees and randomly selected subsets of features which will be used when splitting nodes (this is the bootstrap part of the bagging technique).<br>
{: style="text-align: justify;"}

It means that each individual decision tree in the forest considers a random subset of features when performing splits and it is trained on a randomly sampled subset of the data (where sampling is done with replacement, meaning that there could be repeated values in each of the newly created subsets). <br>
{: style="text-align: justify;"}

Finally, predictions are made by aggregating the predictions of each decision tree (this is the aggregation part of the bagging technique):<br>
{: style="text-align: justify;"}
-   In case of a regression problem, the prediction for a new record is calculated by taking the average of all values predicted by all the individual decision tree; <br>
-   in case of a classification problem, the new record is assigned to the category which has been the most frequent predicted by each individual tree.<br>
{: style="text-align: justify;"}

Bagging is the main reason why Random Forests perform better than individual decision trees. 
{: .notice--info}
{: style="text-align: justify;"}

Indeed, it allows to:
{: style="text-align: justify;"}

1.&nbsp;&nbsp;&nbsp;Overcome the problem of overfitting.
{: style="text-align: justify;"}
2.&nbsp;&nbsp;&nbsp;Decrease the overall variance of the model. By training each tree on different samples, although each tree might have high variance with respect to its particular set of the training data, overall, the entire forest will have lower variance.
{: style="text-align: justify;"}
3.&nbsp;&nbsp;&nbsp;Remove trees correlation, since individual trees are trained on randomly sampled subset if data and features.
{: style="text-align: justify;"}

To recap, given a dataset containing M observations and K features, the steps taken to implement random forest can be generalized as follows:<br>
{: style="text-align: justify;"}
•   Randomly selection (with replacement) of a subset of m data points.<br>
•   Randomly selection (with replacement) of a subset of k features. Whatever feature gives the best split is used to split the node iteratively<br>
•   The above steps are repeated until the desired number of tree n (a hyperparameter of the model) is reached. The prediction is given based on the aggregation of all the individual predictions from the n trees<br>
{: .notice--info}
{: style="text-align: justify;"}


## Hyperparameters<br>
{: style="text-align: center;"}

In order to optimize model’s performance (i.e. to increase its predictive power or to improve its computational efficiency), there are several hyperparameters that should be considered when training a Random Forest algorithm.<br>
{: style="text-align: justify;"}

With reference to the Python sklearn built-in *RandomForest* algorithm, the main parameters to consider are:<br>
{: style="text-align: justify;"}

•   &nbsp;&nbsp;**n_estimators**: The number of trees in the forest.<br>A good rule of thumb is to start with 10 times the number of features.<br>
{: style="text-align: justify;"}

Usually the higher the number of trees the better the model will learn the data. However, adding a lot of trees can affect computational speed without any improvement in model accuracy.<br>
{: style="text-align: justify;"}

•   &nbsp;&nbsp;**max_depth**: The maximum depth of the tree.<br>By default, it is None, meaning that the nodes are expanded until all leaves are pure.<br>
{: style="text-align: justify;"}

The deeper the tree, the more information it is able to learn about the data. However, increasing depth of the tree above a certain level makes the model prone to overfitting. <br>
{: style="text-align: justify;"}

•   **max_features**: The number of features to consider when looking for the best split in each individual tree.<br>
{: style="text-align: justify;"}

There are several options available to set this parameter (for further details check the [documentation](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html#sklearn.ensemble.RandomForestRegressor))<br>
{: style="text-align: justify;"}


•   **min_samples_leaf**: The minimum number of data points allowed in the end node of each decision tree.<br>
{: style="text-align: justify;"}

## Hyperparameters in action<br>
{: style="text-align: center;"}

A practical illustration of how model hyperparameters can affect performance is provided by the the following example.<br>
{: style="text-align: justify;"}

Given different features which are considered important during the application for Master's Programs, we want to build a model to predict a student’s chances of admission for a particular university .<br>
{: .notice--info}
{: style="text-align: justify;"}

The dataset is available [here](https://www.kaggle.com/mohansacharya/graduate-admissions) whereas the full code is available [here](https://github.com/DataStream101/Machine-Learning/blob/master/Machine%20Learning%20Algorithms/Tuning%20Random%20Forest's%20Hyperparameters%20.ipynb).<br>
{: style="text-align: justify;"}

Looking at the data using the Pandas.dataframe *.head()* and *.info()* methods we obtain the following outputs.<br>
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-11-08-inside-the-random-forests-black-box/data.jpg)
<br>
<br>

![image-center]({{ site.url }}{{ site.baseurl }}/images/2019-11-08-inside-the-random-forests-black-box/info.jpg){: .align-center}



The dataset contains information about 400 observations related to 9 features (GRE Scores, TOEFL Scores, University Rating, Statement of Purpose Strength, Letter of Recommendation Strength, Undergraduate GPA, Research Experience, Chance of Admit) which are all numeric. There is no missing values.<br>
{: style="text-align: justify;"}
By using the *.describe()* method we can get some summary statistics to get an idea of the distribution of the features in the dataset.<br>
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-11-08-inside-the-random-forests-black-box/distribution.jpg)

The distribution of the features in the sample seems have no issue.<br>We can move to the next step: extracting features (X) and label (y, i.e. the variable to predict) and split the whole dataset in a training and a test set. <br>
{: style="text-align: justify;"}
```python
y = adm['Chance of Admit ']
X = adm.iloc[:,1:8]
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state = 123)
```

The following code instantiate an object of the class *RandomForestRegressor* with default setting parameters.<br>
{: style="text-align: justify;"}
```python
randomForest = RandomForestRegressor(random_state =123 )
```
Then, the model is trained using the training sample.<br>
{: style="text-align: justify;"}
```python
randomForest.fit(X_train, y_train)
```

Once the model built, it is used to predict the target variable using the test sample.<br>
{: style="text-align: justify;"}
```python
y_pred = randomForest.predict(X_test)
```

To assess the model performance, different metrics can be used:
{: style="text-align: justify;"}
•   &nbsp;&nbsp;Mean absolute error (MAE)<br>
•   &nbsp;&nbsp;Mean squared error (MSE)<br>
•   &nbsp;&nbsp;R-squared scores<br>
•   &nbsp;Adjusted R-squared scores (which is not a built-in metric and we have to compute it manually)<br>
{: style="text-align: justify;"}
```python
mae = mean_absolute_error(y_test, y_pred)
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)
adj_r2 = 1 - (1 - r2)*(X_train.shape[0] - 1)/(X_train.shape[0] - X_train.shape[1] - 1)
```
```python
# Print metrics
print('Mean Absolute Error:', round(mae, 2))
print('Mean Squared Error:', round(mse, 2))
print('R-squared scores:', round(r2, 3))
print('Adj.R-squared scores:', round(adj_r2, 3))
```

![image-center]({{ site.url }}{{ site.baseurl }}/images/2019-11-08-inside-the-random-forests-black-box/metricsNoParam.jpg){: .align-center}

The next step is to explore how tuning model's hyperparameters can affect its performance in making prediction. We consider the Adjusted R-squared score as metric to evaluate the model.<br>
{: style="text-align: justify;"}

 - **max_depth**<br>
 {: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-11-08-inside-the-random-forests-black-box/max_depth.jpg)

We can see that above a certain depth the model starts overfitting. It perfectly predicts all the train data (the Adjusted R2 for the training set is 1) but its predictions are not accurate over the test set.<br>
With a max_depth of 10, the model gets the highest Adjusted R2 (0.695).<br>
{: style="text-align: justify;"}    

 - **n_estimators**<br>

{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-11-08-inside-the-random-forests-black-box/n_estimators.jpg)

We can see that adding a high number of trees doesn’t necessarily improve model accuracy. In this case, with 12 estimators, our model gets the highest Adjusted R2 (0.692).<br>
{: style="text-align: justify;"}

 - **max_features** <br>
{: style="text-align: justify;"}

![image-center]({{ site.url }}{{ site.baseurl }}/images/2019-11-08-inside-the-random-forests-black-box/max_features.jpg){: .align-center}


We have implemented the model by tuning only the max_features parameter with different settings, namely ‘None’, ‘sqrt’, ‘log2’ , ‘int’ (3) and ‘float’ (0.5).<br>
We can see that, in this case, even if with slight differences, setting the parameter using a customized integer number or a customized fraction of features allow to get a highest Adjusted R-squared.<br>
{: style="text-align: justify;"}

 - **min_samples_leaf**<br>

{: style="text-align: justify;"} 
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-11-08-inside-the-random-forests-black-box/min_samples_leaf.jpg)

Increasing the number of data points allowed in the end node leads the model to make not accurate predictions, both on the training and the test set.<br>
In this case with a minimum of 20% of our test data in each leaf node, the model gets an Adjusted R-squared score equals to 0.68.<br>
{: style="text-align: justify;"} 

We can now modify our previous model by tuning its parameters according to our findings.<br>
{: style="text-align: justify;"} 

```python
randomForestTuned = RandomForestRegressor(max_depth = 10, max_features=0.5, n_estimators=12,\
              min_samples_leaf=0.02, random_state=123)
```

![image-center]({{ site.url }}{{ site.baseurl }}/images/2019-11-08-inside-the-random-forests-black-box/metricsTuned.jpg){: .align-center}

When looking at the model evaluation’s metrics we can see that its performance is improved and the Adjusted R-squared is increased from 0.661 to 0.721.<br>
{: style="text-align: justify;"} 

To end this article, I would like to suggest a very interesting paper about Random Forest hyperparameters [*“Hyperparameters and Tuning Strategies for Random Forest”*](https://arxiv.org/pdf/1804.03515.pdf) by Philipp Probst, Marvin Wright and Anne-Laure Boulesteix.  Even if it is focused on implementation of tuning using R rather than Python, it is a useful source for further study.<br>
{: style="text-align: justify;"} 
