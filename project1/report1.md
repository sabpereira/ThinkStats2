# The Contribution of the Opioid Epidemic on the Falling Life Expectancy in the United States

#### Sabrina Pereira


## **Introduction**

In recent years, a downward trend in the the Average Life Expectancy in the US has emerged.

![](https://github.com/sabpereira/ThinkStats2/blob/master/project1/output_5_0.png)

At the same time, the number of deaths by opioid poisoning have risen dramatically. In 1999, there were 6.0 opioid poisoning related deaths for every 100,000 people - by 2017, this had risen to 21.6 deaths per 100,000. What is known as the "Opioid Epidemic" or "Opioid Crisis" was declared a Public Health Emergency by the Trump Administration's Health and Human Services in 2017.

![](https://github.com/sabpereira/ThinkStats2/blob/master/project1/output_7_0.png)

Around 2015, at the same time we start noticing that the number of opioid overdose related deaths start dramatically increasing, the Average Life Expectancy begins to drop.

This prompted me to ask,

_**What is the effect of the increased opioid-related deaths on the Average Life Expectancy in the US?**_

## **Methodology**

To answer this question, I will be attempting to predict what the Average Life Expectancy (ALE) in the US for various years would look like if there were no deaths related to opioid overdoses, and compare how much the actual ALEs differ from this theoretical, Zero-Opioid Scenario ALE.

### Data Sources

I will be using the Centers for Disease Control and Prevention's (CDC) National Center for Health Statistics (NCHS) data for Death rates and life expectancy at birth for the US (Available at https://data.cdc.gov/NCHS/NCHS-Death-rates-and-life-expectancy-at-birth/w9j2-ggv5 ). All further mentions of life expectancies or ALE will relate to the CDC's definition of life expectancy at birth. The Average Life Expectancy is a summary statistic taking account the death rates of various age groups over various years, giving us a snapshot of the health of the population of the US at a point in time.


I will also be using the CDC's Multiple Cause of Death Data for the years 1999-2017 (Available at https://wonder.cdc.gov/mcd.html ) to extract the population size and number of deaths in each age group in the US, as well as the total numbers of deaths due to opioid overdoses in each age group. To define deaths due to opioid overdoses, I used the CDC's definition of the ICD-10 codes that related to "All opioid poisoning" (the chart containing the codes fitting this definition is available at https://www.cdc.gov/drugoverdose/pdf/pdo_guide_to_icd-9-cm_and_icd-10_codes-a.pdf )

In both datasets, populations were taken from the 2000 and 2010 Census data, and intercensal population estimates have been created for all other years.

For more information on the data in the report and how it was organized, please refer to the [project’s notebook](https://github.com/sabpereira/ThinkStats2/blob/master/project1/project1.ipynb). 


### Age-adjusted Death Rate Approach

Recalculating the theoretical life expectancies by removing the effect of the opioid related deaths in order to quantify how much of the drop in life expectancy is explained by the opioid related deaths would be ideal, but it is a very complicated and involved calculation.

Therefore, for simplifications, I will construct a model where I estimate the Average Life Expectancy for a year using the the Age-adjusted Death Rate for the same year. The AADR for the total population is much more easily calculated, and the ALE and the AADR for any given year are closely related - both are summary statistics that are calculated with the age-specific death rates of the population (the death rates for each age group).

I will then be finding what the AADR for a year would look like in a Zero-Opioid Scenario (A theoretical scenario where any deaths related to opioid overdoses do not occur), and use the created model to estimate the theoretical ALE we would see without any opioid related deaths. To look at the calculation for this model and further design explanation, please refer to the [project’s notebook](https://github.com/sabpereira/ThinkStats2/blob/master/project1/project1.ipynb).

After calculating the AADRs, I performed a linear regression with the NCHS’s ALEs and the AADRs to create a linear model and check its goodness of fit. The coefficient of determination was .97, validating that by knowing the AADR, we can get a good estimate of the ALE. There was an outlier in the year 2003, but it did not seem to to affect the fit of the model substantially.

Graphed below are both the ALEs reported by the NCHS and the ones calculated using my regression model. This graph is another validation of my model, as it traces the true ALE very closely.

![](https://github.com/sabpereira/ThinkStats2/blob/master/project1/output_48_0.png)

Excluding the year 2003, my function for finding the Average Life Expectancy from the AADR produces a result accurate to within .15 years of the true ALE, so it is a decently good estimator of the life expectancy we would expect to see if there were no contributing opioid related deaths.

## **Results**

Below is the same graph produced above, overlaid with the Zero-Opioid Scenario ALE. In the earlier years, the ALE for a Zero-Opioid Scenario differs very little from the actual ALE. However, in the most recent years, the gap between the two is wider than it has ever been.

![](https://github.com/sabpereira/ThinkStats2/blob/master/project1/output_51_0.png)

In the graph, we can see in the year 2003 the ALE we would expect to see if there had been no opioid related deaths according to our model is lower than the actual ALE, which is a senseless result. The linear regression that created the model had an outlier in the year 2003, so it explains why our model does not work well in this result.

## **Conclusion**

So, _**what is the effect of the increased opioid-related deaths on the Average Life Expectancy in the US?**_

According to the model, I would expect that the ALE in 2017 would have been about .46 years higher if there had been no opioid-related deaths (79.06 years, compared to the observed 78.6 years). Similarly, in 2016 the ALE would have been .37 years higher in a Zero-Opioid Scenario (79.07 years compared to the observed 78.7).

It is only recently that these deaths have created an observable effect this large. In 1999, the difference between the Zero-Opioid ALE and the observed ALE was .16 years (76.86 years compared to the actual 76.7).

The Average Life Expectancy is a very robust summary statistic that takes information about the overall health of a country to produce one number. The increased number of opioid overdoses taking lives prematurely has more than ever negatively impacted the years of life a newborn would be expected to live.
