# Market Making Notes

Please create an issue or pull request to provide feedback or request for additional topics.

Credit me if you want to re-use this content.

---

# Basic Terminology

A particular trade is defined by:

1. The asset you want to trade
2. Whether you want to buy or sell that asset 
3. The quantity of the asset you want to buy or sell 
4. The price at which you want to buy or sell the asset at your specified quantity 

When you submit your request to trade in the market, these specifications define your open order.

When you are trading as a market maker, bidding is buying and asking is selling. 

When you place a request to trade in the market, i.e place an order, someone in the market can trade against your order by agreeing to take the opposite trade. The opposite trade is a trade in the opposite direction of you. This means that if you are buying, the opposite trade is selling and vice versa. When someone decides to trade against your order, they may decide to trade a portion of your specified quantity. For example, if you made an order to buy 1000 BTC at US$ 100,000, someone may decide to only sell to you 500 BTC at US$100,000. When this happens, then your order was partially filled, and your remaining open order is an order to buy 500 BTC at US$100,000. Once your entire open order has been fulfilled, then your order is closed and removed from the market’s order book.

The fundamental principle of trading is to buy low and sell high. But what is considered low and high? We use the expected value of the asset to determine its fair value, and depending if the price is below or above this expected value conclude if the price is “low” or “high”. 

One important thing to note is that when someone agrees to sell to you 500 BTC at US$100,000, you now have a long position of 500 BTC at US$100,000. Likewise, if someone decided to buy from you, i.e you placed a sell order and it was filled, then you would have a short position. Your collection of long and short positions are your open positions. Furthermore, the person trading against you takes the opposite position in the trade. This means that when you decided to buy BTC and someone sold it to you, you opened a long position while they opened a short position. Moreover, if you decided to sell BTC and someone bought it from you, you opened a short position while they opened a long position. 

This leads us to the idea of adverse selection. Adverse selection is the idea that your trades may be worse than they seem because someone decided to take the opposition position of your trade. We can determine if this is actually the case by assessing whether the person trading against you is an informed trader or a noise trader.

An informed trader is a person who may have better information than you regarding the expected value of the asset. If an informed trader decides to trade against you, then they must believe that they are buying or selling the asset from you at a good price, and so making an expected profit from you. In this case, your trades are bad trades and you need to change the price at which you are trading. 

A noise trader is someone who makes trading decisions that does not correlate with the expected value of the asset. For example, young investors may want to purchase some S&P500 at any price to build up their portfolio.

# Market Making

A market maker provides liquidity to the markets by placing bid and ask orders in the order book and waits for market participants to trade against them (hit your bid/lift ask offer). As a market maker, your bid defines at what price you are willing to purchase the asset, and your ask defines at what price you are willing to sell the asset. When someone hits your bid, you bought the asset and your inventory of the asset increases, and when someone lifts your ask, you sold the asset and your inventory of the asset decreases. Besides making quotes at the right price level, inventory management is crucial for a market maker to avoid excessive exposure (or risks) to the market. A market maker differs from the typical trader because a market maker gives up control over the size and timing their trades in exchange for spread and rebates. 

The general strategy for market making is

1. Determine the expected value of the asset and have a range of what is minimum and maximum possible value of the asset. 
2. If you are confident in the expected value, quote a tight spread and trade a lot. Otherwise, quote a wide spread and trade less frequently as you gather information about what the expected value of the asset is. 
3. Against informed trades, if they hit your bid, that means they believe they are selling to you at a high price, so you should lower your bid (and your ask if you are constrained to, say, a maximum spread of 5). If they lift your ask, that means they believe they are buying from you at a low price, so you should raise your ask (and your bid if you are constrained to, say, a maximum spread of 5). 
4. If you believe that the value of the asset is contained within [minPrice, maxPrice], you should never quote a bid above maxPrice and you should never quote an ask below minPrice. If you decide to bid above maxPrice, then you are buying high, and if you decide to ask below minPrice, you are selling low. 

The key to being a successful market maker is to determine whether the person trading against you is an informed or noise trader. 

## Bid and Ask Management

Adjusting your bid and ask can help you capture more profits, minimise losses, and manage your inventory. A general rule of thumb is to quote a wide spread during uncertain times and quote a tight spread during stable conditions.

### Asks

If someone lifts your ask, it tells you about buying demand for that asset. You should raise your ask if

1. You believe that the fair value of the asset is above your spread. 
2. You are underexposed, i.e lacking in inventory or net short, so by raising your ask people will purchase from you less and give you time to build up your inventory.
3. You observe large, aggressive purchases for the asset indicating that the price of the asset will likely increase. 

