# Data Reproducibility

The data files are not included in this repository because they are manually downloaded, scraped from third-party sites, or generated as intermediate analysis files. To reproduce the project, rebuild the folder structure below and place each file in the expected location.

## Folder Layout

```text
data/
  downloaded/
    archive/
    vanguard_etf_returns.xlsx
    vbk_weekly.csv
    vbr_weekly.csv
    vtv_weekly.csv
    vug_weekly.csv
    tnx_weekly.csv
    sp500_daily.csv
    pareto_20_stocks_daily.csv
    vanguard_holdings_duplicates_comparison.xlsx
    pareto_frontier_example.xlsx
    nyse_tickers.xlsx
  scraped/
    net_income_df.csv
    total_liabilities_df.csv
    price_book_df.csv
```

## Files You Need to Get Manually

**1. Vanguard ETF return workbook**
- Expected file: `data/downloaded/vanguard_etf_returns.xlsx`
- Used by: `notebooks/etfs_part_2.Rmd`
- Contains sheets for VBR, VBK, VTV, and VUG.

**2. Weekly ETF price files**
- Expected files:
  - `data/downloaded/vbk_weekly.csv`
  - `data/downloaded/vbr_weekly.csv`
  - `data/downloaded/vtv_weekly.csv`
  - `data/downloaded/vug_weekly.csv`
- Used by: `notebooks/etfs_part_3.Rmd`
- These are weekly historical price files with the standard columns `Date`, `Open`, `High`, `Low`, `Close`, `Adj Close`, and `Volume`.

**3. Weekly ten-year Treasury yield file**
- Expected file: `data/downloaded/tnx_weekly.csv`
- Used by: `notebooks/etfs_part_3.Rmd`
- This replaces the original browser-download style name `^TNX (1).csv`.

**4. S&P 500 daily historical price file**
- Expected file: `data/downloaded/sp500_daily.csv`
- Used by: `notebooks/pareto.Rmd`
- This replaces the original name `^GSPC_daily_historical_data.csv`.

**5. Twenty-stock Pareto example price file**
- Expected file: `data/downloaded/pareto_20_stocks_daily.csv`
- Used by: `notebooks/pareto.Rmd`
- Contains daily price data for the 20-stock sample used in the Pareto frontier analysis.

**6. Vanguard holdings comparison workbook**
- Expected file: `data/downloaded/vanguard_holdings_duplicates_comparison.xlsx`
- Used by: `notebooks/pareto.Rmd`
- Contains the ETF holdings/ticker universe used to sample stocks for the Pareto example.

**7. Pareto frontier toy example workbook**
- Expected file: `data/downloaded/pareto_frontier_example.xlsx`
- Used by: `notebooks/pareto_SAT_example.Rmd`

**8. NYSE ticker list**
- Expected file: `data/downloaded/nyse_tickers.xlsx`
- Currently referenced only in commented code in `notebooks/pareto.Rmd`.

## Files Created by Scraping

The files in `data/scraped/` are created by scraping Macrotrends pages in `notebooks/pareto.Rmd`.

**Generated files**
- `data/scraped/net_income_df.csv`
- `data/scraped/total_liabilities_df.csv`
- `data/scraped/price_book_df.csv`

The notebook has scraping chunks for:
- `net-income`
- `total-liabilities`
- `price-book`

The report notes that historical metrics were difficult to collect, and the notebook includes long sleep intervals between requests. If these cached CSVs are already present, you can skip the scraping chunks and run the later analysis chunks directly.

## Naming Notes

The downloaded files were renamed away from browser-download names such as `VBR (1).csv` and `^TNX (1).csv`. The new names describe both the asset and frequency, making the notebook paths easier to read and less dependent on local download history.
