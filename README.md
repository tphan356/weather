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

Describe the notebooks and/or scripts used to perform the analysis. Specify the order in which the code should be run to reproduce the results.

---

## Results

Include a short discussion of the findings and what they imply.

---

## Authors

- Your Name - [@PatrickPhan](https://github.com/tphan356/weather)

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgements

- Tools/libraries used
- Tutorials or papers referenced
- Inspiration or collaborators
