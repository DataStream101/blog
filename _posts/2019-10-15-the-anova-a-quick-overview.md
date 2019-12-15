---
title: "The ANOVA : a quick overview"
date: 2019-10-15
tags: [ANOVA, mean comparison, stat]
---

This article explores the principles underlying the Analysis of Variance (ANOVA) as well as the workflow to implement it.<br>
{: style="text-align: justify;"}

## When to perform an Analysis of Variance<br>
{: style="text-align: center;"}

The Analysis of Variance (ANOVA) is used to model a continuous response variable as a function of one (or more) categorical explanatory variable(s).<br>
{: style="text-align: justify;"}

ANOVA models are usually referred to as:<br>
•   One-way ANOVA, when the model considers one categorical explanatory variable that has more than two levels<br>
•   Two-way ANOVA, when the model considers two categorical explanatory variables that have more than two levels<br>
•   and so on.<br>
{: style="text-align: justify;"}

Actually, the term *Analysis of Variance* can be source of misunderstanding since this statistical technique is an extension of the independent t-test (used for comparing means in two different groups, i.e. when the categorical explanatory variable that has just two levels). Therefore, like the t-test, the aim of ANOVA is to analyze means among groups and not variance.
{: .notice--danger}
{: style="text-align: justify;"}

The ANOVA is usually employed in the context of experiments to highlight the impact of a factor (or multiple factors) on a quantitative variable (e.g. in case of medical treatments to assess if some quantitative indicator of recovery is significantly different among groups of patients treated with different drugs).<br>
{: style="text-align: justify;"}

In those case, the ANOVA allows to test if there are differences when comparing the means of the target variable across different groups identified by a level of the factor of interest.<br>
{: style="text-align: justify;"}

## The Underlying Principle<br>
{: style="text-align: center;"}

If we want to check if a given factor plays or not a role in determining the value of a quantitative variable, we can perform a one-way ANOVA. This technique allows to assess if the means of the groups identified by the level of the factor under investigation are significantly different from each other.<br>
{: style="text-align: justify;"}

Considering a factor having k levels, the overall null hypothesis for the ANOVA is
{: style="text-align: justify;"}
<img src="https://latex.codecogs.com/svg.latex?\fn_cs&space;H_{0}&space;:&space;\mu&space;_{1}&space;=&space;\mu&space;_{2}&space;=&space;\mu&space;_{3}&space;=&space;...=\mu&space;_{k}" title="H_{0} : \mu _{1} = \mu _{2} = \mu _{3} = ...=\mu _{k}" />
{: style="text-align: center;"}

The alternative hypothesis is that “at least one of the k population means differs from all of the others”.<br>
{: style="text-align: justify;"}

The statistic which measures if the means of different groups are significantly different or not is called the **F-Ratio** and its mathematical expression is
{: style="text-align: justify;"}

<img src="https://latex.codecogs.com/svg.latex?\fn_cs&space;F-Ratio&space;=&space;\frac{Between-group.Variability}{Within-group.Variability}" title="F-Ratio = \frac{Between-group.Variability}{Within-group.Variability}" />
{: style="text-align: center;"}

The higher the F-Ratio value, (and the lower the related p-value) the higher the evidence that the null hypothesis has to be rejected.<br>
{: style="text-align: justify;"}

From the expression above we can see that the logic underlying the ANOVA is to compare the *inter-group* variability (i.e. the variability of the target variable within each group) and the *intra-group* variability (i.e. the variability of the target variable among groups).<br>
{: style="text-align: justify;"}

## Model Assumptions<br>
{: style="text-align: center;"}

 - Independence of observations (this assumption has to be validated at the experiment-design stage)
 - Homoskedasticity of residuals
 - Normal distribution of residuals
 {: style="text-align: justify;"}

