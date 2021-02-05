
# Project 1: SAT & ACT Analysis

## Problem Statement
Following the release of a new SAT format in 2016, the College Board is keen to drive participation rates for the examination across the country. This project aims to analyze the state participation rates and scores for both the SAT and the ACT examinations in 2017 and 2018, to identify key factors influencing these metrics and provide recommendations on how the College Board can best allocate its funds to further improve the numbers.

## Executive Summary

### Contents:
- [2017 Data Import & Cleaning]
- [2018 Data Import and Cleaning]
- [Exploratory Data Analysis]
- [Data Visualization]
- [Descriptive and Inferential Statistics]
- [Outside Research]
- [Conclusions and Recommendations]

## Data Dictionary

### SAT dataset:
|Feature|Type|Dataset|Description|
|---|---|---|---|
|state|object|2017 SAT| - |
|sat_part_17|integer|2017 SAT|SAT participation rate (in percentage)|
|sat_erw_17|integer|2017 SAT|Average SAT evidence-based reading and writing score for the state (out of 800)|
|sat_math_17|integer|2017 SAT|Average SAT math score for the state (out of 800)|
|sat_math_17|integer|2017 SAT|Average total SAT score for the state (out of 1600)|

### ACT dataset:
|Feature|Type|Dataset|Description|
|---|---|---|---|
|state|object|2017 ACT|-|
|act_participation_17|integer|2017 ACT|ACT participation rate (in percentage)|
|act_eng_17|float|2017 ACT|Average ACT english score for the state (out of 36)|
|act_math_17|float|2017 ACT|Average ACT math score for the state (out of 36)|
|act_reading_17|float|2017 ACT|Average ACT reading score for the state (out of 36)|
|act_sci_17|float|2017 ACT|Average ACT science score for the state (out of 36)|
|act_composite_17|float|2017 ACT|Average ACT composite score for the state (out of 36)|

## Conclusions and Recommendations
Based on the exploration of the SAT and ACT data for 2017 and 2018 we see that average SAT participation has increased marginally from 2017 to 2018. However, the ACT continues to have a stronghold in many states. Not surprisingly, there is an inverse relationship between the SAT participation and ACT participation, suggesting that students seem to prefer to take one exam. Based on research, it also seems that the choice of exam is heavily influenced by state policies and requirements.

While the College Board may require more time to influence state policies and requirements, it can focus on states like Florida in the meanwhile where participation has fallen and there are no mandates from the state requiring students to take a particular exam. The College Board can recreate its success in Colorado by working with schools to administer the SAT during the school day for no cost to students.

For further analysis, it would be great to get official data on the state requirements and resources for both the SAT and ACT to see how those factors influence participation rates.
