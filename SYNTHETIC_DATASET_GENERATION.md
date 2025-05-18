# ilmanala: Synthetic Greenhouse Gas Emissions Dataset (Philippines, 2010–2050) Generation

The project uses the official GHG emissions dataset from the Philippine Statistics Authority (PSA) as the primary data source. It involves cleaning and imputing missing data, generating synthetic emissions projections through 2050, and creating visual tools to communicate trends and sectoral contributions effectively.

To support long-term forecasting and simulation beyond the original dataset, we extended the greenhouse gas emissions data from the historical period (2010–2020) through synthetic data generation for the years 2021 to 2050. This synthetic extension enables forward-looking analysis essential for policy evaluation, sustainability modeling, and scenario planning.

## Data Cleaning & Processing Overview

- **Partial Preservation of Original Data (2010–2020):**  
  The original dataset undergoes cleaning steps including renaming columns, replacing placeholder symbols (`"."`, `".."`) with `NA`, converting emissions data to numeric, and trimming sector names. Rows with all emission values missing (`NA`) are excluded to focus on sectors with at least partial data, while retaining `NA`s within included rows to reflect real-world data noise and uncertainty.

- **Sector-wise Linear Forecasting:**

  - For each combination of sector and gas type (CO2, CH4, N2O, HFCs), a linear regression model was fit using the historical data from 2010 to 2020.
  - The model estimated future emissions by extrapolating existing trends under the assumption of continuity in sectoral behavior.

- **Forecasting Future Emissions (2021–2050):**  
  Synthetic emissions data for years beyond 2020 are generated through statistical modeling based on historical trends.

- **Synthetic Data Generation Criteria:**  
  For each sector-gas combination:

  - If **at least three non-missing data points** exist in the historical period, a simple linear regression model (emissions ~ year) is fitted to imputed historical data, and used to forecast emissions for 2021–2050.
  - If **fewer than three but at least one data point** exists, the last observed emission value is repeated for all future years to maintain continuity.
  - If **no historical data points** exist for a sector-gas, future emissions are set to `NA` to realistically represent missingness.

- **Integration with Historical Data:**

  - The synthetic data (2021–2050) was appended to the cleaned historical dataset (2010–2020), resulting in a continuous time series spanning 41 years.
  - Data was structured in a tidy format with columns for Year, Sector, and each gas type, suitable for downstream analysis and visualization.

- **Imputation of Historical Data:**  
  Missing emission values within the historical period are imputed using linear interpolation between existing data points. Leading and trailing missing values remain as `NA` to preserve authentic data gaps.

- **No Zero-Filling of Missing Values:**  
  At no point are missing values replaced with zeros, preserving the integrity of missingness as genuine absence of data or unreported emissions.

- **Intelligent Fallbacks for Sparse Data:**  
  The approach balances model-based forecasting with pragmatic fallbacks (repeating last known values or using `NA`) to handle sparse or incomplete data responsibly.

  - In cases where insufficient data points were available to build a reliable model, the last known value was carried forward as a conservative estimate.
  - This approach mimics real-world data gaps while ensuring continuity in the dataset.

- **Handling of Missing Values (NA):**

  - Some NA values remain in the synthetic portion due to absent historical patterns for certain sector-gas pairs.
  - These can be treated as indicators of uncertainty or optionally imputed in further analysis depending on the modeling context.

- **Final Dataset Composition:**  
  The resulting dataset combines the cleaned, partially filtered original data (2010–2020) with synthetic forecasts (2021–2050). It includes all sectors with at least some historical data, ordered by sector and year, enabling comprehensive analysis while acknowledging data limitations.

- **Output:**
  The final combined dataset `(phil_synthetic_ghg_emissions_2010_2050.csv)` includes both observed and generated emissions data, ready for statistical modeling, dashboard visualization, and decision support tasks.

### Data Source

