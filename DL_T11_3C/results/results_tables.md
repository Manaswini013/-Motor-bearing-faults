# Auto-generated results (copy into the report)

## Splits
| split               |   windows |   fault_files | note                                        |
|:--------------------|----------:|--------------:|:--------------------------------------------|
| Train (normal only) |      1984 |             0 | normal files 97-100, first 60%, 50% overlap |
| Validation normal   |       325 |             0 | same files, next 20%                        |
| Validation fault    |      2134 |            18 | fault files at 0 and 1 HP; threshold tuning |
| Test normal         |       325 |             0 | same files, last 20%                        |
| Test fault          |      2136 |            18 | fault files at 2 and 3 HP; final test only  |

## Model and bottleneck comparison
| model   |   latent |   params |   val_ap |   test_auc_mean |   test_auc_std |   test_ap_mean |   test_recall |   test_fpr |   sep_ratio |   ms_per_window |   train_mse |   val_normal_mse |
|:--------|---------:|---------:|---------:|----------------:|---------------:|---------------:|--------------:|-----------:|------------:|----------------:|------------:|-----------------:|
| dense   |     1024 |  6297600 |   1.0000 |          1.0000 |         0.0000 |         1.0000 |        1.0000 |     0.0000 |     23.9047 |          0.9773 |      0.1514 |           0.3172 |
| dense   |      256 |  1444608 |   1.0000 |          1.0000 |         0.0000 |         1.0000 |        1.0000 |     0.0000 |     27.6917 |          0.7388 |      0.1538 |           0.2856 |
| dense   |       64 |  1346112 |   1.0000 |          1.0000 |         0.0000 |         1.0000 |        1.0000 |     0.0000 |     25.6677 |          0.6989 |      0.1829 |           0.3027 |
| dense   |       16 |  1321488 |   1.0000 |          1.0000 |         0.0000 |         1.0000 |        1.0000 |     0.0000 |     18.8976 |          0.6955 |      0.3231 |           0.4045 |
| cnn     |     1024 |   104017 |   1.0000 |          1.0000 |         0.0000 |         1.0000 |        1.0000 |     0.0000 |    995.0385 |          1.1842 |      0.0068 |           0.0068 |
| cnn     |      256 |    96325 |   1.0000 |          1.0000 |         0.0000 |         1.0000 |        1.0000 |     0.0000 |    244.9240 |          1.2998 |      0.0299 |           0.0310 |
| cnn     |       64 |    94402 |   1.0000 |          1.0000 |         0.0000 |         1.0000 |        1.0000 |     0.0000 |     27.6774 |          1.0992 |      0.2752 |           0.2779 |

## Operating points (test)
| model                | operating_point   | split   |    thr |   k |   window_recall |   window_precision |   window_fpr |   fa_episodes |   fa_per_24h |   fa_per_24h_upper95 |   events_detected_3 |   events_detected_5min |   n_events |   mean_delay_readings |   cost_rs |
|:---------------------|:------------------|:--------|-------:|----:|----------------:|-------------------:|-------------:|--------------:|-------------:|---------------------:|--------------------:|-----------------------:|-----------:|----------------------:|----------:|
| Dense AE (baseline)  | A: best-F1        | test    | 0.9041 |   1 |          1.0000 |             1.0000 |       0.0000 |             0 |       0.0000 |           11492.2783 |                  18 |                     18 |         18 |                1.0000 |    0.0000 |
| Dense AE (baseline)  | B: cost-optimal   | test    | 2.0144 |   1 |          0.9494 |             1.0000 |       0.0000 |             0 |       0.0000 |           11492.2783 |                  18 |                     18 |         18 |                1.0556 |    0.0000 |
| 1D CNN AE (improved) | A: best-F1        | test    | 0.8553 |   1 |          1.0000 |             1.0000 |       0.0000 |             0 |       0.0000 |           11492.2783 |                  18 |                     18 |         18 |                1.0000 |    0.0000 |
| 1D CNN AE (improved) | B: cost-optimal   | test    | 2.0725 |   1 |          0.9518 |             1.0000 |       0.0000 |             0 |       0.0000 |           11492.2783 |                  18 |                     18 |         18 |                1.0556 |    0.0000 |