You should not raise your ask if you believe that the fair value of the asset is contained within your spread and is unlikely to move. Moreover, you might consider lowering your ask if you are overexposed, i.e have too much inventory of the asset or net long, so that more people will buy from you and you can sell more, letting you offload your risk. 

### Bids

If someone hits your bid, it tells you about selling demand for that asset. You should lower your bid if:

1. You believe that the fair value of the asset is below your spread. 
2. You are overexposed, so by lowering your bid less people will sell to you and you will be purchasing assets at a lower rate, giving you time to sell off excessive inventory. 
3. You observe large, aggressive sell orders for the asset indicating that the price of the asset will likely drop. 

You should not lower your ask if you believe that the fair value of the asset is contained within your spread and is unlikely to move. Moreover, you might consider raising your bid if you are underexposed so more people will sell to you and you can increase your inventory. 

In practice, to manage inventory, if you are underexposed it is better to raise your bid, and if you are overexposed it is better to lower your ask. This way, you can manage inventory without compromising trading volume. A side note: If you are overexposed you will lose money if prices fall, and if you are underexposed you will lose money if prices rise. 

One important takeaway is that your quotes reflect your estimate of the asset’s fair value, and your spread reflects your confidence in that estimate. Furthermore, the one of the goals of a market maker is to maintain a balance neutral position, i.e net balance of zero. This way, they are market neutral, meaning that they are not exposed to the risk of the asset price rising or falling.

On adverse selection, adverse selection normally occurs during high volatility. Some strategies to minimise losses against informed traders include:

1. Quoting a wide spread so ensure that the fair value of your asset is captured within your spread during high volatility 
2. Using real-time market data to dynamically adjust your spreads and minimise mispricing. 

## Notes from StackOverflow

Normally, when you are a market maker, the general strategy is to raise your quotes when someone lifts your ask, i.e someone is buying from you, and lower your quotes when someone hits your bid, i.e someone is selling to you. As a market maker, you job is to determine the true value of the asset by following the flow of informed traders. The real challenge is distinguishing informed trades from uninformed trades in the order book. Ideally, you should adjust your quotes based on 

$$
\frac{\sigma_{\text{informed}}}{\sigma_{\text{uninformed}}}
$$

As a market maker, if you have a range of the true value of the asset, do not place an ask below the minimum value or place a bid above the maximum value. If you lose money, let it be because of a poor estimate of the true value of the asset, not because of poor strategy (it is called scalping yourself). 

Your bid and ask levels reflect your estimate of the true value of the asset. Do not get tricked into focusing only on one side. You never know if the next trade will be a buy or a sell. Furthermore, as a market maker, you are in control. If someone wants to offload all of their inventory, show your bids at lower sizes than your ask, and keep decreasing your bid level if they continue to sell to you. 

As a market maker, partially closing your open positions at favourable prices is a good thing. You will make money this way. 

Some interview tips: Each time you change your quote, explain why. Otherwise, they might assume you are dumb. From an interview perspective, one of the goals may be to quickly recognise you were trading against a noise trader. 

### Case Study

Consider the following MM scenario:

Make a market on the sum of 3 cards. After each round, a card will be revealed. Suppose the interviewer knows the final answer. 

The expected value of 3 cards is 21, so you initially quote bid 20 and ask 22. Your interviewer reveals the first card to be 1 and buys from you. You have two choices. 

1. Either adjust your quotes to the new expected value of 15, and bid 14 and ask 16. 
2. Follow your interviewer’s buy and raise your quotes, say to bid 22 and ask 24. 

In deciding what to do, note that the less informed MM cannot make money trading against an informed trader. If the fair value is inside the spread, the informed trader would not trade. However, if the fair value is above the spread, the informed trader will buy, and if the fair value is below the spread, the informed trader will sell. When an informed trader trades with a market maker, they make an expected profit while giving away some information about the fair value, namely the direction of the fair value. The MM’s job is to assess whether the incoming trade is indeed coming from an informed trader or a noise trader. 

The response a MM should take depends on the situation. If you are only trading with one other person, the informed trader, then the best a MM can do is to avoid trading at all. Here, maximising gains is the same as minimising losses, and against an informed trader, it is via not trading at all by quoting a wide spread. By quoting a spread at or outside the minimum or maximum possible value of the asset, the MM avoids trading with the informed trader. However, if there are other market participants who are uninformed traders, then the MM may trade with the informed trader as a “fee” to determine what the fair value of the asset is. Here, the MM’s job is to trade as cheaply as possible with the informed traders to arrive at the fair value and profit from uninformed traders. 

