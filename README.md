# Movie Recommendation App
## Authors
* Claire Brekken
* Rachel Brynsvold
* Asher Khan
## Description
In this project we study four recommender systems: popularity based on genre, trendiness based on genre, Funk SVD collaborative filtering, and user-based collaborative filtering. We then created an interactive R Shiny app that recommends movies based on two of those systems. The first system uses the user's favorite genre to recommend popular movies in that genre. The second system takes the user's movie ratings to recommend movies with user-based collaborative filtering.
## Technical Details
### System 1
#### Recommend Based on Popularity
Our first approach is to recommend the most popular movies in the user’s favorite genre. We use both the average rating and number of ratings to determine a movie’s popularity. If we just used average rating, we could end up recommending movies that only have one high rating in total. Similarly, if we just used the number of ratings to determine popularity, we could end up recommending movies that have many bad reviews. So, we normalize the average rating by the number of ratings to take both into account.
#### Recommend based on Trendiness
Next, we recommend the top 10 trendiest movies in the user’s favorite genre. We consider movies trendy if they have many reviews that were submitted recently. To measure this, we compare the 75th-percentile timestamp of reviews on each movie and take the 10 movies with the most recent 75th-percentile. This means we are selecting movies with a quarter of their reviews being submitted most recently. We decided not to normalize by number of reviews because new movies might not have many reviews but could still be trending. We also chose not to take average rating into account because we want trending movies to be movies people are talking about and reviewing, whether positively or negatively.
#### Funk SVD
Funk SVD decomposes the original matrix into two lower rank matrices, U and V. U is the user-factor matrix and V is the item-factor matrix. Funk SVD finds latent factors in the data, which in our case is movie genres, and uses those to help predict ratings and recommend movies. Funk SVD uses stochastic gradient descent to minimize the error between the actual and the predicted rating. The learning rate we use for SGD is the default 0.001. The min_epochs and max_epochs are the minimum and maximum iterations per feature and are set to 20 and 50 respectively.
#### User-Based Collaborative Recommendation
User-Based Collaborative Filtering works upon the assumption that good recommendations for a new user can be generated based on the ratings of existing users with similar tastes. We train a recommender that will aggregate the ratings of a group of ‘nearest-neighbor users’, and produce recommendations from them.
