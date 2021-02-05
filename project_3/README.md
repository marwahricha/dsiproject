
# Executive Summary

InfluencerX employees and the influencers under the company's label contribute actively to various entertainment-related subreddits on popular social media site Reddit. These include ones for Netflix and Amazon Prime Video, two of the biggest over-the-top media streaming services.

To streamline content posting, InfluencerX needs a model to help the influencers and its employees label their posts as belonging to either the Netflix subreddit or the Prime Video subreddit.To this end, this project leverages existing posts from the Netflix and Amazon Prime Video subreddits to create a binary classification model that can accurately predict which subreddit a given post belongs to.

After undertaking exploratory data analysis and appropriate data preprocessing, we compare three models, a Naive Bayes classifier, a Logistic Regression classifier and a K Nearest Neighbors (KNN) classifier. For each of the models, we test both a CountVectorizer and Term Frequency-Inverse Document Frequency (TF-IDF) Vectorizer to turn the text into a structured, numeric dataframe.

While the Naive Bayes model with TF-IDF has slightly higher accuracy on the training dataset, the CountVectorizer model performs just a little bit better on the test data with an accuracy of 73.38%. However, there is quite a difference between the train and test scores for both models suggesting overfitting.

Same as with the Naive Bayes model, the CountVectorizer model for Linear Regression performs just a little bit better than the TF-IDF model on the test data (with an accuracy of 74.1%). However, there is quite a difference between the train and test scores for both models suggesting overfitting.

The Linear Regression with CountVectorizer model does a little bit better than the Naive Bayes model with CountVectorizer.

For KNN, the CountVectorizer performs very poorly. The TF-IDF model performs about the same as the Naive Bayes and Logistic Regression models (with a test accuracy of 72.66%). In this case as well, we observe considerable overfitting in both the CountVectorizer and TF-IDF models.

Overall, as Logistic Regression with CountVectorizer has the highest test accuracy at 74.1%, we selected it as our production model.

By deploying the Logistic Regression classifier model with CountVectorizer, InfluencerX can label a post as belonging to either the Netflix subreddit or Prime Video subreddit with 74.1% accuracy.

One of the key limitations of the model at this point is the overfitting on the training dataset. To avoid this, we can look at training models with more data, when available.

Based on an analysis of misclassified posts, we can also look at creating a list of generic words that can be used as stopwords to potentially improve accuracy.

To further improve accuracy, future projects can evaluate other models, should the project scope allow it, and even look at ensembling, which combines predictions from multiple separate models.

As the model is not a 100% accurate at this point, there will likely still be a need for some human intervention before posting. However, the model can help streamline the content posting process and reduce man-hours spent on the process.