With that, given that you are only trading with the interviewer, and your interviewer is an informed trader, the best decision you can make is to either quote a wide spread, say bid 3 and ask 13, or follow your interviewer’s trades and raise your quotes to minimise losses. If instead you were trading with an uninformed trader, then lower your quotes and follow the new expected value of the cards. This decision is solely based on whether if you are trading against an informed or uninformed trader. 

Note: Knowing the expected value of the asset does not justify a tight spread unless you must provide a N% confidence interval. Furthermore, for this particular game, you must stay flat, i.e balance neutral, as you will close your positions at the true value. 

Interview Tip: In an interview, your reasoning is more important than winning. Explain your thought process as you decide to adjust your quotes. Otherwise, the interviewer might think you are dumb. 

Remember, if you are overexposed, you might lower your quotes so more people will buy from you. If you are underexposed, you might raise your quotes so more people will sell to you. Maintaining a neutral position is also important. For example, is you sell at US$47.5 and close at US$45, you still made a profit of US$2.5 and remain risk-free from being inventory neutral.

Further Note: In some games, if may not matter if you go bankrupt in the last round. In these games, in the last round, go all in.

# Cryptocurrency Concepts

## Perpetual Futures

Perpetual futures are a type of derivative that allows one to speculate on the price of the underlying without an expiry date. It is similar to the typical forward contract except that there is no expiry and the settlement price is constantly being influenced by the funding rate. The funding rate is a mechanism that ensures that the price of perpetual futures do not deviate from the price of the underlying. The funding rate works by establishing periodic payments between buyers and sellers of the perpetual future contract. If the funding rate is positive, then the price of the contract is greater than the price of the underlying and it is more beneficial to own the contract than the underlying. The contract is in contango and buyers pay sellers of the contract. If the funding rate is negative, then the price of the contract is less than the underlying and it is more beneficial to own the underlying than the contract. The contract is in backwardation and sellers pay buyers of the contract. In this way, the funding rate incentives traders to take the positions such that the price of the futures contract stays close with the price of the underlying. The exact formula for the funding rate depends on the exchange, but it generally depends on the premium index, which is the price of the contract - price of the underlying, and the interest rate which reflects the cost of borrowing or lending the underlying. 

You can speculate using perpetual futures. If you expect the price of BTC to rise, long the contract to purchase BTC at a cheaper price and sell for a higher price later. If you expect BTC to fall, short the contract to sell BTC at a higher price at a future date and long BTC when the price falls.

You can use perpetual futures to protect your positions against potential losses. For example, if you have 100 BTC, you might consider shorting 100 BTC perpetual futures to guarantee a level of profit in case the price of BTC falls. Furthermore, if you are short 100 BTC, you might consider hedging via longing 100 BTC perpetual futures to guarantee purchasing BTC at a particular price level, limiting your losses, in case the price of BTC rises.  

You can arbitrage when the price of the contract deviates from the underlying. This is because the price for immediate delivery (underlying) is different from the price of unspecified future delivery (contract). If the situation is contango, long the underlying and short the contract. If the situation is backwardation, long the contract and short the underlying. 

Volume of a market is defined as the amount of assets traded over a particular time interval. Open interest is defined is the amount of active contracts that has not been exercised. 

Slippage is the difference between the expected price at which a trade is executed and the actual price a trade is executed. 

Liquidity is defined as how easy it is to buy or sell an asset without moving the price of the asset in the market. High liquidity is reflected by a tight spread, while low liquidity is reflected by a wide spread. 

Market depth is defined by many different price levels are available for trading and how much volume each price level can support. Order book levels that are deep can take large orders without much price swings. Otherwise, the order book is shallow and susceptible to large price swings. 

Turnover Ratio: Total trading volume divided by market cap

Option Greeks:

- Delta is defined as the rate of change of the price of an option due to small changes in the price of the underlying .
- Gamma is defined as the second rate of change of the price of an option due to small changes in the price of the underlying.
- Theta is defined as the rate of change of the price of an option due to small changes in the time to maturity of the option.
- Vega is defined as the rate of change of the price of an option due to small changes in the implied volatility of the option. Implied volatility is the future expectation of the contract’s volatility.
- Rho is defined as the rate of change of the price of an option due to small changes in the interest rate.

# Notes from Other Sources

People trade assets at different prices and sizes. The value of an asset varies over time, which allows us to trade and capture profit over time. In this sense, volatility of an asset is a source of opportunity when we have a signal on the future price of the asset, or a source of risk if we do not have a signal on the future price of the asset. 

