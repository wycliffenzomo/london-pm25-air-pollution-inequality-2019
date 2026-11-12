# Air-Pollution Inequality Across London, United Kingdom: Spatial Differences in PM2.5 Exposure among Socioeconomically Different Urban Environments

## Research Questions

**RQ1.** How did annual mean PM2.5 exposure vary spatially across London LSOAs in 2019, and did statistically significant spatial clusters occur?

**RQ2.** Did annual mean PM2.5 exposure differ systematically across socioeconomic deprivation levels after population distribution was considered?

**RQ3.** Did the deprivation-exposure association persist after spatial dependence was addressed, and how well did LAEI 2019 modeled concentrations agree with independent UK-AIR PM2.5 observations?

---

# CHAPTER THREE: METHODOLOGY

This study used a cross-sectional ecological design to examine spatial inequality in annual mean fine-particulate matter (PM2.5) exposure across Greater London in 2019. The 2011 Lower-layer Super Output Area (LSOA) was selected as the analytical unit because it provides a stable neighbourhood geography for linking modelled pollution, deprivation, population and spatial boundaries. The design focused on unequal environmental exposure between neighbourhoods rather than individual dose. Python was used for data acquisition, statistical modelling and figure export to ensure reproducibility.

Five datasets were integrated:

| Dataset | Spatial/temporal unit | Variables retained | Analytical role |
|---------|-----------------------|--------------------|-----------------|
| LAEI 2019 Concentrations | 20 m grid, 2019 | Annual mean PM2.5 (µg/m³) | Primary exposure surface |
| English Indices of Deprivation 2019 | LSOA, 2019 | IMD score, rank, decile | Socioeconomic inequality |
| ONS Mid-2019 LSOA Population | LSOA, 2019 | Usual resident population | Population weighting |
| London 2011 LSOA Boundaries | LSOA polygons | LSOA code and geometry | Spatial join, mapping, weights |
| UK-AIR 2019 | Hourly monitoring sites | Observed PM2.5, data capture | Independent validation |

All spatial layers were transformed to British National Grid (EPSG:27700). The LAEI concentration archive was processed in chunks. Grid-point coordinates were converted to point geometry and spatially joined to LSOA polygons. The arithmetic mean of all 20 m LAEI cells whose centroids fell within each polygon was calculated to produce the annual mean PM2.5 for every LSOA.

IMD 2019 and the exposure table were joined using the LSOA code and then linked to the mid-2019 population estimates. Duplicate identifiers, unmatched records, missing exposure values and invalid population values were checked before analysis.

### Spatial Analysis (RQ1)

Maximum, minimum, standard deviation, interquartile range and median were calculated together with unweighted and population-weighted London-wide PM2.5 means. A choropleth map displayed LSOA-level exposure. Spatial autocorrelation was assessed with Global Moran’s I using first-order Queen contiguity weights and 9,999 permutations. Local Moran’s I classified statistically significant high-high, low-low, high-low and low-high clusters at p < 0.05. A sensitivity analysis repeated Global Moran’s I using eight-nearest-neighbour weights.

### Inequality Analysis (RQ2)

Deprivation was examined using IMD deciles (1 = most deprived, 10 = least deprived) and continuous IMD score and rank. Population-weighted PM2.5 was calculated within each deprivation decile. The most and least deprived deciles were compared using absolute difference, exposure ratio, Welch’s t-test and Mann-Whitney U test. Spearman’s rank correlation assessed the monotonic association between PM2.5 and continuous deprivation measures.

### Spatial Regression and Validation (RQ3)

Ordinary least squares (OLS) regression estimated the association between annual mean PM2.5 and IMD score while adjusting for the logarithm of LSOA population. Heteroskedasticity-consistent HC3 standard errors were used. Moran’s I was calculated on the OLS residuals. Where residual spatial dependence remained, maximum-likelihood spatial-lag and spatial-error models were estimated. Model coefficients, spatial parameters, log-likelihood and information criteria were compared.

UK-AIR hourly PM2.5 observations for 2019 were cleaned and annual site means calculated after quantifying data capture. LAEI values were extracted at the nearest 20 m grid location to each station. Agreement was summarised using mean bias, mean absolute error (MAE), root mean square error (RMSE) and Pearson correlation. Metrics were also recalculated after excluding the Marylebone Road traffic site.

Software used: Python 3 with pandas, NumPy, GeoPandas, Pyogrio, Matplotlib, SciPy, Statsmodels, libpysal, esda and spreg.

---

# CHAPTER FOUR: ANALYSIS AND DISCUSSION

The analysis combined the 2019 LAEI PM2.5 concentration surface, the 2019 Index of Multiple Deprivation, mid-2019 LSOA population estimates, London LSOA boundary data and 2019 UK-AIR monitoring observations. The first four datasets were merged at the LSOA level. UK-AIR observations were kept separate for validation.

### Descriptive Exposure Statistics

| Metric | Value |
|--------|-------|
| Complete LSOAs | 4,835 |
| Unweighted mean PM2.5 | 5.054 µg/m³ |
| Population-weighted mean PM2.5 | 5.165 µg/m³ |
| Median PM2.5 | 4.343 µg/m³ |
| Interquartile range | 2.227 µg/m³ |
| Minimum / Maximum | 1.522 / 43.381 µg/m³ |
| Global Moran’s I | 0.7413 (p = 0.0001) |

Global Moran’s I of 0.7413 (p = 0.0001) indicated strong positive spatial clustering. The eight-nearest-neighbour sensitivity statistic was 0.5611. Local Moran analysis identified 145 high-high, 196 low-low, 0 high-low and 7 low-high significant clusters (p < 0.05).

