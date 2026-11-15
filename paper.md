# Air-Pollution Inequality Across London, United Kingdom:  
Spatial Differences in PM2.5 Exposure among Socioeconomically Different Urban Environments

## Research Questions

**RQ1.** How did annual mean PM2.5 exposure vary spatially across London LSOAs in 2019, and did statistically significant spatial clusters occur?  

**RQ2.** Did annual mean PM2.5 exposure differ systematically across socioeconomic deprivation levels after population distribution was considered?  

**RQ3.** Did the deprivation-exposure association persist after spatial dependence was addressed, and how well did LAEI 2019 modeled concentrations agree with independent UK-AIR PM2.5 observations?

---

# CHAPTER THREE: METHODOLOGY

This study used a cross-sectional ecological design to examine spatial inequality in annual mean fine particulate matter (PM2.5) exposure across Greater London in 2019. The 2011 Lower-layer Super Output Area (LSOA) was chosen as the analytical unit because it provides a stable neighbourhood geography for linking modelled pollution, deprivation, population and spatial boundaries.

Five datasets were integrated:

| Dataset                              | Spatial/temporal unit      | Variables retained              | Analytical role              |
|--------------------------------------|----------------------------|---------------------------------|------------------------------|
| LAEI 2019 Concentrations             | 20 m grid, 2019            | Annual mean PM2.5 (µg/m³)       | Primary exposure surface     |
| English Indices of Deprivation 2019  | LSOA, 2019                 | IMD score, rank, decile         | Socioeconomic inequality     |
| ONS Mid-2019 LSOA Population         | LSOA, 2019                 | Usual resident population       | Population weighting         |
| London 2011 LSOA Boundaries          | LSOA polygons              | LSOA code and geometry          | Spatial join, mapping, weights |
| UK-AIR 2019                          | Hourly monitoring sites    | Observed PM2.5, data capture    | Independent validation       |

All spatial layers were transformed to British National Grid (EPSG:27700). Annual mean PM2.5 for each LSOA was calculated as the arithmetic mean of all 20 m LAEI cells whose centroids fell inside the LSOA polygon.

---

# CHAPTER FOUR: ANALYSIS AND DISCUSSION

### 4.1 Descriptive Exposure Statistics

| Metric                        | Value                  |
|-------------------------------|------------------------|
| Complete LSOAs                | 4,835                  |
| Unweighted mean PM2.5         | 5.054 µg/m³            |
| Population-weighted mean PM2.5| 5.165 µg/m³            |
| Median PM2.5                  | 4.343 µg/m³            |
| Interquartile range           | 2.227 µg/m³            |
| Minimum / Maximum             | 1.522 / 43.381 µg/m³   |
| Global Moran’s I              | 0.7413 (p = 0.0001)    |

---

### 4.2 Spatial Distribution of PM2.5

**Figure 4.1** shows the spatial distribution of annual mean PM2.5 across London LSOAs in 2019.

![Figure 4.1: Annual mean PM2.5 by London LSOA, 2019](figures/figure_4_1_pm25_map.png)

*Figure 4.1: Annual mean PM2.5 exposure by London LSOA, 2019. Higher concentrations are concentrated in central and inner London areas.*

Global Moran’s I was 0.7413 (p = 0.0001), indicating strong positive spatial clustering. The sensitivity analysis using eight-nearest-neighbour weights produced a value of 0.5611.

---

### 4.3 Local Indicators of Spatial Association (LISA)

**Figure 4.2** presents the Local Moran clusters.

![Figure 4.2: Local Moran clusters of PM2.5](figures/figure_4_2_local_moran.png)

*Figure 4.2: Local Moran clusters of PM2.5 exposure across London LSOAs, 2019 (9,999 permutations, p < 0.05).  
High-high clusters = 145 | Low-low clusters = 196 | High-low = 0 | Low-high = 7.*

---

### 4.4 Socioeconomic Gradient in PM2.5 Exposure

**Table 4.2** and the two figures below show the clear decline in PM2.5 exposure from the most deprived to the least deprived areas.

