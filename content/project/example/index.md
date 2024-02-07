---
title: Predicting California rent prices
summary: Time series forecasting of rent prices in California to the zip code granularity using tree-based models
tags:
  - Deep Learning
date: '2016-04-27T00:00:00Z'

# Optional external URL for project (replaces project detail page).
external_link: 'https://nycdatascience.com/blog/student-works/data-forecasting-zillow-rent-index-in-california/'

image:
  caption: Photo by rawpixel on Unsplash
  focal_point: Smart

links: ''
url_code: https://github.com/Skipp-py/NYCDSA_Capstone
url_pdf: ''
url_slides: ''
url_video: ''

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ''
---

Authors: Karl Lundquist, Cherie Wang, David Kressley & Ayelet Hillel
Data Science Introduction
This data science project was conducted in collaboration with Markerr, a leading data driven real estate firm, and is an attempt to better understand shifting trends in consumer demand. Our main objective is to accurately forecast rent prices in California through identifying the characteristics that significantly impact rent changes.

We focused our analysis on the five biggest metro areas in California:Los Angeles-Long Beach-Anaheim, San Francisco-Oakland-Hayward, Riverside-San Bernardino-Ontario, Sacramento--Roseville--Arden-Arcade and San Diego-Carlsbad. 

Our original dataset began with over 13,000 zip codes across the United States for the years 2010 through 2020. To complete an in depth analysis and yield insightful results our research was isolated to the major metropolitan areas of California. California has continued to see shifting trends in real estate development and as such, served as the basis of our research. 

Data Sources
We used four publicly available data sources: 

1) Zillow Rent Index Data
Housing Rent Price Data

The monthly Zillow Rent Index was selected as the target variable. The data for multifamily (i.e. multiple unit) rental properties includes observations for 764 zip codes across the five biggest metro areas in California from Sept 2010 to Jan 2020. 

2) Building Permits Survey
New Permits for Geographic Regions Data

The Building Permits Survey provides data on the number of new housing units authorized by building permits. Data are available monthly, year-to-date, and annually at the national, Division, Region, state, county, and metropolitan area levels, and for individual jurisdictions between 2004 and 2020 included. For this analysis, we used annual data at the zip code level from 2011 to 2019. 

3) American Community Survey (ACS)
Demographic and Economic Data

The American Community Survey (ACS) is an annual survey taken by the U.S. Census Bureau. Data collected includes information such as educational attainment, income, language proficiency, migration, disability, employment, housing characteristics. ACS provides data for the nation, states, counties and other geographic areas down to the block group level.

In this analysis, we obtained the 2020 ACS 5-year estimate at the zipcode level. The dataset originally includes 252 features that were reduced to 54 features through data cleaning and feature engineering. 

4) Internal Revenue Service Data
Real Estate Taxes & Mortgages Data

The Internal Revenue Service (IRS) is a U.S. government agency responsible for the collection of taxes and enforcement of tax laws. We obtained annual data at the zip code level regarding average real estate taxes, number of real estate tax returns, average mortgage interest paid and number of returns with mortgage interest rate paid. 

Data Cleaning & Feature Engineering 
As our original set of information consisted of missing information and redundant categories it was necessary to address these problems right away before continuing into the analysis. To handle the issue of missing information we used a logical approach to not get rid of valuable information in the data.

We began by limiting the observations to those that contained more than 10% null values, this reduced the zip codes by approximately 8% and less of an impact on the other features.

After the severe missingness cases were handled, the data was imputed. For any missing value where the time periods prior and after were known the average was taken to impute the missing value. 

Once the issue of missingness was addressed feature reduction was necessary to remove the redundant and excessive category information. Several features that represented the same information were dropped from the table (e.g., “households” which was composed of non_family households and family_households).

To further reduce the total number of features, excessive categories were combined together and resulted in a more interpretable analysis.

Employee income in the original dataset was divided into $5,000 increments; however, we combined them into features closely resembling taxable income brackets. The removal of redundant features and combination of excessive categories helped to significantly reduce the number of features, from 252 to 54. 

After all data cleaning and feature reduction the next important step was to normalize the data relative to its respective zip code. This helped to ensure that the features were proportionately equivalent and accounted for the scale differences between zip codes. Further feature engineering was done in the form of developing an index to measure gentrification. 

