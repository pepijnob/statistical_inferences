---
output: html_document
editor_options: 
  chunk_output_type: console
---


# Bias detection{#bias}

In progress, not completed.  

<!-- fix headers -->
<!-- Integrate the explanation of the tests with the results.  -->
<!-- add code for trim and fill -->
<!-- integrate each bias technique with the example, not mention each twice. -->





Bias can be introduced throughout the research process. It is useful to prevent this or to detect it. Some researchers recommend a skeptical attitude towards any claim you read in the scientific literature. For example, the philosopher of science Deborah Mayo [-@mayo_statistical_2018] writes: "Confronted with the statistical news flash of the day, your first question is: Are the results due to selective reporting, cherry picking, or any number of other similar ruses?". You might not make yourself very popular if this is the first question you ask a speaker at the next scientific conference you are attending, but at the same time it would be naïve to ignore the fact that researchers more or less intentionally introduce bias into their claims.

At the most extreme end of practices that introduce bias into scientific research is **research misconduct**: Making up data or results, or changing or omitting data or results such that the research isn’t accurately represented in the research record. For example, [Andrew Wakefield](https://en.wikipedia.org/wiki/Andrew_Wakefield) authored a fraudulent paper in 1998 that claimed a link between the measles, mumps, and rubella (MMR) vaccine and autism. It was retracted in 2010, but only after it caused damage to trust in vaccines among some parts of the general population. The website Retraction Watch maintains a [database](retractiondatabase.org) that tracks reasons why scientific papers are retracted, including data fabrication. It is unknown how often data fabrication occurs in practice, but some estimates suggest that almost 2% of scientists have fabricated, falsified or modified data or results at least once [@fanelli_how_2009].

A different category of mistakes are statistical reporting errors, which range from reporting incorrect degrees of freedom, to reporting *p* = 0.056 as *p* < 0.05 [@nuijten_prevalence_2015]. Although we should do our best to prevent errors, everyone makes them, and data and code sharing become more common, it will become easier to detect errors in the work of other researchers. As Dorothy Bishop [-@bishop_fallibility_2018] writes: "As open science becomes increasingly the norm, we will find that everyone is fallible. The reputations of scientists will depend not on whether there are flaws in their research, but on how they respond when those flaws are noted."

[Statcheck](http://statcheck.io/) is software that automatically extracts statistics from articles and recomputes their *p*-values, as long as statistics are reported following guidelines from the American Psychological Association (APA). It checks if the reported statistics are internally consistent: Given the test statistics and degrees of freedom, is the reported *p*-value accurate? If it is, that makes it less likely that you have made a mistake (although it does not prevent coherent mistakes!) and if it is not, you should check if all the information in your statistical test is accurate. Statcheck is not perfect, and it will make Type 1 errors where it flags something as an error when it actually is not, but it is an easy to use tool to check your articles before you submit them for publication. 

Some inconsistencies in data are less easy to automatically detect, but can be identified manually. For example, @brown_grim_2017 show that many papers report means that are not possible given the sample size (known as the [*GRIM* test](http://nickbrown.fr/GRIM)). For example, Matti Heino noticed in a [blog post](https://mattiheino.com/2016/11/13/legacy-of-psychology/) that three of the reported means in the table in a classic study by Festinger and Carlsmith are mathematically impossible. With 20 observations per condition, and a scale from -5 to 5, all means should end in a multiple of 1/20, or 0.05. The three means ending in X.X8 or X.X2 are not consistent with the reported sample size and scale. Of course, such inconsistencies can be due to failing to report that there was missing data for some of the questions, but the GRIM test has also been used to uncover [scientific misconduct](https://en.wikipedia.org/wiki/GRIM_test). 

<div class="figure" style="text-align: center">
<img src="images/festinger_carlsmith.png" alt="Screenshot of the table reporting the main results from Festinger and Carlsmith, 1959" width="100%" />
<p class="caption">(\#fig:festinger)Screenshot of the table reporting the main results from Festinger and Carlsmith, 1959</p>
</div>

## Publication bias

Publication bias is one of the biggest challenges that science faces. **Publication bias** is the practice of selectively submitting and publishing scientific research, often based on whether or not the results are ‘statistically significant’ or not. The scientific literature is dominated by these statistically significant results. At the same time, we know that many studies researchers perform do not yield significant results. When scientists only have access to significant results, but not to all results, they are lacking a complete overview of the evidence for a hypothesis. In extreme cases, selective reporting can lead to a situation where there are hundreds of statistically significant results in the published literature, but no true effect because there are even more non-significant studies that are not shared. This is known as the **file-drawer problem**, when non-significant results are hidden away in file-drawers (or nowadays, folders on your computer) and not available to the scientific community. Every scientist should work towards solving the publication bias, because it is extremely difficult to learn what is likely to be true as long as scientists do not share all their results.  

Publication bias can only be fixed by making all your research results available to fellow scientists, irrespective of the *p*-value of the main hypothesis test. Registered Reports are one way to combat publication bias, as this type of scientic article is reviewed based on the introduction, method, and statistical analysis plan, before the data is collected. After peer review, the article can get an 'in principle acceptance', which means that as long as the research plan is followed, the article will be published, regardless of the results. Not surprisingly, as shown in Figure \@ref(fig:fig.1.3.1), an analysis of the first Registered Reports revealed that 31 out of 71 (44%) observed positive results, compared to 146 out of 152 (96%) of comparable standard scientific articles published during the same time period [@scheel_excess_2021].  

<div class="figure" style="text-align: center">
<img src="images/scheel.png" alt="Positive result rates for standard reports and Registered Reports. Error bars indicate 95% confidence intervals around the observed positive result rate." width="100%" />
<p class="caption">(\#fig:scheel)Positive result rates for standard reports and Registered Reports. Error bars indicate 95% confidence intervals around the observed positive result rate.</p>
</div>

In the past, Registered Reports did not exist, and scientisits did not share all results [@franco_publication_2014], and as a consequence, we have to try to detect the extent to which publication bias impacts our ability to accurately evaluate the literature. Meta-analyses should always carefully examine the impact of publication bias on the meta-analytic effect size estimate - even though only an estimated 57% of meta-analyses in Psychological Bulletin report that they assessed publication bias [@polanin_transparency_2020]. Several techniques to detect publication bias have been developed, and this continues to be a very active field of research. All techniques are based on specific assumptions, which you should consider before applying a test [@carter_correcting_2019]. There is no silver bullet: None of these techniques can fix publication bias. None of them can tell you with certainty what the true meta-analytic effect size is corrected for publication bias. The best these methods can do is detect publication bias caused by specific mechanisms, under specific conditions. Publication bias can be detected, but it can not be corrected. 

In the chapter on [likelihoods](#likelihoods) we saw how mixed results are to be expected, and can be strong evidence for the alternative hypothesis. It is not only the case that mixed results should be expected, but exclusively observing statistically significant results, especially when the statistical power is low, is very surprising. With the commonly used lower limit for statistical power of 80%, a non-significant result in one out of five studies when there is a true effect. Some researchers have pointed out that *not* finding mixed results can be very unlikely (or ‘too good to be true’) in a set of studies [@francis_frequency_2014; @schimmack_ironic_2012]. We don’t have a very good feeling for what real patterns of studies look like, because we are continuously exposed to a scientific literature that does not reflect reality. Almost all multiple study papers in the scientific literature present only statistically significant results, even though this is unlikely.

The [online Shiny app we used to compute binomial likelihoods](http://shiny.ieis.tue.nl/mixed_results_likelihood/) displays, if you scroll to the bottom of the page, binomial probabilities to find multiple significant findings given a specific assumption about the power of the tests. Francis [@francis_frequency_2014] used these binomial likelihoods to calculate the test of excessive significance [@ioannidis_exploratory_2007] for 44 articles published in the journal Psychological Science between 2009 and 2012 that contained four studies or more. He found that for 36 of these articles, the likelihood of observing four significant results, given the average power computed based on the observed effect sizes, was less than 10%. Given his choice of an alpha of 0.10, this binomial probability is a hypothesis test, and allows the claims (at a 10% alpha level) that whenever the binomial probability of the number of statistically significant results is lower than 10%, the data is surprising, and we can reject the hypothesis that this is an unbiased set of studies. In other words, it is unlikely that this many significant results would be observed, suggesting that publication bias or other selection effects have played a role in these articles. 

One of these 44 articles had been co-authored by myself [@jostmann_weight_2009]. At this time, I knew little about statistical power and publication bias, and beyond accused of improper scientific conduct was stressful. And yet, the accusations were correct - we had selectively reported results, and selectively reported analyses that worked. Having received virtually no training on this topic, we educated ourselves, and uploaded an unpublished study to the website psychfiledrawer.org (which no longer exists) to share our filedrawer. Some years later, we assisted when Many Labs 3 included one of the studies we had published in the set of studies they were replicating [@ebersole_many_2016], and when a null result was observed, we wrote "We have had to conclude that there is actually no reliable evidence for the effect" [@jostmann_short_2016]. I hope this educational materials prevents others from making a fool of themselves like we did. 

## Bias detection in meta-analysis

New methods to detect publication bias are continuously developed, and old methods become outdated (even though you can still see them appear in meta-analyses). One outdated method is known as **fail-safe N**. The idea was to calculate the number of non-significant results one would need to have in file-drawers before an observed meta-analytic effect size estimate would no longer be statistically different from 0. It is [no longer recommended](https://handbook-5-1.cochrane.org/chapter_10/10_4_4_3_fail_safe_n.htm), and Becker [-@becker_failsafe_2005] writes "Given the other approaches that now exist for dealing with publication bias, the failsafe N should be abandoned in favor of other, more informative analyses". Currently, the only use fail-safe N has is as a tool to identify meta-analyses that are not state-of-the-art.  

Before we can explain a second method (Trim-and-Fill), it’s useful to explain a common way to visualize meta-analyses, known as a **funnel plot**. In a funnel plot, the x-axis is used to plot the effect size of each study, and the y-axis is used to plot the ‘precision’ of each effect size. Typically, the y-axis is used to plot the standard error of each effect size estimate. The larger the study, the more precise the effect size estimate, the smaller the standard error, and thus the higher up in the funnel plot the study will be, and an infinitely precise study (with a standard error of 0) would be at the top of y-axis. 

The script below simulates meta-analyses based nsims studies, and stores all the results needed need to examine bias detection tools. The script generates a percentage of significant results as indicated by `pub.bias` - when set to 1, only significant result will be published. In the script, it is set to 0.05, as there is no true effect in the simulation (`m1` and `m2` are equal, so there is no difference between the groups), so only 5% false positives are expected. Finally, a funnel plot is printed. 


```r
library(metafor)
library(truncnorm)

nsims <- 100 # number of simulated experiments
pub.bias <- 0.05 # set percentage of significant results in the literature

m1 <- 0 # too large effects will make non-significant results extremely rare
sd1 <- 1
m2 <- 0
sd2 <- 1
metadata.sig <- data.frame(m1 = NA, m2 = NA, sd1 = NA, sd2 = NA, 
                           n1 = NA, n2 = NA, pvalues = NA, pcurve = NA)
metadata.nonsig <- data.frame(m1 = NA, m2 = NA, sd1 = NA, sd2 = NA, 
                              n1 = NA, n2 = NA, pvalues = NA, pcurve = NA)

# simulate significant effects in the expected direction
if(pub.bias > 0){
for (i in 1:nsims*pub.bias) { # for each simulated experiment
  p <- 1 # reset p to 1
  n <- round(truncnorm::rtruncnorm(1, 20, 1000, 100, 100)) # n based on truncated normal
  while (p > 0.025) { # continue simulating as along as p is not significant
    x <- rnorm(n = n, mean = m1, sd = sd1) 
    y <- rnorm(n = n, mean = m2, sd = sd2) 
    p <- t.test(x, y, alternative = "greater", var.equal = TRUE)$p.value
  }
  metadata.sig[i, 1] <- mean(x)
  metadata.sig[i, 2] <- mean(y)
  metadata.sig[i, 3] <- sd(x)
  metadata.sig[i, 4] <- sd(y)
  metadata.sig[i, 5] <- n
  metadata.sig[i, 6] <- n
  out <- t.test(x, y, var.equal = TRUE)
  metadata.sig[i, 7] <- out$p.value
  metadata.sig[i, 8] <- paste0("t(", out$parameter, ")=", out$statistic)
}}

# simulate non-significant effects (two-sided)
if(pub.bias < 1){
for (i in 1:nsims*(1-pub.bias)) { # for each simulated experiment
  p <- 0 # reset p to 1
  n <- round(truncnorm::rtruncnorm(1, 20, 1000, 100, 100))
  while (p < 0.05) { # continue simulating as along as p is significant
    x <- rnorm(n = n, mean = m1, sd = sd1) # produce  simulated participants
    y <- rnorm(n = n, mean = m2, sd = sd2) # produce  simulated participants
    p <- t.test(x, y, var.equal = TRUE)$p.value
  }
  metadata.nonsig[i, 1] <- mean(x)
  metadata.nonsig[i, 2] <- mean(y)
  metadata.nonsig[i, 3] <- sd(x)
  metadata.nonsig[i, 4] <- sd(y)
  metadata.nonsig[i, 5] <- n
  metadata.nonsig[i, 6] <- n
  out <- t.test(x, y, var.equal = TRUE)
  metadata.nonsig[i, 7] <- out$p.value
  metadata.nonsig[i, 8] <- paste0("t(", out$parameter, ")=", out$statistic)
}}

# Combine significant and non-significant effects
metadata <- rbind(metadata.nonsig, metadata.sig)

# Use escalc to compute effect sizes
metadata <- escalc(n1i = n1, n2i = n2, m1i = m1, m2i = m2, sd1i = sd1, 
  sd2i = sd2, measure = "SMD", data = metadata[complete.cases(metadata),])
# add se for PET-PEESE analysis
metadata$sei <- sqrt(metadata$vi)

#Perform meta-analysis
result <- metafor::rma(yi, vi, data = metadata)

# Print a Funnel Plot
metafor::funnel(result, level = 0.95, refline = 0)
abline(v = result$b[1], lty = "dashed") #  vertical line at meta-analytic ES
points(x = result$b[1], y = 0, cex = 1.5, pch = 17) # add point
```

The number of studies that are simulated is set to 100, and the script allows you to specify the amount of publication bias. When set to 1, all studies are significant, when set to 0, all studies will be non-significant (we will for now ignore the possibility that Type 1 errors will occur and could be published, even when there is no true effect). The unbiased percentage of significant results depends on the power (if there is a true effect) or the Type 1 error rate. Two groups of observations are simulated based on equal population means of 100. Thus, there is no true effect. Let’s start by looking at what unbiased research looks like. Because we set a seed, the simulation will yield the same results every time it is run - remove the set.seed function to get different results each time.


```
## 
## Random-Effects Model (k = 100; tau^2 estimator: REML)
## 
## tau^2 (estimated amount of total heterogeneity): 0 (SE = 0.0019)
## tau (square root of estimated tau^2 value):      0
## I^2 (total heterogeneity / total variability):   0.00%
## H^2 (total variability / sampling variability):  1.00
## 
## Test for Heterogeneity:
## Q(df = 99) = 88.6816, p-val = 0.7620
## 
## Model Results:
## 
## estimate      se    zval    pval    ci.lb   ci.ub 
##   0.0236  0.0122  1.9294  0.0537  -0.0004  0.0476  . 
## 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

<img src="13-bias_files/figure-html/metasim1-1.png" width="100%" style="display: block; margin: auto;" />

We see there are 100 studies in the meta-analysis (k = 100), and there is no statistically significant heterogeneity (*p* = 0.988, which is not surprising because we programmed the simulation so that all studies have the same true effect sizes, there is no heterogeneity in effect sizes). We also get the results for the meta-analysis. The meta-analytic estimate is d = 0.0049. The meta-analytic effect size is very close to 0 (as it should be, because the true effect size is indeed 0). The standard error around this estimate is 0.0132. With 100 studies, we have a very accurate estimate of the true effect size. The Z-value for the test against d = 0 is 0.3725, and the *p*-value for this test is 0.7095. There is no statistically significant difference, so we can not reject the hypothesis that the true effect size is 0. The CI around the effect size estimate (-0.021, 0.031) includes 0.  

It is easy to create a forest plot, where each effect size from each study is plotted on a separate line. 


```r
# Forest plot with 95% CI 
metafor::forest(result, level = 0.95)
```

<div class="figure" style="text-align: center">
<img src="13-bias_files/figure-html/forestplot-1.png" alt="Forest plot." width="100%" />
<p class="caption">(\#fig:forestplot)Forest plot.</p>
</div>

The forest plot is a bit big, with 100 studies, but we see they randomly vary around 0 as they should. The small diamond at the bottom represents the meta-analytic effect size estimate (the center of the diamond) and the 95% CI around it (the left and right edge of the diamond).  

We can also easily plot a beautifully unbiased funnel plot.

<div class="figure" style="text-align: center">
<img src="13-bias_files/figure-html/funnelexample-1.png" alt="Funnel plot without bias." width="100%" />
<p class="caption">(\#fig:funnelexample)Funnel plot without bias.</p>
</div>

The meta-analytic effect size estimate of 0.0049 is indicated by the triangle at the top of the figure. All studies (the black dots) fall within the white triangle, which indicates the 95% CI around 0 for different standard errors (and thus, for studies of different sizes). Studies with a small standard error (and thus a large number of observations) are at the top, while studies with less observations have a larger standard error, and are on the bottom of the plot.  





In the funnel plot below, there are no studies with a standard error less than 0.066, which means that there are no studies in the meta-analysis with such large sample sizes that they have this high level of precision.  

<div class="figure" style="text-align: center">
<img src="images/funnelplot1.png" alt="Default funnel plot." width="100%" />
<p class="caption">(\#fig:funnelplot1)Default funnel plot.</p>
</div>

You see a white triangle against the gray background, which is what gives the funnel plot its name. The funnel indicates the 95% CI around the meta-analytic effect size estimate (indicated by the horizontal vertical line at 0.4 in the plot above. That is, if the true effect size is d = 0.4 in the plot above, we should expect 95% of the effect size estimates to fall within the funnel. If sample sizes are small, effect size estimates will vary more around the true effect size (as you can see at the bottom of the funnel), and if sample sizes are larger, the effect size estimates vary more narrowly around the true effect size (as you can see at the top of the funnel). Some points fall outside the funnel plot (when the funnel plot is based on the 95% CI, 5% of the effects should fall outside of the funnel, in the long run). In real life meta-analyses, it isn’t very likely that all studies are sampled from a population with a true effect size of d = 0.4. Thus, the figure above is an idealistic representation. When the number of studies in a meta-analysis is small, it is very difficult to interpret a funnel-plot.  

Sometimes, it can be useful to center the funnel at 0, instead of at the meta-analytic effect size estimate. Below, you can see the same data as above, but now presented against a background of a funnel centered at 0. The funnel now indicates the effect sizes we should expect if there is no true effect. Studies that fall outside the funnel have a 95% confidence interval that does not include 0. These studies will thus be statistically significant. Therefore, a funnel centered at zero allows you to easily see which studies are statistically significant, and which are not. When there is no publication bias, as in the figure below, effect sizes should be distributed randomly around the true effect size. This means there will be a reasonable number of non-significant effects.  

<div class="figure" style="text-align: center">
<img src="images/funnelplot2.png" alt="Funnel plot with funnel centered at 0." width="100%" />
<p class="caption">(\#fig:funnelplot2)Funnel plot with funnel centered at 0.</p>
</div>

If there is extreme publication bias, as in the figure below, all the points within the funnel would be missing. Instead of normal variation around the true effect size, there is asymmetry in the effect size distribution. Several techniques that aim to detect publication bias focus on this asymmetry.  

<div class="figure" style="text-align: center">
<img src="images/funnelplot3.png" alt="Funnel plot with publication bias." width="100%" />
<p class="caption">(\#fig:funnelplot3)Funnel plot with publication bias.</p>
</div>

When there is publication bias because researchers only publish statistically significant results (p \< alpha), and you calculate the effect size in a meta-analysis, the meta-analytic effect size estimate is **higher** when there is publication bias (where researchers publish only effects with p \< alpha) compared to when there is no publication bias. This is because publication bias filters out the smaller, non-significant, effect sizes. which are then not included in the meta-analysis. This leads to a meta-analytic effect size estimate that is larger than the true population effect size. With strong publication bias, we know the meta-analytic effect size is inflated, but we don't know by how much. The true effect size could just be a bit smaller, but the true effect size could also be 0, in the most extreme case.

## Trim and Fill  

Trim and fill is a technique that aims to augment a dataset by adding hypothetical ‘missing’ studies (that may be in the ‘file-drawer’). The procedure starts by removing (‘trimming’) small studies that bias the meta-analytic effect size, then estimates the true effect size, and ends with ‘filling’ in a funnel plot with studies that are assumed to be missing due to publication bias. In the picture below, you can see the same data as above, but now with added unfilled circles which represent ‘imputed’ studies. If you look closely, you’ll see these points each have a mirror image on the opposite side of the meta-analytic effect size estimate (this is clearest in the lower half of the funnel plot).  


<div class="figure" style="text-align: center">
<img src="images/trimfill1.png" alt="Funnel plot with assumed missing effects added through trim-and-fill." width="100%" />
<p class="caption">(\#fig:trimfill1)Funnel plot with assumed missing effects added through trim-and-fill.</p>
</div>

Trim-and-fill is not created to examine publication bias based on whether studies yield significant p-values, or not. Instead, it's created for publication bias caused by effects that are strongly (perhaps even significantly!) in the opposite direction of the remaining studies or the effect a researcher wants to find. Think of a meta-analysis on the benefits of some treatment, where the 8 studies that revealed the treatment actually makes people feel much worse are hidden in the file drawer.  

Trim-and-fill is not very good under many realistic publication bias scenarios. The method is criticized for its reliance on the strong assumption of symmetry in the funnel plot. When publication bias is based on the *p*-value of the study (arguably the most important source of publication bias in many fields) the trim-and-fill method does not perform well enough to yield a corrected meta-analytic effect size estimate that is close to the true effect size (Peters, Sutton, Jones, Abrams, & Rushton, 2007; Terrin, Schmid, Lau, & Olkin, 2003). When the assumptions are met, it can be used as a **sensitivity analysis.** When the difference between the trim-and-fill corrected effect size estimate and the uncorrected meta-analytic effect size estimate is small, publication bias due to the *p*-value of the individual studies is unlikely to change the conclusions of the meta-analysis. Researchers should not report the trim-and-fill corrected effect size estimate as a realistic estimate of the true effect size if there would not be publication bias (Peters et al., 2007). Many meta-analysts make this error, but regrettably, that’s not how trim-and-fill can be used.  

## PET-PEESE  

A more novel class of solutions to publication bias is **meta-regression**. Instead of plotting a line through individual data-points, in meta-regression a line is plotted through data points that each represent a study. As with normal regression, the more data meta-regression is based on, the more precise the estimate is, and therefore, the more studies in a meta-analysis, the better meta-regression will work in practice. If the number of studies is small, all bias detection tests lose power, and this is something that one should keep in mind when using meta-regression. Furthermore, regression requires sufficient variation in the data, which in the case of meta-regression means a wide range of sample sizes (recommendations indicate meta-regression performs well if studies have a range from 15 to 200 participants in each group – which is not typical for most research areas in psychology). Meta-regression techniques typically estimate the population effect size if precision was perfect (so when the standard error = 0).  

One meta-regression technique is known as PET-PEESE (for a discussion, see Stanley, 2017). It consists of a ‘precision-effect-test’ (PET) which can be used in a Neyman-Pearson framework to test whether there is a true effect beyond the inflation due to selective reporting. The PET test works as follows: When the 95% CI around the PET estimate at the intercept SE = 0 does not contain an effect size of 0, we can reject the null hypothesis of no true effect.  

The estimated effect size for PET is calculated with: d = β0 + β1SEi + ui where d is the estimated effect size, SE is the standard error, and the equation is estimated using weighted least squares (WLS), with 1/SE2i as the weights. The PET estimate underestimates the effect size when there is a true effect. Therefore, the PET-PEESE procedure recommends first using PET to test whether there is a true effect or not. If PET suggests there is a true effect, then PEESE should be used to estimate the meta-analytic effect size. In PEESE, the standard error (used in PET) is replaced by the variance (i.e., the standard error squared): d = γ0 + γ1SE2i + ui, which Stanley and Doucouliagos (2014) find reduces the bias of the estimated meta-regression intercept.  

PET-PEESE has limitations, as all bias detection techniques have. The biggest limitations are that it does not work well when there are few studies, all studies in a meta-analysis have small sample sizes, or when there is large heterogeneity in the meta-analysis (Stanley, 2017). When these situations apply (and they will in practice), PET-PEESE might not be a good approach. Furthermore, there are some situations where there might be a correlation between sample size and precision, which in practice will often be linked to heterogeneity in the effect sizes included in a meta-analysis. For example, if true effects are different across studies, and people perform power analyses with accurate information about the expected true effect size, large effect sizes in a meta-analysis will have small sample sizes, and small effects will have large sample sizes. Meta-regression is, like normal regression, a way to test for an association, but you need to think about the causal mechanism behind the association.  

## P-curve Analysis  

Another novel approach to examining publication bias is *p*-curve analysis. This is a meta-analytic technique that does not focus on effect sizes, but analyzes the *p*-values of the statistical tests for the main hypothesis in a paper (Simonsohn, Nelson, & Simmons, 2014a). A similar meta-analytic technique is *p*-uniform (van Assen, van Aert, & Wicherts, 2015). When the null-hypothesis is true, *p*-values are uniformly distributed (see week 1 of my first MOOC). When there is a true effect p-values are skewed to the right, which means there should be more small *p*-values (e.g., *p* = 0.01) than high *p*-values (*p* = 0.04) in a set of studies.  

*P*-curve analysis tests whether the curve of the *p*-values is flatter than what would be expected if the studies you analyze had 33% power (which suggests the distribution looks more like one expected when the null-hypothesis is true), or more right-skewed than a uniform *p*-value distribution (which suggests the studies might have examined a true effect and had at least some power). As an example, let’s consider Figure 3 from Simonsohn and colleagues (2014). The authors compared 20 papers in the Journal of Personality and Social Psychology that used a covariate in the analysis, and 20 studies that did not use a covariate. The authors suspected that researchers might add a covariate in their analyses to try to find a *p*-value smaller than 0.05, when the first analysis they tried did not yield a significant effect. This is exactly what they found.  

When you look at the *p*-curve, you can see five points in the blue line. *P*-curve analysis is performed *only* on statistically significant results, based on the assumption that these are always published. Thus, it looks at the distribution of *p*-values below 0.05, and the 5 points illustrate all *p*-values between 0 and 0.01, 0.01 and 0.02, 0.02 and 0.03, 0.03 and 0.04, and 0.04 and 0.05. In the figure on the right, you see a relatively normal right-skewed *p*-value distribution with more low than high *p*-values. The *p*-curve analysis shows the blue line in the right figure is more right-skewed than the uniform red line (where the red line is the distribution you’d expect if there was no true effect).  


<div class="figure" style="text-align: center">
<img src="images/pcurve.png" alt="Figure 3 from Simonsohn et al (2014) showing a p-curve with and without bias." width="100%" />
<p class="caption">(\#fig:pcurve)Figure 3 from Simonsohn et al (2014) showing a p-curve with and without bias.</p>
</div>

In the left figure we see the opposite pattern, with mainly high *p*-values around 0.05, and almost no *p*-values around 0.01. Because the blue line is significantly less right-skewed than the green line, the *p*-curve analysis suggests this set of studies lacks ‘evidential value’. Using the term ‘evidential value’ is not formally correct when talking about *p*-values (evidence is always relative, and better reserved for when talking about likelihoods for example), so it’s best to interpret this as ‘the data do not look as if they come from a *p*-value distribution that reflects the presence of a true effect’.  

P-curve analysis is a useful tool. But it is important to correctly interpret what a *p*-curve analysis can tell you. A right-skewed *p*-curve does not prove that there is no bias, or that the hypothesis is true. A flat *p*-curve does not prove that the theory is incorrect, but it does show that the studies you analyzed do not provide evidence for the presence of a true effect. When many people have studied a particular topic, and the result is a flat *p*-value distribution, this is probably not an effect you want to build on. The two tests for right-skewed and a flat distribution perform relatively well even when there is some heterogeneity in the effect size distribution.  

### TIVA  

A more powerful test than the Test for Excessive Significance is the Test of Insufficient Variance proposed by Uli Schimmack (published on a [blog](https://replicationindex.wordpress.com/2014/12/30/the-test-of-insufficient-variance-tiva-a-new-tool-for-the-detection-of-questionable-research-practices/) instead of in a scientific journal). It also uses *p*-values from reported tests, and builds on the relationship between *p*-values and *Z*-values. If all studies examine the same fixed effect, the Z-scores related to p-values should follow a normal distribution, and individual studies vary as a function of sampling variability. The variance of an unbiased set of Z-scores is not smaller than 1. The variance can be larger than 1, for example when the studies have different true effects. In biased sets of studies, for example when significant results are selectively reported, the variance of the *Z*-scores can be smaller than 1. When non-significant studies are not published, the variance decreases. Another reason for low variance is the use of flexibility during the data-analysis, such as analyzing the data in multiple ways, ad only reporting tests that yield a significant result. TIVA tests whether the variance that is observed is surprising, assuming the dataset is unbiased. A significant p-value for the TIVA test allows you to reject the hypothesis that the studies are unbiased. Uli Schimack shows how the studies reported by @bem_feeling_2011 in his article on pre-cognition are biased. The online [p-checker Shiny app](https://shinyapps.org/apps/p-checker) by Felix Schönbrodt allows you to perform the test of excessive significance, TIVA, and a related bias test, the R-Index.  

The Test of Insufficient Variance (TIVA) is another new meta-analytic method (published on a [blog](https://replicationindex.wordpress.com/2014/12/30/the-test-of-insufficient-variance-tiva-a-new-tool-for-the-detection-of-questionable-research-practices/) instead of in a scientific article!) developed by Uli Schimmack. It also uses *p*-values from reported tests, and builds on the relationship between *p*-values and Z-values. If all studies examine the same fixed effect, the Z-scores related to *p*-values should follow a normal distribution, and individual studies should vary as a function of sampling variability. The variance of an unbiased set of Z-scores is not smaller than 1. The variance can be larger than 1, for example, when the studies have different true effects.  

In biased sets of studies, the variance of the Z-scores can be smaller than 1. When non-significant studies are not published, the variance decreases. Another reason for low variance is the use of flexibility during the data-analysis, such as performing multiple analyses, but only reporting those analyses that yield a significant result.  

TIVA tests whether the variance that is observed is surprising, assuming the dataset is unbiased. A significant *p*-value for the TIVA test allows you to reject the hypothesis that the studies are unbiased. Uli Schimmack shows how the studies reported by Bem (2011) in his article on pre-cognition are biased, which suggests that the observed effect size in these studies is inflated. TIVA provides a more powerful test than related tests aimed to detect the presence of publication bias, such as the Test for Excessive Significance (Ioannidis & Trikalinos, 2007).  



### Let’s Detect Some Bias!


### Introducing bias

Now that we know what a real null effect looks like, let’s introduce bias. We can set extreme publication bias by including only significant results in the meta-analysis, setting bias to 1. The forest plot now looks much more peculiar.

<div class="figure" style="text-align: center">
<img src="13-bias_files/figure-html/metasimbias-1.png" alt="Forest plot with bias." width="100%" />
<p class="caption">(\#fig:metasimbias)Forest plot with bias.</p>
</div>


The forest plot in the figure looks quite peculiar, as the studies have confidence intervals that only just fail to include 0, suggesting most studies are only just statistically significant. This suggests publication bias.  

All studies are significant. A fixed effect meta-analytic effect size estimate is indicated on the bottom of the plot, and is estimated to be d = 0.31. We can also look at the meta-analysis results:


```r
# perform a meta-analysis with the metafor package
result <- metafor::rma(yi, vi, data = metadata, method = "FE")
result
```

```
## 
## Fixed-Effects Model (k = 100)
## 
## I^2 (total heterogeneity / total variability):   0.00%
## H^2 (total variability / sampling variability):  0.58
## 
## Test for Heterogeneity:
## Q(df = 99) = 57.1108, p-val = 0.9998
## 
## Model Results:
## 
## estimate      se     zval    pval   ci.lb   ci.ub 
##   0.3144  0.0139  22.5530  <.0001  0.2871  0.3417  *** 
## 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

As we see, even thought the true effect size in our simulation is 0, with extreme publication bias, all individual studies are significant, and the meta-analytic effect size estimate will be severely inflated (d = 0.31 instead of d = 0), such that it can give the impression there is overwhelming support for H1 when H0 is true.  

### Bias detection techniques

Let’s explore how PET-PEESE meta-regression attempts to give us an unbiased effect size estimate, under specific assumptions of how publication bias is caused. 


```r
# PET PEESE code below is adapted from Joe Hilgard: https://github.com/Joe-Hilgard/PETPEESE/blob/master/PETPEESE_functions.R
# PET
PET <- metafor::rma(yi = yi, sei = sei, mods = ~sei, data = metadata, method = "FE")

# PEESE
PEESE <- metafor::rma(yi = yi, sei = sei, mods = ~I(sei^2), data = metadata, method = "FE")

# Funnel Plot 
metafor::funnel(result, level = 0.95, refline = 0, main = paste("FE d =", round(result$b[1],2),"PET d =", round(PET$b[1],2),"PEESE d =", round(PEESE$b[1],2)))
abline(v = result$b[1], lty = "dashed") #draw vertical line at meta-analytic effect size estimate
points(x = result$b[1], y = 0, cex = 1.5, pch = 17) #draw point at meta-analytic effect size estimate
# PET PEESE code below is adapted from Joe Hilgard: https://github.com/Joe-Hilgard/PETPEESE/blob/master/PETPEESE_functions.R
# PEESE line and point
sei <- (seq(0, max(sqrt(result$vi)), .001))
vi <- sei^2
yi <- PEESE$b[1] + PEESE$b[2]*vi
grid <- data.frame(yi, vi, sei)
lines(x = grid$yi, y = grid$sei, typ = 'l') # add line for PEESE
points(x = (PEESE$b[1]), y = 0, cex = 1.5, pch = 5) # add point estimate for PEESE
# PET line and point
abline(a = -PET$b[1]/PET$b[2], b = 1/PET$b[2]) # add line for PET
points(x = PET$b[1], y = 0, cex = 1.5) # add point estimate for PET
segments(x0 = PET$ci.lb[1], y0 = 0, x1 = PET$ci.ub[1], y1 = 0, lty = "dashed") #Add 95% CI around PET
```

<div class="figure" style="text-align: center">
<img src="13-bias_files/figure-html/petpeese-1.png" alt="Funnel plot with PET_PEESE regression lines." width="100%" />
<p class="caption">(\#fig:petpeese)Funnel plot with PET_PEESE regression lines.</p>
</div>

In addition to the funnel plot, we see 3 lines through the plots. The vertical line at d = 0.31 is the meta-analytic effect size estimate, which is upwardly biased because we are averaging over statistically significant studies only. There are 2 additional lines, which are the meta-regression lines for PET-PEESE based on the formulas detailed previously. The straight line gives us the PET estimate at a SE of 0 (an infinite sample, at the top of the plot), indicated by the circle. The dotted line around this PET estimate is the 95% confidence interval around the estimate. In this case, the 95% CI contains 0, which means that based on the PET estimate of d = 0.02, we cannot reject a meta-analytic effect size of 0. Note that even with 100 studies, the 95% CI is quite wide. Meta-regression is, just like normal regression, only as accurate as we have data. This is one limitation of PET-PEESE meta-regression: With small numbers of studies in the meta-analysis, it has low accuracy.  

 The general procedure for PET-PEESE is to perform PET, and if we can reject an effect of 0, the PEESE estimate is the best estimate for the unbiased effect size (the diamond at SE = 0). The PEESE estimate is d = 0.18, but this should not be used since we can not reject the null based on the PET estimate. The only difference between PET and PEESE is that PET is based on the standard error, while the PEESE estimate uses the variance. Using PET-PEESE meta-regression we can conclude there is reason to worry. Although we can’t be certain, the normal meta-analytic effect size estimate seems to be affected (maybe severely) by some form of bias.
 
Let’s explore our biased meta-analysis with other bias detection tools. Code code below allows us to perform the Test of Insufficient Variance. 


```r
# TIVA code (Uli Schimmack: https://replicationindex.wordpress.com/2014/12/30/the-test-of-insufficient-variance-tiva-a-new-tool-for-the-detection-of-questionable-research-practices/)
k = length(metadata$pvalues) 
z = qnorm(1 - metadata$pvalues/2)
var.z = var(z) 
tiva.p = pchisq(var.z * (k - 1),k - 1) 
var.z 
```

```
## [1] 0.117546
```

```r
round(tiva.p,3)
```

```
## [1] 0
```

The variance is very small (0.11, much lower than 1) and a test against the normal variance we would expect shows the observed variance is statistically different from 1 (*p* \< 0.001). This suggests strong bias, and there is no good reason to assume the normal meta-analytic effect size estimate is accurate.  

Finally, the script provides the test statistics for the 100 simulated *t*-tests that are included in the meta-analysis. The first few rows look like:  


```r
cat(metadata$pcurve[1:5],sep = "\n")
```

```
## t(146)=2.6766329007035
## t(258)=2.84977661171535
## t(188)=2.73540213686467
## t(76)=2.34374683727237
## t(170)=2.13211285378042
```

<!-- You can go to the online *p*-curve app at  <http://www.p-curve.com/app4/> where you can paste all test results, and click the ‘Make the p-curve’ button. Note that the p-curve app will only yield a result when therre are *p*-values smaller than 0.05 - if all test statistics yield a *p* \> 0.05, the *p*-curve cannot be computed.  -->

<!-- Below, we will compute the p-curve based on the p-values directly.  -->

<!-- ```{r, cache = TRUE} -->
<!-- #Adapted from https://github.com/nicebread/p-checker/blob/master/p-curve.R -->

<!-- ncp33z <- function(power=1/3, p.crit=.05) {       -->
<!--       xc = qnorm(p=1-p.crit/2) -->
<!--       #Find noncentrality parameter (ncp) that leads 33% power to obtain xc -->
<!-- 	  f = function(delta, pr, x) pnorm(x, mean = delta) - (1-power) -->
<!-- 	  out = uniroot(f, c(0, 37.62), x = xc) -->
<!-- 	  return(out$root)  -->
<!-- } -->

<!-- theoretical_power_curve <- function(power=1/3, p.max=.05, normalize=TRUE) { -->
<!-- 	# compute arbitrary test statistics for requested power -->
<!-- 	library(pwr) -->
<!-- 	d <- 0.2 -->
<!-- 	n <- pwr.t.test(d=0.2, power=power)$n*2 -->

<!-- 	crit <- seq(0.01, p.max, by=.01) -->
<!-- 	pdens <- c() -->
<!-- 	for (cr in crit) { -->
<!-- 		pdens <- c(pdens, pwr.t.test(d=0.2, power=NULL, n=n/2, sig.level=cr)$power) -->
<!-- 	} -->
<!-- 	p.dens <- diff(c(0, pdens)) -->
<!-- 	if (normalize == TRUE) p.dens <- p.dens/sum(p.dens) -->

<!-- 	names(p.dens) <- as.character(crit) -->
<!-- 	return(p.dens) -->
<!-- } -->

<!-- p.crit=.05 -->
<!-- power=1/3 -->

<!-- #get p-values from metadata -->
<!-- p_vals <- metadata$pvalues -->
<!-- res <- data.frame() -->

<!-- z <- qnorm(p_vals/2, lower.tail=FALSE) -->
<!-- ppr <- p_vals*(1/p.crit)	# pp-value for right-skew  -->
<!-- ppl <- 1-ppr		# pp-value for left-skew -->
<!-- ncp33 <- ncp33z(power=power, p.crit=p.crit) -->
<!-- pp33 <- (pnorm(z, mean=ncp33, sd=1)-(1-power))*(1/power) -->

<!-- res <- rbind(res, data.frame(p=p_vals, ppr=ppr, ppl=ppl, pp33=pp33)) -->

<!-- #recode extreme values	 -->

<!-- res$ppr[res$ppr < .00001] <- .00001 -->
<!-- res$ppl[res$ppl < .00001] <- .00001 -->
<!-- res$pp33[res$pp33 < .00001] <- .00001 -->
<!-- res$ppr[res$ppr > .99999] <- .99999 -->
<!-- res$ppl[res$ppl > .99999] <- .99999 -->
<!-- res$pp33[res$pp33 > .99999] <- .99999 -->

<!-- #remove non-significant values -->
<!-- res[res$p > p.crit, ] <- NA -->

<!-- #New p-curve computation (p-curve app 3.0) -->
<!-- p_curve_3 <- function(pps) { -->

<!-- 	pps <- na.omit(pps) -->

<!-- #STOUFFER: Overall tests aggregating pp-values -->
<!-- 	ktot <- sum(!is.na(pps$ppr)) -->
<!-- 	Z_ppr <- sum(qnorm(pps$ppr))/sqrt(ktot)          # right skew -->
<!-- 	Z_ppl <- sum(qnorm(pps$ppl))/sqrt(ktot)          # left skew -->
<!-- 	Z_pp33<- sum(qnorm(pps$pp33))/sqrt(ktot)         # 33% -->

<!-- 	p_ppr <- pnorm(Z_ppr) -->
<!-- 	p_ppl <- pnorm(Z_ppl) -->
<!-- 	p_pp33<- pnorm(Z_pp33) -->

<!-- 	return(list( -->
<!-- 		Z_evidence = Z_ppr,  -->
<!-- 		p_evidence = p_ppr,  -->
<!-- 		Z_hack = Z_ppl,  -->
<!-- 		p_hack = p_ppl,  -->
<!-- 		Z_lack = Z_pp33,  -->
<!-- 		p_lack = p_pp33, -->
<!-- 		inconclusive = ifelse(p_ppr>.05 & p_ppl>.05 & p_pp33>.05, TRUE, FALSE))) -->
<!-- } -->

<!-- #p_curve_3(pps = res) -->

<!-- #Create p-curve plot -->

<!-- plot(NA, xlim=c(0, p.crit), ylim=c(0, 100), xlab="p-value", ylab="Percentage of p values") -->
<!-- abline(h=1/p.crit, col="red", lty="dashed", lwd=2) -->
<!-- legend("topright", lty=c("solid", "dotted", "dashed"), col=c("dodgerblue", "darkgreen", "red"), legend=c("Observed p-curve", paste0(round(power,2), "% power curve"), "Nil effect"), bty="n") -->

<!-- bins <- table(cut(res$p, breaks=seq(0, p.crit, by=.01))) -->
<!-- perc <- (bins/sum(bins))*100 -->

<!-- # empirical p-curve -->
<!-- lines(x=seq(0, p.crit-.01, by=.01)+.005, y=perc, col="dodgerblue", lwd=2) -->

<!-- # 33% (or any other) power curve -->
<!-- lines(x=seq(0, p.crit-.01, by=.01)+.005, y=theoretical_power_curve(power, p.max=p.crit)*100, col="darkgreen", lty="dashed", lwd=2) -->

<!-- text(x=seq(0, p.crit-.01, by=.01)+.006, y=perc + 8, col="black", label=paste0(round(perc), "%"), cex=) -->

<!-- legend("topleft", legend=c(paste0("Test for right skewness: p = ", round(p_curve_3(pps = res)$p_evidence,2)), paste0("Test for flatness: p = ", round(p_curve_3(pps = res)$p_lack,2))), bty="n") -->

<!-- ``` -->

The output will in the p-curve app will look similar to the figure above. The *p*-curve analysis shows that there is no evidential value in the set of studies (the curve is not right-skewed, as we would expect if there is a true effect and decent power to detect such an effect), and the *p*-value distribution is flatter than we would expect if we have 33% power, so the curve lacks evidential value.  

Based on the continuous Stouffer’s test for the full *p*-curve, we can conclude the observed *p*-value distribution is not skewed enough to be interpreted as the presence of a true effect size, and it is flatter than we would expect if the studies had 33% power. **Therefore, we can conclude these studies do not provide support for the theory that generated these studies**. The theory might still be true - but the set of studies we have analyzed here do not provide support for the theory.

### Z-curve analysis

GRAB EXAMPLE FROM SCIENCEVERSE. 

For recent examples, see [@sotola_garbage_2022]. 

A relatively novel technique is *z*-curve, which is basically a meta-analysis of observed power (Bartos & Schimmack, 2020; Schimmack & Brunner, 2020). This analysis can be used to examine selection bias in the literature. Scientists often selectively report only statistically significant results in their manuscript, and fail to report non-significant tests they have performed. This selection for significant results introduces bias in the scientific literature. 

Like a traditional meta-analysis, *z*-curve transforms observed test results (*p*-values) into *z*-scores. Using mixtures of normal distributions centered at means 0 to 6, *z*-curve aims to estimate the average power of the studies. The newest version of *z*-curve then calculates the *observed discovery rate* (the percentage of significant results, or the observed power), the *expected discovery rate* (EDR: the proportion of the area under the curve on the right side of the significance criterion) and the expected replication rate (ERR: the proportion of successfully replicated significant studies from all significant studies). *Z*-curve is able to correct for selection bias for positive results (under specific assumptions), and can estimate the EDR and ERR using only the significant *p*-values.

To examine the presence of bias, it is preferable to submit non-significant and significant *p*-values to a *z*-curve analysis, even if only the significant *p*-values are used to produce estimates. Publication bias can then be examined by comparing the ODR to the EDR. If the results of studies are shared in a well-structured meta-study file, all the *p*-values needed to perform a *z*-curve analysis are directly available, and it is clear which statistical test is related to a hypothesis is researchers are interested in including only specific analyses in the *z*-curve.

Since our simulated studies have bias, the *z*-curve analysis should be able to indicate this. 


```r
# devtools::install_github("FBartos/zcurve")
# Get the p-value for each analysis
p_vals <- metadata$pvalues
z <- qnorm(1-p_vals/2)
# Perform the z-curve analysis using the z-curve package
z_res <- zcurve::zcurve(z, method = "EM", bootstrap = 1000)
plot(z_res, annotation = TRUE, CI = TRUE)
```

<img src="13-bias_files/figure-html/unnamed-chunk-2-1.png" width="100%" style="display: block; margin: auto;" />

```r
print(z_res)
```

```
## Call:
## zcurve::zcurve(z = z, method = "EM", bootstrap = 1000)
## 
## Estimates:
##        ERR        EDR 
## 0.04247541 0.05470193
```

```r
summary(z_res, all = TRUE)
```

```
## Call:
## zcurve::zcurve(z = z, method = "EM", bootstrap = 1000)
## 
## model: EM via EM
## 
##               Estimate  l.CI   u.CI
## ERR              0.042 0.025  0.147
## EDR              0.055 0.050  0.142
## Soric FDR        0.910 0.319  1.000
## File Drawer R   17.281 6.062 19.000
## Expected N        1828   706   2000
## Missing N         1728   606   1900
## 
## Model converged in 18 + 113 iterations
## Fitted using 100 z-values. 100 supplied, 100 significant (ODR = 1.00, 95% CI [0.95, 1.00]).
## Q = -7.69, 95% CI[-22.84, 8.62]
```

We see that  out of 100 studies were significant, which makes the observed power (across all these studies with different sample sizes) 100% (95% CI[0.95;1]). The expected discovery rate (EDR) is only 5%, which differs statistically differ from the observed discovery rate, which means there is clear indication of selection bias based on the *z*-curve analysis. The expected replicability rate for these studies is 6% 95% CI[0.05;0.06] which is in line with the expectation that we will only observe 5% Type 1 errors. Thus, even though we only entered significant *p*-values, Z-curve analysis correctly suggests that we should not expect these results to replicate.    

### Conclusion  

Publication bias is a big problem in science. It is present in almost all meta-analyses performed on the primary hypothesis test in scientific articles, because these articles are much more likely to be submitted and accepted for publication if this test is statistically significant. Meta-analytic effect size estimates that are not corrected for bias will almost always overestimate the true effect size. Publication bias inflates the effect size estimate to an unknown extent – but it could even be the case that the true effect size is zero! 

There is a lot of activity in the literature on tests for publication bias. There are many different tests, and you need to carefully check the assumptions of each test before applying it. Most tests don’t work well when there is large heterogeneity, and heterogeneity is quite likely. I’d currently recommend applying multiple tests that should, based on the literature, give informative results based on the studies in your meta-analysis. When you plan to perform a meta-analysis, you should always examine whether there is publication bias. Given that bias detection tests is an active field, read up on the latest work in this area. None of the bias detection techniques discussed in this assignment will be a silver bullet, but they will be better than naively interpreting the uncorrected effect size estimate from the meta-analysis.  

