## Notebooks Overview

This folder contains the Jupyter notebooks used for data collection and delivery volume analysis.

### 1_Auto_Bhav_CSV.ipynb
- Downloads daily NSE bhavcopy data using public sources.
- Cleans and consolidates raw files into a single master bhav CSV.
- Prepares a consistent dataset for downstream delivery volume analysis.

### 2_VolumesTrigger.ipynb
- Aggregates delivery volumes at weekly and yearly levels for EQ-series stocks.
- Computes historical average weekly delivery per stock.
- Identifies abnormal delivery volume spikes using trigger-based logic.
- Supports interactive ticker-based checks to evaluate trigger hits and spike magnitude (`X_TIMES`).
