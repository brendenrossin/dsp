# Statistics

# Table of Contents

[1. Introduction](#section-a)  
[2. Why We Are Using Think Stats](#section-b)  
[3. Instructions for Cloning the Repo](#section-c)  
[4. Required Exercises](#section-d)  
[5. Optional Exercises](#section-e)  
[6. Recommended Reading](#section-f)  
[7. Resources](#section-g)

## <a name="section-a"></a>1.  Introduction

[<img src="img/think_stats.jpg" title="Think Stats"/>](http://greenteapress.com/thinkstats2/)

Use Allen Downey's [Think Stats (second edition)](http://greenteapress.com/thinkstats2/) book for getting up to speed with core ideas in statistics and how to approach them programmatically. This book is available online, or you can buy a paper copy if you would like.

Use this book as a reference when answering the 6 required statistics questions below.  The Think Stats book is approximately 200 pages in length.  **It is recommended that you read the entire book, particularly if you are less familiar with introductory statistical concepts.**

Complete the following exercises along with the questions in this file. Some can be solved using code provided with the book. The preface of Think Stats [explains](http://greenteapress.com/thinkstats2/html/thinkstats2001.html#toc2) how to use the code.  

Communicate the problem, how you solved it, and the solution, within each of the following [markdown](https://guides.github.com/features/mastering-markdown/) files. (You can include code blocks and images within markdown.)

## <a name="section-b"></a>2.  Why We Are Using Think Stats 

The stats exercises have been chosen to introduce/solidify some relevant statistical concepts related to data science.  The solutions for these exercises are available in the [ThinkStats repository on GitHub](https://github.com/AllenDowney/ThinkStats2).  You should focus on understanding the statistical concepts, python programming and interpreting the results.  If you are stuck, review the solutions and recode the python in a way that is more understandable to you. 

For example, in the first exercise, the author has already written a function to compute Cohen's D.  **You could import it, or you could write your own code to practice python and develop a deeper understanding of the concept.** 

Think Stats uses a higher degree of python complexity from the python tutorials and introductions to python concepts, and that is intentional to prepare you for the bootcamp.  

**One of the skills to learn here is to understand other people’s code.  And this author is quite experienced, so it’s good to learn how functions and imports work.**

---

## <a name="section-c"></a>3.  Instructions for Cloning the Repo 
Using the [code referenced in the book](https://github.com/AllenDowney/ThinkStats2), follow the step-by-step instructions below.  

**Step 1. Create a directory on your computer where you will do the prework.  Below is an example:**

```
(Mac):      /Users/yourname/ds/metis/metisgh/prework  
(Windows):  C:/ds/metis/metisgh/prework
```

**Step 2. cd into the prework directory.  Use GitHub to pull this repo to your computer.**

```
$ git clone https://github.com/AllenDowney/ThinkStats2.git
```

**Step 3.  Put your ipython notebook or python code files in this directory (that way, it can pull the needed dependencies):**

```
(Mac):     /Users/yourname/ds/metis/metisgh/prework/ThinkStats2/code  
(Windows):  C:/ds/metis/metisgh/prework/ThinkStats2/code
```

---


## <a name="section-d"></a>4.  Required Exercises

*Include your Python code, results and explanation (where applicable).*

### Q1. [Think Stats Chapter 2 Exercise 4](statistics/2-4-cohens_d.md) (effect size of Cohen's d)  
Cohen's D is an example of effect size.  Other examples of effect size are:  correlation between two variables, mean difference, regression coefficients and standardized test statistics such as: t, Z, F, etc. In this example, you will compute Cohen's D to quantify (or measure) the difference between two groups of data.   

You will see effect size again and again in results of algorithms that are run in data science.  For instance, in the bootcamp, when you run a regression analysis, you will recognize the t-statistic as an example of effect size.

first_weight = firsts.totalwgt_lb.mean()

others_weight = others.totalwgt_lb.mean()

weight_diff = first_weight - others_weight

print(weight_diff)

cohen_weight = CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)

print(cohen_weight)

First children, on average, tend to weigh slightly less than other children. The first children tend to be about 0.09 standard deviations less than other children, which most likely does not have any statistical significance to us.

### Q2. [Think Stats Chapter 3 Exercise 1](statistics/3-1-actual_biased.md) (actual vs. biased)
This problem presents a robust example of actual vs biased data.  As a data scientist, it will be important to examine not only the data that is available, but also the data that may be missing but highly relevant.  You will see how the absence of this relevant data will bias a dataset, its distribution, and ultimately, its statistical interpretation.

resp = nsfg.ReadFemResp()

pmf = thinkstats2.Pmf(resp.numkdhh, label='numkdhh')

thinkplot.Pmf(pmf)

thinkplot.Config(xlabel='Kidts under 18', ylabel='Pmf')

biased_pmf = BiasPmf(pmf, label='observed')

thinkplot.PrePlot(2)

thinkplot.Pmfs([pmf, biased_pmf])

thinkplot.Config(xlabel='Children under 18', ylabel='PMF')

print('Actual mean', pmf.Mean())

print('Observed mean', biased_pmf.Mean())

There is a clear representation of the bias that would occur if the children were surveyed and their responses were logged, due to the greater number of responses that would be given with a greater number of children in a household. This more than doubles the average number of children per household. This highlights the importance of data collection and validating the results and what implicit bias they might hold.

### Q3. [Think Stats Chapter 4 Exercise 2](statistics/4-2-random_dist.md) (random distribution)  
This questions asks you to examine the function that produces random numbers.  Is it really random?  A good way to test that is to examine the pmf and cdf of the list of random numbers and visualize the distribution.  If you're not sure what pmf is, read more about it in Chapter 3.  

sample = np.random.random(1000)

pmf = thinkstats2.Pmf(sample, label='random')

thinkplot.Pmf(pmf)

thinkplot.Config(xlabel='Random', ylabel='PMF')

cdf = thinkstats2.Cdf(sample, label='random')

thinkplot.Cdf(cdf)

thinkplot.Config(xlabel='Random', ylabel='CDF', loc='upper left')

Because the random sample function is pulling from the range uniformly, each number within the range has an equal probability of being chosen. This is shown with the CDF of percentile ranks being close to a straight line, which indicates a uniform trend and that there are no spikes to indicate a jump in probability at a specific percentile rank.

### Q4. [Think Stats Chapter 5 Exercise 1](statistics/5-1-blue_men.md) (normal distribution of blue men)
This is a classic example of hypothesis testing using the normal distribution.  The effect size used here is the Z-statistic.

mu = 178

sigma = 7.7

dist = scipy.stats.norm(loc=mu, scale=sigma)

type(dist)

bottom = dist.cdf(177.8)

top = dist.cdf(185.42)

bmg_range = top - bottom

print(bmg_range)

Approximately 34.3% of men would be eligible to join the Blue Man Group based off of their height alone.

### Q5. Bayesian (Elvis Presley twin) 

Bayes' Theorem is an important tool in understanding what we really know, given evidence of other information we have, in a quantitative way.  It helps incorporate conditional probabilities into our conclusions.

Elvis Presley had a twin brother who died at birth.  What is the probability that Elvis was an identical twin? Assume we observe the following probabilities in the population: fraternal twin is 1/125 and identical twin is 1/300.  

Knowing that Elvis was a twin to a brother, we have to calculate the individual probabilities that he could have a twin brother given the two scenarios. Identical twins can either be both boys or both girls, so we multiply the odds of being identical twins by the odds of those twins being boys. Next, we calculate the probability that two fraternal twins are boys. There are 4 possibilities of fraternal twins, given that order matters -- M/M, M/F, F/M, FF. The probability of identical boys is then divided by the sum of the probability of identical boys and the probability of fraternal boys.

pr_ident_brothers = (1/300) * (1/2)

pr_frat_brothers = (1/125) * (1/4)

elvis_identical = pr_ident_brothers / (pr_ident_brothers + pr_frat_brothers)

print(elvis_identical)

Therefore, there was approximately a 45.5% chance that Elvis was an identical twin, given that he was a twin.

---

### Q6. Bayesian &amp; Frequentist Comparison  
How do frequentist and Bayesian statistics compare?

Frequentist and Bayesian statistics present two different ways to approach the concept of probabilities. Frequentist statistics never quantifies the uncertainty in fixed by unkown values, and views random events probabilistically. Therefore, it would be able to quantify a known probability such as a fair coin flip, but would never guess at the probability of a non-recurring event. Bayesian statistics, however, use probabilities to represent uncertainty in any case. Then, sample data is used to update the probability distribution to help close in on a more accurate "posterior" probability.

---

## <a name="section-e"></a>5.  Optional Exercises

The following exercises are optional, but we highly encourage you to complete them if you have the time.

### Q7. [Think Stats Chapter 7 Exercise 1](statistics/7-1-weight_vs_age.md) (correlation of weight vs. age)
In this exercise, you will compute the effect size of correlation.  Correlation measures the relationship of two variables, and data science is about exploring relationships in data.

import first

live, firsts, others = first.MakeFrames()

live = live.dropna(subset=['agepreg', 'totalwgt_lb'])

ages = live.agepreg

weights = live.totalwgt_lb

thinkplot.Scatter(ages, weights)

thinkplot.Show(xlabel = 'Mothers Age',
               ylabel = 'Birth Weight',
              alpha = 0.5)
              
print('Correlation', Corr(ages, weights))

print('SpearmanCorr', SpearmanCorr(ages,weights))

bins = np.arange(10,45,3)

indices = np.digitize(live.agepreg, bins)

groups = live.groupby(indices)

ages = [group.agepreg.mean() for i, group in groups][1:-1]

cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for i, group in groups][1:-1]

thinkplot.PrePlot(3)

for percent in [75,50,25]:
    weights = [cdf.Percentile(percent) for cdf in cdfs]
    label = '%dth' % percent
    thinkplot.Plot(ages, weights, label=label)
    
thinkplot.Config(xlabel="Mother's Age (years)",
                ylabel="Birth weight (lbs)",
                xlim=[14,45], legent=True)
                
The scatterplot and correlations show a weak linear relationship between the variables. Pearson's correlation is almose 0.07, while Spearman's correlation is over 0.09, which indicates that the relationship is either non-linear, or affected by outliers/skewed. By plotting the percentiles of weight versus age we can see that the relationship isn't entirely linear, with birth weight increasing faster between mother's 15 to 25 than anywhere else in the range.

### Q8. [Think Stats Chapter 8 Exercise 2](statistics/8-2-sampling_dist.md) (sampling distribution)
In the theoretical world, all data related to an experiment or a scientific problem would be available.  In the real world, some subset of that data is available.  This exercise asks you to take samples from an exponential distribution and examine how the standard error and confidence intervals vary with the sample size.

### Q9. [Think Stats Chapter 6 Exercise 1](statistics/6-1-household_income.md) (skewness of household income)

median = Median(sample)

mean = RawMoment(sample, 1)

pearson_skew = PearsonMedianSkewness(sample)

The mean is significantly higher the median, indicating a right skew to income. Pearson's skewness is positive, which also indicates a right skew, and is consistent with the general sentiment of the skew of income values.

high_log_sample = InterpolateSample(income_df, log_upper=7.0)

log_cdf = thinkstats2.Cdf(high_log_sample)

thinkplot.Cdf(log_cdf)

thinkplot.Config(xlabel='Household income (log $)',
               ylabel='CDF')
               
high_sample = np.power(10,high_log_sample)

cdf = thinkstats2.Cdf(high_sample)

thinkplot.Cdf(cdf)

thinkplot.Config(xlabel='Household income ($)',
               ylabel='CDF')

high_median = Median(high_sample)

high_mean = RawMoment(high_sample, 1)

high_pearson_skew = PearsonMedianSkewness(high_sample)

perc_below_highmean = cdf.Prob(high_mean)

The discrepancy between the mean and the median of the income values increases with the upper bound increased to 10 million because the mean increases significantly while the median isn't affected (no "new" values present). This insinuates that the skew is even further right. However, Pearson's skew is still skewed right, but to a lesser degree.

### Q10. [Think Stats Chapter 8 Exercise 3](statistics/8-3-scoring.md) (scoring)
### Q11. [Think Stats Chapter 9 Exercise 2](statistics/9-2-resampling.md) (resampling)

---

## <a name="section-f"></a>6.  Recommended Reading

Read Allen Downey's [Think Bayes](http://greenteapress.com/thinkbayes/) book.  It is available online for free, or you can buy a paper copy if you would like.

[<img src="img/think_bayes.png" title="Think Bayes"/>](http://greenteapress.com/thinkbayes/) 

---

## <a name="section-g"></a>7.  More Resources

Some people enjoy video content such as Khan Academy's [Probability and Statistics](https://www.khanacademy.org/math/probability) or the much longer and more in-depth Harvard [Statistics 110](https://www.youtube.com/playlist?list=PL2SOU6wwxB0uwwH80KTQ6ht66KWxbzTIo). You might also be interested in the book [Statistics Done Wrong](http://www.statisticsdonewrong.com/) or a very short [overview](http://schoolofdata.org/handbook/courses/the-math-you-need-to-start/) from School of Data.
