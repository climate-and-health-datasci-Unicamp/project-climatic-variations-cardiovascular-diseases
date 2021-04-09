# Exploratory Study of Correlations between Extreme Variations of Meteorological Parameters and Hospitalizations and Deaths due to Cardiovascular Diseases in Campinas, São Paulo

This project aims to assess the influence of variations of the climatic parameters on the number of hospitalizations and deaths in Campinas, SP.

## Abstract

The increase in the frequency and intensity of extreme weather events is considered one of the evidences and one of the most immediate effects of climate change on our planet. Such changes have a direct impact on human health. The study of the correlation between meteorological parameters and the occurrence of some diseases makes it possible to develop systems of resilience and adaptation to climate change, such as the development of health alert systems when the detection of an extreme weather event occurs. In this project, the objective is to study the correlation between extreme variations of meteorological parameters and hospitalizations and deaths associated with diseases of the circulatory system, through the analysis of meteorological and health databases in the city of Campinas. The KDD (Knowledge Discovery in Databases) model will be used as a data science guideline.

## Introduction

This project is part of the study of global climate change and its notorious impacts on human health [McMichael 2003, Campbell-Lendrum, Corvalán e Prüss–Ustün2003]. One of the more evident effects of climate change is the increased frequency and intensity of extreme climatic events [Seneviratne et al. 2012]. Understanding the health impact of these events is crucial to develop mitigation and adaptation strategies [Council et al. 2011]. Studying these events on a regional scale is essential, as their effects differ to factor such as phenotypic plasticity, access to technological resources, and socioeconomic aspects [Murray et al. 2020].

In this context, this project objective is to identify extreme variations of meteorological parameters in Campinas, São Paulo, and to study the existing correlations between those variations and health indicators. As a specific objective, this project aims to study the relationship between extreme climatic variations and the main cause of global death, cardiovascular diseases [World Health Organization]. In this work, cardiovascular diseases were considered as all events associated with codes from Chapter IX (Diseases of the circulatory system) from the International Classification of Diseases [World Health Organization 1993].

All databases used in this project were collected in the FAPESP project 17/20013-0, entitled "Human Health and Adaptation to Climate Change in Brazil: A Data Science Approach", with a project at the Committee for Ethics in Research (CEP) under CAAE 95503318.4.0000.5404.

## Data

|Database | Description|
|----- | ----- |
|Hospitalizations database (SSC - Health Secretary of Campinas)| Hospitalizations in Campinas from 2014 to 2018|
|Deaths database (SSC - Health Secretary of Campinas) | Deaths that occured in Campinas from 2001 to 2019|
|Viracopos| Daily values of minimum and maximum temperature, mean atmospheric pressure, minimum and maximum humidity from 1983 to 2018|

