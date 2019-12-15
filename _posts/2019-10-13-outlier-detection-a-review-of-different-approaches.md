---
title: "Outlier detection - a review of different approaches"
date: 2019-10-13
tags: [outliers, data-preprocessing, ml]
---

<p style="font-family: times, serif; font-size:17pt; font-style:italic">
    “Il est impossible que l’improbable n’arrive jamais” -- Emil Gumbel 
</p>

<figure>
   <img src="https://farm4.staticflickr.com/3164/2574611403_8884a7e936_o.jpg">
    <figcaption><a href="https://farm4.staticflickr.com/3164/2574611403_8884a7e936_o.jpg"></a></figcaption>
</figure>

An outlier is an observation that diverges (i.e. it is distant) from other observations in a sample.<br>Outliers are also referred to as observations whose probability to occur is low.<br>
{: style="text-align: justify;"}

Outliers can impact the results of analysis and statistical modelling, by altering the relationship between variables.<br>
However, when trying to detect outliers in a dataset it is very important to keep in mind the context.<br>
{: style="text-align: justify;"}

Indeed, unusual observations are not necessarily outliers; in some cases, they are legitimate observations that accurately describe the variability in the data and may contain valuable information.<br>
{: .notice--danger}
{: style="text-align: center;"}


Even if determining whether or not an observation qualifies as an outlier is necessarily a subjective matter, several approaches and techniques can come to the aid.<br>
{: style="text-align: justify;"}

## Outliers Detection Techniques<br>
{: style="text-align: center;"}

Different approaches can be adopted to detect anomaly observations:
{: style="text-align: justify;"}
•	&nbsp;&nbsp;*univariate approach*, in which a single variable is analysed
{: style="text-align: justify;"}
•	&nbsp;*multivariate approach*, in which more than one variable are analysed at the same time
{: style="text-align: justify;"}
•	&nbsp;&nbsp;*parametric approach*, which involves statistical metrics based on parameters of the feature’s 	distribution
{: style="text-align: justify;"}
•	&nbsp;&nbsp;*non-parametric approach*<br>
{: style="text-align: justify;"}

Some of the most popular methods for outlier detection are:<br>
{: style="text-align: justify;"}
•	&nbsp;&nbsp;&nbsp;*Extreme Value Analysis*<br>
•	&nbsp;&nbsp;&nbsp;*Probabilistic and Statistical Modelling*<br>
•	&nbsp;&nbsp;&nbsp;*Linear Regression Modelling*<br>
•	&nbsp;&nbsp;&nbsp;*Proximity-Based Models*<br>
{: style="text-align: justify;"}

•	**Extreme Value Analysis**: this is a univariate parametric approach which qualifies as outliers those values which are too large or to small compared to some threshold defined on the basis of some parameter’s distribution, such as the *Z-scores* or the *Tukey’s IQR – Interquartile Range*.<br>
{: style="text-align: justify;"}
>The **Z-scores** approach quantifies the unusualness of an observation in terms of how many standard deviations a data point is from the sample’s mean, assuming a gaussian distribution.<br>
For any data point <img src="https://latex.codecogs.com/svg.latex?\bg_black&space;\fn_cs&space;\large&space;x_{i}" title="\large x_{i}" />, its zi-score can be calculated by subtracting the mean and dividing by the standard deviation as follows
{: style="text-align: justify;"}

<img src="https://latex.codecogs.com/gif.latex?\fn_cs&space;z_{i}&space;=&space;\frac{x_{i}&space;-&space;\mu&space;}{\sigma&space;}" title="z_{i} = \frac{x_{i} - \mu }{\sigma }" />
{: style="text-align: center;"}

>The further away an observation’s z-score is from zero (above or below), the more unusual it is.
The probability distribution below displays the distribution of Z-scores in a standard normal distribution.
{: style="text-align: justify;"}
![alt]({{ site.url }}{{ site.baseurl }}/images/2019-10-13-outlier-detection-a-review-of-different-approaches/normal.jpg)<span style = "font-family: times, serif; font-size:12pt; font-style:italic; color: #B6B3B2; text-align: center;">Source: Wikipedia</span> 
{: style="text-align: justify;"}
> As we can see, the probability to observe data point having z-scores beyond +/- 3 is extremely low (0.0026, i.e. 0.0013 * 2).<br>
For that, a standard cut-off value for finding outliers are Z-scores of +/-3 or further from zero.<br><br>
**Pros of Z-scores**: <br><br>
Simple method when dealing with parametric distributions in a low dimensional setting.<br><br>
**Cons of Z-scores**:
-	This approach assumes data follow the normal distribution (if not may consider to transform the data)<br>
-	It can be used in multivariate settings<br>
-	If the distribution has outliers, the Z-scores will be naturally biased since it inflates the distribution’s parameters (mean and standard deviation) used to compute them.<br>
{: style="text-align: justify;"}

