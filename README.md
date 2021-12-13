# data-512-final-project
This is our final project of Data512 Human-Centered Data Science. Our goal is to practice how to complete the whole data science project, from gathering data, processing data, then setting up our researching questions(Null Hypotheis), proposaling the proper methodology, then leading to the final conclusion. For this project, I used cov-19 related data around Daily Cases, Infection Rate and Vaccine Data to find the correlation between Infection Rate and Vaccine Rate. All analysis are performed in a single Jupyter notebook, named hcds-final-project.ipynb.

## Data sources

+ The CDC dataset of masking mandates by county.
https://data.cdc.gov/Policy-Surveillance/U-S-State-and-Territorial-Public-Mask-Mandates-Fro/62d6-pm5i
  + Licesnse: Public Use (User Agreement: https://www.cdc.gov/nchs/data_access/restrictions.htm)
  + These columns in this data are used in this project
    + 'Date'
    + 'Order Code'
    + 'FIPS' - the FIPS code
    + 'Face_Masks_Required_in_Public' - whether face mask is mandated
 
+ The RAW_us_confirmed_cases.csv file from the Kaggle repository of John Hopkins University COVID-19 data.
https://www.kaggle.com/antgoldbloom/covid19-data-from-john-hopkins-university?select=RAW_us_confirmed_cases.csv
  + License: Attribution 4.0 International (CC BY 4.0)
  + Three columns in this data are used: 'FIPS' - the FIPS code
  + All the date columns recording the raw confirmed cases are used

+ The New York Times mask compliance survey data. 
https://github.com/nytimes/covid-19-data/tree/master/mask-use
  + License: Copyright 2021 by The New York Times Company
  + All columns are used in this project: COUNTYFP - the FIPS code
  + All columns representing the frequency of mask wearing

+ CDC’s COVID Data Tracker provides COVID-19 vaccination data in the United States
https://www.cdc.gov/coronavirus/2019-ncov/vaccines/distributing/reporting-counties.html
  + Licesnse: Public Use (User Agreement: https://www.cdc.gov/nchs/data_access/restrictions.htm)
  + These columns in this data are used in this project
    + 'Date'
    + 'FIPS' - the FIPS code
    + 'Series_Complete_Pop_Pct' - Vaccine Rate


## Data processing
+ Data cleaning and drop unneeded columns
+ Melt the confirm case data so each row represent confirmed case each day
+ Standardize the FIPS column among the three datasets
+ Filter out only Palm Beach,FL data(FIPS == '12099')


## Data Visualization
+ Estimated Prevalence of Mask Wearing in Palm Beach County, FL
+ Time series visualize Accumulate Covid Cases, Palm Beach Country, FL
+ Daily New Covid Cases & 7 days rolling average, Palm Beach Country, FL
+ 7 days rolling average infection rate(Daily new cases / Population), Palm Beach Country, FL
+ 7 days rolling average infection rate Diff, Palm Beach Country, FL

## Data Analysis
+ As we can see, Palm Beach's Infection rate has no much change, specially using the 7 days rolling average visualization
+ Since Palm Beach county doesn't have mandate mask policy, try to find another county with similar mask wearing data but with have mark mandate policy
+ Using Mask-Wearing Survey Data to look for another city with the similar mask wearing %
+ Found a similar county(Spotsylvania County, VA) which has similar mask wearing %, specially "ALWAYS == 0.785"

## Research Questions:

Based on the data visualization "7 days rolling average infection rate and Vaccine rate at Palm Beach, FL", we can see when the Cov-19 vaccine started at 2021-01, the infection rate went down until Delta variant came to the picture around 2021-07.

NULL Hypotheis:
 There is no correlation between Vaccine Rate and Daily Infection Rate of 7 days rolling average
 
Considering Delta Variant Impact: 
+ Jul 2021: DELTA variant started https://www.newsweek.com/first-us-covid-delta-variant-cases-how-did-it-mutate-1617871
+ Other impact facts: Summer break and Nationwide reopening, etc.

Therefore, I splitted the data to 3 time period to find the correlation between Infections Rate and Vaccine Rate.
+ Before 2021-01 Vaccine started
+ After 2021-01 Before 2021-07 Vaccine rate increase and infection rate decrease
+ After 2021-07 Delta variant

## Conclusion:
Using Pandas .corr() function and seaborn heatmap, we can see:
+ No correlation between Infection Rate and Vaccine Rate Before 2021-01 Vaccine started
+ Very Strong Negative correlation between Infection Rate and Vaccine Rate after 2021-01 Vaccine started and before 2021-07 Delta Variant, Vaccine helped a lot.
+ Very slight negative correlation between Infection Rate and Vacine Rate after 2021-07 Delta variant, Vaccine didn’t help a lot for Delta variant

From the statsmodels.api OLS Regression Results:

+ P_Value is 0.000 which < 0.05, so we can reject NULL Hypotheis: There is no correlation between Vaccine Rate and Daily Infection Rate of 7 days rolling average.
+ R-squared is 0.851, meaning the goodness of LinearRegression model fit.

