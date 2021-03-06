# Geospatial_visualization_cardiovascular

###### The initial goal of this project was to build a mapping of AS incidence in Montreal region, later the project was expanded to investigate the cause of difference in AS incidence rate in Montreal

### Flow of data
##### Define AS cases and surgical procedure (SAVR) between 2000 and 2010 [01_define case and savr.R](https://github.com/nancyzhu24/Geospatial_visualization_cardiovascular/blob/master/01_define%20case%20and%20savr.R)
Cases of AS were determined from both in-hospital admission diagnostic data and out-patient physician billing data. The date at which a patient was diagnosed was defined as the cohort entry date. SAVR were determined from hospital intervention data confirmed with out-patient billing data.

##### Mapping AS cases and SAVR
As a first attempt, the absolute count of AS cases over 10 years were mapping in Montreal based on CLSC regions [02_explore_geographic_AS.R](https://github.com/nancyzhu24/Geospatial_visualization_cardiovascular/blob/master/02_explore_geographic_AS.R) Following that, incidence rate of AS per 1000 pyr above 65 was mapped to CLSC regions [Mapping_AS.Rmd](https://github.com/nancyzhu24/Geospatial_visualization_cardiovascular/blob/master/Mapping_AS.Rmd) The 2017 Quebec CLSC map files are downloaded from [MSSS](http://www.msss.gouv.qc.ca/professionnels/informations-geographiques-et-de-population/information-geographique/)   are available in the folder [clsc_map](https://github.com/nancyzhu24/Geospatial_visualization_cardiovascular/tree/master/clsc_map) 

To further explore the cause of difference in AS cases over time in Montreal areas, age adjusted rate of AS and SAVR were calculated. The 2006 population data were extracted from census data provided by Statistic Canada [https://www12.statcan.gc.ca/datasets/Index-eng.cfm](https://www12.statcan.gc.ca/datasets/Index-eng.cfm). XML files were downloaded and parsed into R with script [03_parse_census_xml.R](https://github.com/nancyzhu24/Geospatial_visualization_cardiovascular/blob/master/03_parse_census_xml.R)

The 2006 Canadian age-specific population were used as the standard population in our age-specific rate calculation. Age-specific rate were calculated in each FSA region in Montreal. [03_age-adjusted-rate-calculation.R](https://github.com/nancyzhu24/Geospatial_visualization_cardiovascular/blob/master/03_age-adjusted-rate-calculation.R)

To map age-specific rate, FSA map are downloaded from [StatCan](https://www12.statcan.gc.ca/census-recensement/2011/geo/bound-limit/bound-limit-eng.cfm) and stored in [FSA_map](https://github.com/nancyzhu24/Geospatial_visualization_cardiovascular/tree/master/FSA_map) 
[05_Mapping_age_standarized_AS.Rmd](https://github.com/nancyzhu24/Geospatial_visualization_cardiovascular/blob/master/05_Mapping_age_standarized_AS.Rmd) includes all the script to map and report age-standarized rate of AS cases and SAVR for individuals over 65 between 2000 and 2010 in Greater Montreal area

##### Modelling AS cases and SAVR
From mapping, we observed variance in AS and SAVR incidence rate between Montreal FSA regions even after age adjustment. To investigate the cause of the variance, we applied two models: poisson regression model for an ecological study and Cox regression model for individual level.

Confounders in both models include SEC, past history of acute MI, diabetes, hypertension, chronic kidney diseases, COPD

SEC status are ascertained from deprivation index available in the RAMQ database. Deprivation index provides index for both social and material deprivation. The median value of each index were calculated for each FSA region between 2000 and 2010 and were used in the models. [04_deprivation_cal.R](https://github.com/nancyzhu24/Geospatial_visualization_cardiovascular/blob/master/04_deprivation_cal.R)

###### Poisson model
The data pre-processing steps for fitting a Poisson model can be found at [04_confounders_for_model.R](https://github.com/nancyzhu24/Geospatial_visualization_cardiovascular/blob/master/04_confounders_for_model.R). Briefly, the steps for data cleaning includes confounders ascertainment from diagnostic and prescription history for each FSA region between 2000 and 2010. The model fitting and results can be found in [Poisson-regression.Rmd](https://github.com/nancyzhu24/Geospatial_visualization_cardiovascular/blob/master/Poisson-regression.Rmd)

###### Cox model
The data pre-processing steps are available in [data_clean_Cox_model.R](https://github.com/nancyzhu24/Geospatial_visualization_cardiovascular/blob/master/data_clean_Cox_model.R). This file includes all code to select study cohort and ascertain covariates. Several models, including a mixed effect cox model, competing risk effect model were performed to investigate the association between SEC and rate of SAVR among AS patients in Montreal. The results and code for those models can be found in [Cox model.Rmd](https://github.com/nancyzhu24/Geospatial_visualization_cardiovascular/blob/master/Cox%20model.Rmd)



