# Background
Public screening of movies dates back to as early as the 1800s, and movies have since become an integral form of mass media and entertainment. However, we have all witnessed and contributed to the shift from theatrical to home entertainment, led by the growth of online streaming services like Netflix, Amazon Prime and Apple TV. In fact, according to industry reports, the home entertainment market has grown from 15.8 billion USD in 2014 to 42.6 billion USD in 2018.

This change in consumer habits has been further accelerated by the Covid-19 pandemic and subsequent restrictions on large public gatherings. As online consumption of movies and other video entertainment continues to grow, the competition in the online streaming industry is also intensifying, with greater investments from established players and new players entering the market.

# Problem Statement
A new online movie streaming service, Binge, is planning to launch operations in Singapore. As members of its product development team, we have been tasked with creating:

<li>A storyline-based genre prediction system for classification of new movies on the platform</li>
<li>A system to provide personalized movie recommendations</li>

# Data
The dataset was retrieved from Kaggle and was originally scraped from the publicly available website https://www.imdb.com. All movies with more than 100 votes were scraped as of 01/01/2020.

It includes 85,855 movies with attributes such as movie description, average rating, number of votes, genre, etc.

# Modeling - Movie Genre Prediction
The prediction of genres is essentially a multi-label classification as we have seen that movies can belong to multiple genres. However, most traditional models are developed for single-label classification. Therefore, we looked at our multi-label classification as multiple single-label classifications (also known as a OneVsRest approach).

After the necessary data cleaning and initial exploratory analysis to get a better understanding of the available data, we ran 3 models used commonly for classification, K-Nearest Neighbors, Logistic Regression and Multinomial Naive Bayes.   

Each model was run through a pipeline with a vectorizer (we used CountVectorizer and TfidfVectorizer). As drama was the genre with the most number of movies under it, we tested each of the pipeline models using the drama category and then ran the best-performing variant across all categories.

Overall, the Multinomial Naive Bayes classifier with the TfidfVectorizer and the Logistic Regression classifier with the TfidfVectorizer performed roughly the same (0.72 test accuracy), although both models were overfitted.

Multinomial Naive Bayes with TfidfVectorizer was chosen as the production model. We observed that the genres from the top 10 with more distinct words, such as the adventure and sci-fi genres, performed a lot better than genres such as drama and comedy. In general, the model seemed to perform a lot better for the less common genres such as family, fantasy and western.

Overall, although the model had relatively low hamming loss, the subset accuracy was poor likely due to misclassification of the more common genres such as drama, comedy and romance where storylines are less distinct.

# Model Limitations and Next Steps

In using the OneVsRest Classifier for training our model, we ignored any correlation between genres for movies with multiple labels. However, this may not always be the case.

In addition, labels are predicted based purely on the unique genres found within the IMDB dataset. Further iterations of the model maybe required to train for new genre.

# Modeling - Recommender System

As new online streaming services enter the market, customer experience and satisfaction are becoming increasingly important for attracting and retaining an audience. In the fight for customer engagement and dollars, personalization can be key.

For the purpose of this project, we created two content-based movie recommender systems, one based on movie storylines and the other based on a combination of movie genres and description.

While the storyline-based recommendation system provided some relevant recommendations, the recommender based on both the genres and movie description appeared to give a better set of recommendations, moving beyond just recommending movies with the same/similar characters. This will benefit Binge as customers are more likely to discover new content.

# Model Limitations and Next Steps

The recommender models developed are simple models based on the exhaustive list of movies marked to be in English within the IMDB dataset. Expanding the pool of movies will increase the richness of the recommendations provided.

In addition, these recommender systems are purely content-based as the Binge platform is currently under development and the company does not have access to any user data.

Once the platform has been launched and user data is available, Binge can look into developing collaborative recommender systems that can provide recommendations based on user profiles.

# Conclusion
New content is being generated everyday. IMDB recorded 9906 feature film releases in 2020 alone.

The genre prediction and recommender systems provide a good starting point for Binge to optimize its internal operations and create an entertainment platform that can engage and vow users.

Once Binge rolls out its services, it can also look into collecting user feedback and undertaking A/B testing to improve its content classification and recommendation capabilities.
