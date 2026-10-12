# Factor Models and Macroeconomic Forecasting with FRED-MD

**Author: Davide Mascioli**

This Python project was developed in 2024 for my Master's course in Advanced Econometrics, held by Professor Giuseppe Ragusa at Sapienza University of Rome. Inspired by work and MATLAB code of McCracken and Ng (2015), it uses FRED-MD to estimate common macroeconomic factors and compare forecasts of U.S. Industrial Production and CPI inflation. I revised it for upload in 2026 and contextually I added forecasts based on the FRED-MD release of September 2026. 

## Approach

- Transform the series using FRED-MD codes, treat outliers and impute missing values through iterative PCA.
- Select the factor dimension using Bai–Ng and examine explained variance and factor associations.
- Produce direct forecasts at horizons of one to six months, using full-sample regressions and the most recent 120 complete training observations.
- Evaluate accuracy with 120-observation rolling regressions and factors re-estimated from an expanding panel at each origin.

| Model | Selection by BIC |
| --- | --- |
| Baseline factor model | Autoregressive and factor lag orders, retaining all Bai–Ng factors. |
| Target-specific factor model | Number of leading principal components and both lag orders. |
| AR benchmark | Autoregressive order. |

IP forecasts are expressed in index levels; inflation forecasts are monthly log changes in percent. The 2026 extension also reports year-on-year inflation.

Accuracy is reported using RMSE and pairwise RMSE ratios: Baseline/AR, Target/AR and Target/Baseline. A ratio below one favours the model in the numerator.

## Files and data

Using fixed local vintages preserves reproducibility as the underlying economic data are updated.

| File | Content |
| --- | --- |
| [FRED_MD_Forecasting.ipynb](FRED_MD_Forecasting.ipynb) | Analysis, forecasts and evaluation. |
| [2024-05.csv](2024-05.csv) | May 2024 vintage; data through April 2024. |
| [2026-09-MD.csv](2026-09-MD.csv) | September 2026 vintage; data through August 2026. |

Download the [September 2026 source CSV](https://www.stlouisfed.org/-/media/project/frbstl/stlouisfed/research/fred-md/monthly/2026-09-md.csv) or find newer vintages on the [official FRED-MD page](https://www.stlouisfed.org/research/economists/mccracken/fred-databases).

## Running the notebook

Keep all three files in the same directory; the notebook reads the CSVs using relative paths. Open it in Jupyter Notebook or JupyterLab, select the appropriate Python kernel. You can set `RUN_EVALUATION = True` to execute the rolling window evaluation; note that it might be computationally intensive.

Requires Python 3, NumPy, pandas, SciPy, scikit-learn, Matplotlib, IPython and Jupyter Notebook or JupyterLab.

## Overview of main findings

For IP, model rankings vary across horizons and historical periods;  however, there is evidence of better perfomance by factor models compared to autoregressive benchmarks. For monthly inflation, the AR benchmark has the lowest overall RMSE at all six horizons. Factor selection dependent on target variable generally improves on the baseline that retains all factors selected by Bai-Ng criterium.  

## Notes

The original analysis uses data through April 2024 to forecast Industrial Production and monthly inflation for May–October 2024. The September 2026 extension uses data through August 2026 to forecast the same variables for September 2026–February 2027.

The rolling evaluation separately assesses historical forecast accuracy using the May 2024 vintage; historical revisions and publication lags are not reproduced.

For the 2026 inflation forecasts, the missing October 2025 log CPI level is interpolated. Year-on-year inflation is calculated from seasonally adjusted CPIAUCSL.

## References and acknowledgements

- McCracken, M. W., and Ng, S. (2015). [FRED-MD: A Monthly Database for Macroeconomic Research](https://doi.org/10.20955/wp.2015.012). St. Louis Fed Working Paper 2015-012.
- Bai, J., and Ng, S. (2002). [Determining the Number of Factors in Approximate Factor Models](https://doi.org/10.1111/1468-0262.00273). *Econometrica*, 70(1), 191–221.
- Stock, J. H., and Watson, M. W. (2002). [Macroeconomic Forecasting Using Diffusion Indexes](https://doi.org/10.1198/073500102317351921). *Journal of Business & Economic Statistics*, 20(2), 147–162.

The preprocessing, factor-estimation and explained-variance routines adapt the MATLAB code distributed with FRED-MD. Forecasting comparisons and the 2026 extension were implemented for this project.
