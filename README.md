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
|Hospitalizations database (SSC - Campinas Health Department)| Hospitalizations in Campinas from 2014 to 2018|
|Deaths database (SSC - Campinas Health Department) | Deaths that occured in Campinas from 2001 to 2019|
|Viracopos| Daily values of minimum and maximum temperature, mean atmospheric pressure, minimum and maximum humidity from 1983 to 2018|
|CEPAGRI| Temperature and humidity every 10 minutes from 1997 to 2018|

There were inconsistences and gaps in the first months of 2017 for the Viracopos  humidity data. A linear regression using CEPAGRI data was perfomed to fill this data. The code for this is available at [].

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

The occurence at these events in Campinas SP was analysed using Viracopos data for the time period of 2001 to 2018 and is available at [**TR 2020/05**](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-circulatory-diseases/blob/main/notebooks/TR_2020_05_Extreme_climatic_events_for_Campinas.ipynb). 
   
Occurence of extreme events in Campinas between 2001 and 2018
|Extreme event | Number of events| Total number of days | Longest event|
| ---------- |---------- |---------- |---------- |
|Extreme thermal range | 647 | 647  |  - |
|Extreme difference of temperature between days | 84 | 84  | -  |
|Low pressure waves | 65 | 261 | 8 |
|High pressure waves | 93 | 399 | 10 |
|Diferença extrema de pressão entre dias | 611 | 611 |  - |
|Low humidity waves | 37 | 168 | 16 |
|High humidity waves | 43 | 151 | 6 |
|Extreme humidity range | 915 | 915  | - |
|Extreme difference of humidity between days | 79 | 79  | -  |

##Day and night variation

Days with a small variation between day and night were hypothesized as disruptive of the biologicalrhythms and potentially dangerous to human health. We created two events to evaluate differences in temperature and humidity during day and night, using a similar methodology to the one described above. We compared the temperature and humidity differences between dawn (00h-6h), coldest and more humid period, with the ones from the afternoon (12h-18h), hottes and drier. The event was defined as days with the differences below the 10th.

From 2001 to 2018, they were 660 days with temperature variation between day and night belowthe 10th percentile. For humidity, there were 620 days.

## Association study

The influence of climatic parameters and extreme climatic events in the health of the population of Campinas we used different methodologies: Pearson correlations, Rate Ratios, Mann-Whitney U test, case cross-over design to evaluate incidence rate ratios, Poisson regression to evaluate relative risk.

### Pearson correlation

Pearson correlation [Rodgers e Nicewander 1988] was used to analyse the correlation between month medians. The level of significance was 5%. This analysis is available at:

- [**TR 2021/02**](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-circulatory-diseases/blob/main/notebooks/TR_2021_02_Correlations_between_cardiovascular_hospitalizations_and_climatic_variables.ipynb): Pearson correlation between climatic variables and hospitalizations

|Climatic variable| Pearson coefficient| p value| Correlation|
|----------|----------|---------- |---------- |
|Minimum temperature(°C) |-0.58 |  0.0492 |  moderate |
|Maximum temperature(°C) | -0.48 |  0.1147 |  -    |
|Thermal range (°C) |0.50 |  0.0980 |   - |
|Mean atmospheric pressure (HPA)| 0.59 |  0.0417 | moderate |
|Minimum humidity(%) | -0.31 |  0.3297 |    - |
|Maximum humidity(%) | -0.26 |  0.4161 |  - |
|Humidity range(%) |0.24 |  0.4595 |     - |

- [**TR 2021/03**](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-circulatory-diseases/blob/main/notebooks/TR_2021_03_Correlations_between_cardiovascular_deaths_and_climatic_variables.ipynb): Pearson correlation between climatic variables and deaths
|Climatic variable| Pearson coefficient| p value| Correlation|
|----------|----------|---------- |---------- |
|Minimum temperature(°C) |  -0.93 |  <0.0001  | very strong|
|Maximum temperature(°C) |   -0.86 |  0.0003 |  strong|
|Thermal range (°C) |   0.71 |  0.0094 |    strong |
|Mean atmospheric pressure (HPA) |   0.90 |  0.0001 | strong|
|Minimum humidity(%) |   -0.74 |  0.0062 | strong|
|Maximum humidity(%) |    -0.6 |  0.0384 | moderate|
|Humidity range(%) |  0.71 |  0.0091 | strong|

### Rate ratios

Rate ratio is a relative difference measure used to compare the incidence rates of events occurring at any given point in time, frequently used in epidemiology. Rate ratios from days under extreme events effect and control days were compared. A rate ratio above 1.0 indicates an increased risk associated with that event [CDC]. The analysis was conducted for the total data and for some stratifications (sex, age, age and sex, race) and is available at:

- [**TR 2021/04**](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-cardiovascular-diseases/blob/main/notebooks/TR_2021_04_Rate_ratio_for_cardiovascular_hospitalizations_and_extreme_events.ipynb): Rate ratio for extreme climatic events and hospitalizations

|Event| Rate ratio| Confidence interval|
|------|-----------|----------|
|Extreme thermal range | 0.96 | 0.89 - 1.03|
|**Extreme difference of temperature between days** | **1.16** | **1.00 - 1.35**|
|Low pressure waves | **1.09** | 0.98 - 1.22 |
|High pressure waves | 1.00 | 0.94 - 1.06 |
|Extreme difference of pressure between days| **1.05** | **0.99 - 1.11** |
|Low humidity waves | 0.90 | 0.84 - 0.97|
|High humidity waves | **1.05** | 0.76 - 1.45|
|Extreme humidity range | **1.01** | 0.96 - 1.08 |
|Extreme difference of humidity between days | 0.98 | 0.92 - 1.04|

- [**TR 2021/05**](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-cardiovascular-diseases/blob/main/notebooks/TR_2021_05_Rate_ratio_for_cardiovascular_deaths_and_extreme_events.ipynb): Rate ratio for extreme climatic events and deaths

|Event| Rate ratio| Confidence interval|
|------|-----------|----------|
|Extreme thermal range | **1.01** | 0.98 - 1.04|
|Extreme difference of temperature between days | 0.89 | 0.82 - 0.96|
|Low pressure waves | 0.97 | 0.93 - 1.01 |
|High pressure waves | **1.01** | 0.98 - 1.05 |
|Extreme difference of pressure between days| 1.00 | 0.97 - 1.03 |
|**Low humidity waves** | **1.09** | **1.04 - 1.15**|
|High humidity waves | 0.99 | 0.94 - 1.05|
|**Extreme humidity range** | **1.02**  | **1.00 - 1.04**  |
|Extreme difference of humidity between days | 0.97 | 0.94 - 1.00|

-[](): Rate ratio for day and night variations

Hospitalizations
|Event| Rate ratio| Confidence interval|
|------|-----------|----------|
|Day and night variation of temperature | **1.02** | 0.96 - 1.08|
|Day and night variation of humidity | 0.98| 0.92 - 1.04|

Deaths
|Event| Rate ratio| Confidence interval|
|------|-----------|----------|
|Day and night variation of temperature | **1.04** | **1.01 - 1.07**|
|Day and night variation of humidity | 0.97 | 0.94 - 1.00|

### Mann-Whitney U

Mann-Whitney U is a nonparametric test used to compare two distributions s [MacFarland e Yates 2016]. The test was used to compare the distributions of hospitalizations/deaths between under extreme events effect and control days. The analysis was conducted for the total data and for some stratifications (sex, age, age and sex, race) and is available at:

- [**TR 2021/06**](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-cardiovascular-diseases/blob/main/notebooks/TR_2021_06_Mann_Whitney_U_test_for_cardiovascular_hospitalizations_and_extreme_climatic_events.ipynb): Mann-Whitney U test for extreme climatic events and hospitalizations
- [**TR 2021/07**](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-cardiovascular-diseases/blob/main/notebooks/TR_2021_07_Mann_Whitney_U_test_for_cardiovascular_deaths_and_extreme_climatic_events.ipynb): Mann-Whitney U test for extreme climatic events and deaths

### Case crossover

In a case-crossover study design, each person serves as his own control. The period immediately before the adverse outcome (death or hospitalization) is then compared with a period when no adverseoutcome occurred [L Gordis, 2013]. The IRR were estimated using a logistic regression.

-[](): IRR for hospitalizations
|Event| IRR | Confidence interval|
|------|-----------|----------|
|Extreme thermal range | 0.88 | 0.83 - 0.93|
|Extreme difference of temperature between days | **1.08** | 0.97 - 1.12|
|Low pressure waves | **1.12** | **1.00 - 1.25** |
|High pressure waves | **1.02** | 0.96 - 1.09 |
|Extreme difference of pressure between days | 0.97 | 0.92 - 1.02 |
|Low humidity waves | **1.03** | 0.95 - 1.11|
|High humidity waves | 0.37 | 0.27 - 0.49|
|Extreme humidity range | 0.93| 0.89 - 0.98 |
|Extreme difference of humidity between days | **1.01** | 0.91 - 1.12|

-[](): IRR for deaths
|Event| IRR | Confidence interval|
|------|-----------|----------|
|Extreme thermal range | 1.00 | 0.97 - 1.03|
|Extreme difference of temperature between days | 0.97 | 0.92 - 1.02|
|Low pressure waves | 0.97 | 0.93 - 1.02|
|High pressure waves | 1.00 | 0.96 - 1.03 |
|Extreme difference of pressure between days | 0.99 | 0.96 - 1.01 |
|Low humidity waves | **1.05** | 0.99 - 1.11|
|High humidity waves | **1.01** | 0.96 - 1.07|
|Extreme humidity range | 1.00 | 0.97 - 1.02|
|Extreme difference of humidity between days | 1.00 | 0.95 - 1.05|

