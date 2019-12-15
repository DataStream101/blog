---
title: "Linear Models' Assumptions"
date: 2019-10-02
tags: [linear regeression, residuals plot, diagnostic ,stat]
---

The aim of this article is to present regression assumptions as well as how to visually check if a data set validate those assumptions (both visually and using statistical tests).
{: style="text-align: justify;"}

# Focus on Linear Regression
{: style="text-align: center;"}

Linear regression models allow to predict a continuous outcome as a function of one or multiple continuous variables. <br>
{: style="text-align: justify;"}

Linear Regression models are divided in: <br>
{: style="text-align: justify;"}

* **Univariate Linear Regression** (or Simple Linear Regression), if the model deals with one input (referred to as *independent or predictor variable*) and one output variable (referred to as *dependent or response variable*) <br>
* **Multivariate Linear Regression** if the model deals with more than one input variable<br>
{: style="text-align: justify;"}

The aim of linear regression is to establish a function that explains the relationship between the predictor variable(s) and the response variable.<br>
{: style="text-align: justify;"}
This mathematical equation can be generalized as a linear equation in the following form: <br>
{: style="text-align: justify;"}

<img src="https://latex.codecogs.com/svg.latex?\fn_cs&space;\large&space;y&space;=&space;\beta&space;_{0}&space;&plus;&space;\beta&space;X&space;&plus;&space;\varepsilon" title="\large y = \beta _{0} + \beta X + \varepsilon" />
{: style="text-align: center;"}

where
*	<img src="https://latex.codecogs.com/svg.latex?\fn_cs&space;\large&space;X" title="\large X" />   is the vector of independent variables
	{: style="text-align: justify;"}
*	<img src="https://latex.codecogs.com/svg.latex?\fn_cs&space;\large&space;y" title="\large y" />      is the response variable <br>
*	<img src="https://latex.codecogs.com/svg.latex?\fn_cs&space;\large&space;\beta&space;_{0}" title="\large \beta _{0}" /> is the predicted value you get when <img src="https://latex.codecogs.com/svg.latex?\fn_cs&space;\large&space;X&space;=&space;0" title="\large X = 0" /><br>
*	<img src="https://latex.codecogs.com/svg.latex?\fn_cs&space;\large&space;\beta" title="\large \beta" /> is a vector of values explaining the change in <img src="https://latex.codecogs.com/svg.latex?\fn_cs&space;\large&space;y" title="\large y" /> when each variable in <img src="https://latex.codecogs.com/svg.latex?\fn_cs&space;\large&space;X" title="\large X" /> change by 1 unit <br>
*	ε is the error term, or *residual*, i.e. the part of <img src="https://latex.codecogs.com/svg.latex?\fn_cs&space;\large&space;y" title="\large y" /> the regression model is unable to explain.<br>
Residuals are defined for each observation as the difference between the actual and predicted values
<img src="https://latex.codecogs.com/svg.latex?\fn_cs&space;\large&space;\varepsilon&space;=&space;y&space;-&space;\hat{y}" title="\large \varepsilon = y - \hat{y}" />
{: style="text-align: justify;"}

# Regression Diagnostic
{: style="text-align: center;"}


Regression is a *parametric* approach. **‘Parametric’** means it makes some restrictive assumptions about data for the purpose of analysis. <br>
{: style="text-align: justify;"}

Once these assumptions get violated, regression makes biased, erratic predictions (in those cases, a non-linear model is the only solution) .<br>
{: style="text-align: justify;"}

Therefore, to be sure to build an accurate regression model, it’s essential to validate these assumptions.<br>
{: style="text-align: justify;"}

## Linear Model's Assumptions
{: style="text-align: center;"}

The five standard assumptions for regression analysis are:<br>
{: style="text-align: justify;"}

+ **Linear relationship assumption**<br>
This assumption implies that there should be a linear and additive relationship between the response variables and the predictor(s).<br>
{: style="text-align: justify;"}

>A linear relationship means that change in response y due to one unit change in X is constant<br>
{: style="text-align: justify;"}
>An additive relationship suggests that the effect of X on y is independent of other variables
{: style="text-align: justify;"}

When this assumption is validated, we are sure that our estimator and predictions are unbiased.
justify;"}

+ **Absence of Multicollinearity**, i.e. the independent variables should be not correlated.<br> 
{: style="text-align: justify;"}

+ **Absence of Autocorrelation**, i.e. residuals should be not correlated. <br>
{: style="text-align: justify;"}

