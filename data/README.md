# Data Reproducibility

The data files are not included in this repository because they are manually downloaded, scraped from third-party sites, or generated as intermediate analysis files. To reproduce the project, rebuild the folder structure below and place each file in the expected location.

`vanguard_etf_returns.xlsx` is included because it is a manually compiled workbook from publicly available Vanguard return tables. Other downloaded holdings and historical price files are excluded because of licensing, redistribution restrictions, or provider access limits.

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

Files from sections 1-4 were originally downloaded from [Yahoo Finance](https://finance.yahoo.com/) historical data pages. As of June 2026 it appears Yahoo Finance restricts CSV downloads without a paid subscription. Users may need to recreate these files using the free trial of Yahoo Finance Gold, using yfR to scrape the data, or via another free historical price website.

**1. Weekly ETF price files**
- Expected files:
  - `data/downloaded/vbk_weekly.csv`
  - `data/downloaded/vbr_weekly.csv`
  - `data/downloaded/vtv_weekly.csv`
  - `data/downloaded/vug_weekly.csv`
- Used by: `notebooks/etfs_part_3.Rmd`

**2. Weekly ten-year Treasury yield file**
- Expected file: `data/downloaded/tnx_weekly.csv`
- Used by: `notebooks/etfs_part_3.Rmd`

**3. S&P 500 daily historical price file**
- Expected file: `data/downloaded/sp500_daily.csv`
- Used by: `notebooks/pareto.Rmd`

**4. Twenty-stock Pareto example price file**
- Expected file: `data/downloaded/pareto_20_stocks_daily.csv`
- Used by: `notebooks/pareto.Rmd`

**5. Vanguard holdings comparison workbook**
- Go to https://investor.vanguard.com/investment-products/list/etfs.
- Download the "Portfolio Composition" file for each of VBK, VBR, VTV, and VUG.
- Combine all four into one long list and create a column labeled "ETF" to store which ETF it comes from: "Large Value", "Large Growth", "Small Value", "Small Growth"
- Expected file: `data/downloaded/vanguard_holdings_duplicates_comparison.xlsx`
- Used by: `notebooks/pareto.Rmd`
- The file is called "duplicates comparison" but the Rmd just reads the full list. It's important to have the "ETF" column because the code will use said column to group the tickers from each ETF.

**6. NYSE ticker list**
- Go to https://ftp.nyse.com/Reference%20Data%20Samples/NYSE%20GROUP%20SECURITY%20MASTER/
- Download `NYSEGROUP_US_REF_SECURITYMASTERPREMIUM_EQUITY_4.0_20240328.xls`. As of June 2026 this is the file dated 02-Apr-2024 with trailing number 27708928.
- Don't worry about all the other columns, simply rename the "Stock Symbol" column to "Symbol" that is all that's used in the code.
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

Historical metrics were difficult to collect, and the notebook includes long sleep intervals between requests to avoid getting blocked by bot detection.
