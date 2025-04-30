# Volatility and Tweet Volume Correlation Analysis

## Goal
Determine whether there is a statistically significant correlation between tweet volume and daily volatility of high watched stocks.

## Methodology
1. Tweets were grouped by ticker and date to count daily tweet volume.

2. For each stock, intraday volatility was computed as
$
Volatility = \frac{High - Low}{Open}
$

3. Statistical Analysis:
    - Pearson correlation coefficient $r$ and p-value $p$ were calculated between tweet volume and same-day volatility.
    - A secondary test was done for tweet column compared to next-week volatility (lagged correlation test)

$
r = \frac{\sum_{i=1}^{n} (x_i - \bar{x}) (y_i - \bar{y})}{\sqrt{\sum_{i=1}^{n} (x_i - \bar{x})^2} \cdot \sqrt{\sum_{i=1}^{n} (y_i - \bar{y})^2}}
$


$
p = 2 \cdot (1 - t.cdf(|r \cdot \sqrt{\frac{n-2}{1- r^2}}|, df = n-2))
$


## Key Findings

### 1. Evidence of Moderate Correlation for Some Stocks
Several stocks show a moderate, statistically significant positive correlation between tweet count and volatility:

|Ticker|r-value|p-value|Sample Days|
|-|-|-|-|
|NFLX|0.38|< 0.0001|228|
|TSLA|0.36|< 0.0001|252|
|NOC|0.46|0.024|24|



While most correlations are weak to moderate, many are statistically significant due to large sample sizes.

- TSLA and NFLX stand out as stocks where tweet column relably reflect or conincides with high volatililty
- Public attention seems to track media-driven or speculative movement in popular tech stocks

### 2. Lagged Correlation Observations
In addition to same-day correlation, a test was done to see whether tweet volume might precede changes in volatility by examining correlation between tweet count on day $t$ and volatility on day $t+7$.

For most stocks, the lagged correlation was similar in magnitude to the same-day correlation.

In general, the similarity suggests that tweet volume is more concurrent with market volatility than it is predictive.

## Conclusion
While tweet volume and volatility clearly move together for some stocks, there is little evidence that tweet volume leads volatililty in a statistically strong way than it simply reflects it.