- **Original Dataset:**  
  [PSA Emissions of Greenhouse Gases (Philippines)](https://openstat.psa.gov.ph/PXWeb/pxweb/en/DB/DB__3A/0143A5EGHG1.px/table/tableViewLayout1/?rxid=bdf9d8da-96f1-4100-ae09-18cb3eaeb313)
- **Unit:** Gigagrams of CO2 equivalent (Gg CO2e)
- **Sectors Covered:** Energy, Transport, Agriculture, Forestry, Industrial Processes, Waste, and sub-sectors
- **Gases Covered:** CO2, CH4, N2O, HFCs
- **Coverage:** 2010–2020 (original), extended to 2050 (synthetic)
- **License:** Philippine Greenhouse Gas Inventory Report, Climate Change Commission

#### Footnotes from Source

- 2010 Greenhouse Gas Inventory was originally expressed in million metric tons CO2 equivalent (Mt CO2e). One Mt CO2e is equivalent to 1,000 Gg CO2e.
- Figures are results of actual registration without any adjustment for under-registration.

### Data Preparation and Synthetic Dataset Generation

#### 1. Data Acquisition

The original dataset was downloaded from the PSA OpenStat portal as a CSV file.

#### 2. Data Cleaning

- **Column Renaming:** Columns were renamed for clarity (Year, Sector, CO2, CH4, N2O, HFCs).
- **Missing Values:** Missing values (NA, ".", "..") were identified and handled appropriately.
- **Sector Names:** Leading/trailing whitespace and formatting artifacts were removed from sector names.

#### 3. Imputation (Linear Interpolation)

- **Within Historical Data (2010–2020):**  
  For each sector and gas, missing values between observed years were imputed using linear interpolation (via the `na.approx` function from the `zoo` R package).
- **Leading/Trailing NAs:**  
  If a sector-gas time series had missing values at the start or end, these were filled using the nearest available value (forward/backward fill), reflecting real-world data reporting practices.

#### 4. Synthetic Data Generation (2021–2050)

- **Trend Forecasting:**  
  For each sector and gas, a linear regression model was fitted to the imputed historical data (2010–2020).
- **Extrapolation:**  
  The fitted model was used to forecast annual emissions for each sector-gas combination from 2021 to 2050.
- **Fallback:**  
  If there were insufficient data points for regression, the last known value was carried forward. If no data existed for a sector-gas, values remained NA to reflect true missingness.

#### 5. Dataset Structure

The final dataset includes:

| Year | Sector | CO2 | CH4 | N2O | HFCs |
| ---- | ------ | --- | --- | --- | ---- |
| 2010 | ...    | ... | ... | ... | ...  |
| ...  | ...    | ... | ... | ... | ...  |
| 2050 | ...    | ... | ... | ... | ...  |

- **2010–2020:** Original (cleaned and imputed) data
- **2021–2050:** Synthetic, regression-based forecasts

#### 6. Output

- **File:** `phil_synthetic_ghg_emissions_2010_2050.csv`
- **Format:** CSV, with columns for Year, Sector, CO2, CH4, N2O, HFCs

### Reproducibility

All data cleaning, imputation, and synthetic data generation were performed in R using the following key packages: `dplyr`, `tidyr`, `zoo`, `purrr`, `stringr`, `ggplot2`, `readr` and etc.

---

###Citation

If you use this synthetic dataset, please cite:

> Philippine Greenhouse Gas Inventory Report, Climate Change Commission  
> Data processed and extended by [Arnel Imperial](https://github.com/imperionite), 2025.

---

### Disclaimer

The dataset provided here is a cleaned, processed, and synthetically extended version of the original greenhouse gas emissions data published by the Philippine Statistics Authority (PSA). It is not the original raw dataset but has been modified to handle missing values, correct formatting issues, and extend emissions estimates through 2050 using statistical methods.

Users should be aware that:
The historical data (2010–2020) have undergone cleaning and imputation to address missing or inconsistent values.
The data for years 2021–2050 are synthetic projections based on linear regression models and should be interpreted as scenario-based estimates, not official statistics.

This dataset is intended for research, educational, and exploratory purposes only.
Please refer to the original PSA source for official and authoritative greenhouse gas emissions data.
