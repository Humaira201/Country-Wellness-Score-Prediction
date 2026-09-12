# Country Happiness Forecasting

Temporal forecasting of country-level happiness (World Happiness Report
Cantril Ladder scores), enriched with World Bank GDP per capita data.
Core contribution: reframing happiness prediction as a next-year
forecasting task (LSTM) rather than the static, same-year regression used
in most existing published work, combined with a stacking ensemble of
RF + XGBoost + LSTM and SHAP-based explainability.

## Status: data pipeline complete, modeling in progress

## Repo structure
```
data/raw/whr_worldbank_merged.csv   -- merged WHR + World Bank dataset
data/processed/                     -- train/val/test splits, ready to model
scripts/merge_whr_worldbank.py      -- pulls + merges raw data from OWID API
scripts/preprocess_data.py          -- cleaning, lag features, chronological split
scripts/train_baselines.py          -- RF + XGBoost baselines (in progress)
```

## Pipeline (run in this order)
1. `python scripts/merge_whr_worldbank.py` → produces `data/raw/whr_worldbank_merged.csv`
2. `python scripts/preprocess_data.py` → produces everything in `data/processed/`
3. `python scripts/train_baselines.py` → trains RF/XGBoost, saves OOF predictions for stacking

**See `data/processed/data_dictionary.md` for a full column-by-column
description of the processed dataset** — read this before writing any
modeling code, especially the note about which columns to use for the
LSTM vs. the classical models.

## Next steps (not yet done)
- [ ] LSTM sequence model (uses raw, unlagged columns — see data dictionary)
- [ ] Stacking meta-learner (combine RF + XGBoost + LSTM out-of-fold predictions)
- [ ] SHAP explainability on the tree-based models
- [ ] Final comparison table: naive persistence vs. RF vs. XGBoost vs. LSTM vs. stacked ensemble

## Data sources
- World Happiness Report (Cantril Ladder scores), via Our World in Data
- World Bank GDP per capita (constant international $), via Our World in Data
