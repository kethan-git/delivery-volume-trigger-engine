# Delivery Volume Trigger Engine

*1_Auto_Bhav_CSV.ipynb retrieves multi-yearly bhav data of all the listed stocks on NSE and creates a **Master CSV** file. 
2_VolumesTrigger.ipynb then analyzes multi-year NSE delivery volume data to detect abnormal spikes using percentile rankings and trigger thresholds.*


## Features
- Retrieves multi-yearly bhav data of all the listed stocks on NSE and creates a **Master CSV** file. 
- Ingests this master bhav CSVs for NSE equities (EQ series).
- Aggregates deliverable quantities by week and year.
- Computes average weekly delivery per stock and the most recent week's delivery.
- Flags a WEEK_TRIGGER when the current weekly delivery > historical average.
- Returns X_TIMES = CURRENT_WEEKLY_DELIV / AVG_WEEKLY_DELIV_QTY for spike magnitude.
- Interactive ticker-check: enter a symbol to get trigger status and X_TIMES.


## Data Source
This project uses daily bhavcopy data of all the NSE-listed stocks aggregated into a master_bhav.csv 
(this can be done by using the 1_Auto_Bhav_CSV.ipynb file) 


## How it works 
1_Auto_Bhav_CSV.ipynb
- Retrives the bhav data from the jugaad-data package (filters out the holidays i.e. weekends, festivals, other non-trading days) 

2_VolumesTrigger.ipynb 
- Load master bhav CSV and filter rows where SERIES == 'EQ' 
- Convert dates to datetime, create weekly buckets (week starting Monday) and extract YEAR 
- Aggregate DELIV_QTY per stock by week and by year 
- Compute AVG_WEEKLY_DEVLIV_QTY = DELIV_QTY_YEAR / WEEKS_TRADED 
- Extract the latest week's delivery per stock (CURRENT_WEEKLY_DELIV) 
- Compute X_TIMES = CURRENT_WEEKLY_DELIV / AVG_WEEKLY_DEVLIV_QTY and set WEEK_TRIGGER = YES/NO 
- Provide an input prompt to check a stock symbol and print trigger status + X_TIMES


## Quick Start 
1. Clone:
   ```python
   git clone https://github.com/<your-username>/delivery-volume-trigger-engine.git
   cd delivery-volume-trigger-engine
2. Download Requirements:
   ```python
   pip install pandas numpy jugaad-data nse-workday
3. Put your master_bhav.csv where the notebook expects it (or change the notebook path).
   Example paths used: /content/master_bhav.csv
4. Open and run the notebooks in order (download → analysis). The final cell will prompt for a ticker symbol.


## Usage Example 
```python
  Enter stock symbol: TCS
  Stock TCS Triggered: YES
  X_TIMES value: 2.14
```
Interpretation: TCS's most recent weekly delivery is ~2.14× its historical average weekly delivery → flagged as a trigger. 
