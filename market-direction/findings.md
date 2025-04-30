# Aggregate Sentiment as a Predictor of Market Movements

## Goal
Determine if aggregate sentiment from stock related tweets can explain or predict market directions or returns, as measured by SPY.


## Methodology

### 1. Aggregate Sentiment Calculation
Noisy, ticker-level tweet sentiment was transformed into a single daily market sentiment signal.

Each tweet corresponds to an individual stock and holds three separate sentiment scores: positive, negative, and neutral.

A scalar sentiment value was computed per tweet:
$$
\text{net-sentiment}_i = \text{positive}_i - \text{negative}_i
$$

Tweets were then grouped by date, and the mean sentiment score per day was computed:
$$
\text{sentiment}_t = \frac{1}{N_t} \sum_{i=1}^{N_t}  \text{net-sentiment}_i
$$
where $N_t$ is the number of tweets on day $t$.

Finally, the sentiment measurement was smoothed to explore the persistence of sentiment and reduce volatility.
This was done by computing rolling averages of daily sentiment over 3 and 5 days. These rolling versions will be tested as alternative predictors.

Example: $$\text{sentiment}_{t}^{(3)} = \frac{1}{3} (\text{sentiment}_{t} + \text{sentiment}_{t-1} + \text{sentiment}_{t-2})$$

### 2. Market Return Target
1. Using SPY close prices:
$$
\text{return}_t = \frac{\text{close}_t - \text{close}_{t-1}}{\text{close}_{t-1}}
$$

2. Directional:
$$
y_t = 
\begin{cases}
1 & \text{if } \text{return}_t > 0 \\
0 & \text{otherwise}
\end{cases}
$$

The first metric is used to test for predicting market return, and then second metric is used to test for predicting market direction.

### 3. Analysis
#### 3.1 Correlation Analysis
Computed Pearson correlation between $\text{sentiment}_{t}^{(k)}$ for $k \in \{1, 3, 5\}$

This tested the strength of linear association between sentiment and market movement.

#### 3.2 Linear Regression
Modelled SPY return as a function of sentiment:
$$
\text{return}_{t} = \alpha + \beta \cdot \text{sentiment}_{t} + \epsilon_t
$$

This model was ran on each sentiment window (1-day, 3-day, 5-day), and the $\beta\$ and p-values were analyzed.

#### 3.3 Logistic Regression
Modelled probability of an upward movement in SPY:
$$
P(y_t = 1) = \frac{1}{1 + e^{-(\alpha + \beta \cdot \text{sentiment}_t)}}
$$

Again, ran on each sentiment window.

The $\beta$, classification accuracy, and ROC curve / AUC were evaluated.


## Key Findings