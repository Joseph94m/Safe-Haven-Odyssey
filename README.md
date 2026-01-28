# Safe Haven: The Mathematics of Tail Risk Hedging

**Companion code for the Medium article: [PLACEHOLDER - Link will be added upon publication]**

---

## Overview

This repository contains the Jupyter notebook and analysis behind my exploration of **tail risk hedging** and the **safe haven** investment strategy as described by Mark Spitznagel in his book [Safe Haven](https://www.amazon.com/Safe-Haven-Investing-Financial-Storms/dp/1119401798/ref=sr_1_2?crid=2QO0ZQ2MI73P0&dib=eyJ2IjoiMSJ9.Dpy61VhZJB56n6ZJknGNP80GtAukpI7QZrD02V_hA8ryZImRfuvt9Te-SQf4ZQHk97FEbcvxU2HU6tm79tDKp067yyDkPSkGoqhfY3jB5EzJyzQpif3-TFz7T4PmPuItgU_ZLnno3TJx6otQH1iLEMbNDz37i2hYzv1TyPypB3mzUWSHg381R_tp2w1U37W53fXDREqxENqfD-8MbJk3vdGBTy-CGywT7GGQmFYKoK4.mN0ZN1SicJO_WbNTVtWgdI7kwqHz_mpnlK-H4w29G1k&dib_tag=se&keywords=safe+haven&qid=1769579773&sprefix=safe+hav%2Caps%2C276&sr=8-2). The core question: *Can a small allocation to "insurance" against market crashes actually improve long-term returns, not just reduce risk?*

The answer, backed by 98 years of S&P 500 data and 10,000 Monte Carlo simulations, is a resounding **yes**.

## The Problem: Fat Left Tails Destroy Compounding

Markets don't follow normal distributions. The left tail, i.e. catastrophic years where the S&P 500 drops 20%, 30%, or even 40% has a disproportionate impact on returns.

A 50% loss requires a 100% gain to recover. This asymmetry means that avoiding the worst years matters more than capturing the best years for longterm wealth accumulation.

By the way, the historical returns do not actually reflect the real statistical properties of returns: the tail is likely fatter than what we have seen, we just need to wait longer.

## The Strategy

The notebook explores a simple insurance mechanism:
- **98%** of the portfolio in S&P 500 (passive exposure)
- **2%** allocated to "crash insurance" (e.g., deep OTM puts)
- If the market drops **≥15%**, the insurance pays **15x** (turning 2% into 30%)
- If the market doesn't crash, the 2% is lost (cost of insurance)
- Finally, we perform a grid paramter search over multiple thresholds and payment multiplers.

## Key Findings

From 10,000 bootstrap simulations over 25 year horizons:

| Metric | Uninsured | Insured |
|--------|-----------|---------|
| Median Final Wealth | Lower | **Higher** |
| 5th Percentile (Worst Cases) | Much Lower | **Significantly Better** |
| Probability of Outperformance | - | ~60% of trials |

The insured portfolio doesn't just reduce risk, it often **increases terminal wealth** by avoiding the devastating drawdowns that cripple compounding.


## Running the Notebook

### Requirements
`jupyter notebook installed`

 `numpy, matplotlib, scipy, seaborn`


### Quick Start
```bash
jupyter notebook Safe-Haven-Medium.ipynb
```

The notebook is self-contained with:
- Historical S&P 500 data (1928-2025)
- Distribution analysis with left tail visualization
- Bootstrap Monte Carlo simulation engine
- Side-by-side comparison of hedged vs. unhedged portfolios

## Visualizations

The notebook generates:
1. **Return Distribution Plot**: Histogram + KDE showing the fat left tail
2. **Monte Carlo Fan Charts**: 10,000 wealth trajectories with percentile bands
3. **Comparative Analysis**: Insured vs. uninsured portfolio outcomes

## The Math Behind It

The insurance payoff structure:

```
If S&P return < -15%:
    Portfolio return = 0.98 × SPX_return + 0.02 × 15 = 0.98 × SPX_return + 0.30
Else:
    Portfolio return = 0.98 × SPX_return - 0.02
```

This creates **convex payoff** in the left tail—exactly when you need it most.

## Further Reading

- **Medium Article**: [PLACEHOLDER - Coming Soon]
- Spitznagel, M. - *Safe Haven: Investing for Financial Storms*
- Taleb, N.N. - *Antifragile* & *The Black Swan*

## License

MIT License - Feel free to use, modify, and build upon this work.

## Author

For business: joseph.moukarzel@jmclarity.com  
Personal: moukarzeljoseph@gmail.com

---

