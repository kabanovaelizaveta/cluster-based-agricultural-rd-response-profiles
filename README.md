# Heterogeneous Effects of Agricultural R&D Investments on Productivity Growth

## Overview

This repository contains materials for the research paper:

**"Heterogeneous Effects of Agricultural R&D Investments on Productivity Growth: A Cluster-Based Dynamic Response Analysis"**

The project investigates how agricultural research and development (R&D) investments affect agricultural productivity growth across different groups of countries. 
The main idea of the study is that the effect of R&D investments is not the same for all countries. Countries differ in their economic development, agricultural structure, demographic characteristics, environmental conditions, and ability to adopt innovations. Because of this, agricultural R&D may produce different productivity responses across different country groups.
This study proposes a cluster-based dynamic response framework that combines country clustering, causal machine learning, and cluster-specific lag analysis.

---

## Author

**Yelizaveta I. Kabanova**  
ORCID: https://orcid.org/0009-0001-2692-5066  
Email: yelizavetakabanova@gmail.com

---

## Abstract

This work studies the heterogeneous effects of agricultural R&D investments on agricultural productivity growth using a cross-country panel dataset.

Agricultural R&D is an important driver of productivity growth, but its effects are not immediate. The transformation of research investments into measurable productivity improvements requires time because of knowledge creation, technology development, and adoption processes.

The study proposes a cluster-based framework that groups countries according to structural economic, demographic, agricultural, and environmental characteristics. Then, causal machine learning and lag analysis are used to estimate how R&D investments affect agricultural production across different country clusters.

The results show that countries can be grouped into structurally different clusters and that the estimated effect of R&D investments differs across these clusters. The analysis also suggests that the timing of R&D effects may vary between country groups.

---

## Motivation

Agricultural R&D investments are important for long-term productivity growth, food security, and technological development. However, their effects are usually delayed and may depend on the structural conditions of each country.

Countries with stronger economic capacity, stable production systems, and better innovation adoption mechanisms may benefit from R&D investments faster and more effectively. In contrast, low-income or agriculture-dependent economies may face constraints that reduce or delay the impact of R&D.

Therefore, analysing only average effects across all countries may hide important differences. This project focuses on identifying these differences and describing country-specific response patterns.

---

## Research Objective

The main objective of this study is to investigate whether the effects of agricultural R&D investments differ across groups of structurally similar countries and whether these effects appear over different time horizons.

The study aims to:

- construct a cross-country dataset using agricultural, economic, demographic, environmental, and R&D indicators;
- identify groups of structurally similar countries using clustering methods;
- estimate heterogeneous effects of agricultural R&D investments using causal machine learning;
- analyse short-, medium-, and long-term investment effects within each cluster;
- formulate cluster-specific investment response profiles.

---

## Research Hypotheses

The study tests the following hypotheses:

- **H1:** Countries can be classified into distinct clusters based on economic, demographic, and environmental characteristics.
- **H2:** The effect of agricultural R&D investments on productivity differs across country clusters.
- **H3:** The timing of agricultural R&D effects differs across country clusters.

---

## Scientific Contributions

The main contributions of this work are:

- development of a cluster-based framework for analysing heterogeneous agricultural R&D effects;
- integration of country clustering with causal machine learning methods;
- estimation of heterogeneous treatment effects of R&D investments across country groups;
- incorporation of cluster-specific lag structures for short-, medium-, and long-term effects;
- introduction of a dynamic response profile framework based on timing, magnitude, stability, and statistical confidence.

---

## Data

The analysis is based on a cross-country panel dataset constructed from multiple international data sources.

### Data Sources

The main data sources are:

- **FAOSTAT**
  - agricultural R&D investments;
  - value of agricultural production.

- **World Bank**
  - GDP per capita;
  - total population;
  - rural population share;
  - rural land share;
  - annual mean temperature.

### Time Period

The dataset covers the period:

**2005–2022**

### Final Dataset

The final dataset includes:

- **110 countries**
- **1080 observations**
- **12 variables**

For the clustering stage, countries with fewer than five valid observations for agricultural production were removed. The final clustering dataset includes:

- **80 countries**

---

## Variables

| Variable | Description | Source |
|---|---|---|
| `log_rd` | Agricultural R&D investments | FAOSTAT |
| `log_production` | Value of agricultural production | FAOSTAT |
| `gdp_per_capita` | GDP per capita | World Bank |
| `log_population` | Total population | World Bank |
| `rural_pop_pct` | Rural population percentage | World Bank |
| `rural_land_pct` | Rural land area percentage | World Bank |
| `temperature` | Annual mean temperature | World Bank |
| `rd_trend` | Average annual growth trend of R&D investments | Computed |
| `gdp_trend` | Average annual growth trend of GDP per capita | Computed |
| `CV` | Coefficient of variation of agricultural production | Computed |