## Steps to implement ANOVA<br>
{: style="text-align: center;"}
<br>
1.&nbsp;&nbsp;&nbsp;&nbsp;EDA:  Side-by-side Boxplots<br>
2.&nbsp;&nbsp;&nbsp;&nbsp;ANOVA test<br>
3.&nbsp;&nbsp;&nbsp;&nbsp;Multiple pairwise-comparison and Results Interpretation<br>
4.&nbsp;&nbsp;&nbsp;&nbsp;Model Validation<br>
{: style="text-align: justify;"}

1.&nbsp;&nbsp;&nbsp;&nbsp;**EDA:  Side-by-side Boxplots**<br>
{: style="text-align: center;"}
The first step is to visualize how the target variable is distributed across the groups identified by each level of the categorical variable.<br>
{: style="text-align: justify;"}
The appropriate plot for that is a box-plot which resumes a lot of information about the target variable distribution and allow to formulate some initial hypothesis.
{: style="text-align: justify;"}
<figure>
   <img src="https://www.r-graph-gallery.com/264-control-ggplot2-boxplot-colors_files/figure-html/unnamed-chunk-1-2.png">
    <figcaption><a href="https://www.r-graph-gallery.com/264-control-ggplot2-boxplot-colors_files/figure-html/unnamed-chunk-1-2.png"></a><span style = "font-family: times, serif; font-size:12pt; font-style:italic; color: #B6B3B2; text-align: center;">Source: The R Graph Gallery</span> </figcaption>
</figure>

2.&nbsp;&nbsp;&nbsp;&nbsp;**ANOVA test**<br>
{: style="text-align: center;"}
After inspecting the data and formulating the hypothesis,an ANOVA test is performed in order to assess if there is any significant difference between the average value of the target variable across the groups.<br>
{: style="text-align: justify;"}

Statistical software display ANOVA results in a table as follows:<br>
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-10-15-the-anova-a-quick-overview/tab.png)
{: style="text-align: center;"}


The ANOVA table includes:<br>
{: style="text-align: justify;"}
-	The factor(s) to be examined (which represents the source of variation). In this case, it is identified by the variable 'Trt'.<br>
-	Sum of Squares (SS) for each source of variation<br>
-	Mean Square, i.e. the sum of squares for each factor divided by its associated degrees of freedom (Df)<br>
-	F-statistic: built as the mean square of the factor divided by the mean square of the residuals<br>
-	Prob > F: the p-value<br>
{: style="text-align: justify;"}
 
In order to evaluate the results of the test we need to consider the p-value.<br>
{: style="text-align: justify;"}
The smaller the p-value is, the higher the evidence that the mean values across groups are different<br><br>
At the opposite, we have to evaluate the null hypothesis that all the means are the same true<br>
{: .notice--info}
{: style="text-align: justify;"}

3.&nbsp;&nbsp;&nbsp;&nbsp;**Multiple pairwise-comparison and Results Interpretation**<br>
{: style="text-align: center;"}

An ANOVA is a *global test* which does not explain where is located the source of the difference, i.e. which mean or means differs from the other.<br>
{: style="text-align: justify;"}

In order to answer this question, we have to use the Tukey multiple-pairwise comparison t-test.<br>
{: style="text-align: justify;"}

![alt]({{ site.url }}{{ site.baseurl }}/images/2019-10-15-the-anova-a-quick-overview/tukey.png)
{: style="text-align: center;"}

The output gives the difference in means, confidence levels and the adjusted p-values for all possible pairs.<br>
In the example above, the factor of interest has only 2 levels (trt1 and trt2) and the p-value shows that there is a significant between-group difference for the two treatments.
{: style="text-align: justify;"}

4.&nbsp;&nbsp;&nbsp;&nbsp;**Model Validation**<br>

The final step is to assess whether ANOVA Assumptions are validated or not. This can be achieved by analyzing residuals' distribution.
{: style="text-align: justify;"}

Further details about assessing assumptions validation can be found [here](https://datastream101.github.io/blog/linear-models-assumptions/)
{: style="text-align: justify;"}