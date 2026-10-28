# Air Quality and Respiratory Health in Indian Cities

India has some of the most polluted cities in the world, so you would expect the states with the worst air to carry the heaviest burden of respiratory disease. When I checked, the data said the opposite, and working out why turned out to be the interesting part of this project.

The study combines four years of air quality measurements from the Central Pollution Control Board with state-level respiratory disease estimates from the Global Burden of Disease 2023 study, and introduces a Multi-Pollutant Health Index that weights five pollutants against World Health Organization guideline values.

## The data

703 city-years, covering 258 cities across 29 states and union territories, from January 2020 to December 2023. Daily CPCB measurements of PM2.5, PM10, NO2, SO2 and O3, plus temperature, humidity, wind speed and wind direction, aggregated to annual city means. Only city-years with valid readings for all five pollutants were kept.

| File | Contents |
|---|---|
| `data/CPCB_city_year_2020-2023.csv` | Annual city-level pollutant and weather means, with the Multi-Pollutant Health Index |
| `data/Merged_dataset_full.csv` | The same, joined to state-level respiratory prevalence and mortality from GBD 2023 |

The health columns are `prev_allages_pct` and `prev_agestd_rate` for prevalence, and `mort_allages_rate` and `mort_agestd_rate` for mortality. Having both crude and age-standardised versions is what makes the central result visible.

## What I found

Crude respiratory prevalence is weakly **negatively** correlated with pollution across states (r = −0.21, p = 0.28, n = 29). Delhi, at roughly 101 µg/m³ PM2.5, reports 4.4% prevalence; Bihar at 93 µg/m³ reports 4.1%; Kerala, one of the cleanest states at 32 µg/m³, reports the highest prevalence at 7.0%.

That is not pollution protecting anyone. It reflects differences in population age structure and in how much respiratory disease actually gets diagnosed and recorded. Kerala has an older population and far better healthcare reporting than Bihar, so it finds more of the disease that is there.

Once outcomes are age-standardised, the association flips to the expected positive direction, and is clearest for age-standardised respiratory mortality (r = +0.21, p = 0.28). So the sign of the relationship depends on which outcome you use and whether you adjust for age — which is the main thing this project demonstrates.

Neither correlation reaches statistical significance at n = 29 states. With that few units and this much confounding, the honest reading is that the direction of the effect is informative and the magnitude is not.

The index itself is robust to how it is weighted. Across all 703 city-years it correlates at r = 0.998 with an equally weighted index and r = 0.996 with one that puts all the weight on particulate matter, because the pollutants move together so strongly.

## What's here

```
data/      the two datasets described above
figures/   figures and tables from the manuscript
paper/     the full write-up
```

## What's not here

The analysis scripts aren't in this repository. The datasets and the manuscript are the complete record of the work; the processing and plotting code was written in a working environment I no longer have in a runnable state, so rather than publish something that won't execute, I've left it out. The data is here, and every number in the write-up can be recomputed from it.

## Sources

Air quality: Central Pollution Control Board, Government of India. Respiratory health: Global Burden of Disease Study 2023, Institute for Health Metrics and Evaluation. Pollutant guideline values: World Health Organization Global Air Quality Guidelines.

This is a student research project and an ecological study at state level. It cannot establish causation, and the usual caveats about ecological inference apply.
