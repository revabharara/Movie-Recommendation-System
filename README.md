# 📡Movie-Recommendation-System

This movie recommendation system that uses content-based, popularity-based, and collaborative filtering techniques is a powerful tool for improving user engagement and satisfaction. By leveraging multiple models and datasets, the system can recommend movies based on a user's preference and help them discover new content.

# ❓ Need of the model

We need this movie recommendation system model to help users discover movies that they are likely to enjoy based on their past preferences and behavior. By using different types of recommendation models (content-based, popularity-based and collaborative-filtering-based), we can provide a personalized and diverse selection of movie recommendations to cater to different user tastes. This can enhance the user experience, increase user engagement, and ultimately drive revenue for the platform.


## ⚖️ About the Dataset

 This project uses three datasets:
 1. movies.csv - used for making content based and popularity based recommendation systems
 2. movie_names.csv and ratings.csv - used for collaborative filtering based recommendation system
 
### 📝1. movies.csv:

| Column ID  | Column Name            | Data type | Description                                   |
|------------|-----------------------|-----------|-----------------------------------------------|
| 0          | index                 | int64     | Unique identification for each item           |
| 1          | budget                | int64     | Budget of the movie                           |
| 2          | genres                | object    | Genres of the movie                           |
| 3          | homepage              | object    | Homepage of the movie                          |
| 4          | id                    | int64     | ID of the movie                                |
| 5          | keywords              | object    | Keywords associated with the movie             |
| 6          | original_language     | object    | Original language of the movie                 |
| 7          | original_title        | object    | Original title of the movie                    |
| 8          | overview              | object    | Overview or plot of the movie                  |
| 9          | popularity            | float64   | Popularity score of the movie                   |
| 10         | production_companies  | object    | Production companies associated with the movie |
| 11         | production_countries  | object    | Production countries associated with the movie |
| 12         | release_date          | object    | Release date of the movie                      |
| 13         | revenue               | int64     | Revenue generated by the movie                 |
| 14         | runtime               | float64   | Runtime of the movie in minutes                 |
| 15         | spoken_languages      | object    | Spoken languages in the movie                  |
| 16         | status                | object    | Status of the movie                            |
| 17         | tagline               | object    | Tagline of the movie                           |
| 18         | title                 | object    | Title of the movie                              |
| 19         | vote_average          | float64   | Average rating of the movie                     |
| 20         | vote_count            | int64     | Number of votes received by the movie           |
| 21         | cast                  | object    | Cast members in the movie                      |
| 22         | crew                  | object    | Crew members involved in the movie             |
| 23         | director              | object    | Director of the movie                          |

### 📝2. movie_names.csv:

| Column ID  | Column Name | Data type | Description |
|------------|-------------|----------|-------------|
| 0          | movieId     | int64    | Unique identification for each movie |
| 1          | title       | object   | Title of the movie |
| 2          | genres      | object   | Genres of the movie |

### 📝3. rating.csv:

| Column ID | Column Name | Data type | Description |
| --------- | ----------- | --------- | ----------- |
| 0         | userId      | int64     | Unique identification for each user |
| 1         | movieId     | int64     | Unique identification for each movie |
| 2         | rating      | float64   | The rating given by the user for the movie |
| 3         | timestamp   | object    | The timestamp when the rating was given |



# 🛣️ Roadmap for the project

## 🔭 Data exploration

Exploratory analysis involves cleaning and analyzing the dataset to gain insights about the movies' characteristics, such as genre distribution, popularity, and ratings. The data is explored to identify patterns and correlations that can be useful for building the recommendation models. The insights are then used to inform the subsequent stages of the project.

## ⚙️ Data Preprocessing:

In this section we will:
1. *Clean the data*
    * We will be replacing the missing values of the feature that we will be using but since there were none in the required set of features this step was not             performed.  
    
2. *Extract the features*
    * For the content based recommendation we will be using the TFIdfvectorizer from sklearn.feature_extraction.text and convert the content into numerical vectors         that can be processed later
    * We will also be using cosine similarity to get the similarity matrix and thereafter recommend the similar movies with similarity score closer to 1.
    * Difflib was used to process user input in case there are any typos.
    

## 	🌎 Collaborative filtering based recommendation system
This is a movie recommendation system that uses collaborative filtering to recommend movies to users. The system uses K-means clustering to group users and movies into clusters based on their similarity, which helps identify similar users and recommend movies to them.

### 🌑 Data Preparation
The first step in creating a collaborative filtering-based recommendation system is to prepare the data. This includes cleaning the data, removing duplicates, and ensuring that it is in a format that can be used by the model. There were two data frames the movies and the rating, I had to merge then appropriately to make use of them.

### 🌒 Dataset Analysis

### 1. Finding the average user rating of each movie
To find the average user rating of each movie, I grouped the ratings by movie ID and calculated the mean rating for each movie. This information can be useful in the popularity-based recommender system.

