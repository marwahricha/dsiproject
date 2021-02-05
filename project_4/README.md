# Background
West Nile virus (WNV) is the leading cause of mosquito-borne disease in the United States.

While only round 20% of people who become infected with the virus develop symptoms (ranging from mild symptoms like a persistent fever, to serious neurological illnesses that can result in death), cost of medical treatment can be high. As per the Centers for Disease Control and Prevention, no vaccine or specific antiviral treatments are available. As such, prevention of the disease relies largely on management of mosquitos through various control tactics.

In 2002, the first human cases of WNV were reported in Chicago. By 2004, the City of Chicago and the Chicago Department of Public Health (CDPH) established a comprehensive surveillance and control program that is still in effect today. Every week from late spring through the fall, mosquitos in traps across the city are tested for the virus. The results of these tests influence when and where the city will spray airborne pesticides to control adult mosquito populations.

# Analysis and Predictive Modeling

This project aimed to provide aggregated analysis of weather, spray and trap data in the city of Chicago during the period 2007 to 2013, for the purpose of constructing a predictive model for forecasting occurrences of WNV.

After thorough data cleaning and exploratory analysis, we ran 10 models using Logistic Regression, K Nearest Neighbors, Decision Trees, Bagging Tree, Gradient Boosting, Extra Trees, Random Forest, AdaBoost, SVC and XG Boost. As the classes were heavily unbalanced, we used the Synthetic Minority Oversampling TEchnique (SMOTE) as a means to oversample the positive class (WNV-present).

For model evaluation, we recorded train and test scores, ROC-AUC scores, specificity, sensitivity and F1 scores for each of the 10 models. We settled on sensitivity as our key evaluation metric. This was as a result of our established priority to reduce the incidences of false negatives (predicted as WNV-negative, when in reality that trap is WNV-positive). While presence of false positives would technically drive down the overall accuracy score, especially when the majority class is WNV-negative, it obscures the reality that the high cost of patient treatment for WNV illness far surpasses the cost of mosquito surveillance measures.

Although the Gradient Boosting and XG Boost models performed best in terms of accuracy (0.91 and 0.92 respectively), both models had rather low sensitivity scores (0.12 and 0.14 respectively), i.e. they did not do a great job of predicting the positive class (presence of the WNV). In this regard, Logistic Regression and AdaBoost classifiers come out on top, with sensitivity scores of 0.84 and 0.73 and ROC-AUC scores of 0.78 each. Ultimately, Logistic Regression was chosen as the production model as it had the highest sensitivity score (0.84) and ROC-AUC score (0.78) amongst all the models.

Upon evaluating the coefficients from the Logistic Regression model, Week of Year had the strongest coefficient value. Other time-centric features like month_of_year also tended to influence the outcome of WNV occurrence.

WetBulb had the second strongest coefficient value. The positive value indicated that a high wet bulb temperature would contribute to the likelihood of a trap being classified as WNV-positive. Other weather-centric features, particularly the historical weather features such as WetBulb_mean_past7day, Tavg_mean_past14day and Tavg_mean_past7day also featured in the top 15 features. Interestingly, DewPoint had a strong negative coefficient, seemingly indicating that lower humidity leads to higher likelihood of WNV occurrence. The earlier EDA phase revealed inconsistent trends when monthly mean dew point was plotted against mosquito-count and WNV-occurrence. Based on this coefficient analysis, perhaps historical dew point feature may shed more light as to whether a certain level of humidity in a preceding period could have an impact on WNV occurrence.

Culex Territans species was seen to have a negative coefficient, mostly owing to the fact that it is not one of the carrier species of WNV, thus presence of this species in an observation would lower the likelihood of WNV prediction.

# Model Limitations

It is worth noting that the model is limited to usage within Chicago as weather patterns differs within states and countries, as do the species of mosquitos.

Official cost figures of the spray were unavailable and the frequency of spray count was inconsistent. As a result, we cannot further view a trend between the number of mosquitos and the spray count.

As the spray data was dropped during the EDA process, only inputs from train, especially the trap, and the weather dataset were used to build the final production model. Hence, the cost benefit effectiveness of the spray cannot be measured as the model only measures against certain weather patterns.

# Cost-Benefit Analysis

According to a study on the outbreak of WNV disease in Sacramento County, California in 2005, treatment costs for patients were approximately USD 2,140,409 and the total costs including productivity loss was approximately USD 2,844,338 (across 46 patients). This amounts to roughly USD46,500 per person for medical costs and USD15,500 per person in terms of productivity loss. Based on the average number of cases in Chicago in the past 3 years (roughly 50), total expected loss amounts to approximately USD 3.1 million.

On the other hand, spray procedures based on bi-weekly spray of traps and hotspots during breeding season (assumed to be 6 months) is estimated to cost roughly USD 706,320 (USD 155,520 to spray traps + USD 550,800 for sprays in the city).