### Socioeconomic Gradient

Population-weighted mean PM2.5 declined from 5.793 µg/m³ in the most deprived decile to 3.580 µg/m³ in the least deprived decile (absolute difference = 2.213 µg/m³; ratio = 1.618).

Spearman correlation between IMD score and PM2.5 was 0.3274 (p < 0.0001). Correlation with IMD rank was –0.3274 (p < 0.0001). Welch’s t-test comparing the most and least deprived deciles produced t = 7.436 (p < 0.0001); Mann-Whitney U = 20,039 (p < 0.0001).

### Spatial Regression Results

| Model | IMD coefficient | Spatial parameter | Model fit / diagnostic |
|-------|-----------------|-------------------|------------------------|
| OLS with HC3 SE | 0.0578 | — | R² = 0.0831; residual Moran = 0.7028 |
| Spatial lag | 0.0339 | ρ = 0.4755 | AIC = 11,359.79 |
| Spatial error | 0.0411 | λ = 0.4776 | AIC = 11,396.49 |

The deprivation association remained positive and statistically significant after accounting for spatial dependence.

### UK-AIR Validation

| Site | Environment | Observed PM2.5 | LAEI PM2.5 | Bias |
|------|-------------|----------------|------------|------|
| London Marylebone Road | Urban traffic | 14.348 | 79.136 | +64.788 |
| London Harlington | Urban industrial | 9.538 | 3.225 | –6.313 |
| London Teddington Bushy Park | Urban background | 11.822 | 2.821 | –9.001 |
| London Bloomsbury | Urban background | 10.751 | 10.690 | –0.060 |
| London Honor Oak Park | Urban background | 9.933 | 3.761 | –6.172 |

Background-only MAE was 5.387 µg/m³ and RMSE was 6.304 µg/m³ after excluding the Marylebone Road site.

### Interpretation

The results demonstrate clear spatial inequality in modelled ambient PM2.5 across London in 2019. Higher exposure was concentrated in more deprived neighbourhoods, and this pattern persisted after spatial dependence was modelled. Validation against UK-AIR showed variable agreement by site type, limiting interpretation to modelled ambient concentrations rather than personal exposure.

---

# CHAPTER FIVE: CONCLUSION, LIMITATIONS AND PUBLICATION IMPLICATIONS

## 5.1 Conclusion

Citywide unweighted mean PM2.5 was 5.054 µg/m³ and population-weighted mean was 5.165 µg/m³. Strong spatial clustering was present (Global Moran’s I = 0.7413, p = 0.0001). Population-weighted exposure fell from 5.793 µg/m³ in the most deprived decile to 3.580 µg/m³ in the least deprived decile. The positive association with deprivation remained after spatial lag and spatial error models. Independent monitoring comparison showed site-specific variation in agreement.

## 5.2 Achievement of Research Questions

- **RQ1** was answered by the exposure distribution, Global Moran’s I and Local Indicators of Spatial Association (LISA) map.  
- **RQ2** was answered by decile summaries, population weighting, continuous correlations and group comparisons.  
- **RQ3** was answered by spatial-model sensitivity analysis and UK-AIR validation.

## 5.3 Limitations

The design is ecological and cross-sectional. LAEI concentrations are modelled outdoor annual means, not personal dose. IMD is an area-level index. LSOA aggregation smooths near-source gradients. The validation network is small. Spatial weights represent statistical dependence rather than atmospheric transport. The single-year design prevents inference about temporal change.

## 5.4 Key Publication Contribution

The main contribution is the integration of a 20 m final-LAEI exposure surface with LSOA deprivation, population weighting, explicit spatial autocorrelation, spatial regression and independent monitor validation in one reproducible workflow. The study tests whether fine-resolution ambient exposure inequality remains visible after population distribution and spatial dependence are explicitly treated, and incorporates model validation into the inequality argument.

---

## References

Anselin, L. (1995). Local indicators of spatial association—LISA. *Geographical Analysis*, 27(2), 93–115.

Ferguson, L., et al. (2021). Systemic inequalities in indoor air pollution exposure in London, UK. *Buildings & Cities*, 2(1), 425–448.

Ferguson, L., et al. (2023). Analysis of inequalities in personal exposure to PM2.5. *Science of the Total Environment*, 905, 167056.

Gohlke, J. M., et al. (2023). State-of-the-science data and methods need to guide place-based efforts to reduce air pollution inequity. *Environmental Health Perspectives*, 131(12), 125003.

Goodman, A., et al. (2011). Characterising socio-economic inequalities in exposure to air pollution. *Health & Place*, 17(3), 767–774.

Gray, N. R., et al. (2024). Evaluating disparities in air pollution as a function of ethnicity, deprivation and sectoral emissions in England. *Environment International*, 194, 109146.

Rivas, I., et al. (2017). Exposure to air pollutants during commuting in London. *Environment International*, 101, 143–157.

Tonne, C., et al. (2018). Socioeconomic and ethnic inequalities in exposure to air and noise pollution in London. *Environment International*, 115, 170–179.

### Official data sources

- Greater London Authority (2023). London Atmospheric Emissions Inventory 2019.  
- Ministry of Housing, Communities and Local Government (2019). English Indices of Deprivation 2019.  
- Office for National Statistics (2020). Lower layer Super Output Area mid-year population estimates: Mid-2019.  
- UK Department for Environment, Food & Rural Affairs (2019). UK-AIR monitoring data.