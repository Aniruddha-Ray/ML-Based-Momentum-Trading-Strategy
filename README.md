# Machine Learning–Based Long-Only Momentum Trading Strategy (2015–2025)
Asset Universe: NIFTY Large-Cap Stocks (10) 
Author: Aniruddha Ray 
Data Period: 2015–2025
# Problem Statement & Objective
The objective of this study is to design and back-test a machine learning-based long-only momentum trading strategy that predicts the probability of a positive next-week return for a fixed universe of Indian large-cap stocks. The strategy converts model predictions into a systematic weekly portfolio, selecting the top-ranked stocks and holding them for one week under realistic transaction cost assumptions. 
The solution must: 
● Long-only 
● Weekly horizon 
● Equal-weighted 
● Fully rule-based Data description & Assumptions:
                  ●Daily OHLCV data 
                  ● 10 specified stocks 
                  ● Time period: 2015-2025 
                  ● Weekly sampling on Fridays for rebalancing before next weekday to avoid lookahead bias 
Weekly observations are constructed by selecting the last trading day of each week, ensuring alignment between features and the next-week return target.
# FEATURE ENGINEERING & MODELING Feature Engineering: 
## Momentum & Trend Features: 
Momentum is captured using multi-horizon return features (5-day, 20-day, and 60-day returns), along with normalized distance from moving averages. These features reflect both short-term and medium-term trend persistence. Volatility Features: Rolling return volatility and True Range are used to capture regime-dependent risk and price dispersion, which influence momentum reliability. Volume-Based Features: Volume change and volume-to-average ratios are included to identify participation-driven price movements, helping distinguish strong trends from low-conviction moves. Technical Indicators: RSI, MACD, and ADX indicators are incorporated to capture momentum strength, trend direction, and trend quality. Target Variable Construction: The prediction target is defined as a binary indicator of whether the next-week return is positive. This framing aligns directly with the portfolio’s weekly rebalancing horizon.
### Features:
5_day _ret 20_ day _ret 60_ day _ret dma_ 20 roll_ std_ 10 roll_ std_ 20 ATR vol_cha nge_5 vol_r atio RSI _14 macd_histo gram adx_14
# MODEL & BACKTEST DESIGN Model Architecture 
A Voting Classifier is used to estimate the probability of a positive next-week return for each stock. An ensemble-based approach is chosen to improve robustness by combining multiple base learners, thereby reducing model-specific bias and sensitivity to market regimes. Rather than generating binary buy/sell signals, the model produces probabilistic outputs , which are more suitable for portfolio construction. These probabilities are used to rank stocks cross-sectionally each week, allowing the strategy to select assets with the highest relative conviction. The ranking-based framework ensures that portfolio decisions depend on the relative strength of signals across stocks, making the strategy less sensitive to absolute probability calibration and more stable over time. Training & Validation Methodology The dataset is divided chronologically to prevent lookahead bias. The model is trained and validated exclusively on data from January 2015 to December 2022 , during which all feature engineering, model selection, and strategy design decisions are made.
The period from January 2023 to December 2025 is reserved strictly for out-of-sample evaluation and is not used in any form during model development. Weekly observations are constructed using only information available up to the decision date, with the target defined as the sign of the next-week return. This time-consistent training and evaluation framework ensures that the reported results reflect genuine out-of-sample performance. 
## Portfolio Construction Logic 
1. Weekly probabilities predicted for each stock
2. Stocks ranked cross-sectionally
3. Top 2 selected
4. Equal weights (50% each)
5. One-week holding period
6. Weekly rebalancing Transaction costs of 10 basis points per side are applied on both entry and exit to ensure realistic performance estimation.

# PERFORMANCE RESULTS Performance Matrices Equity Curve(Cumulative return)
The cumulative return profile exhibits steady growth with periodic but controlled drawdowns, as reflected by a moderate maximum drawdown, indicating a balanced risk–return trade-off typical of momentum-based strategies. 
## SCORES BEFORE TRANSACTION COST & AFTER TRANSACTION COST 
1. Annualized Sharpe (Jan 2023 – Dec 2025) 1.8467077018205231 || 1.3119917037494606 
2. Cumulative Return (Jan 2023 – Dec 2025) 1.059181497246915 || 0.6841441281105385 
3. Max Drawdown (Jan 2023 – Dec 2025) -0.15450678209188884 || -0.17135815634204932 
4. Mean Monthly Return (Jan 2023 – Dec 2025) 0.02134505500242613 || 0.015650080524847326 
5. Standard Deviation of Monthly Returns (Jan 2023 – Dec 2025) 0.0473137524372272 || 0.0469045869380736 
6. Weeks traded 147
# INSIGHTS, LIMITATIONS & CONCLUSION 
## Key Insights 
● Probability-based ranking outperforms binary signals 
● Volume-confirmed momentum improves stability 
● Transaction costs reduce returns but do not eliminate edge
## Limitations & Future Work Limitations: 
● Limited asset universe 
● No short exposure 
● Weekly granularity only 
● Potential regime sensitivity 
## Future Extensions: 
● Dynamic position sizing 
● Risk-parity weights 
● Regime detection 
# Conclusion 
This study shows that a machine learning–based momentum framework, when paired with a clear portfolio construction process and realistic transaction cost assumptions, can generate stable out-of-sample performance in Indian equities. By using probabilistic predictions and a disciplined weekly rebalancing strategy, the approach translates model signals into actionable and systematic investment decisions. The results highlight the importance of combining predictive modeling with robust trading rules rather than relying on model accuracy alone.
