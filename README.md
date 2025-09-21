# Bitcoin Price Behavior Analysis
This repository contains a Jupyter Notebook that conducts a detailed analysis of the daily price behavior of Bitcoin (BTC-USD). The analysis explores its statistical properties, volatility patterns, and correlations with other major financial assets, including the S&P 500 ETF (SPY), a Gold ETF (GLD), and the US Dollar Index (DX-Y.NYB).


## Data and Methodology
- **Data Source:** All historical daily price data was downloaded from Yahoo Finance using the yfinance Python library.

- **Metrics:** The primary metric for analysis is the daily percentage return, calculated from the adjusted closing prices.

- **Analysis Period:** The data spans from the earliest available date for all tickers from October 1, 2014 to July 30, 2025.


## Analysis and Key Findings
The notebook is structured to investigate several stylized facts of financial time series data as they apply to Bitcoin.

  **1. Summary Statistics**
  - **High Volatility:** Bitcoin exhibits a much higher standard deviation (volatility) of daily returns (4.26%) compared to SPY (1.13%), GLD (0.92%), and the Dollar Index (0.44%).

  - **Higher Returns:** Correspondingly, its mean daily return (0.30%) is significantly higher than that of the other assets.

  - **Fat Tails:** The kurtosis for Bitcoin returns is 6.55, which is much higher than a normal distribution (3). This indicates a higher probability of extreme price movements (i.e., "fat tails").

  **2. Autocorrelation and Volatility Clustering**
  - As is common with financial assets, Bitcoin's daily returns show no significant autocorrelation, aligning with weak-form market efficiency.

  - However, the absolute (or squared) returns show significant and persistent autocorrelation. This is a clear sign of volatility clustering, where large price changes are often followed by more large changes, and small changes are followed by more small changes. This pattern is visualized in the time series and ACF plots.


  **3. Mean Equation Modeling (OLS)**
  - An Ordinary Least Squares (OLS) regression was performed to determine if Bitcoin's daily return could be predicted by the previous day's returns of itself and the other assets.

  - **Result:** The model had a near-zero R-squared value (0.001), and none of the lagged returns were statistically significant predictors. This confirms that past returns do not reliably predict future returns.


  **4. Volatility Modeling (GARCH)**
  - To model the observed volatility clustering, GARCH(1,1) and GJR-GARCH(1,1) models were fitted to Bitcoin's returns.

  - **Result:** The models successfully captured the volatility dynamics. The sum of the ARCH (alpha) and GARCH (beta) parameters was close to 1, indicating that volatility shocks are highly persistent. The leverage effect term (gamma) in the GJR-GARCH model was not statistically significant, suggesting that negative and positive shocks have a symmetric impact on Bitcoin's volatility.


  **5. Correlation Analysis**
  - The analysis explored both static and dynamic correlations between the assets.

  - **Simple Correlation:** Overall, Bitcoin shows a low correlation with the Dollar Index (-0.068) and Gold (0.078), and a slightly higher positive correlation with the S&P 500 (0.216).

  - **Dynamic Correlation (EWMA):** An Exponentially Weighted Moving Average correlation plot reveals that these relationships are not stable and fluctuate significantly over time.

  - **Conditional Correlation:** The analysis segmented the data into three regimes based on Bitcoin's signed 30-day volatility:

    - **Extreme Negative Volatility:** During periods of sharp Bitcoin price drops, its correlation with the S&P 500 increases to 0.322.

    - **Stagnation:** In normal periods, the correlation is lower at 0.238.

    - **Extreme Positive Volatility:** During periods of sharp Bitcoin price increases, its correlation with the S&P 500 becomes negligible at 0.010.

This finding suggests that Bitcoin's behavior as a diversification asset changes depending on its own market conditions. It tends to move more closely with the broader stock market during its own downturns.

## Requirements and Setup
- **Python Version:** This analysis was conducted using Python 3.13.

- **Environment:** A working installation of Jupyter Notebook or JupyterLab is required to run the bitcoin-price-behavior.ipynb file.

- **Dependencies:** All required libraries are listed in the requirements.txt and environment.yml files. You can set up the environment using either pip or conda:

**Using pip:**

`pip install -r requirements.txt`

**Using conda:**

`conda env create -f environment.yml`
