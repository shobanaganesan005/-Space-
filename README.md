# Advanced Time Series Forecasting with Hierarchical ARIMA and State Space Models

This project implements a complete, modular Python pipeline for hierarchical time series
forecasting and backtesting, matching the assignment brief.

## Main Features

- **Synthetic hierarchical dataset generator** with at least 3 levels
  (e.g. Total -> Region -> Product), including both trend and seasonality.
- **ARIMA-based hierarchy forecasting** with:
  - Bottom-Up reconciliation (sum child forecasts to parents).
  - Simple Optimal Combination reconciliation using a MinT-style projection.
- **State Space Modeling (SSM)** using `statsmodels` structural time series
  (local level + trend + seasonal components) fitted per series.
- **Rolling-origin cross-validation** (minimum 5 folds) over the hierarchy,
  computing **MASE** and **sMAPE** at every level for both ARIMA and SSM.
- Clean project structure with re-usable modules and a report template.

## Project Structure

- `src/data_generator.py` – build synthetic hierarchical time series.
- `src/hierarchy_utils.py` – hierarchy definition, summing and reconciliation matrices.
- `src/metrics.py` – MASE, sMAPE and helper functions.
- `src/arima_models.py` – ARIMA fitting and hierarchical reconciliation.
- `src/state_space_models.py` – SSM fitting using structural time series.
- `src/rolling_backtest.py` – rolling origin evaluation for both methods.
- `data/hierarchical_data.csv` – example generated dataset.
- `outputs/` – placeholder directory for backtest results.
- `report/report.md` – detailed report template.

## Quick Start

1. Install dependencies:

```bash
pip install -r requirements.txt
```

2. Generate / regenerate the dataset:

```bash
python src/data_generator.py --output data/hierarchical_data.csv
```

3. Run rolling-origin backtest for ARIMA and SSM:

```bash
python src/rolling_backtest.py \
  --data-path data/hierarchical_data.csv \
  --n-folds 5 \
  --horizon 6
```

Results (MASE and sMAPE per level and method) are written into `outputs/`.

You can use and extend the provided report template to describe your dataset,
modeling choices, reconciliation strategy, and comparative analysis.