---

## Methodology

The methodology consists of four main stages:

1. Data collection and preprocessing.
2. Country clustering.
3. Causal machine learning analysis.
4. Cluster-specific lag analysis and response profile classification.

---

## 1. Data Collection and Preprocessing

The datasets were collected from FAOSTAT and the World Bank and transformed into a unified country-year panel format.

The preprocessing steps included:

- standardising country names;
- removing non-country observations;
- transforming all datasets into a Country-Year-Feature structure;
- merging datasets by country and year;
- analysing missing values and outliers;
- applying logarithmic transformations to skewed variables;
- imputing missing temperature values.

Logarithmic transformations were applied to:

- agricultural R&D expenditures;
- agricultural production;
- total population.

Missing temperature observations were imputed using:

- within-country linear interpolation;
- country-level medians;
- global median fallback.

---

## 2. Country Clustering

Country clustering was used to identify groups of structurally similar countries.

Two clustering algorithms were applied:

- **Gaussian Mixture Model (GMM)**
- **Agglomerative Hierarchical Clustering**

Three clustering specifications were tested:

| Model | Description |
|---|---|
| Model A | Baseline mean variables |
| Model B | Baseline mean variables + dynamic growth trends |
| Model C | Baseline mean variables + dynamic growth trends + production volatility |

Model C was selected as the main clustering model because it better captures dynamic economic heterogeneity and shows higher cluster stability.

---

## Cluster Interpretation

The final clustering solution identifies three country groups.

### Cluster 0: High-income and stable economies

Countries in this cluster are characterised by:

- highest agricultural R&D expenditures;
- high GDP per capita;
- low rural population share;
- lower temperature;
- lowest production volatility;
- faster R&D investment growth.

This cluster represents countries with stronger structural capacity to transform R&D investments into productivity growth.

### Cluster 1: Low-income agriculture-dependent economies

Countries in this cluster are characterised by:

- low R&D investments;
- low GDP per capita;
- high rural population share;
- high agricultural land dependence;
- high temperature;
- highest production volatility.

This cluster represents economies where structural constraints may reduce the effectiveness of R&D investments.

### Cluster 2: Mixed and transitional economies

Countries in this cluster are characterised by:

- moderate income levels;
- relatively low agricultural R&D expenditures;
- medium production stability;
- transitional economic structure.

This cluster may require more time to transform R&D investments into productivity outcomes.

---

## 3. Causal Machine Learning Analysis

Causal Forest was used to estimate heterogeneous effects of agricultural R&D intensity on agricultural productivity.

The model estimates the **Conditional Average Treatment Effect (CATE)**, which shows how strongly agricultural productivity responds to changes in R&D intensity for countries with different structural characteristics.

### Causal Model Variables

| Role | Variable |
|---|---|
| Treatment | Average agricultural R&D intensity |
| Outcome | Average agricultural production |
| Covariates | GDP per capita, population, rural population share, rural land share, temperature |

### Causal Forest Results

| Cluster | CATE |
|---|---:|
| Cluster 0 | 0.290 |
| Cluster 1 | 0.172 |
| Cluster 2 | 0.169 |

The results show that Cluster 0 has the strongest estimated response to R&D investments. Clusters 1 and 2 show weaker effects, which may be related to lower income levels, higher agricultural dependence, and higher production volatility.

---

## 4. Cluster-Specific Lag Analysis

To analyse the timing of agricultural R&D effects, cluster-specific lag analysis was conducted.

Because yearly lagged R&D variables were highly correlated, the lags were grouped into three investment horizons:

| Horizon | Definition |
|---|---|
| Short-term | 1–2 years |
| Medium-term | 3–4 years |
| Long-term | 5 years |

A fixed-effects regression model was estimated for each cluster using:

- lagged R&D investment variables;
- GDP per capita;
- rural population share;
- rural land share;
- temperature;
- total population;
- country fixed effects.

---

## Lag Analysis Results

| Cluster | Short-term | Short-term p-value | Medium-term | Medium-term p-value | Long-term | Long-term p-value |
|---|---:|---:|---:|---:|---:|---:|
| Cluster 0 | -0.016 | 0.5305 | 0.0334 | 0.5667 | -0.1048 | 0.0559 |
| Cluster 1 | 0.0326 | 0.5610 | 0.0365 | 0.6032 | 0.0161 | 0.7931 |
| Cluster 2 | 0.0286 | 0.7364 | 0.0302 | 0.7396 | 0.0474 | 0.4584 |

The results suggest different response patterns across clusters:

- Cluster 0 shows the strongest positive response in the medium term.
- Cluster 1 shows weak positive effects across all horizons, with the highest value in the medium term.
- Cluster 2 shows the strongest positive response in the long term.

However, the coefficients are not statistically significant. Therefore, these results should be interpreted as suggestive patterns rather than definitive evidence.

---

##  Cluster-Specific Response Profile Framework

Based on the estimated cluster-specific lag structures, this study develops an investment response profile framework to translate econometric results into interpretable investment profiles.

The purpose of this framework is to summarize the estimated dynamic response patterns of each cluster using several key indicators:

- the overall causal magnitude of the investment;
- the dominant investment horizon;
- the magnitude of the estimated R&D effect;
- production stability;
- statistical confidence of the estimated coefficients.

The proposed response profile classification for cluster `c` is represented as:

```text
Sc = {CMc, Tc, cmax, CVc, SCc}
```
where:

| Indicator | Meaning |
|---|---|
| `CMc` | Average causal magnitude from Causal Forest |
| `Tc` | Dominant investment horizon |
| `cmax` | Maximum positive estimated R&D response coefficient |
| `CVc` | Average coefficient of variation of agricultural production |
| `SCc` | Statistical confidence based on significant lag effects |


| Cluster | Dominant Horizon | cmax | CVc | SCc | CMc | Response Profile |
|---|---|---:|---:|---:|---:|---|
| Cluster 0 | Medium-term | 0.033 | 0.090 | 0 | 0.290 | Stable medium-term response signal |
| Cluster 1 | Medium-term | 0.036 | 0.191 | 0 | 0.172 | Volatile weak medium-term response signal |
| Cluster 2 | Long-term | 0.047 | 0.119 | 0 | 0.169 | Stable delayed response signal |

Cluster 0 demonstrates a stable medium-term response signal. The largest positive lag coefficient is observed in the medium-term horizon, while production volatility is the lowest among all clusters.

Cluster 1 represents a volatile weak medium-term response signal. The dominant horizon is also medium-term, but the estimated coefficient is small and statistically insignificant.

Cluster 2 demonstrates a stable delayed response signal. The largest positive coefficient is observed in the long-term horizon, suggesting that R&D investments may require more time to influence agricultural production in mixed or transitional economies.

---

## Key Results

The results of this study demonstrate that the effectiveness and timing of R&D investments are highly heterogeneous and depend on the structural characteristics of countries, including their economic development level, demographic structure, agricultural dependence, and production stability.

The clustering analysis identified three groups of countries with distinct structural characteristics. The clusters differed substantially in terms of agricultural R&D investment levels, GDP per capita, rural population share, environmental conditions, and production stability.

The causal forest results demonstrated the strongest estimated treatment effect for Cluster 0, which consists of high-income and structurally stable economies.

The cluster-specific lag analysis provided additional evidence that R&D effects differ across countries. Although the estimated coefficients were not statistically significant, the observed patterns suggested that different country groups may experience different investment horizons.

The proposed profile framework integrates the estimated magnitude, timing, stability, and statistical reliability of R&D effects into a single interpretable classification.

---

## Hypothesis Evaluation

| Hypothesis | Result | Explanation |
|---|---|---|
| H1 | Supported | The clustering results support H1 and demonstrate that countries can be grouped according to their economic, demographic, and environmental characteristics. |
| H2 | Supported | The causal forest analysis supports H2 by showing that the magnitude of agricultural R&D effects differs across country clusters. |
| H3 | Partially supported | The estimated investment horizons differed across clusters, but the lag coefficients were not statistically significant. |

---

## Conclusions

This study investigated whether agricultural R&D investments generate different productivity responses across structurally similar groups of countries and whether these effects emerge over different time horizons.

By combining country clustering, causal machine learning, and lag analysis, the study developed a framework for identifying heterogeneous agricultural R&D response patterns.

Overall, the findings highlight that the effectiveness of R&D depends on the structural environment of countries.

The proposed dynamic response profile framework provides an approach for identifying different investment response patterns and offers a more detailed perspective than average-effect approaches.

---

## Limitations

Several limitations should be considered.

First, although causal machine learning methods allow flexible estimation of heterogeneous effects, the results cannot fully eliminate the influence of unobserved factors.

Second, the limited number of countries reduces the statistical power of cluster-specific estimations, particularly in the lag analysis.

Third, the dataset does not include all factors that may influence innovation adoption.

---

## Future Work

Future research should extend this framework by:

- incorporating additional institutional and technological indicators;
- analysing longer time periods;
- evaluating the identified response profiles across different regions;
- improving robustness checks for cluster-specific lag analysis;
- comparing alternative causal machine learning methods.

---
