# Correlation Matrix Denoising using RMT (MP Law)
Empirical study of S&P 500 correlation structure across market regimes using RMT (random matrix theory) and then denoising via Marchenko-Pastur law. Adding to it rolling stress detection, and comapring against other methods (Sample, constant correlation, Ledoit-Wolf) by training on sample regime and post sample method validation

## results(on post sample analysis)

| Method       | Ann Vol | Max DD  |
|--------------|---------|---------|
| Sample       | 15.8%   | -33.3%  |
| Ledoit-Wolf  | 15.8%   | -33.2%  |
| Const Corr   | 15.2%   | -29.9%  |
| RMT Denoised | 15.7%   | -33.1%  |

- these are shown on the plot comparing the 4 methods as well

## methods:

- Data: S&P 500 daily returns 2005-2024 (~450 stocks)
- Marchenko-Pastur (MP) law to identify noisy eigenvalues
- KL divergence fitting to calibrate σ²
- Eigenvalue clipping and matrix reconstruction
- Compared against: sample covariance, Ledoit-Wolf, constant correlation
- Split time into 3 regimes, namely the GFC (global financial crisis), Normal and COVID time

## plots to show results

- MP law vs EV 
- Raw vs Denoised heatmaps 
- EV loadings across all 3 regimes (top 40 stocks)
- rolling lambda_max vs VIX 2005-2024
- Signal dimensionality over time
- Portfolio cumulative returns and drawdown

## requirements:
numpy, pandas, scipy, sklearn, yfinance, matplotlib

## running it locally
1. Clone the repo
2. pip install -r requirements.txt
3. Run notebook.ipynb top to bottom
   (cell 2 downloads data on first run, 
    cell 12 uses cache after first run)

## Limitations

- 60-day rolling window means q=1.2, limiting signal detection
- σ² is refitted every 20 trading days rather than daily, may lag during fast moving crises like COVID / GFC
- No transaction costs in portfolio evaluation
- Survivorship bias in S&P 500 ticker list

### p.s run this on a venv (virtual enviroment), install libraries after launching venv