Overall, estimated costs in terms of medical treatment and productivity loss far exceed the spray costs. This reiterated the project's focus on reducing false negatives as the medical and human costs of the virus spreading are much higher than any potential additional expenditure on vector control which may be incurred as a result of executing mosquito surveillance measures on false positives.

# Conclusion
The production model did a decent job in providing the most predictive features. The model can be used to help the city in identifying potential outbreaks. As the model has the least False Negatives among the other models, it's more likely to detect the areas with WNV presence in them. Combined with vigilant monitoring on the ground and educating the public on the prevention of mosquito breeding, we believe that this could significantly decrease the number of mosquitos as well as the presence of WNV.

Should resources permit, we can also do a study on reducing the number of reservoir hosts (dead birds) within the city to effectively kill the source of the WNV.

# Data Dictionary
Based on train_final_v2_daylight.csv features used for selected production model.

| Column               | Type  | Origin                               | Description                                                                                     |
|----------------------|-------|--------------------------------------|-------------------------------------------------------------------------------------------------|
| Latitude            | float | train.csv                                   |  Latitude of trap                                        |
| Longitude        | float   | train.csv                            | Longitude of trap                                        |
| WnvPresent        | int   | train.csv                                   | Whether West Nile Virus is present (1 denotes present, 0 denotes absent)                   |
| species_culex_erraticus   | int | Feature Engineered                                  | Whether the Culex Erraticus species is present in trap (1 denotes present, 0 denotes absent)        |
| species_culex_pipiens           | int                              |  Feature Engineered                         | Whether the Culex Pipiens species is present in trap (1 denotes present, 0 denotes absent)                |
| species_culex_pipiens_restuans       | int                             | Feature Engineered                          | Whether the Culex Pipiens-Restuans species is present in trap (1 denotes present, 0 denotes absent)                               |
| species_culex_restuans       | int                             | Feature Engineered                          | Whether the Culex Restuans species is present in trap (1 denotes present, 0 denotes absent)                                   |
| species_culex_salinarius       | int                             | Feature Engineered                          | Whether the Culex Salinarius species is present in trap (1 denotes present, 0 denotes absent)                                |
| species_culex_tarsalis       | int                             | Feature Engineered                          | Whether the Culex Tarsalis species is present in trap (1 denotes present, 0 denotes absent)                                |
| species_culex_territans      | int                             | Feature Engineered                          | Whether the Culex Territans species is present in trap (1 denotes present, 0 denotes absent)                                  |
| species_unspecified_culex       | int                             | Feature Engineered                          | Whether the unspecified Culex species is present in trap (1 denotes present, 0 denotes absent)                                   |
| month_of_year        | int                             | Feature Engineered                          | Month of the year                                 |
| week_of_year       | int                             | Feature Engineered                          | Week of the Year                                 |
| Tavg       | int                             | weather.csv                         | Average temperature in Degrees Fahrenheit                                |
| Depart      | int                             | weather.csv                         | Departure from 30 year normal temperature for the particular date. A minus (-) is number of degrees below normal. A zero (0) indicates that the average for that day was the normal.                                |
| DewPoint      | int                             | weather.csv                         | Average dew point in Degrees Fahrenheit                                |
| WetBulb      | int                             | weather.csv                         | Average wet bulb in Degrees Fahrenheit                                |
| Heat     | int                             | weather.csv                         | Heating measured in degree days (base 65 Degree Fahrenheit, season begins with July)   |
| Cool     | int                             | weather.csv                         | Cooling measured in degree days (base 65 Degree Fahrenheit, season begins with January)     |
| PrecipTotal     | float                             | weather.csv                         | Water equivalent of rainfall and melted snow in inches     |
| StnPressure     | float                            | weather.csv                         | Average station pressure (inches of hg)   |
| SeaLevel     | float                             | weather.csv                         | Average sea level pressure (inches of hg)    |
| ResultSpeed     | float                             | weather.csv                         | Resultant wind speed in miles per hour     |
| ResultDir    | int                             | weather.csv                         | Resultant direction (whole degrees)     |
| AvgSpeed     | float                             | weather.csv                         | Average wind speed in miles per hour     |
| CodeSum_BR    | int                             | Feature Engineered                         | Presence of mist (1 denotes present, 0 denotes absent)    |
| CodeSum_DZ    | int                           | Feature Engineered                         | Presence of drizzle (1 denotes present, 0 denotes absent)     |
| CodeSum_FG    | int                             | Feature Engineered                         | Presence of fog (1 denotes present, 0 denotes absent)     |
| CodeSum_HZ    | int                             | Feature Engineered                         | Presence of haze (1 denotes present, 0 denotes absent)     |
| CodeSum_RA    | int                             | Feature Engineered                         | Presence of rainfall (1 denotes present, 0 denotes absent)     |
| CodeSum_TS    | int                             | Feature Engineered                         | Presence of thunderstorm (1 denotes present, 0 denotes absent)     |
| CodeSum_TSRA    | int                             | Feature Engineered                         | Presence of thunderstorm and rainfall (1 denotes present, 0 denotes absent)     |
| CodeSum_VCTS    | int                             | Feature Engineered                         | Presence of thunderstorm in the vicinity (1 denotes present, 0 denotes absent)     |
| Tavg_mean_past7day   | float                             | Feature Engineered                         | Tavg mean in the past 7 days     |
| WetBulb_mean_past7day    | float                             | Feature Engineered                         | WetBulb mean in the past 7 days     |
| Heat_mean_past7day    | float                            | Feature Engineered                         | Heat mean in the past 7 days     |
| Cool_mean_past7day    | float                           | Feature Engineered                         | Cool mean in the past 7 days     |
| AvgSpeed_mean_past7day     | float                            | Feature Engineered                         | Tavg mean in the past 7 days     |
| PrecipTotal_mean_past7day    | float                            | Feature Engineered                         | PrecipTotal mean in the past 7 days     |
| CodeSum_RA_sum_past7day    | int                             | Feature Engineered                         | Presence of rainfall in the past 7 days (1 denotes present, 0 denotes absent)     |
| CodeSum_TSRA_sum_past7day    | int                             | Feature Engineered                         | Presence of thunderstorm and rainfall in the past 7 days (1 denotes present, 0 denotes absent)     |
| CodeSum_DZ_sum_past7day    | int                             | Feature Engineered                         | Presence of drizzle in the past 7 days (1 denotes present, 0 denotes absent)     |
| Tavg_mean_past14day     | float                             | Feature Engineered                         | Tavg mean in the past 14 days     |
| WetBulb_mean_past14day     | float                            | Feature Engineered                         | WetBulb mean in the past 14 days     |
| Heat_mean_past14day    | float                            | Feature Engineered                         | Mean Heat in the past 14 days     |
| Cool_mean_past14day     | float                            | Feature Engineered                         | Cool mean in the past 14 days     |
| AvgSpeed_mean_past14day     | float                            | Feature Engineered                         | Mean AvgSpeed in the past 14 days  |
| PrecipTotal_mean_past14day    | float                            | Feature Engineered                         | PrecipTotal mean in the past 14 days     |
| CodeSum_RA_sum_past14day    | int                            | Feature Engineered                         | Presence of rainfall in the past 14 days (1 denotes present, 0 denotes absent)     |
| CodeSum_TSRA_sum_past14day    | int                            | Feature Engineered                         | Presence of thunderstorm and rainfall in the past 14 days (1 denotes present, 0 denotes absent)     |
| CodeSum_DZ_sum_past14day    | int                            | Feature Engineered                         | Presence of drizzle in the past 14 days (1 denotes present, 0 denotes absent)     |
| CodeSum_RA_sum_past21day   | int                            | Feature Engineered                         | Presence of rainfall in the past 21 days (1 denotes present, 0 denotes absent)     |
| CodeSum_TSRA_sum_past21day    | int                             | Feature Engineered                         | Presence of thunderstorm and rainfall in the past 21 days (1 denotes present, 0 denotes absent)     |
| CodeSum_DZ_sum_past21day    | int                             | Feature Engineered                         | Presence of drizzle in the past 21 days (1 denotes present, 0 denotes absent)     |
| Daylight_duration_in_minutes    | float                             | Feature Engineered                         | Duration of daylight in minutes derived from Sunrise and Sunset timing    |