## Target check
| model                | op              | target                                                          | value                                                           | result                              |
|:---------------------|:----------------|:----------------------------------------------------------------|:----------------------------------------------------------------|:------------------------------------|
| Dense AE (baseline)  | A: best-F1      | Recall on fault events >= 0.85 (window-level)                   | 1.000                                                           | PASS                                |
| Dense AE (baseline)  | A: best-F1      | Recall on fault events >= 0.85 (event-level, within 3 readings) | 18/18                                                           | PASS                                |
| Dense AE (baseline)  | A: best-F1      | False alarms < 2 per 24 h (point estimate)                      | 0.00 (95% upper bound 11492; only 28 s of normal test data)     | PASS (not statistically verifiable) |
| Dense AE (baseline)  | A: best-F1      | Detection delay < 5 min (or within 3 readings)                  | 18/18 within 5 min; 18/18 within 3 readings; mean 1.00 readings | PASS                                |
| Dense AE (baseline)  | A: best-F1      | No labelled fault data used for training                        | train windows from normal files 97-100 only                     | PASS (by construction)              |
| Dense AE (baseline)  | B: cost-optimal | Recall on fault events >= 0.85 (window-level)                   | 0.949                                                           | PASS                                |
| Dense AE (baseline)  | B: cost-optimal | Recall on fault events >= 0.85 (event-level, within 3 readings) | 18/18                                                           | PASS                                |
| Dense AE (baseline)  | B: cost-optimal | False alarms < 2 per 24 h (point estimate)                      | 0.00 (95% upper bound 11492; only 28 s of normal test data)     | PASS (not statistically verifiable) |
| Dense AE (baseline)  | B: cost-optimal | Detection delay < 5 min (or within 3 readings)                  | 18/18 within 5 min; 18/18 within 3 readings; mean 1.06 readings | PASS                                |
| Dense AE (baseline)  | B: cost-optimal | No labelled fault data used for training                        | train windows from normal files 97-100 only                     | PASS (by construction)              |
| 1D CNN AE (improved) | A: best-F1      | Recall on fault events >= 0.85 (window-level)                   | 1.000                                                           | PASS                                |
| 1D CNN AE (improved) | A: best-F1      | Recall on fault events >= 0.85 (event-level, within 3 readings) | 18/18                                                           | PASS                                |
| 1D CNN AE (improved) | A: best-F1      | False alarms < 2 per 24 h (point estimate)                      | 0.00 (95% upper bound 11492; only 28 s of normal test data)     | PASS (not statistically verifiable) |
| 1D CNN AE (improved) | A: best-F1      | Detection delay < 5 min (or within 3 readings)                  | 18/18 within 5 min; 18/18 within 3 readings; mean 1.00 readings | PASS                                |
| 1D CNN AE (improved) | A: best-F1      | No labelled fault data used for training                        | train windows from normal files 97-100 only                     | PASS (by construction)              |
| 1D CNN AE (improved) | B: cost-optimal | Recall on fault events >= 0.85 (window-level)                   | 0.952                                                           | PASS                                |
| 1D CNN AE (improved) | B: cost-optimal | Recall on fault events >= 0.85 (event-level, within 3 readings) | 18/18                                                           | PASS                                |
| 1D CNN AE (improved) | B: cost-optimal | False alarms < 2 per 24 h (point estimate)                      | 0.00 (95% upper bound 11492; only 28 s of normal test data)     | PASS (not statistically verifiable) |
| 1D CNN AE (improved) | B: cost-optimal | Detection delay < 5 min (or within 3 readings)                  | 18/18 within 5 min; 18/18 within 3 readings; mean 1.06 readings | PASS                                |
| 1D CNN AE (improved) | B: cost-optimal | No labelled fault data used for training                        | train windows from normal files 97-100 only                     | PASS (by construction)              |
