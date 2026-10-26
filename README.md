# Seattle vs. Berkeley Precipitation Analysis

This project investigates whether it rains more in Seattle, Washington than in Berkeley, California using daily precipitation data from 2018 through 2022.

---

## Project Overview

Daily precipitation patterns were compared between Seattle and Berkeley using NOAA weather data. The analysis included data cleaning, missing-value estimation, monthly and seasonal comparisons, visualization, and statistical testing.
Overall, Seattle was wetter than Berkeley. Seattle averaged approximately 0.113 inches of precipitation per day, compared with 0.053 inches per day in Berkeley. The largest seasonal differences occurred during summer, fall, and winter.

- **Objective:** Determine whether it rains more in Seattle, WA than in Berkeley, CA.
- **Domain:** Weather / Climate Data
- **Key Techniques:** Data cleaning, missing-value imputation, exploratory data analysis, K-Nearest Neighbors regression, visualization, and statistical testing.

---

## Project Structure

```
├── data/                                    # Raw and processed data
│   ├── seattle_rain.csv                       # Raw Seattle data from 01/01/2018 to 12/31/2022
│   ├── berkeley_rain.csv                      # Raw Berkeley data from 01/01/2018 to 12/31/2022
│   ├── berkeley_25_years.csv                  # Historical Berkeley data used for model training
│   └── clean_seattle_berkeley_weather.csv     # Clean data             
├── code/                                    # Jupyter notebooks and Python scripts
│   └── Weather_Data.ipynb                     # Main notebook
├── reports/                                 # Generated reports and visualizations
├── requirements.txt                         # Dependencies
└── README.md                                # Project documentation
```

---

## Data

- **Source:** NOAA National Centers for Environmental Information (NCEI), Global Historical Climatology Network Daily (GHCN-Daily)
- Source Link: https://www.ncei.noaa.gov/cdo-web/search?datasetid=GHCND
- Main Analysis Period: 2018–2022
- Historical Berkeley Data: 1998–2017 used to help estimate missing Berkeley precipitation values.
- Clean Dataset: 3,652 city-day observations representing 1,826 days for both Seattle and Berkeley.
  
- **Description:** The main variables used in the cleaned dataset are:
- date: observation date
- city: SEA for Seattle and BER for Berkeley
- precipitation: daily precipitation in inches
- day_of_year: day number within the year

---

## Analysis

The main analysis is contained in:

code/Weather_Data.ipynb

Major steps included:

- Cleaning and combining daily precipitation records

- Estimating missing precipitation values

- Comparing overall and monthly precipitation patterns

- Comparing seasonal precipitation totals

- Using statistical tests to evaluate differences between Seattle and Berkeley

Berkeley had several long periods of missing data, so historical precipitation patterns were used to estimate missing observations. Seattle's smaller number of missing observations was estimated using average precipitation for the corresponding day of the year.

---

## Results

The analysis found that:

- Seattle averaged approximately 0.113 inches of precipitation per day, compared with 0.053 inches in Berkeley.

- Monthly precipitation differed significantly between the cities in most months.

- Seasonal precipitation differed significantly during winter, summer, and fall.

- Berkeley received very little precipitation during summer compared with Seattle.

Overall, the results support the conclusion that it rains more in Seattle than in Berkeley.

---

## Project Files

All data preparation, missing-value imputation, exploratory analysis, visualization, and statistical testing are performed in:

- [`code/Weather_Data.ipynb`](code/Weather_Data.ipynb)

Clean dataset:

- [`data/clean_seattle_berkeley_weather.csv`](data/clean_seattle_berkeley_weather.csv)

Final communication report:

- [`reports/Weather_Reports.pdf`](reports/Weather_Reports.pdf)

---

## Authors

- [@PatrickPhan](https://github.com/tphan356/weather)

---

## License

This project is licensed under the MIT License

---

## Requirements

This project was developed in Python using Jupyter Notebook. The main libraries used are:

- pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy
- scikit-learn
- statsmodels

All required Python packages are listed in:

`requirements.txt`

---
## Acknowledgements

- NOAA National Centers for Environmental Information (NCEI)
- Python
- pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy
- statsmodels
- scikit-learn