More information about the health data and its preprocessing can be found at the [data-health repository](https://github.com/climate-and-health-datasci-Unicamp/data-health).

## Extreme climatic events

A library of functions was developed to identify and compute the metrics of extreme climatic events is disponibilizes at [py-climate-health-toolbox](https://github.com/climate-and-health-datasci-Unicamp/py-climate-health-toolbox). The definition of these events is based on Geirinhas et al. 2018 methodology.

The analysed extreme events were:

- **Extreme thermal range:** days in which the thermal range is above the 90th percentile.
- **Extreme difference of temperature between days:** days in which the difference between maximum and minimum temperature in relation to the previous days is above the 90th percentile.
- **Low pressure waves:** three or more consecutive days in which the maximum and minimum pressure were below the 10th percentile.
- **High pressure waves:** three or more consecutive days in which the maximum and minimum pressure were above the 90th percentile.
- **Extreme difference of pressure between days:** days in which the difference between maximum and minimum pressure in relation to the previous days is above the 90th percentile.
- **Low humidity waves:** three or more consecutive days in which the maximum and minimum humidity were below the 10th percentile.
- **High humidity waves:** three or more consecutive days in which the maximum and minimum humidity were above the 90th percentile.   
- **Extreme difference of humidity between days:** days in which the difference between maximum and minimum humidity in relation to the previous days is above the 90th percentile.
- **Extreme humidity range:** days in which the humidity variation (max humidity - min humidity) is above the 90th percentile.

The occurence at these events in Campinas SP was analysed using Viracopos data for the time period of 2001 to 2018 and is available at [TR 03/2020](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-circulatory-diseases/blob/main/notebooks/TR_03_2020_Extreme_climatic_events_for_Campinas.ipynb). 
   
Occurence of extreme events in Campinas between 2001 and 2018
|Extreme event | Number of events| Total number of days | Longest event|
| ---------- |---------- |---------- |---------- |
|Extreme thermal range | 647 | 647  |  - |
|Extreme difference of temperature between days | 84 | 84  | -  |
|Low pressure waves | 65 | 261 | 8 |
|High pressure waves | 93 | 399 | 10 |
|Diferença extrema de pressão entre dias | 610 | 610 |  - |
|Low humidity waves | 35 | 160 | 16 |
|High humidity waves | 43 | 151 | 6 |
|Extreme humidity range | 900 | 900  | - |
|Extreme difference of humidity between days | 77 | 77  | -  |

## Association study

The influence of climatic parameters and extreme climatic events in the health of the population of Campinas was analysed using the Pearson correlations, comparing rate ratios and with the Mann-Whitney U test.

### Pearson correlation

Pearson correlation was used to analyse the correlation between month medians. The level of significance was 5%. This analysis is available at:

- [TR 02/2021](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-circulatory-diseases/blob/main/notebooks/TR_02_2021_Correlations_between_circulatory_hospitalizations_and_climatic_variables.ipynb): Pearson correlation between climatic variables and hospitalizations

|Climatic variable| Pearson coefficient| p value| Correlation|
|----------|----------|---------- |---------- |
|Minimum temperature(°C) |-0.73 |  0.0069 |  strong |
|Maximum temperature(°C) | -0.55 |  0.0627 |  -    |
|Thermal range (°C) |0.58 |  0.0458 |   moderate |
|Mean atmospheric pressure (HPA)| 0.76 |  0.0045 | strong |
|Minimum humidity(%) | -0.49 |  0.1037 |    - |
|Maximum humidity(%) | -0.34 |  0.2829 |  - |
|Humidity range(%) |0.54 |  0.0708 |     - |


- [TR 03/2021](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-circulatory-diseases/blob/main/notebooks/TR_03_2021_Correlations_between_circulatory_deaths_and_climatic_variables.ipynb): Pearson correlation between climatic variables and deaths

|Climatic variable| Pearson coefficient| p value| Correlation|
|----------|----------|---------- |---------- |
|Minimum temperature(°C) |  -0.91 |  0.0000  | very strong|
|Maximum temperature(°C) |   -0.76 |  0.0039 |  strong|
|Thermal range (°C) |   0.88 |  0.0002 |    strong |
|Mean atmospheric pressure (HPA) |   0.84 |  0.0006 | strong|
|Minimum humidity(%) |   -0.87 |  0.0002 | strong|
|Maximum humidity(%) |    -0.81 |  0.0014 | strong|
|Humidity range(%) |  0.88 |  0.0001 | strong|

### Rate ratios

Rate ratio is a relative difference measure used to compare the incidence rates of events occurring at any given point in time, frequently used in epidemiology. Rate ratios from days under extreme events effect and control days were compared. A rate ratio above 1.0 indicates an increased risk associated with that event. The analysis was conducted for the total data and for some stratifications (sex, age, age and sex, race) and is available at:

- [TR 04/2021](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-circulatory-diseases/blob/main/notebooks/TR_04_2021_Rate_ratio_for_circulatory_hospitalizations_and_extreme_events.ipynb): Rate ratio for extreme climatic events and hospitalizations

|Event| Rate ratio| Confidence interval|
|------|-----------|----------|
|Extreme thermal range | 0.96 | 0.89 - 1.03|
|**Extreme difference of temperature between days** | **1.16** | **1.00 - 1.35**|
|Low pressure waves | **1.09** | 0.98 - 1.22 |
|High pressure waves | 1.00 | 0.94 - 1.06 |
|Diferença extrema de pressão entre dias | **1.05** | **0.99 - 1.11** |
|Low humidity waves | 0.90 | 0.84 - 0.97|
|High humidity waves | **1.05** | 0.76 - 1.45|
|Extreme humidity range | **1.01** | 0.96 - 1.07  |
|Extreme difference of humidity between days | 0.96 | 0.81 - 1.13|

- [TR 05/2021](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-circulatory-diseases/blob/main/notebooks/TR_05_2021_Rate_ratio_for_circulatory_deaths_and_extreme_events.ipynb): Rate ratio for extreme climatic events and deaths

|Event| Rate ratio| Confidence interval|
|------|-----------|----------|
|Extreme thermal range | **1.01** | 0.98 - 1.04|
|Extreme difference of temperature between days | 0.89 | 0.82 - 0.96|
|Low pressure waves | 0.97 | 0.93 - 1.01 |
|High pressure waves | **1.01** | 0.98 - 1.05 |
|Diferença extrema de pressão entre dias | 1.00 | 0.97 - 1.03 |
|**Low humidity waves** | **1.09** | **1.03 - 1.15**|
|High humidity waves | 0.99 | 0.94 - 1.05|
|**Extreme humidity range** | **1.02**  | **1.00 - 1.04**  |
|Extreme difference of humidity between days | 0.98 | 0.91 - 1.06|

### Mann-Whitney U

Mann-Whitney U is a nonparametric test used to compare two distributions. The test was used to compare the distributions of hospitalizations/deaths between under extreme events effect and control days. The analysis was conducted for the total data and for some stratifications (sex, age, age and sex, race) and is available at:

- [TR 06/2021](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-circulatory-diseases/blob/main/notebooks/TR_06_2021_Mann_Whitney_U_test_for_circulatory_hospitalizations_and_extreme_climatic_events_.ipynb): Mann-Whitney U test for extreme climatic events and hospitalizations
- [TR 07/2021](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-circulatory-diseases/blob/main/notebooks/TR_07_2021_Mann_Whitney_U_test_for_circulatory_deaths_and_extreme_climatic_events.ipynb): Mann-Whitney U test for extreme climatic events and deaths

Women and elderly were the most affect by the extreme climatic events.

## Low humidity waves

The occurence of the extreme event of Low Humidity Waves (LHW), three or more consecutive days with both minimum and maximum humidity below the 10th percentile, was analysed for the city of Campinas, SP for the time period from 1983 to 2018. This event was analysed due to its impact on health.

The analysis revealed that low humidity waves are increasing in frequency, intensity and duration, and is available at [TR 01/2021](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-circulatory-diseases/blob/main/notebooks/TR_01_2021_Low_humidity_waves_analysis_for_Campinas.ipynb).

Yearly metrics of low humidity waves
|     |       |1983-1994|1995-2006|2007-2018|Total|
|:----:|------|----------|----------|---------- |---------- |
|LHWN | Metric<br>Mean value/year<br>Standard deviation | 3<br>0.25<br>0.62 | 17<br>1.42<br>1.24  | 30<br>2.5<br>3.23 | 50<br>1.39<br>2.18|
|LHWD |Metric<br>Mean value/year<br>Standard deviation  | 8<br>0.67<br>1.61 | 39<br>3.25<br>2.22 | 55<br>4.58<br>4.94 | 102<br>2.83<br>3.57|
|LHWF |Metric<br>Mean value/year<br>Standard deviation  | 11<br>0.92<br>2.39 | 65<br>5.42<br>4.4 | 139<br>11.58<br>16.05 | 215<br>5.97<br>10.42|

Trend analysis for low humidity waves
|   Metric  |Cox-Stuart test|Mann-Kendall test|Modified Mann-Kendall test|
|:---------:|---------------|-----------------|--------------------------|
|LHWN | Increasing<br>trend<br>p = 0.03271 | Slope = 0.032796<br>p = 0.00727<br>Positive trend | Slope = 0.03815<br>p = 0.008973<br>Positive trend  |
|LHWD | Increasing<br>trend<br> p = 0.04614 | Slope = 0.10913<br>p = 0.003737<br>Positive trend | & Slope = 0.10902<br>p = 0.007588<br>Positive trend | 
|LHWF |Increasing<br>trend<br>p = 0.04614  | Slope = 0.14286<br>p = 0.008177<br>Positive trend | Slope = 0.16758<br>p = 0.011012<br>Positive trend | 

## References

CAMPBELL-LENDRUM, D.; CORVALÁN, C.; PRÜSS–USTÜN, A. How much diseasecould climate change cause? In:Climate change and human health: risks and responses.[S.l.]: Geneva, World Health Organization, 2003. cap. 7.

COUNCIL, N. R. et al.Advancing the science of climate change. [S.l.]: National AcademiesPress, 2011.

GEIRINHAS, J. L. et al. Climatic and synoptic characterization of heat waves in brazil.International Journal of Climatology, Wiley Online Library, v. 38, n. 4, p. 1760–1776, 2018

MCMICHAEL, A. Global climate change and health: an old story writ large. In:Climatechange and human health: risks and responses. [S.l.]: Geneva, World Health Organization,2003. cap. 1

MURRAY, C. J. et al. Global burden of 87 risk factors in 204 countries and territories,1990–2019: a systematic analysis for the Global Burden of Disease Study 2019.The Lancet,Elsevier, v. 396, n. 10258, p. 1223–1249, 2020.

SENEVIRATNE, S. et al. Changes in climate extremes and their impacts on the naturalphysical environment. 2012.

WORLD HEALTH ORGANIZATION(WHO). (1993). The ICD-10 classification of mental and behavioural disorders. World Health Organization.

WORLD HEALTH ORGANIZATION.Cardiovascular diseases (CVDs). Available at:<https://www.who.int/news-room/fact-sheets/detail/cardiovascular-diseases-(cvds)>. Access date: 26 april 2020
