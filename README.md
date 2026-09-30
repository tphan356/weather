# Project Title

This project comprares precipitation in Seattle, WA, and Berkeley, CA, from Jan 1 2018 to Dec 31 2022

---

## Project Overview


- **Objective:** Compare precipitation between Seattle, WA and Berkeley, CA
- **Domain:** Weather
- **Key Techniques:** Data Processing

---

## Project Structure

```
├── data/                 # Raw and processed data
├── code/                 # Jupyter notebooks and Python scripts
├── reports/              # Generated reports and visualizations
├── requirements.txt      # Dependencies
└── README.md             # Project documentation
```

---

## Data

- **Source:** https://www.ncei.noaa.gov/cdo-web/search?datasetid=GHCND
- **Description:** Dataset include 3 features DATE, city, precipitation and 3652 rows
- **License:** (if applicable)

### Data Preparation

The Seattle and Berkeley precipitation datasets were first loaded and explored for missing values and date ranges. The `DATE` columns were converted to datetime format. Only the `DATE` and `PRCP` columns were kept, and the two datasets were combined using an outer join so that all available dates from both cities were retained.

The combined data was reshaped into a tidy format with `date`, `city`, and `precipitation` columns. City values were renamed to `SEA` for Seattle and `BER` for Berkeley.

To handle missing precipitation values, a `day_of_year` column was created. Missing values for each city were replaced with the mean precipitation for the same day of the year across the available years. Berkeley still had one missing average for day 366, which was replaced with `0` because the precipitation values for the nearest days were also 0.

The data preparation is performed in:

`code/Weather_Data.ipynb`

The cleaned data file is:

`clean_seattle_berkeley_weather.csv`

---

## Analysis

The analysis compares precipitation patterns in Seattle, Washington and Berkeley, California from 2018 through 2022.

Exploratory data analysis includes:

Daily precipitation trends for both cities

Summary statistics for precipitation

Overall mean daily precipitation

Monthly precipitation distributions

Mean precipitation by month

Proportion of days with any precipitation

Monthly proportion of days with precipitation

Two statistical tests were also performed for each month.

First, a Welch's two-sample t-test was used to test whether the mean daily precipitation differed between Seattle and Berkeley.

[
H_0: \mu_{Seattle} = \mu_{Berkeley}
]

[
H_a: \mu_{Seattle} \neq \mu_{Berkeley}
]

Second, a two-proportion z-test was used to test whether the proportion of days with precipitation differed between the two cities.

[
H_0: p_{Seattle} = p_{Berkeley}
]

[
H_a: p_{Seattle} \neq p_{Berkeley}
]

A significance level of (\alpha = 0.05) was used for both tests.

All data preparation, exploratory analysis, visualization, and statistical testing are performed in:

code/Weather_Data.ipynb

---

## Results

The analysis shows clear differences in precipitation patterns between Seattle and Berkeley.

For mean daily precipitation, the Welch's t-tests found statistically significant differences between the cities in every month except March at the 0.05 significance level.

The two-proportion z-tests produced a similar result. The proportion of days with precipitation was significantly different between Seattle and Berkeley in every month except March.

These results suggest that Seattle and Berkeley generally have different precipitation patterns throughout the year, both in the amount of precipitation and in how frequently precipitation occurs. March was the only month where the analysis did not find sufficient evidence of a difference between the cities for either measure.

---

## Authors

- [@PatrickPhan](https://github.com/tphan356/weather)

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgements

- Tools/libraries used
- Tutorials or papers referenced
- Inspiration or collaborators