If this assumption is not satisfied, our estimator will suffer from high variance.
{: style="text-align: justify;"}

+ **Homoskedasticity**, i.e. residuals must have constant variance.<br>
{: style="text-align: justify;"}

When this assumption is not validated, we talk about *heteroskedasticity*.<br>
{: style="text-align: justify;"}

Generally, non-constant variance arises in presence of outliers or extreme leverage values. These values get too much weight, hence disproportionately influences the model’s performance. When this phenomenon occurs, the confidence interval for out of sample prediction tends to be unrealistically wide or narrow.<br>
{: style="text-align: justify;"}

+ **Normality of Residuals**. The error terms should have a normal distribution, with mean 0. <br>
{: style="text-align: justify;"}

How would you check (validate) if a data set follows all regression assumptions? 
{: style="text-align: justify;"}

The most intuitive tools to check it are the **Residuals Plots** (explained below) along with some statistical test.
{: style="text-align: justify;"}

## Visually check for assumptions validation.
{: style="text-align: center;"}

+ **Linearity**<br>
To check the linearity assumption is enough to plot the predictors versus response variable.<br>
{: style="text-align: justify;"}

+ **Absence of Multicollinearity**.<br> 
To check if there is multicollinearity, we can compute correlation cofficients. Predictors that are multicollinear have high correlation coefficient (0.80 or higher).<br>
Another way is to perform a Principal Component Analysis and analyze the variable's plot looking for variables which are correlated each other.

+ **Absence of Autocorrelation** and **Homoskedasticity**<br>
To check for those assumption, the standardized residual plot against fitted values (predicted values) is used.
{: style="text-align: justify;"}

Residual plots are a valuable source of information to check for a large part of assumptions. The logic is: <span style = "font-family: arial, serif; font-size:16pt; font-style:italic; color:#1210A5; text-align: center;">if the selected independent variables describe the relationship so thoroughly, then only random error will remain. Non-random patterns in residuals suggest that the explication power of the model can be further improved.</span><br>
{: style="text-align: justify;"}

When those assumptions are validated, residuals are randomly distributed as in the plot below<br>
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-10-02-linear-regression-assumptions/residuals1.jpeg)
{: style="text-align: center;"}

Any noticeable pattern in such plots indicates violation of those assumptions.
The most typical pattern for nonconstant variance is a plot of residuals versus fits with a pattern that resembles a sideways cone as in the plot below
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-10-02-linear-regression-assumptions/hetero.png)
{: style="text-align: center;"}

+ **Normality of Residuals**<br>
Checking if residuals follow a normal distribution, by examining a normal probability plot of standardized residuals. 
A straight-line pattern for a normal probability plot indicates that the assumption of normality is validated as in the plot below
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-10-02-linear-regression-assumptions/qqplot.png)
{: style="text-align: center;"}

When the data is not normally distributed a non-linear transformation (e.g., log-transformation) might fix this issue.
{: style="text-align: justify;"}



## Statistical test for assumptions validation.
{: style="text-align: center;"}
+ **Linearity**<br>
<span style = "font-family: arial, serif; font-size:16pt; font-style:bold; color: #1512DE; text-align: center;">Harvey-Collier test</span>,  which is a t- test for 0 mean (it tests whether recursive residuals have mean 0 - which they should under the null hypothesis of linearity)
{: style="text-align: justify;"}


+ **Absence of Autocorrelation** <br>
<span style = "font-family: arial, serif; font-size:16pt; font-style:bold; color: #1512DE; text-align: center;">Durbin-Watson test</span>, which tests the null hypothesis that the residuals are not linearly auto-correlated. 
{: style="text-align: justify;"}

The statistical test can assume values between 0 and 4.
As a rule of thumb values between 1.5 and 2.5 show that there is no auto-correlation in the data.
{: style="text-align: justify;"} 


+ **Homoskedasticity**<br>
<span style = "font-family: arial, serif; font-size:16pt; font-style:bold; color: #1512DE; text-align: center;">Goldfeld-Quandt test</span> can also be used to test for heteroscedasticity.  The test splits the data into two groups and tests to see if the variances of the residuals are similar across the groups.
{: style="text-align: justify;"}

+ **Normality of Residuals**<br>
<span style = "font-family: arial, serif; font-size:16pt; font-style:bold; color: #1512DE; text-align: center;">Shapiro-Wilk test</span>
{: style="text-align: justify;"}






