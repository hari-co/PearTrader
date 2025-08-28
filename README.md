# PearTrader — Stock Correlation Calculator  
## Overview
Investors face an overwhelming number of options when choosing stocks. Traditional approaches often rely on news, trends, or guesswork, which can lead to risky decisions. **PearTrader** helps investors make more informed choices by analyzing historical price movements and finding correlations among top-performing stocks.


## Features  
- **Correlation Analysis**: Calculates Pearson correlation coefficients between stocks.  
- **Recommendation Engine**: Suggests stocks that are highly correlated with a user-selected stock.  
- **Data Visualization**: Displays correlations in an intuitive and interactive way.  
- **Historical Data Analysis**: Uses real-world stock data for reliable insights.  

---

## Tech Stack  
- **Python 3**  
- **Pandas** – for data manipulation  
- **Matplotlib / Seaborn** – for visualization  
- **Yahoo Finance API** – for historical stock price data  

---

## How to Use  

1. **Clone the repository**  
   ```bash
   git clone https://github.com/yourusername/PearTrader.git
   cd PearTrader
   ```
   
2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run**
    ```bash
    python main.py
    ```

## Context  

Our approach is grounded in **Modern Portfolio Theory (MPT)**, which states that a portfolio’s overall risk and return are affected not only by individual assets but also by the **correlation among them**. By understanding these correlations, investors can better manage risk and optimize returns.  

Moreover, our system supports trading strategies such as **pairs trading**, which exploits historical correlations between two stocks to profit when their prices deviate from their usual relationship.  

For example:  
- If **Stock A** and **Stock B** historically share a high correlation of 0.9, but Stock A suddenly rises while Stock B lags (dropping their correlation to 0.5), a pairs trader can:
  - Go **long** on the underperforming stock.
  - Go **short** on the overperforming stock.  
  - Expect profits when the correlation reverts to its historical norm.  

By integrating these concepts into an accessible recommendation tool, we empower investors to make **data-driven decisions**, **reduce guesswork**, and **gain deeper insights** into the interconnected nature of the stock market.  

---

## Data Collection and Processing  

- **Data Collection**:  
  Historical stock data is fetched from **Yahoo Finance** using the yfinance package. We retrieve adjusted closing prices for a predefined list of stock tickers over a user-specified date range.  
  - Implemented in the filter_data() function, which downloads the raw data and performs initial cleaning.  

- **Percentage Change Computation**:  
  For each stock, the daily percentage change is computed using the formula:  

```math
  pct\_change(t) = (P_t - P_{t-1}) / P_{t-1}  
```
  where P_t is the adjusted closing price at time t.  
  This calculation uses **pandas DataFrame operations**.  

- **Correlation Matrix Computation**:  
  We compute the correlation matrix using pandas’ built-in corr() method.
  
  This calculates the **Pearson correlation coefficient** for all stock pairs. After computing the daily percentage changes and cleaning the data with dropna(), we call corr() on the resulting DataFrame.  

  The Pearson correlation coefficient is defined as:  
```math
  ρ(A, B) = Σ(A_t - Ā)(B_t - B̄) / √(Σ(A_t - Ā)² · Σ(B_t - B̄)²)  
```
  This produces a symmetric matrix quantifying the linear relationship between every pair of stocks.  

---

## Graph Construction and Community Detection  

- **Graph Construction**:  
  We use the **networkx** package to represent stock relationships as an undirected graph G = (V, E).  
  - Each stock is a **node** in V.  
  - An **edge** between two stocks is added if their correlation coefficient exceeds a predefined threshold (see **Limitations** section).  
  - Implemented in the analyze_stocks() function, with edge weights corresponding to correlation values.  

- **Community Detection**:  
  To identify clusters of highly correlated stocks, we apply the **Greedy Modularity algorithm** from networkx.algorithms.community.greedy_modularity_communities.  
  - This algorithm partitions the graph into **disjoint communities**, where each represents a group of stocks that tend to move together.  


## Contributors
- Alec Jiang
- Yuanzhe Li
- Luke Zhengqi Pan
- Junchen Liu


