# Crop Classification in Côte d’Ivoire Using Sentinel-2 and XGBoost

## Overview

This project applies remote sensing and machine learning to classify **Cocoa, Palm and Rubber** from multitemporal Sentinel-2 imagery. Developed for the Côte d’Ivoire Byte-Sized Agriculture Challenge, it converts monthly satellite observations into sample-level features and uses an **XGBoost classifier** to distinguish the three crop types.

The model achieved a **weighted F1-score of 0.8961** and **89.53% accuracy** on a stratified validation set, demonstrating the potential of seasonal spectral information for crop identification.

## Data

The dataset contains 2024 Sentinel-2 imagery with 12 spectral bands, associated observation records and crop labels.

| Dataset | Unique samples | Monthly records |
|---|---:|---:|
| Training | 953 | 11,436 |
| Test | 282 | 3,384 |

Training samples comprise **235 Cocoa**, **313 Palm** and **405 Rubber** examples. Some monthly records lack imagery; feature extraction uses the available observations.

## Approach

- **Image preprocessing:** Validate band order, exclude no-data pixels and scale spectral values.
- **Feature extraction:** Calculate mean, median and standard deviation for six spectral bands and four vegetation indices—NDVI, NDMI, EVI and SAVI.
- **Temporal aggregation:** Combine monthly statistics and calendar-month NDVI values into **72 features per sample**.
- **Model development:** Train XGBoost using an 80:20 stratified split, with missing-value imputation fitted only on the training partition.
- **Evaluation:** Assess weighted F1, accuracy and class-level performance on 191 held-out samples. All monthly observations from a sample remain in the same partition.

## Results

| Metric | XGBoost validation result |
|---|---:|
| Weighted F1-score | 0.8961 |
| Accuracy | 89.53% |
| Cocoa F1-score | 0.94 |
| Palm F1-score | 0.88 |
| Rubber F1-score | 0.88 |

Cocoa recorded the strongest class-level F1-score, while Palm and Rubber achieved comparable performance. These figures reflect the notebook’s recorded local validation results, rather than a leaderboard score.

## Scope and Limitations

The workflow predicts one crop label per sample. It demonstrates geospatial data processing, vegetation-index analysis, temporal feature engineering and supervised classification. Explicit cloud masking is not included, and the random sample split does not establish performance in new geographic areas or years.

## Tools

**Python · Rasterio · NumPy · pandas · Matplotlib · scikit-learn · XGBoost · Google Colab**

## Data Source

[Zindi: Côte d’Ivoire Byte-Sized Agriculture Challenge](https://zindi.world/competitions/cote-divoire-byte-sized-agriculture-challenge) · [Competition data](https://zindi.world/competitions/cote-divoire-byte-sized-agriculture-challenge/data)
