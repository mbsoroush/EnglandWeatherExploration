# 🌦️ England Weather Analysis

An exploratory data analysis (EDA) of **hourly weather records**, covering about ten years of temperature, wind speed, pressure, and humidity. The notebook cleans out physically impossible readings, then uses plots and correlations to see how humidity relates to the other measurements and how the data is spread over time.

![Python](https://img.shields.io/badge/Language-Python%203.9-3776AB?style=flat-square)
![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-F37626?style=flat-square)
![pandas](https://img.shields.io/badge/Library-pandas-150458?style=flat-square)
![Task](https://img.shields.io/badge/Task-EDA-6A5ACD?style=flat-square)

## 📦 Dataset

`EnglandWeather.csv` is included in this repository: **96,453 hourly records** from April 2006 to September 2016.

| Column | Description |
|--------|-------------|
| `Formatted Date` | Timestamp of the reading |
| `Summary` | Short weather description (27 categories, e.g. *Partly Cloudy*) |
| `Precip Type` | Type of precipitation: `rain` or `snow` |
| `Temperature (C)` | Temperature in °C |
| `Wind Speed (km/h)` | Wind speed in km/h |
| `Pressure (millibars)` | Atmospheric pressure in millibars |
| `Humidity` | Relative humidity (0 to 1) |

## 🧹 Data Cleaning

- Removed rows where `Wind Speed`, `Pressure`, or `Humidity` is **0**, since a pressure of 0 mbar is not physically possible (2,568 rows). This fixes the pressure range, which goes from a minimum of 0 to a realistic 973.8 to 1046.4 mbar.
- Removed rows with a missing `Precip Type` (517 rows).
- Result: **93,368 clean rows** with no missing values.

## 🔍 What the Notebook Explores

- **Humidity against** temperature, wind speed, pressure, and weather summary (scatter and bar plots)
- **Correlation heatmap** of the numeric features
- **Distributions:** weather summary counts, a humidity histogram, and a humidity box plot
- **Time analysis:** humidity over time, the number of records per year and per month, and average humidity per year

## 📌 Key Findings

| Pair | Correlation |
|------|:-----------:|
| Temperature and humidity | **−0.64** |
| Temperature and pressure | −0.31 |
| Wind speed and pressure | −0.25 |
| Wind speed and humidity | −0.22 |
| Pressure and humidity | 0.04 |
| Temperature and wind speed | 0.01 |

Humidity is mainly tied to temperature: warmer hours are clearly less humid. Pressure has almost no relationship with humidity.

## 📁 Repository Structure

```
EnglandWeather/
├── EnglandWeather.ipynb   # Cleaning, plots, correlations, time analysis
├── EnglandWeather.csv     # Hourly weather data
└── README.md
```

## 🚀 Getting Started

1. Clone the repository:
   ```bash
   git clone <this-repository-url>
   cd <repository-folder>
   ```
2. Install the dependencies (the notebook was run with Python 3.9):
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```
3. Open the notebook and change the data path in the first cells to the local file:
   ```python
   data = pd.read_csv('EnglandWeather.csv')
   ```
4. Launch Jupyter and run the cells in order:
   ```bash
   jupyter notebook EnglandWeather.ipynb
   ```

> With pandas 2.0 or newer, the heatmap cell needs `df.corr(numeric_only=True)`, because the table also has text columns.
