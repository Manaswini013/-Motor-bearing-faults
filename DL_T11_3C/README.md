# DL_T11_3C: Unsupervised Anomaly Detection in Motor-Bearing Vibration (CWRU)

MGIT (Autonomous), Hyderabad | CM701PC / CM751PC Deep Learning | Task 3, Variant 3C, Team 11
Team: 23261A6649 (data lead), 23261A6644 (model lead), 23261A6622 (evaluation and report lead)

Dense and 1D-CNN autoencoders learn normal bearing vibration (CWRU, 12 kHz drive end). High reconstruction error flags a fault. **No fault data is used for training**; fault labels are used only to tune thresholds (loads 0, 1 HP) and to test (loads 2, 3 HP).

## Run
1. Open `DL_T11_3C.ipynb` in Google Colab, Runtime > Run all (CPU is enough; the full 21-model run took on the order of 30 to 60 minutes on CPU).
2. Outputs go to `/content/outputs` (tables, figures, `run_settings.json`, zip). Quick test: set environment variables `EPOCHS=3 N_SEEDS=1`.
3. Local run: `pip install -r requirements.txt`, then run the notebook; set `CWRU_DIR` and `OUT_DIR` if needed. See `data/README.md`.

## Contents
* `DL_T11_3C.ipynb` - all code (data, splits, models, experiments, thresholds, cost, plots, target check)
* `report/` - 4-page report (PDF and Word)
* `results/` - tables (`table_*.csv`), figures (`fig_*.png`), `results_tables.md`, `run_settings.json`, AI declaration
* `docs/` - one-page note for plant engineers
* `data/README.md` - where the data come from

## Design
Windows of 1024 samples (85 ms). Train = first 60% in time of each normal file; validation/test normal = next/last 20% with a one-window gap. Scaler fitted on training data only. Seeds fixed (42, 43, 44). Models chosen by validation average precision. Threshold A = best F1; B = minimum cost (Rs 4 lakh per missed fault, Rs 2,000 per false alarm) with 1 to 3 consecutive alarms.

## Results summary (test split, from `results/`)
All models: AUC and AP 1.000; 18 of 18 fault files detected, mean delay about 1 reading (85 ms); 0 false alarms in 27.7 s of normal test data. The false-alarm target (< 2 per 24 h) cannot be statistically verified (95% upper bound 11,492 per day). A signal-energy score with no model also reaches AUC 0.99999, so CWRU is an easy benchmark. Details and limitations are in the report.

## Reproducibility notes
Seeds are fixed, but GPU runs can differ slightly. Timings depend on the machine.

## AI tools
See `results/AI_usage_declaration.txt` and the report appendix.
