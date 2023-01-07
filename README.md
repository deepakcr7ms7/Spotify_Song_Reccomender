# Spotify_Song_Reccomender


## TABLE OF CONTENTS

* [Introduction](#introduction)
* [Recommendation System Pipeline](#recommendation-system-pipeline)
* [Data Collection](#data-collection)
* [Data Pre-Processing](#data-preprocessing)
* [Recommeder Model](#recommeder-model)
* [Result](#result)
* [Summary](#summary)
* [References](#references)


<hr>

## INTRODUCTION 

You might have heard the term “Recommendation System (RS)” when YouTubers are discussing the latest tactics to get more views or when you or your friends compare the “Recommended for you” list on Netflix. In a nutshell, recommendation systems recommend things that the people might like based on your own watch history or you and friends watch history as a collective. From a non-Data Science practitioner’s perspective, that’s pretty much all you need to know about RS… Oh, but you ARE a Data Science practitioner. If that’s the case, we need to dig a little bit deeper into the ideas and code behind a recommendation system.

Before we deep dive into the RS and the code, let’s take a step back and clarify some questions:

What is a recommendation system?
As I have mentioned before, the goal of a recommendation algorithm is to recommend or predict items a user might like based on their data or based on the entire user database. We will talk about precisely how to do this and the different types of RS later on, but for now, here’s a conceptual pipeline to show the process of recommending a song.

<img src="https://github.com/deepakcr7ms7/Spotify_Song_Reccomender/blob/main/images/SR.jpg" style="width:100%;">

Why should we use a recommendation for song prediction tasks?
The other question is why recommendation systems are used in a song prediction task. As you read in Part II, it is possible to use a cluster-based algorithm to predict the songs, however, it lacks the flexibility to add other features to the system, such as a classification predictor.
In other words, a clustered-based algorithm is one type of recommendation system. However, compared to the two other types of RS introduced below, a cluster-based algorithm lacks flexibility. In fact, Both content-based filtering and collaborative filtering can include the clustering outcome into the models, creating a hybrid RS.

<hr>

## Recommendation System Pipeline

<img src="https://github.com/deepakcr7ms7/Spotify_Song_Reccomender/blob/main/images/1_ykSeY0--iyoq7xRqCPZS_g.jpg" height=300 style="width:100%;">

<hr> 

## DATA-COLLECTION 

Spotify keeps a lot of data on its songs internally, that we can access through the Spotify API. The Spotify API is a great public tool, allowing the use of Spotify’s wealth of data on music to build many kinds of systems. I used this API through Python’s Spotipy package to extract data from unique song identifiers.

<li> Package used: spotipy</li>
<li>Number of songs collected = 1 million playlist data</li>
<li>No null values identified</li>

<hr>

## DATA-PREPROCESSING
<b> Data Cleaning </b> 
<li> Dropped duplicate songs</li> 
<li> Selected features that are relevant using feature engineering (more information in full notebook)</li> 
<li> After selecting the useful data, due to the import format of a dataframe, convert the genres columns back into a list</li> 
<br><img src="https://github.com/deepakcr7ms7/Spotify_Song_Reccomender/blob/main/images/1__g-kOo6eZ9Gzw5TLkgwrSQ.jpg" height=300 style="width:100%;">

<li> Processed metadata using TfidfVectorizer() </li>

<li> Normalised songs audion features using MinMaxScaler() function in scikit learn </li>
<li> Conducted sentiment analysis finding the polarity and subjectivity of the track name using TextBlob.sentiment  </li>
<br> 

<hr> 

## Recommeder Model

I used content-based filtering algorithm to make recommendations
<br> Two steps were implemented in the algorithm. These two steps are needed every time some enters a new playlist query:
* Playlist Summarization:
<br> Added all the feature values of each song in the playlist together to create a summarization vector
<br> <img src="https://github.com/deepakcr7ms7/Spotify_Song_Reccomender/blob/main/images/1_SAIvaJvq7UWGPm5G-xG97Q.jpg" height=400 style="width:100%;">
* Similarity and Recommendation:
<br>After retrieving the playlist summarized vector and the non-playlist songs, we can find the similarity between each individual song in the database and the playlist. The similarity metric chosen is cosine similarity.

<br>Cosine similarity is a mathematical value that measures the similarities between vectors. Imagining our songs vectors as only two-dimensional, the visual representation would look similar to the figure below.
<br><img src="https://github.com/deepakcr7ms7/Spotify_Song_Reccomender/blob/main/images/0_l9DGLIR87oVI5Aq7.jpg" height=300 style="width:100%;">

<br>I used the cosine_similarity() function from scikit learn to measure the similarity between each song and the summarized playlist vector.

## Result
One of the biggest problems with this model is that there are almost no metrics to evaluate whether the recommendation is good or bad. Since in this project, a clustering-based approach was conducted in Part II. We’ve decided to compare the two recommendations to see if there is any consensus or not.
#
Comparison
<p float="left" >
  <img src="https://github.com/deepakcr7ms7/Spotify_Song_Reccomender/blob/main/images/SR_result1.jpg" alt="Preprocessing" height="500"width="400"  />
  <img src="https://github.com/deepakcr7ms7/Spotify_Song_Reccomender/blob/main/images/SR_result2.jpg" alt="Augmented Images" height="500" width="400" />
</p>
<br> Top 20 songs in Mom’s playlist (left) and the recommended result by two recommendation algorithms (right). Here, the two methods are the content-based filtering approach and the clustering method using K-nearest neighbors. 

## Summary
In this project, I first learned the basics of recommendation systems, involving the two general approaches of content-based filtering and collaborative filtering methods. Then, built a content-based filtering recommendation system using Spotify playlists data from scratch. This involves the procedure of feature preprocessing, feature generation, and recommendation modeling. Lastly, I compared the recommendation with other song recommendation systems, specifically, the clustering methodology, and see the difficulties in measuring success for recommendation systems in an open-source environment.

## References
<li> Google Developers, Content-based Filtering (2021) </li>
<li> A. Roy, Introduction To Recommender Systems- 1: Content-Based Filtering And Collaborative Filtering (2020), on Towards Data Science</li>
<li>M. Thaker, Spotify Recommendation System (2020), on Github </li>
<li> W. Scott, TF-IDF from scratch in python on a real-world dataset. (2019), on Towards Data Science </li>
<li> P. Shah, Sentiment Analysis using TextBlob (2020), on Towards Data Science</li>
<li> Spotipy, spotipy documentation (n.d.) </li>