Gentrification index 
Gentrification processes include demographic and physical changes in neighborhoods that bring in wealthier residents, greater investment, and more development. Tracking gentrification processes may yield meaningful insights regarding migration patterns that might influence rent prices.

We calculated gentrification index scores for each zip code based on percentage change in three demographic measures indicative of gentrification: income per capita, number of newcomers and Gini index.

The newcomers feature was engineered based on two variables from the ACS dataset: different_house_year_ago_different_city + different_house_year_ago_same_city. The overall rank is simply an average of the ranks of all three measures. Tracking gentrification processes may yield meaningful insights regarding migration patterns that might influence rent prices. 

Figure 1 conveys average rent by year and gentrification rank for all five biggest metro areas in California. It indicates that the two least gentrified zip code groups have slightly higher average rent compared to the two most gentrified groups, for all years. 


Figure 1.

However, when we zoom in, focusing merely on one metro area, we witness very different trends. As Figure 2 suggests, the least gentrified zip code group in Riverside-San Bernardino has the lowest average rent for 2013 and 2015, and the highest average rent for 2016 and 2018. This signals that in order to gain full understanding of the rental market in California, we should look into smaller subsets of our data.  

Figure 2.

PCA and Clustering Data Analysis
We now have 54 features which are geo-social-demographic characteristics for a total of 764 zip codes in five major metro areas in California. To further uncover relationships between different features we used principal component analysis (PCA), a technique for reducing dimensionality and increasing interpretability of datasets. 

Data Forecasting Zillow Rent Index
Data Forecasting Zillow Rent Index

Figure 3.



Figure 4.

The first 10 principal components contain about 75 percent of the total variance. We will need about 40 principal components to describe 100 percent of the variance. The amount of variance explained drops dramatically after the 3rd PC. The first PC is highly correlated with a group of features which describe highly educated adults of working or retirement age in our census and IRS dataset in these five metro areas. 

Feature	Pearson's Correlation with 1st PC
income_100000_199999	0.87
degree_bachelors	0.87
degree_graduate_professional	0.82
income_200000_or_more	0.79
white_pop	0.76
households	0.64
Real_estate_taxes_amount	0.62
male_64_over	0.60
female_40_to_64	0.58
female_64_over	0.54
The second PC is highly correlated with features that describe young adults and the density of the living units.

Feature	Pearson’s Correlation with 2nd PC
dwellings_1_unit	-0.86
income_less_10000	0.72
dwellings_2_to_49_units	0.72
households	0.67
male_30_to_39	0.67
commuters_walked_to_work	0.66
dwellings_50_or_more_units	0.65
income_10000_39999	0.65
male_19_under	-0.64
female_19_under	-0.61
female_20_to_29	0.56
vacant_housing_units_for_rent	0.53
commuters_by_public_transportation	0.53
male_20_to_29	0.51
housing_units	0.51
N_returns_mortgage_interest_paid	-0.50
 K-means Clusters
Next using K-means and with the first 40 PCs, each zip code at any year was assigned to a cluster. 



Figure 5.

Each PC is a linear combination of our original demographic features, and a change in the cluster assignment through the years in one zip code indicates that this area went through some demographic changes. The next part of our exploratory analysis will focus on zip codes with dynamic social demographic changes. 

Here is a map that demonstrates the cluster assignment. From one to four, the number of times a zip code became placed in a different cluster is a good indication of how dynamic the local demographic and economic outlook changed in the years 2013 to 2018. 

To find out whether this dynamic could signal real estate development trends we looked at how average rent growth differed in these zip codes. After 2016, the zip codes that had demographic cluster change four times continued to have higher rent growth than the rest of the zip codes. 

 

Figure 6.

Change in social-demographic clusters is also associated with increased total number of permits issued. 



Figure 7.

Lastly, we inspected the trend of the amount of real estate taxes collected in the areas with geo-demographic cluster changes. The total amount of real estate taxes amount is a significant feature for predicting rent prices in the 5 metro areas



Figure 8.

The decrease in the amount of real estate tax collected from 2017-2018 is visibly less in areas which changed clusters 4 times over this six years period as opposed to the other areas that changed 1,2 or 3 times.  

There are only two zip codes in the five metro areas which are grouped into 4 different geo-demographic clusters over the six years period included in our data: Lucerne Valley, CA, and Landers, CA. 

