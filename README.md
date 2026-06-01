# Bitcoin Sentiment × Trader Behaviour Analysis
### Hiring Assignment — PrimeTrade.ai | Data Science Role

---

## About This Project

This project explores the relationship between the Bitcoin Fear & Greed Index and real trader behaviour on Hyperliquid, a decentralised perpetual exchange.

The goal is not just to describe the data, but to find patterns that are actually useful — things like whether traders make better decisions in greed periods vs fear periods, whether high leverage consistently hurts performance, and how different trader archetypes behave under different market conditions.

I tried to keep the analysis grounded and honest — the findings are based on what the numbers actually show, not what I wished they showed.

---

## Methodology

To ensure robust and reliable conclusions, the analysis followed a rigorous workflow:
1. **Data Cleaning**: Handled missing values, standardized formats, and removed anomalous zero-dollar trades.
2. **Timestamp Alignment**: Parsed IST timestamps and converted them to UTC to align precisely with sentiment index dates.
3. **Dataset Merging**: Combined Hyperliquid trade history with daily Fear & Greed sentiment scores on trade execution dates.
4. **EDA (Exploratory Data Analysis)**: Evaluated profitability across sentiment regimes, assessed the impact of leverage, and compared asset-specific performance.
5. **Statistical Analysis**: Applied Kruskal-Wallis and Spearman correlation tests to validate observed patterns beyond random chance.
6. **Trader Clustering**: Utilized K-Means clustering to segment the 32 trader accounts into distinct behavioral archetypes based on risk and performance metrics.
7. **Business Recommendations**: Translated data insights into actionable product and risk-management features for PrimeTrade.ai.



## Datasets

**1. Bitcoin Fear & Greed Index** (`data/fear_greed_index.csv`)
- 2,644 daily sentiment readings from February 2018 to mid-2025
- Each row has a date, a score (0–100), and a label (Extreme Fear, Fear, Neutral, Greed, Extreme Greed)
- Source: Alternative.me Fear & Greed API

**2. Hyperliquid Trade History** (`data/historical_data.csv`)
- 211,224 individual trades from 32 unique trader wallets
- Covers roughly April 2023 to June 2025
- Includes trade side (BUY/SELL), size in USD, direction (open/close long/short), realised PnL, and fees

---

## Project Structure

```
primetrade-sentiment-analysis/
├── data/                                      ← raw datasets (excluded via .gitignore)
├── notebook/
│   └── primetrade_sentiment_analysis.ipynb    ← main notebook (run this)
├── outputs/
│   └── executive_summary.pdf                  ← business recommendations
├── .gitignore
├── README.md
└── requirements.txt
```
*(Note: Raw datasets are excluded from this submission to maintain a clean repository structure, but the notebook is fully documented for reproducibility.)*

---

## How to Run

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Open the notebook
python -m jupyter notebook notebook/primetrade_sentiment_analysis.ipynb
```

The notebook is self-contained. Run cells top to bottom.

---

## Key Questions Explored

1. Do traders make more money during fear or greed periods?
2. Does higher leverage lead to better or worse outcomes?
3. Are BUY trades more profitable than SELL trades?
4. Which assets have the best and worst track records?
5. Can we group traders into meaningful behaviour clusters?
6. What should PrimeTrade.ai do differently based on these findings?

---

## Summary of Findings

*(Full analysis with supporting charts in the notebook)*

- **Win rate** across all closing trades was around 82% — but this is skewed by a small group of very active, consistently profitable traders.
- **Leverage**: Medium leverage (roughly 3–8x) tends to show better average PnL than very high leverage, which produces more volatile outcomes. The correlation between leverage and PnL is weak.
- **Sentiment**: Sentiment regime is statistically associated with differences in PnL distribution. Fear periods have wider outcome distributions; greed periods are more consistent.
- **BUY vs SELL**: On this dataset, BUY side trades edged out SELL side trades in median PnL, though the difference is modest.
- **HYPE token** dominates both volume and absolute PnL on this platform, creating concentration risk.
- **Trader Heterogeneity**: K-Means clustering identified 2 distinct trading styles. About two-thirds of traders are net profitable, but a few drive most of the aggregate PnL.

---

## Recommendations for PrimeTrade.ai

1. **Sentiment-Triggered Trading Prompts**: Consider displaying risk warnings for high-leverage entries when sentiment is complacent or extreme.
2. **Leverage Defaults Tied to Sentiment**: Automatically reduce default pre-filled leverage when sentiment is at Extreme Fear or Extreme Greed.
3. **Behavioural Alerts for At-Risk Traders**: Detect loss-chasing behaviour (e.g., 3+ consecutive losses plus increased position size) and prompt traders to take a break.
4. **Trader Segmentation for Product Personalisation**: Retrain segmentation models periodically to personalise default settings, fee structures, and educational content.
5. **Symbol Concentration Monitoring**: Track platform-wide concentration of dominant assets (like HYPE) to monitor systemic risk.
6. **Performance Dashboard with Risk-Adjusted Metrics**: Surface genuinely skilled traders by showing profit factor alongside total PnL leaderboards.

---

## Limitations

- Only 32 trader accounts — too small for strong statistical generalisations
- The Fear & Greed Index is BTC-specific, but most trades here include altcoins
- Leverage is approximated from position size and start position — not directly logged
- The analysis period is mostly bullish — results could differ in a bear market

---

*Built as part of a data science hiring assignment. All analysis is original.*