>The **Tukey’s IQR** approach quantifies the unusualness of an observation based on the IQR rule, according to which data point below (Q1-1.5\*IQR) or above( Q3+1.5\*IQR) have to be considered outliers.<br><br>
The IQR method has two advantages over the Z-scores method:<br>
-	since it uses percentiles, it doesn’t rely on the assumption of a specific distribution.<br>
-	percentiles are relatively robust to the presence of outliers compared to mean-based methods.<br>
{: style="text-align: justify;"}

•	**Probabilistic and Statistical Modelling**: this is a parametric approach which assumes a specific probability distribution for data and estimates parameters of this distribution by using the expectation-maximization algorithm.<br>The estimated probability density function of this distribution gives the probability that an observation belongs to the distribution.<br> The smaller this value, the more likely that an observation is an outlier.<br>
{: style="text-align: justify;"}

•	**Linear Regression Modelling**: this is a multivariate parametric approach which models linear data correlations into a lower dimensional sub-space.<br>The distance of each observation from the estimated hyperplane, referred to as residual, quantifies its deviation from the model.<br>Residuals’ analysis allows to identify large deviations and outliers.
{: style="text-align: justify;"}

•	**Proximity-Based Models**: this is a class of non-parametric unsupervised models which qualifies as outliers those observations that are isolated from the rest of observations.<br> 
{: style="text-align: justify;"}
>This class can be further split into 3 categories of models:<br>
-	**Cluster Based Models**: Partitioning Cluster analysis (hierarchical clustering, k-means, PAM clustering). Normal data belong to large and dense clusters, whereas outliers belong to small or sparse clusters, or do not belong to any clusters<br>
-	**Density Based Models**:  such as Density Based Clustering analysis (DBSCAN)<br>
-	**Distance Based Models**: such as K-nearest neighbours <br>
{: style="text-align: justify;"}


# Outliers Treatment<br>
{: style="text-align: center;"}
Once the outliers are identified, in order to choose how to handle them, we must understand which type of outliers we are dealing with.<br>
{: style="text-align: justify;"}

•	*Error outliers*, data points that lie at a distance from other observations because they are the result of inaccuracies, such as measurement or data entry errors.<br>
•	*Sample outliers*, data points that are not part of the same population as the rest of the sample.<br>
•	*Interesting outliers*, which are accurate data points that lie at a distance from other data points and may contain valuable information.<br>
{: style="text-align: justify;"}

According to the type of outliers the possible approaches are:<br>
{: style="text-align: justify;"}
<ol>
	<li>	If the outlier in question is an Error outlier, it should be corrected if possible. If not, it’s better to remove that observation.</li>
	<li>	If the outlier in question is a Sampling outlier, it is legitimate to remove it.</li>
	<li>	If the outlier is a natural part of the phenomenon under study and appropriately reflects the research question/phenomenon under study, it should be kept, even if it lies well outside the range of the other values for the sample and even if it reduces statistical significance. Indeed, excluding them will force the phenomenon to appear less variable than it is in reality, leading to distort results.<br><br>
	When deciding to keep outliers, possible approaches are:<br>
	- <span style = "font-style:italic">data transformation</span>, by applying a mathematical function to all observed data points (e.g., to take the log) in order to reduce the variance and skewness of the data<br> 
	– <span style = "font-style:italic">data imputation</span>, through some capping method such as <span style = "font-style:italic">Winsorization</span> where all outliers are transformed to a value at a certain percentile of the data<br><br>
	An alternative approach is to conduct the analysis both with and without the outliers and compare the differences</li>
</ol>
{: style="text-align: justify;"}



When deciding to remove outlier, it’s important to document which observations have been removed as well as for which reason.<br>
{: style="text-align: justify;"}



