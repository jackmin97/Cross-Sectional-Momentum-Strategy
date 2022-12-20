# Cross-Sectional-Momentum-Strategy
Cross sectional momentum is trend based investment strategy, where you can choose top 'n' percentile to go long and bottom 'n' percentile to go short from the universe of assets.


### 1. Read price and volume data
We will read a condensed data file called the pickle file. The pickle file contains the price and volume data of the S&P 500 constituents.

### 2. Filter the stocks
The assets are filtered on the basis of turnover. The following steps are performed:

1. Multiply price and volume over n periods
2. Take an average or mean of the above product to get average dollar volume
3. Average dollar volume or average daily turnover (defined as number of shares traded to the number of shares outstanding) are used to predict the magnitude and the persistence of future price momentum
4. Momentum is stronger among high average turnover or average dollar volume stocks

The value of n is taken as 90.

### 3. Cross sectional momentum strategy
We backtest the strategies tweaking the parameters in 3 ways:

1. Long short: Consider a 180 day lookback period over which we measure the asset's past performance or rank the relative performance, and 41 day holding period with generated trading signals
2. Long short with skip period: For the above strategy we add 5 skip_days between the lookback and the holding periods, to safeguard against any microstructure effects (bid-ask spread, lead-lag effect, short-term price pressure) affecting the inference
3. Long only: Only long trading signals are generated for top 20 percentile with above-used lookback, holding and skip periods

#### 3.1 Long-short cross-sectional momentum strategy
Long trading signals are generated for top 10 percentile and short signals for bottom 10 percentile with
a. Lookback days = 180
b. Holding days = 41

These values are for illustration and can be changed.

Strategy logic:

1. Calculate the stock returns over the lookback period and holding period
2. Rank the stock returns based on the lookback returns
3. Long stocks with highest 10 percentile lookback retuns and short stocks with lowest 10 percentile lookback returns
4. Include trading cost
5. Calculate the strategy returns

The transaction cost is taken as 0.1%.

#### 3.2 Long-short cross-sectional momentum strategy with skip-days
Long trading signals are generated for top 10 percentile and short signals for bottom 10 percentile with: 
a. Lookback days = 175
b. Skip days = 5
c. Holding days = 41

Strategy logic:

1. Calculate the stock returns over the lookback period by skipping 1 week (to avoid short term price reversal) and holding period.
2. Rank the stock returns based on the lookback returns
3. Long stocks with highest 10 percentile lookback retuns and short stocks with lowest 10 percentile lookback returns
4. Include transation cost
5. Calculate the strategy returns

The transaction cost is taken as 0.1%.

#### 3.3 Long-only cross-sectional momentum strategy
Long only strategy on top 20 percentile stocks with:
a. Lookback days = 175
b. Skip days = 5
c. Holding days = 41

Strategy logic:

1. Calculate the stock returns over the lookback period by skipping 1 week (to avoid short term price reversal) and holding period.
2. Rank the stock returns based on the lookback returns
3. Long stocks with highest 20 percentile lookback retuns
4. Include trading cost
5. Calculate the strategy returns

The transaction cost is taken as 0.1%


We can see that strategy generated better returns when we introduced the skip period.

Long-only momentum strategy performed even better than the long-short momentum strategy with skip days, but the long-only strategy is slightly risky because it is exposed to market risks.