### Poisson regression

A generalized poisson regression was used to estimate the relative risk associated with each extreme event [Consul,1989].

-[](): RR for hospitalizations
|Event| RR | Confidence interval|
|------|-----------|----------|
|Extreme thermal range | 0.95 | 0.88 - 1.04|
|Extreme difference of temperature between days | **1.05** | 0.88 - 1.25|
|Low pressure waves | **1.18** | **1.04 - 1.35** |
|High pressure waves | 0.97 | 0.89 - 1.04 |
|Extreme difference of pressure between days  | **1.04** | 0.97 - 1.11 |
|Low humidity waves | 0.92 | 0.85 - 0.99|
|High humidity waves | **1.06** | 0.74 - 1.54 |
|Extreme humidity range | 1.00 | 0.95 - 1.07 |
|Extreme difference of humidity between days | **1.05** | 0.88 - 1.26|

-[](): RR for deaths
|Event| RR | Confidence interval|
|------|-----------|----------|
|Extreme thermal range | 0.99 | 0.97 - 1.02|
|Extreme difference of temperature between days | 0.85 | 0.79 - 0.93|
|Low pressure waves | **1.03** | 0.98 - 1.08|
|High pressure waves | 0.95 | 0.91 - 0.99 |
|Extreme difference of pressure between days | 0.99 | 0.96 - 1.02|
|Low humidity waves | **1.06** | **1.00-1.12**|
|High humidity waves | **1.01** | 0.96 - 1.07|
|Extreme humidity range | **1.02** | 0.99 - 1.04|
|Extreme difference of humidity between days | **1.01** | 0.93 - 1.09|

## Low humidity waves

The occurence of the extreme event of Low Humidity Waves (LHW), three or more consecutive days with both minimum and maximum humidity below the 10th percentile, was analysed for the city of Campinas, SP for the time period from 1983 to 2018. This event was analysed due to its impact on health.

The analysis revealed that low humidity waves are increasing in frequency, intensity and duration, and is available at [**TR 2021/01**](https://github.com/climate-and-health-datasci-Unicamp/project-climatic-variations-circulatory-diseases/blob/main/notebooks/TR_2021_01_Low_humidity_waves_analysis_for_Campinas.ipynb).

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

CENTERS FOR DISEASE CONTROL AND PREVENTION (CDC).Principles ofEpidemiology in Public Health Practice, Third Edition An Introduction to AppliedEpidemiology and Biostatistics. Available at: <https://www.cdc.gov/csels/dsepd/ss1978/lesson3/section5.html>. Access date: mar 2021.

CONSUL, P.C., Generalized Poisson distributions: properties and applications.  M. Dekker, 1989.

COUNCIL, N. R. et al.Advancing the science of climate change. [S.l.]: National AcademiesPress, 2011.

GEIRINHAS, J. L. et al. Climatic and synoptic characterization of heat waves in brazil.International Journal of Climatology, Wiley Online Library, v. 38, n. 4, p. 1760–1776, 2018.

GORDIS, L. , “Epidemiology, Saunders Elsevier”, Philadelphia, Pa, USA, 2013.

MACFARLAND, T. W.; YATES, J. M. Mann–whitney u test. In:Introduction tononparametric statistics for the biological sciences using R. [S.l.]: Springer, 2016. p. 103–132.

MCMICHAEL, A. Global climate change and health: an old story writ large. In:Climatechange and human health: risks and responses. [S.l.]: Geneva, World Health Organization,2003. cap. 1.

MURRAY, C. J. et al. Global burden of 87 risk factors in 204 countries and territories,1990–2019: a systematic analysis for the Global Burden of Disease Study 2019.The Lancet,Elsevier, v. 396, n. 10258, p. 1223–1249, 2020.

RODGERS, J. L.; NICEWANDER, W. A. Thirteen ways to look at the correlationcoefficient.The American Statistician, Taylor & Francis Group, v. 42, n. 1, p. 59–66, 1988.

SENEVIRATNE, S. et al. Changes in climate extremes and their impacts on the naturalphysical environment. 2012.

WORLD HEALTH ORGANIZATION(WHO). (1993). The ICD-10 classification of mental and behavioural disorders. World Health Organization.

WORLD HEALTH ORGANIZATION.Cardiovascular diseases (CVDs). Available at:<https://www.who.int/news-room/fact-sheets/detail/cardiovascular-diseases-(cvds)>. Access date: 26 april 2020.