# Sources
1) Centers for Disease Control and Prevention <br>
 (https://www.cdc.gov/westnile/index.html) <br>
2) West Nile Virus: An Historical Overview <br>
(https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3111838/) <br>
3) Economic Cost Analysis of West Nile Virus Outbreak, Sacramento County, California, USA, 2005 <br>
(https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3322011/#R6) <br>
4) Healthy Chicago Data Brief West Nile Virus <br>
(https://www.chicago.gov/content/dam/city/depts/cdph/food_env/general/West_Nile_Virus/WNV_2018databrief_FINALJan102019.pdf) <br>
5) Comparison of the Efficiency and Cost of West Nile Virus Surveillance Methods in California <br>
(https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4340646/) <br>
6) City to Spray Insecticide Thursday to Kill Mosquitoes <br>
(https://www.chicago.gov/city/en/depts/cdph/provdrs/healthy_communities/news/2020/august/city-to-spray-insecticide-thursday-to-kill-mosquitoes0.html#:~:text=CHICAGO%20%2D%20The%20Chicago%20Department%20of,Thursday%2C%20August%2027%2C%202020) <br>
7) Cost of Spray <br>
(https://www.forestrydistributing.com/aqua-zenivex-e20-ulv-insecticide-zeocon) <br>
8) Mosquito Control Resources for Professionals <br>
(https://www.centralmosquitocontrol.com/resources/calculator) <br>