When you purchase 1 BTC at US$50,000, you have a long open position worth US$50,000. If the price of BTC is US$51,000, you have a profit of US$1,000, even if you have not realised it. Your risk is correlated with the size and direction of your open position. 

Profit and loss can be calculated via

$$
\text{PnL} = q(m - p) = qp\left(\frac{m}{p} - 1\right)

$$

Here, q is the quantity traded, m is the market price, and p is the price at which you traded. So, qp denotes the notional amount of your open position, and m/p the return on your trade. The expression on the RHS is preferred because it is normalised, i.e provides good comparisons across different assets. 

We can also calculate cumulative profit and loss via

$$
\text{Cumulative PnL} = \sum q_i m - \sum q_i p_i
$$

We arrive at the expression by applying summation on the expression for profit and loss. Here, the first summation represents the open position, and the second summation total invested capital. Note that quantity is positive for buys and negative for sells. One important fact to consider is that if the sum of your positions is zero, i.e balance neutral, then it does not matter what the current market price of the asset is. 

Risk is a subjective measure, hence why we have the notion of risk aversion of an individual. We define risk as the uneasiness from holding a sizeable unwanted position in a volatile asset instead of cash. The term volatile comes from the fact that the value of the asset varies over time. If it did not, it would be as good as cash, and the word unwanted is because we do not have a signal on the future price of the asset. Because we do not have a signal, we do not have a reason to hold the asset. Instead, because it is volatile, we have reasons not to hold it. The uneasiness comes from our open positions. The more sizeable the open positions, the greater the risk. It does not matter how the open positions came about. What matters is that it exists, its size and its direction.

Risk aversion is a subjective measure of ho much risk a person can tolerate. There are two types of risks:

1. Local risks, which is the sensitivity of the portfolio’s value due to small changes in the price of the underlying. One way to alleviate this is to choose a gamma neutral portfolio where its delta is close enough to zero. It is important to note that local risk models tend to break down.
2. Tail risk or Value at Risk. This can be thought as systematic risk, or risk that affects the whole market. To accurately capture how exposed is the portfolio to tail risk, it is important to do scenario analysis to capture deviations from conventional assumptions. 

We can formulate a formula for local risk as

$$
\text{Local Risk} = P \cdot \sigma
$$

Where P is the USD value of open positions and sigma is the volatility of the asset. We can re-express profit and loss as

$$
\text{PnL} = P \cdot r = P \cdot \sigma \cdot \frac{r}{\sigma}, \quad \text{where } Y = \frac{r}{\sigma}
$$

Y is the volatility adjusted returns and can be modelled as a normal distribution. Volatility can be defined as the squared-root of the variance of asset returns. A fundamental assumption in quantitative research is that prices are independent and identically distributed for non-overlapping time periods. Furthermore, it is not strictly a martingale, i.e a portion of price can be predicted. Refresher: A martingale is a stochastic process where the expected value of the next observation strictly depends on the current observation, implying no predictable trend or bias. 

Systematic trading is a three step process:

1. Collect the data
2. Feed the data to a trading model and let the model make a decision
3. Execute the trade based on the model’s decision

A model is a formula which consumes historical data and a set of parameters and returns a set of outputs. A model is evaluated based on its ability to make money net of transaction costs and adverse selection. Another consideration is capital consumption, i.e the returns and size of the trades the model can run. All things equal, we prefer models that produce the same returns using less capital and those that can be scaled with larger size. 

To gain extra assurance of the model’s performance, we backtest the model. A fundamentally driven model, i.e from arbitrage or human behaviour, is likely to last longer than a data driven model because backtesting assumes some variables remain the constant. During backtesting, you give the model historical data and see what the model does, and evaluate whether it is doing the right thing. During backtesting, the utility model to optimise is:

$$
U = \text{PnL} - \text{cost} - y \cdot \text{risk}, \quad \text{where } y \text{ is risk aversion.}
$$

Here, risk is a convex function so U will be a concave function. Its concavity will depend on y. If y is greater then 0, then U will be concave. If y is 0, there is no concavity or convexity. If y is less than 0, U is convex. The size of y will determine the size of the portfolio and the optimal size if linear with y. For example, if y is large, the model will not let the size grow too large otherwise the negative coefficient will penalise U.

Note that the model will optimise the expected value of the utility function based on historical data. So a fundamental assumption is that the markets are not weak-form efficient, i.e you can make abnormal profits by relying on historical data. 

When placing orders in the market, we always run the risk of adverse selection. Future price prediction is an important component to mitigate against adverse selection so we can evaluate the bids and asks we are getting filled on.
