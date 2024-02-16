# Predictive Model for Higher Education Entrants: Potential Expansion Assessment
## Project Overview
This model is developed to quantify the potential of new students enrolling in Company Y's distance learning courses in cities where the company currently does not have a presence. Utilizing a robust dataset with demographic, educational, socioeconomic, and infrastructure variables, the model aims to predict student enrollment in areas where Company Y considers expanding its educational hubs.

**Context and Justification**
* **Data-Driven Expansion:** The decision to establish new educational hubs is complex and multifaceted. This model seeks to simplify this decision by providing quantitative predictions that support strategic expansion.
* **Training and Validation:** The model will be initially trained and validated in cities where Kroton already operates, ensuring that the predictions are based on reliable historical data.
* **Strategic Application:** After validation, the model will be used to estimate the number of potential entrants in target cities, informing the feasibility and planning of the expansion.
  
**Analytical Variables**
* The analysis will include variables such as higher education census data (`ENTRANTS`, `ENROLLMENTS`, `APPLICATIONS`, `VACANCIES`), technological infrastructure (`BROADBAND_HOUSEHOLDS`, `4G_5G_TELEPHONY`, `NUMBER_OF_ISPS`), socioeconomic indicators (`GDP_PER_CAPITA`, `AVERAGE_INCOME`), demographic data (`POPULATION`, `HOUSEHOLDS`, `POP_DENSITY`), among others (a total of 49 features).
* `EAD_Y_ENTRANTS`: The target variable representing the number of new students in Company Y's distance learning program.

## Data Collection
**Open Data Utilization**

In line with my commitment to transparency and the principles of open science, the dataset foundational to my model is derived from openly available government databases. These data sources, released by federal entities like INEP for educational statistics, ANATEL for technological infrastructure, and IBGE for demographic and socioeconomic information, are publicly accessible. This approach underscores my dedication to employing publicly available data to advance educational opportunities and insights.

* Education Source: [INEP](https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/censo-da-educacao-superior)
* Infrastructure Source: [ANATEL](https://informacoes.anatel.gov.br/paineis/acessos)
* Demographic and Socioeconomic: [IBGE](https://www.ibge.gov.br/estatisticas/sociais/populacao/22827-censo-demografico-2022.html?edicao=37225&t=resultados)

## Preprocessing and Feature Engineering
After obtaining the data, I needed to clean it up so that it was usable for my model. I made the following changes and created the following variables:
* 
* An 75/25 train/test split was used and as my data contained dates, the most recent 25% of the data became the test set.
* Any missing values in a categorical feature were assigned a new category 'NONE' and missing values in numeric features were imputed using the median. Some heuristic functions were also used to impute systematic missing values. 
* One-hot-encoding was used to encode categorical features and ordinal encoding was used to encode ordinal features. Target encoding was also used for a few categorical features. 

## Model Building 
In this step, I built a few different candidate models and compared different metrics to determine which was the best model for deployment. Three of those models were:
* Dummy Classifier (simply returns average kudos) - Baseline for the model.
* Lasso Regression - Because of the sparse data from the many categorical variables, I thought a normalized regression like lasso would be effective.
* Random Forest - Again, with the sparsity associated with the data, I thought that this would be a good fit.
* XGBRegressor - Well... this model just always seems to work.

Feature selection was performed using a mix of SHAP values and feature importance from XGB

