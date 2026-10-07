# Seattle vs. Berkeley Precipitation Analysis

---

## Project Overview

This project investigates whether it rains more in Seattle, Washington than in Berkeley, California. Daily precipitation data from NOAA were analyzed from 2018 through 2022. Missing observations were cleaned and imputed using historical precipitation patterns, and the two cities were compared using daily, monthly, and seasonal analyses. The results show that Seattle generally receives more precipitation than Berkeley, with especially large differences during summer, fall, and winter.

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


### Data Preparation

The Seattle and Berkeley precipitation datasets were first loaded and inspected for data types, date ranges, missing values, and available columns.
The DATE columns were converted to datetime format. Only the date and precipitation variables were needed for the main analysis.
The Seattle and Berkeley datasets were combined using an outer join so that all available dates were retained. A complete daily date range from January 1, 2018 through December 31, 2022 was then created to ensure that all 1,826 calendar days were represented.
The combined dataset was reshaped into tidy long format with one observation per city per day. The columns were renamed using clear lowercase names, and the city values were renamed:
- SEA = Seattle
- BER = Berkeley

#### Missing Berkeley Data

Berkeley contained 471 missing precipitation values between 2018 and 2022. Many of these values occurred in long consecutive blocks, making a simple average across the five-year period unreliable.
An ARIMA model was first evaluated for imputation. Although ARIMA performed reasonably for short-term prediction, its predictions became nearly constant during long missing periods and did not preserve Berkeley's strong seasonal precipitation pattern.
A K-Nearest Neighbors (KNN) regression model was therefore selected for the final Berkeley imputation.
Historical Berkeley precipitation data were divided into:
- Training: 1998–2013
- Testing: 2014–2017
- Target period: 2018–2022
Cyclical sine and cosine features based on the day of the year were used so that the KNN model could learn Berkeley's repeating annual precipitation pattern.
The KNN test results were:
- MAE: 0.1171 inches
- RMSE: 0.2915 inches
Although the KNN model had slightly higher MAE and RMSE than ARIMA, it better preserved the annual seasonal pattern during long periods of missing data. The final KNN model was retrained using historical observations from 1998 through 2017 and used only to replace missing Berkeley values. Original observed values were kept unchanged.

#### Missing Seattle Data

Seattle contained fewer missing values. These were replaced using the mean precipitation for the corresponding day of the year across the available five-year period.
After imputation, the cleaned dataset contained no missing precipitation values.
The data preparation and analysis are performed in:
code/Weather_Data.ipynb
The cleaned data file is:
data/clean_seattle_berkeley_weather.csv

#### Exploratory Data Analysis

The analysis compares precipitation patterns in Seattle and Berkeley using several approaches:
- Daily precipitation trends
- Summary statistics
- Overall mean daily precipitation
- Monthly precipitation distributions
- Mean daily precipitation by month
- Proportion of days with precipitation
- Seasonal precipitation totals by year
- Statistical comparisons of monthly and seasonal precipitation
Seattle had a higher overall mean daily precipitation:
- Seattle: approximately 0.113 inches per day
- Berkeley: approximately 0.053 inches per day
Berkeley generally receives very little precipitation during the summer, while Seattle continues to receive some precipitation throughout the summer months.

---

## Analysis

The full data preparation and analysis workflow is contained in `code/Weather_Data.ipynb`. The analysis included cleaning and combining the datasets, handling missing precipitation values, exploring daily, monthly, and seasonal precipitation patterns, and performing statistical tests to compare Seattle and Berkeley.

### Monthly Precipitation

A Welch's two-sample t-test was performed separately for each month to test whether mean daily precipitation differed between Seattle and Berkeley.

For each month:

$$
H_0: \mu_{\text{Seattle}} = \mu_{\text{Berkeley}}
$$

$$
H_a: \mu_{\text{Seattle}} \neq \mu_{\text{Berkeley}}
$$

A significance level of $\alpha = 0.05$ was used.

The results showed statistically significant differences in mean precipitation for every month except March and April.

### Seasonal Precipitation

Total precipitation was calculated for winter, spring, summer, and fall for each year. A paired t-test was used because Seattle and Berkeley seasonal totals were paired by year.

For each season:

$$
H_0: \mu_{\text{Seattle}} = \mu_{\text{Berkeley}}
$$

$$
H_a: \mu_{\text{Seattle}} \neq \mu_{\text{Berkeley}}
$$

| Season | Seattle Mean | Berkeley Mean | p-value | Significant |
|---|---:|---:|---:|:---:|
| Winter | 19.10 in | 9.62 in | 0.044 | Yes |
| Spring | 7.92 in | 5.92 in | 0.369 | No |
| Summer | 2.95 in | 0.06 in | 0.001 | Yes |
| Fall | 11.40 in | 3.77 in | 0.011 | Yes |

Seattle received significantly more precipitation than Berkeley during winter, summer, and fall.
Spring was the only season where the difference was not statistically significant at the 0.05 level.
Berkeley also experienced an unusually wet winter in 2019, when its seasonal precipitation exceeded Seattle. This was an exception to the overall pattern and was associated with major Pacific storms and atmospheric river events affecting Northern California.

---

## Results

The analysis provides evidence that Seattle generally receives more precipitation than Berkeley.
Seattle's average daily precipitation was approximately 0.113 inches, compared with approximately 0.053 inches in Berkeley.
The monthly analysis found statistically significant differences between the cities in most months, with March and April as the exceptions.
The seasonal analysis also showed significant differences during winter, summer, and fall. The largest relative seasonal contrast occurred during summer, when Seattle averaged approximately 2.95 inches of precipitation compared with only 0.06 inches in Berkeley.
Although Berkeley occasionally experienced unusually wet periods, the overall daily, monthly, and seasonal patterns support the conclusion that it rains more in Seattle than in Berkeley.

---

## Analysis Files

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
