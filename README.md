# Mobile Device Activity in Yogyakarta

Exploratory analysis of how mobile-device activity relates to population across the
subdistricts (*kapanewon*) of Yogyakarta, and whether weekday vs. weekend patterns tell us
more about mobility.

**Research questions**

1. Do subdistricts with a larger population have more assigned home devices?
2. Does comparing weekend and weekday device activity in each subdistrict explain more about mobility?

> All findings are interpretations of the data analysed here. Association is not causation.

## Data

- BPS 2021 population
- JogjaPulse home-device assignments (Dec 2021 - Apr 2022) and December 2021 hourly presence

The workbook is expected at `data/yogyakarta_complete_comparison.xlsx` (see [`data/README.md`](data/README.md)).

## Repository structure

```
yogyakarta-mobility-analysis/
├── main/
│   └── yogyakarta_mobility_analysis.ipynb   # full analysis
├── figures/                                 # charts exported by the notebook
├── data/                                    # source Excel workbook goes here
├── requirements.txt
└── README.md
```

## How to run

```bash
git clone https://github.com/<your-username>/yogyakarta-mobility-analysis.git
cd yogyakarta-mobility-analysis
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab main/yogyakarta_mobility_analysis.ipynb
```

Running the notebook regenerates every chart into `figures/`.

## Key results

| Question | Result |
|---|---|
| 1. Population vs. assigned home devices (78 subdistricts) | Pearson r = 0.720, Spearman rho = 0.609, OLS R² = 0.519, slope ≈ 0.22 devices per person |
| Regression outliers (studentized residual > 2) | Depok, Ngaglik, Pakem (Sleman) and Gondomanan (Yogyakarta) |
| 2. Weekday vs. weekend presence (39 complete-coverage subdistricts) | Weekend mean is 7.37 devices lower on average (paired t-test p = 0.056, Wilcoxon p = 0.128) |
| Outlier residual vs. weekend change | Spearman rho = -0.426 (p = 0.007, n = 39), exploratory |

## Figures

| | |
|---|---|
| ![Population vs devices](figures/01_population_vs_devices.png) | ![Device-population ratios](figures/02_device_population_ratios.png) |
| ![Weekday vs weekend](figures/03_weekday_vs_weekend_scatter.png) | ![Weekend change by area](figures/04_weekend_change_by_area.png) |
| ![Hourly profiles](figures/05_hourly_normalized_profiles.png) | ![Outliers vs weekend change](figures/06_outliers_vs_weekend_change.png) |

## Limitations

- Assigned home devices do not necessarily represent the number of people or device ownership rates.
- Only 39 of 78 subdistricts have complete hourly coverage for the weekday/weekend comparison.
- Neighbouring areas and repeated hours may be dependent, so p-values are descriptive/exploratory.
- Different observation periods and non-random device sampling prevent causal claims.