Clustering analysis helped us identify these two areas and other areas with social-demographic changes, which is associated with real estate development in these areas. We believe further research into the association between clusters and real estate development will offer insights into the investment potentials of these areas. 

Data Model Selection and Evaluation
Lagging the dataset

In order to use standard machine learning algorithms and give them forecasting ability, we need to lag the target variable. This is done by shifting target variables by some amount of time with respect to the independent variables. For instance if we lagged our dataset by one year then we would use the 2013 features to predict 2014 rent, 2014 features to predict 2015 rent and so on.

This is helpful because it allows the use of current data to make predictions into the future and the current rent can also be used as an independent variable to predict future rent.

Say we wanted to make predictions for 2022 but we only have data for 2013 to 2018 (as is the case with our dataset). In this case we could predict 2022 rent prices by using a four-year lag -- 2013 data would be trained on 2017 as a target and so on, and then we could input the 2018 data into our model to get the 2022 rent as our output.

For this project, due to limitations in the availability of the ACS data and Zillow Observed Rent Index (ZORI) targets, we used data from 2013 to 2018 with a lag of one year and 2018 input data was set aside as our test dataset to predict 2019 rent (shown in Figure 9).



Figure 9. Table illustrating models with lagged targets. Data used in this project is shown in green with the test dataset in bold. Future targets are shown in red.   

Feature reduction with VIF
Our original dataset had 252 features. With binning and removing redundant variables we reduced this to a dataset that had 54 variables. To reduce the number of features even further we wanted to remove those with high levels of multicollinearity.

We did this by iteratively sorting the variables by their variance inflation factors (VIF), removing the variable with the highest VIF provided it was above a certain cutoff, and then we repeated this until there were no more variables with VIFs above our cutoff. A flowchart of this procedure is shown in Figure 10. 

 


Figure 10. Flowchart of procedure to reduce multicollinearity by iteratively removing variables with high VIF (right). 

To determine the impact of eliminating highly multicollinear variables from our dataset we repeated our VIF feature reduction procedure for a number of cutoff values and trained linear models for each of the resulting feature sets.

In Fig. 11 we show density plots for the distribution of R2 test scores for each of these feature sets where we split the data 100 times randomly and then trained a linear model. There's a major cluster of scores for the feature sets between 0.95 and 1 and then two distributions with scores under 0.85.

The difference between these two groups is that those in the cluster above 0.95 included current rent whereas the ones below 0.85 did not. In Fig. 11 in can be seen that the feature set with a VIF cutoff of 50 (brown) is below 0.85, whereas the one with a cutoff of 55 (purple) is in the group above 0.95 and there is only one feature that differs between these two sets (Fig 11, legend). This distinguishing feature is the current year’s rent, and it clearly plays a significant role on the test scores.

In light of this, we made a new feature set which includes those features down to a VIF of 5 (Fig 11, gray) in addition to the current rent (Fig 11, pink, 21 features). Indeed, including current rent allows this feature set to perform about as well as the other distributions with scores over 0.95. 



Figure 11. Scoring for linear models based on feature sets with a range of VIF cutoffs. 

Moving forward, we used three feature sets for our final modeling. Our minimal feature set had 20 variables all of which had VIFs under 5 (encompassed by green rounded rectangle in Fig. 12). In addition, we used a slightly-modified version of the minimal feature set which included, in addition, current rent, totalling 21 variables (orange rounded rectangle in Fig. 12).

Finally we also used the full feature set with 54 variables (blue rounded rectangle, Fig. 12). Each of these three feature sets were used in all model testing going forward. To note, the VIF procedure removed all gendered variables, nearly all information about age, several of the race features, as well as most of the income brackets. It retained much of the information about commute times and the type and age of housing. 



Figure 12. Variables included in each of the three feature sets used in the model testing. 

Model selection and testing
Once we completed our feature reduction and selection of candidate feature sets we set out to determine which combinations of features sets and machine learning algorithms performed the best. We performed this testing using two methods. In the first method we split our one-year-lagged datasets 100 times randomly, allocating 25% of the data to the test set and 75% for training.

For each of these random splits we trained our model on the 75% and calculated an R2 value fo the the remaining 25%, giving us a distribution of test scores for each model and feature set. In the second testing method, we create a single split using the data from 2013 to 2017 for our training set and the data from 2018 as our test set.

