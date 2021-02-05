
# Project 2: Analysis of Ames Housing Data

## Background
NexProp is a property consultancy that represents prospective sellers in Ames, Iowa. As part of their offering, they would like to help prospective sellers price their properties competitively and also provide guidance on how sellers can command greater value for their houses.

## Problem Statement
Using the Ames housing dataset, NexProp would like to create a model that will help sellers accurately estimate the sale price of their house. The model should also help showcase which features are likely to increase the value of a house, so that NexProp employees can help customers in increasing the value of their property.

## Executive Summary

Through thorough data cleaning, exploratory visualizations and preprocessing, NexProp has built 3 robust models (Linear Regression, Ridge and Lasso) to accurately predict the sale price of a property in Ames, Iowa. Based on the evaluation, the ridge model performed best in reducing the root mean squared error. As such, the model was chosen to be deployed.

## Business Recommendations
Using the ridge model, NexProp can help prospective sellers get a fairly close estimate of the sale price of their house, given its features.

While factors such as living area, neighborhood, lot frontage and lot configuration can't much be changed, quality of the house also plays a key role in making it more attractive to the market. NexProp can help prospective sellers focus on improving the overall quality, external quality, kitchen and basement quality of their houses. Prospective sellers may also consider remodelling to increase the value of their property. If remodelling, it is worth noting that brick face exteriors and hip style roofs command greater value. 

Overall, the model will help NexProp and its customers in being market-ready. However, it is worth noting that the model may not perform well in predicting properties with higher SalePrice as the current dataset did not have many datapoints for higher-priced properties. Also, the existing model is based closely on the housing features within the Ames housing dataset. To make it more generalizable to other areas, NexProp will need to focus more closely on universal housing features such as area, rooms, facilities etc.
