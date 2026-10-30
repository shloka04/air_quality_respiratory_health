# Air Quality and Respiratory Health in Indian Cities

India contains some of the most polluted cities on earth. So when I lined up four years of air quality measurements against respiratory disease rates across 29 states, I expected the dirtiest states to carry the heaviest disease burden.

They didn't. The correlation came out **negative**. Delhi, averaging 101 µg/m³ of PM2.5, reports 4.4% chronic respiratory prevalence. Kerala, at 32 µg/m³ — one of the cleanest states in the country — reports the highest prevalence at 7.0%.

Working out why that happens, and what it takes to make the real signal visible, is what this project is about.

## The dataset

**703 city-years. 258 cities. 29 states and union territories. January 2020 to December 2023.**

Daily Central Pollution Control Board measurements of PM2.5, PM10, NO2, SO2 and O3, alongside temperature, humidity, wind speed and direction, aggregated to annual city means. Only city-years with valid readings for all five pollutants were retained. These are joined to state-level respiratory prevalence and mortality from the Global Burden of Disease 2023 study.

| File | Contents |
|---|---|
| `data/CPCB_city_year_2020-2023.csv` | Annual city-level pollutant and weather means, with the Multi-Pollutant Health Index |
| `data/Merged_dataset_full.csv` | The same, joined to GBD 2023 respiratory prevalence and mortality |

## The Multi-Pollutant Health Index

India's National Air Quality Index reports whichever single pollutant is worst on a given day. That suits daily public advisories, but it discards information when the question is long-term exposure, where several pollutants act together over years.

The Multi-Pollutant Health Index instead combines all five pollutants, weighted against World Health Organization guideline values so that each contributes in proportion to its documented chronic health risk. Northern cities score highest on it, southern cities lowest.

I tested whether the weighting was doing real work or just adding complexity. Across all 703 city-years the index correlates at **r = 0.998** with a naive equal-weighted index and **r = 0.996** with one placing all weight on particulate matter. The pollutants co-vary so strongly across Indian cities that the weighting scheme barely matters — a negative result about my own method, and worth reporting.

## Why the correlation came out backwards

Two things drive it, and neither is pollution protecting anyone.

**Age structure.** Chronic respiratory disease accumulates with age. States with older populations record more of it regardless of air quality.

**Diagnosis.** You can only count the disease that gets found. Kerala has among the strongest healthcare reporting in India; Bihar does not. Crude prevalence partly measures how thoroughly a state looks for illness.

Age-standardising the outcomes removes the first of these, and the association flips to the expected positive direction. It is clearest for age-standardised respiratory **mortality** — the measure least sensitive to diagnostic completeness, since deaths get recorded whether or not the underlying disease was ever diagnosed.

| Outcome measure | Correlation with the index |
|---|---|
| Crude all-ages prevalence | r = −0.21 |
| Age-standardised mortality | r = +0.21 |

Neither reaches significance at α = 0.05 with 29 states, and I report them as such. With this few units and this much confounding, the informative result is the **direction reversing under age-standardisation**, not the magnitude of either coefficient.

That reversal is the finding. The relationship between pollution and respiratory health in ecological data depends entirely on which outcome you measure and whether you adjust for age — and a study that skipped that step could report either direction and look convincing.

## Repository contents

```
data/      the two datasets described above
figures/   figures and tables from the manuscript
paper/     the full write-up
```

## Sources

Air quality: Central Pollution Control Board, Government of India. Respiratory health: Global Burden of Disease Study 2023, Institute for Health Metrics and Evaluation. Guideline values: WHO Global Air Quality Guidelines.

This is an ecological study at state level. It identifies associations, not causes, and the usual limits on ecological inference apply.