Since the dataset is lagged, this allows us to evaluate the forecasting ability of our models as 2018 data would forecast 2019 rent. 

These two testing methods are shown for multiple linear regression in Fig. 13. The random splitting results are shown on the left and the R2 and RMSE values are shown for the forecasting method on the right. It can be observed that linear regression performs poorly for the minimal 20-variable feature set with scores of 0.779 and 0.765 for the random split and forecasting methods respectively.

The 21-variable feature set and the full feature sets both perform well and are close to identical. In fact, the linear model for 21-variable feature set slightly outperforms the full feature set for forecasting (0.965 vs. 0.962), however this could be within the error range of the measurement.

Linear Regression Data


Figure 13. Testing the three final feature sets with a multiple linear regression model. 

Our random forest model outperforms the linear model across the board. The minimal (20-variable) feature set has an average test score of 0.917 for random splitting and 0.832 for forecasting compared to 0.779 and 0.765 for the linear model respectively (Fig. 14).

There’s a slight difference between the performance of the 21- and 54 variable feature sets with the full set outperforming the 21-variable set for both random splitting and forecasting.

However again, both sets perform significantly better than the linear model. One may note that there is a significant difference between the train and test in forecasting for the 20-variable feature set, indicating some amount of overfitting which may be an indication that further parameter tuning is needed. 

Random Forest Data


Figure 14. Testing the three features sets with a random forest model

We also looked at the feature importances for random forest models. It can be seen that for the full feature set, there are several features with similar importances (Fig 15. blue). This points to high levels of multicollinearity in our data for the full feature set, whereas this is not the case for the other two feature sets (Fig. 15 green, orange).

For the 20- and 21-variable feature sets, the most important features seem to be the number of vacant housing units, commute time, and black and asian population. Interestingly, although the current rent was included as an independent variable in the 21- and 54-variable feature sets, it does not appear as one of the top 15 most important features in Fig. 15. 



Figure 15. Feature importance for random forest models

Finally, the gradient boosting algorithm did by far the best for the random splitting with average scores oof 0.947, 0.992, and 0.992 for the 20-, 21, and 54-variable feature sets respectively. However, for forecasting, it performs slightly worse than random forest for the 21- and 54-variable sets.

Gradient Boosting Data


Figure 16. Testing our three features sets with a gradient boosting model

For gradient boosting, similar to the feature importances in random forest there are a large number of features in the full set with similarly high levels of importance for the full dataset indicative of high multicollinearity. Also similar to random forest, commuting and black population variables played a high degree of importance for the 20- and 21 variable feature sets.

For gradient boosting, however, real estate taxes and high-occupancy dwellings were highly important in contrast to random forest. 


Figure 17. Feature importance for gradient boosting models

To summarize, the performing feature set across the board was the full 54-variable set. But since this had over twice as many features as the other two, the 21-variable feature set provides a better balance of performance with interpretability and simplicity. For this feature set, the random forest model performed the best in terms of forecasting 2019 rent.

For the 20-variable feature set that does not include current rent and only includes VIFs less than 5, probably we would choose the gradient boosting model, since that has the lowest RMSE. All in all, random forest with the 21-variable feature set provides the best balance of performance and simplicity. 



Figure 18. Summary of RMSE scores for the ML models and feature sets tested.

Conclusions
We gathered data from three sources including the American Community Survey, the Internal Revenue Service, and the Building Permits Survey to form a dataset with 252 variables. Through a process of feature engineering, removing redundancies, and combining similar variables, we reduced the dataset to 54 variables. We further reduced this to 20- and 21-variable feature sets with an iterative VIF elimination strategy.

We used these final 20- 21-, and 54-variable feature sets to tune and test the performance of multiple linear regression, random forest, and gradient boosting models. Therefore, we concluded that random forest with the 21-variable feature set provided the best combination of performance and simplicity. 

Real Estate trends will continue to evolve over time and are impacted by a multitude of factors including public health and safety, increased standards of living and human preferences. In our research we wanted to discover which factors aided in forecasting rent prices. Through feature engineering and reduction our final set consisted of 21 features.

The features related to broader categories such as housing conditions, gentrification, work transportation and income inequality. Through the use of these features in multiple machine learning models we were able to forecast to within $100 of the actual housing rent price.