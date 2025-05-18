# ilmanala

This project is part of the People and Earth's Ecosystem course, focusing on addressing greenhouse gas (GHG) emissions in the Philippines through data-driven approaches. The core activities include data analysis, visualization, and the development of a digital advocacy platform aimed at raising awareness and promoting informed action on GHG emissions in the country.

The project uses the official GHG emissions dataset from the Philippine Statistics Authority (PSA) as the primary data source. It involves cleaning and imputing missing data, generating synthetic emissions projections through 2050, and creating visual tools to communicate trends and sectoral contributions effectively.

As the project progresses, additional datasets, sources, and references-such as national climate policies, energy statistics, and international reports-will be integrated to enrich the analysis and advocacy content. This evolving approach ensures a comprehensive understanding of the Philippines’ emissions landscape and supports evidence-based environmental advocacy.

## Project Setup in Jupyter Lab with R

```sh

# Create a New Conda Environment with R and JupyterLab; r-essentials packages installed at least 200 essential EDA packages
conda create -n r_env -c conda-forge r-irkernel r-base r-essentials jupyterlab
# Activate virtual env
conda activate r_env
# Register the R Kernel with Jupyter
R -e "IRkernel::installspec(user = FALSE)"
# List the packages installed
conda list
# Run Jupyter lab
jupyter lab
# Generating virtual env's package listing
conda list -n r_env > environment.txt
```

## Synthetic Greenhouse Gas Emissions Dataset (Philippines, 2010–2050) Generation

This project provides a cleaned, imputed, and extended synthetic dataset of greenhouse gas (GHG) emissions in the Philippines by sector, covering the years 2010–2050. The synthetic data is generated using linear interpolation and regression-based forecasting, based on the official dataset from the Philippine Statistics Authority (PSA). For more details on the generation process of the synthetic dataset, please refer to the [documentation provided](https://github.com/imperionite/ilmanala/blob/main/SYNTHETIC_DATASET_GENERATION.md) provided and to the [synthetic dataset generation notebook project](https://github.com/imperionite/ilmanala/blob/main/SYNTHETIC_GHG.ipynb).


### Disclaimer

The dataset provided here is a cleaned, processed, and synthetically extended version of the original greenhouse gas emissions data published by the Philippine Statistics Authority (PSA). It is not the original raw dataset but has been modified to handle missing values, correct formatting issues, and extend emissions estimates through 2050 using statistical methods.

Users should be aware that:
The historical data (2010–2020) have undergone cleaning and imputation to address missing or inconsistent values.
The data for years 2021–2050 are synthetic projections based on linear regression models and should be interpreted as scenario-based estimates, not official statistics.

This dataset is intended for research, educational, and exploratory purposes only.
Please refer to the original PSA source for official and authoritative greenhouse gas emissions data.


### Author/Developer

[Arnel Imperial](https://github.com/imperionite)