| IMD Decile | Number of LSOAs | Population   | Unweighted mean | Population-weighted mean | Median  |
|------------|------------------|--------------|-----------------|---------------------------|---------|
| 1 (Most deprived) | 107     | 183,727     | 5.900           | **5.793**                 | 5.330   |
| 2          | 688              | 1,276,188    | 5.916           | 6.004                     | 5.114   |
| 3          | 811              | 1,615,929    | 5.526           | 5.603                     | 4.930   |
| 4          | 661              | 1,290,596    | 5.376           | 5.481                     | 4.719   |
| 5          | 559              | 1,061,353    | 4.996           | 5.055                     | 4.285   |
| 6          | 532              | 985,705      | 5.021           | 5.126                     | 4.245   |
| 7          | 438              | 787,966      | 4.501           | 4.594                     | 3.916   |
| 8          | 413              | 720,774      | 4.599           | 4.712                     | 3.902   |
| 9          | 407              | 683,676      | 3.913           | 3.993                     | 3.503   |
| 10 (Least deprived) | 219   | 356,075      | 3.528           | **3.580**                 | 3.182   |

**Figure 4.3** – Distribution of annual mean PM2.5 across IMD deciles.

![Figure 4.3: PM2.5 distribution by IMD decile](figures/figure_4_3_pm25_by_imd_decile.png)

*Figure 4.3: Distribution of annual mean PM2.5 across Index of Multiple Deprivation deciles.*

**Figure 4.4** – Population-weighted mean PM2.5 by IMD decile.

![Figure 4.4: Population-weighted PM2.5 by IMD decile](figures/figure_4_4_population_weighted.png)

*Figure 4.4: Population-weighted annual mean PM2.5 by IMD decile, showing a clear declining gradient from most to least deprived areas.*

- Absolute difference (Decile 1 vs Decile 10): **2.213 µg/m³**  
- Exposure ratio: **1.618**  
- Spearman correlation (IMD score vs PM2.5): **0.3274** (p < 0.0001)

---

### 4.5 Spatial Regression Results

| Model              | IMD coefficient | Spatial parameter | Model fit / diagnostic              |
|--------------------|-----------------|-------------------|-------------------------------------|
| OLS (HC3 SE)       | 0.0578          | —                 | R² = 0.0831; Residual Moran = 0.7028 |
| Spatial Lag        | 0.0339          | ρ = 0.4755        | AIC = 11,359.79                     |
| Spatial Error      | 0.0411          | λ = 0.4776        | AIC = 11,396.49                     |

The positive association between deprivation and PM2.5 remained after accounting for spatial dependence.

---

### 4.6 Model Validation against UK-AIR

**Figure 4.5** compares observed and modelled annual mean PM2.5.

![Figure 4.5: Observed vs Modelled PM2.5](figures/figure_4_5_validation_scatter.png)

*Figure 4.5: Observed UK-AIR versus modelled LAEI 2019 annual PM2.5 at five monitoring sites.*

| Site                        | Environment          | Observed | LAEI   | Bias    |
|----------------------------|----------------------|----------|--------|---------|
| London Marylebone Road     | Urban traffic        | 14.348   | 79.136 | +64.788 |
| London Harlington          | Urban industrial     | 9.538    | 3.225  | –6.313  |
| London Teddington Bushy Park | Urban background   | 11.822   | 2.821  | –9.001  |
| London Bloomsbury          | Urban background     | 10.751   | 10.690 | –0.060  |
| London Honor Oak Park      | Urban background     | 9.933    | 3.761  | –6.172  |

Background-only MAE = 5.387 µg/m³, RMSE = 6.304 µg/m³ (after excluding Marylebone Road).

---

# CHAPTER FIVE: CONCLUSION

The analysis shows clear spatial inequality in modelled ambient PM2.5 across London in 2019. Higher exposure was concentrated in more deprived neighbourhoods, and this pattern persisted after spatial dependence was accounted for. Validation against UK-AIR indicated variable performance by site type, so results should be interpreted as inequality in modelled ambient concentrations.

**Key numbers:**
- Population-weighted mean: 5.165 µg/m³  
- Most deprived decile: 5.793 µg/m³  
- Least deprived decile: 3.580 µg/m³  
- Global Moran’s I: 0.7413 (p = 0.0001)