### 2. Finding the likability of each genre
To find the likability of each genre, I calculated the percentage of ratings that each genre received out of the total number of ratings. This information can be useful in both the content-based and collaborative filtering recommender systems.

![image](https://user-images.githubusercontent.com/89579327/230011527-67f22cf1-679e-429d-83a4-f49fa8fb6269.png)


### 3. Number of movies in each genre
To get an idea of the distribution of movies across genres, I counted the number of movies in each genre. This information can be useful in the content-based recommender system.

![image](https://user-images.githubusercontent.com/89579327/230011577-099610bf-edf0-4d24-89b3-499cf60770d3.png)


### 🌓 Model Initialization
The next step is to initialize the collaborative filtering model. This involves selecting the appropriate parameters and fitting the model to the data.
The best parameters selecetd were as follows:
```
KMeans(init='k-means++', n_clusters=5, n_init=12)
```
### 🌔 Clustering
Once the model is initialized, the system uses K-means clustering to group users and movies into clusters based on their similarity. This is done by calculating the similarity between users and movies and grouping them into clusters based on their similarity scores.

### 🌕 Elbow Method
To find the optimal number of clusters, the system uses the elbow method. This involves plotting the within-cluster sum of squares for different values of k and selecting the value where the curve starts to flatten out. The best value of the clusters was found out to be 5.


![image](https://user-images.githubusercontent.com/89579327/230010311-3a70dffa-6ca7-48f0-a46c-508f8be25e03.png)


------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 	🎬 Content based recommendation system

This system recommends movies to users based on their similarity to other movies in the dataset with similar content, such as genre keywords, tagline, cast, crew, director and title. This involves the following processes:

### 🌒 Feature Extraction
The next step after the data is preprocessed involves feature extraction, where the content-based recommendation system converts the movie content into numerical vectors that can be processed by the algorithm. This is done using the TF-IDF vectorizer, which assigns weights to each word in the dataset based on its frequency and importance in the movie content.

### 🌓 Processing User Input
To provide personalized movie recommendations to users, the content-based recommendation system uses difflib to process user input and correct spelling errors. This helps improve the accuracy of the recommendations and ensures that the user's input is processed correctly.

### 🌔 Similarity Score Calculation
After processing user input, the content-based recommendation system uses cosine similarity to calculate the similarity score between the user's input and the movies in the dataset. The similarity score is used to identify the most relevant movies and to rank them based on their similarity to the user's input.

<img width="406" alt="image" src="https://user-images.githubusercontent.com/89579327/229286477-b13e87f1-579a-4656-942c-561a1c928b8a.png">


### 🌕 Movie Recommendation
Based on the similarity score, the content-based recommendation system recommends movies to the user that have similar content to their input. These recommendations are provided in a list, which can be sorted by the user based on their preference.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 	🔥 Popularity based recommendation system

The popularity-based recommendation system is one of the three types of models used in the movie recommendation system project. This system recommends movies to users based on their popularity, user rating, and vote count.

### ✨Approach 1: Conditional-Based Recommendation

#### 1️⃣ Condition-Based Filtering: Only recommend movies that meet certain conditions, such as having a vote count greater than 100, a user rating of 8 and above, or higher popularity.

#### 2️⃣ Movie Recommendation: Provide a list of movies that meet the conditions and sort them based on the user's preference.

### ✨Approach 2: IMDB Weighted Rating Formula

#### 1️⃣ Calculation of IMDB Weighted Rating Formula: Calculate the IMDB weighted rating formula, which takes into account the average rating, the number of votes, and the popularity of the movie.

#### 2️⃣ Movie Recommendation: Recommend movies based on the calculated IMDB weighted rating formula. These recommendations can be sorted by the user based on their preference.

### 🎋 GUI:

### 🎍 Conclusion:
In conclusion, the movie recommendation system that uses content-based, popularity-based, and collaborative filtering techniques can significantly improve user engagement and satisfaction. While there are limitations to the project, such as expanding the feature space and improving the accuracy of the models, the system has promising future prospects for applications in the movie industry and beyond.


### 🧮 Limitations:
1. Limited scalability: The system may struggle to scale to larger datasets or a larger number of users, which may impact its efficiency and accuracy.

2. Limited feature space: The system relies on a limited set of features, such as genre, title, and user ratings, which may not capture all aspects of a movie that may be important to users, such as director, actors, or plot.


### 🔮 Future Prospects:

1. Incorporation of advanced techniques: Advanced techniques such as deep learning, natural language processing, or sentiment analysis could be incorporated to improve the recommendations and make them more nuanced.

2. Improvement of the user interface: The user interface of the recommendation system could be improved to enhance the user experience and make it more visually appealing and intuitive.


### 👩‍🦱 Credits:
Reva Bharara

Email : revabharara@gmail.com, bhararareva@gmail.com

Linkedin : https://www.linkedin.com/in/reva-bharara-a83a78241/
