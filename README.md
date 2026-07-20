# Uber Pickups

> Mandatory project for **block 3** (Predictive analysis of structured data using
> artificial intelligence) of the French **CDSD certification** — Concepteur Développeur en Science
> des Données | RNCP35288 | JEDHA

Analysis of historical Uber pickup data in New York (2014) to identify **hotspots**—areas with the highest demand, hour by hour and day by day—and recommend them to drivers.<br>
Each row in the dataset represents a pickup.

## Problem statement

Uber aims to optimize its customer pickup process: if the wait exceeds 5 to 7 minutes, customers often end up cancelling their ride. The goal is to leverage past pickup data to identify **where** and **when** to position vehicles, using exploratory data analysis and unsupervised clustering.

## Installation

```bash
git clone https://github.com/geoffrey-madalinski/Projet_Uber.git
cd Projet_Uber
```

## Technical stack

- Python — Pandas, NumPy, scikit-learn (KMeans, DBSCAN, StandardScaler),
  plotly.express, Matplotlib

## Usage

```bash
jupyter notebook Projet-Uber_GM.ipynb
```

## Project structure

```
Projet_Uber/
├── data/
│   └── raw/
│       └── uber-raw-data-*14.csv     # 6 files (avr. → sept. 2014)
├── docs/
│   ├── 01-Uber_Pickups.ipynb         # project statement
├── notebooks/
│   └── Projet-Uber_GM.ipynb          # main notebook
├── reports/
│   └── figures/                      # data visualization
└── README.md
```

## Data

- **Source** : Uber pickup data for 2014 (April → September), ~4.5 million trips
- **Columns** : `Date/Time`, `Lat`, `Lon`, `Base` (renamed to `datetime`, `lat`, `lon`, `base`)
- **Granularity** : one raw = one hadling of a customer
- **Derived features** : `hour`, `dayofweek`, `dayname`, `month`

## Approach

1. **Data loading & preparation** — concatenating the 6 CSV files, converting dates,
extracting temporal features, checking for missing values
2. **Exploratory Data Analysis (EDA)** — pickups by hour and day, plus a cross-tabulated
day × hour heatmap to identify peak periods
3. **K-Means clustering** — initially on a specific peak (Friday at 6 PM), then
generalized to every day of the week to map activity centers (hot zones)
4. **DBSCAN clustering** — density-based approach without a fixed number of clusters,
handling noise and coordinate normalization
5. **K-Means vs. DBSCAN comparison** — summary table of strengths and limitations
6. **Conclusion** — summary and product recommendations

## Key findings

| Question | Key Finding |
|---|---|
| Peak demand times | Two peaks: morning (7–9 AM) and, most notably, 4–7 PM. |
| Peak demand days | Demand peaks on **Thursdays** and **Fridays**. |
| K-Means | 8 zones that remain stable from day to day (Midtown, Lower Manhattan, airports, train stations). |
| DBSCAN | One large cluster covering Manhattan + isolated pockets at the airports (JFK, LaGuardia, Newark). |
| K-Means vs. DBSCAN | Consistent and complementary results. |

> **Bottom line for Uber:** K-Means is best suited for generating the
> recommendation "here are the N zones to position yourself in today," while DBSCAN
> confirms that these zones correspond to genuine pockets of demand and allows for
> the detection of potential emerging zones.

## Author

**Geoffrey MADALINSKI** — Certification CDSD (RNCP35288) - JEDHA

---
