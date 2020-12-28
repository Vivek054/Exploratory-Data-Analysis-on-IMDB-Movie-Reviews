# Exploratory-Data-Analysis-on-IMDB-Movie-Reviews

We have the data for the 100 top-rated movies from the past decade along with various pieces of information about the movie, its actors, and the voters who have rated these movies online. Using this data, we will try to find some interesting insights into these movies and their voters, using Python.

- Read the movies data file provided and store it in a dataframe movies.

![Capture](https://user-images.githubusercontent.com/59309459/103193494-a0b65c00-4902-11eb-83f3-db1ba93410ff.JPG)

- Inspect the dataframe for dimensions, null-values, and summary of different numeric columns.

- Now that we have loaded the dataset and inspected it, we see that most of the data is in place. As of now, no data cleaning is required, so let's start with some data manipulation, analysis, and visualisation to get various insights about the data.

  - These numbers in the budget and gross are too big, compromising its readability. Let's convert the unit of the budget and gross columns from $ to million $ first.
![Capture](https://user-images.githubusercontent.com/59309459/103193579-e115da00-4902-11eb-8c82-15b09aae2439.JPG)
  
- Let's Talk Profit!

  - Create a new column called profit which contains the difference of the two columns: gross and budget.
  - Sort the dataframe using the profit column as reference.
  - Extract the top ten profiting movies in descending order and store them in a new dataframe - top10.
  - Plot a scatter or a joint plot between the columns budget and profit and write a few words on what you observed.
  - Extract the movies with a negative profit and store them in a new dataframe - neg_profit
  
![Capture](https://user-images.githubusercontent.com/59309459/103193646-19b5b380-4903-11eb-9627-eab68449a73e.JPG)

### Plot for Profit vs Budget:

![Capture](https://user-images.githubusercontent.com/59309459/103193729-5a153180-4903-11eb-9108-158a6ce42644.JPG)

The dataset contains the 100 best performing movies from the year 2010 to 2016. However scatter plot tells a different story. You can notice that there are some movies with negative profit. Although good movies do incur losses, but there appear to be quite a few movie with losses. What can be the reason behind this? Lets have a closer look at this by finding the movies with negative profit.

### Find the movies with negative profit:

- movies[movies["profit"]<0]

## The General Audience and the Critics:

We might have noticed the column MetaCritic in this dataset. This is a very popular website where an average score is determined through the scores given by the top-rated critics. Second, we also have another column IMDb_rating which tells you the IMDb rating of a movie. This rating is determined by taking the average of hundred-thousands of ratings from the general audience.

As a part of this, we have to find out the highest rated movies which have been liked by critics and audiences alike.

- Firstly we will notice that the MetaCritic score is on a scale of 100 whereas the IMDb_rating is on a scale of 10. First convert the MetaCritic column to a scale of 10.
- Now, to find out the movies which have been liked by both critics and audiences alike and also have a high rating overall, we need to

    - Create a new column Avg_rating which will have the average of the MetaCritic and Rating columns
    - Retain only the movies in which the absolute difference(using abs() function) between the IMDb_rating and Metacritic columns is less than 0.5. Refer to this link to know         how abs() funtion works - https://www.geeksforgeeks.org/abs-in-python/ .
    - Sort these values in a descending order of Avg_rating and retain only the movies with a rating equal to higher than 8 and store these movies in a new dataframe.
    
### Change the scale of MetaCritic:

- movies["MetaCritic"]=movies["MetaCritic"]/10

### Find the average ratings:

- movies["Avg_rating"]=(movies["IMDb_rating"]+movies["MetaCritic"])/2

### Find the movies with metacritic-IMDb_rating < 0.5 and also with the average rating of >8:

    - df=df.sort_values(by="Avg_rating",ascending=False)
      UniversalAcclaim=df.loc[df["Avg_rating"]>=8]
      UniversalAcclaim
      
### Find the Most Popular Trios - I:

I am a producer looking to make a blockbuster movie. There will primarily be three lead roles in your movie and you wish to cast the most popular actors for it. Now, since i don't want to take a risk, you will cast a trio which has already acted in together in a movie before. The metric that i've chosen to check the popularity is the Facebook likes of each of these actors.

  - The dataframe has three columns to help me out for the same, viz. actor_1_facebook_likes, actor_2_facebook_likes, and actor_3_facebook_likes. Mhy objective is to find the       trios which has the most number of Facebook likes combined. That is, the sum of actor_1_facebook_likes, actor_2_facebook_likes and actor_3_facebook_likes should be maximum.     I have to find out the top 5 popular trios, and output their names in a list.
  
![Capture](https://user-images.githubusercontent.com/59309459/103194102-7cf41580-4904-11eb-9633-3560194a9a49.JPG)

### Find the Most Popular Trios - II:

In the previous subtask we found the popular trio based on the total number of facebook likes. Let's add a small condition to it and make sure that all three actors are popular. The condition is none of the three actors' Facebook likes should be less than half of the other two. For example, the following is a valid combo:

  - actor_1_facebook_likes: 70000
  - actor_2_facebook_likes: 40000
  - actor_3_facebook_likes: 50000
But the below one is not:

  - actor_1_facebook_likes: 70000
  - actor_2_facebook_likes: 40000
  - actor_3_facebook_likes: 30000  

Since in this case, actor_3_facebook_likes is 30000, which is less than half of actor_1_facebook_likes.

Having this condition ensures that i am aren't getting any unpopular actor in my trio (since the total likes calculated in the previous question doesn't tell anything about the individual popularities of each actor in the trio.).

I can do a manual inspection of the top 5 popular trios you have found in the previous subtask and check how many of those trios satisfy this condition. Also, which is the most popular trio after applying the condition above? 

![Capture](https://user-images.githubusercontent.com/59309459/103194363-68fce380-4905-11eb-83ff-197a760f4837.JPG)

### Runtime Analysis:

There is a column named Runtime in the dataframe which primarily shows the length of the movie. It might be intersting to see how this variable distributed. I am ploting a histogram or distplot of seaborn to find the Runtime range most of the movies fall into.

![Capture](https://user-images.githubusercontent.com/59309459/103194399-892ca280-4905-11eb-9f2d-bfa76a6074ca.JPG)

### R-Rated Movies:

Although R rated movies are restricted movies for the under 18 age group, still there are vote counts from that age group. Among all the R rated movies that have been voted by the under-18 age group, i am finding the top 10 movies that have the highest number of votes i.e.CVotesU18 from the movies dataframe. And i am storing these in a dataframe named PopularR.

![Capture](https://user-images.githubusercontent.com/59309459/103194432-aa8d8e80-4905-11eb-970e-be737b3eb9a7.JPG)

## Demographic analysis:

If we take a look at the last columns in the dataframe, most of these are related to demographics of the voters. We also have three genre columns indicating the genres of a particular movie. We will extensively use these columns for the third and the final stage of our analysis wherein we will analyse the voters across all demographics and also see how these vary across various genres. So, let's get started with demographic analysis.

###  Combine the Dataframe by Genres:
There are 3 columns in the dataframe - genre_1, genre_2, and genre_3. As a part of this subtask, you need to aggregate a few values over these 3 columns.
  - First we create a new dataframe df_by_genre that contains genre_1, genre_2, and genre_3 and all the columns related to CVotes/Votes from the movies data frame. There are 47     columns to be extracted in total.
  - Now, Add a column called cnt to the dataframe df_by_genre and initialize it to one. We will realise the use of this column by the end of this subtask.
  - First group the dataframe df_by_genre by genre_1 and find the sum of all the numeric columns such as cnt, columns related to CVotes and Votes columns and store it in a           dataframe df_by_g1.
  - Perform the same operation for genre_2 and genre_3 and store it dataframes df_by_g2 and df_by_g3 respectively.
  - Now that we have 3 dataframes performed by grouping over genre_1, genre_2, and genre_3 separately, it's time to combine them. For this, add the three dataframes and store it     in a new dataframe df_add, so that the corresponding values of Votes/CVotes get added for each genre.There is a function called add() in pandas which lets us do this. We can     refer to this link to see how this function works. https://pandas.pydata.org/pandas-docs/version/0.23.4/generated/pandas.DataFrame.add.html
  - The column cnt on aggregation has basically kept the track of the number of occurences of each genre.Subset the genres that have atleast 10 movies into a new dataframe           genre_top10 based on the cnt column value.
  - Now, take the mean of all the numeric columns by dividing them with the column value cnt and store it back to the same dataframe. We will be using this dataframe for further     analysis in this task unless it is explicitly mentioned to use the dataframe movies.
  - Since the number of votes can't be a fraction, type cast all the CVotes related columns to integers. Also, round off all the Votes related columns upto two digits after the     decimal point.
  
### Genre Counts:

![Capture](https://user-images.githubusercontent.com/59309459/103194606-2c7db780-4906-11eb-9168-7c682060edd7.JPG)

### Gender and Genre:

If we have closely looked at the Votes- and CVotes-related columns, we might have noticed the suffixes F and M indicating Female and Male. Since we have the vote counts for both males and females, across various age groups, let's now see how the popularity of genres vary between the two genders in the dataframe.

  - I will make the first heatmap to see how the average number of votes of males is varying across the genres. Using seaborn heatmap for this analysis. The X-axis should           contain the four age-groups for males, i.e., CVotesU18M,CVotes1829M, CVotes3044M, and CVotes45AM. The Y-axis will have the genres and the annotation in the heatmap tell the     average number of votes for that age-male group.
  - I will make the second heatmap to see how the average number of votes of females is varying across the genres. Use seaborn heatmap for this analysis. The X-axis should           contain the four age-groups for females, i.e., CVotesU18F,CVotes1829F, CVotes3044F, and CVotes45AF. The Y-axis will have the genres and the annotation in the heatmap tell       the average number of votes for that age-female group.
  - Make sure that we plot these heatmaps side by side using subplots so that we can easily compare the two genders and derive insights.

- Note : Use genre_top10 dataframe.

### Set of heat maps for CVotes-related columns:

![Capture](https://user-images.githubusercontent.com/59309459/103194679-6bac0880-4906-11eb-8346-e1913d4aca3a.JPG)

## Inferences:
A few inferences that can be seen from the heatmap above is that males have voted more than females, and Sci-Fi appears to be most popular among the 18-29 age group irrespective of their gender.

  - Inference 1: Genre romance has got the least number of votes among any age group of males, but there is no such pattern among the females
  - Inference 2:Action seems to be the more popular genre among the under 18 males, and Animation appears to be the most popular genre among under 18 females.
  - Inference 3: 18-29 age group seems to be most actively voting for any genre irrespective of gender

### Set of heat maps for Votes-related columns:

![Capture](https://user-images.githubusercontent.com/59309459/103194825-c5acce00-4906-11eb-81f8-1e05fcf5cc7c.JPG)

## Inferences:
Sci-Fi appears to be the highest rated genre in the age group of U18 for both males and females. Also, females in this age group have rated it a bit higher than the males in the same age group.

  - Inference 1: The ratings among males, seems to be decreasing with increasing age group. There is a similar pattern among females but with a few exceptions.
  - Inference 2: Crime genre has the second highest rating among U18 age group of males, but among U10 females it has got the least rating.
  - Inference 3: Romance genre has got the least rating among both 45 above males and females.

### US vs non-US Cross Analysis:
The dataset contains both the US and non-US movies. Let's analyse how both the US and the non-US voters have responded to the US and the non-US movies.

  - We will create a column IFUS in the dataframe movies. The column IFUS should contain the value "USA" if the Country of the movie is "USA". For all other countries other than     the USA, IFUS should contain the value non-USA.
  - Now we will make a boxplot that shows how the number of votes from the US people i.e. CVotesUS is varying for the US and non-US movies. We will make use of the column IFUS       to make this plot. Similarly, we will make another subplot that shows how non US voters have voted for the US and non-US movies by plotting CVotesnUS for both the US and         non-US movies.
  - Again we will do a similar analysis but with the ratings. We will make a boxplot that shows how the ratings from the US people i.e. VotesUS is varying for the US and non-US     movies. Similarly, we will make another subplot that shows how VotesnUS is varying for the US and non-US movies.

### Box plot - 1: CVotesUS(y) vs IFUS(x):

![Capture](https://user-images.githubusercontent.com/59309459/103194959-3ce26200-4907-11eb-8e65-017cf4d6f7a7.JPG)

## Inferences:

  - Inference 1: In general US movies have got a high number of votes from both the US and non-US voters when we compare the medians of box plots.
  - Inference 2: Non-US movies have a more uniform distribution of the number of votes as compared to the US movies, which is evident from the values of the quartiles.
  
### Box plot - 2: VotesUS(y) vs IFUS(x):

![Capture](https://user-images.githubusercontent.com/59309459/103195047-761ad200-4907-11eb-8c17-599f78624b5c.JPG)

## Inferences:

  - Inference 1: Non-US voters have rated both the US and non-US movies lower as compared to the US voters, which is evident from the medians.
  - Inference 2: US movies have received higher ratings from US voters.
  - Inference 3: Some US movies have got exceptionally high ratings from both the US and non-US voters. There are no such extreme ratings for any of the non-US movies.
  
### Top 1000 Voters Vs Genres:

We have also observed the column CVotes1000. This column represents the top 1000 voters on IMDb and gives the count for the number of these voters who have voted for a particular movie. Let's see how these top 1000 voters have voted across the genres.

  - We will sort the dataframe genre_top10 based on the value of CVotes1000in a descending order.
  - We will make a seaborn barplot for genre vs CVotes1000.
  
### Barplot for CVotes1000 according to Genre:

![Capture](https://user-images.githubusercontent.com/59309459/103195176-c2fea880-4907-11eb-95d2-add798dcc16b.JPG)

## Inferences:

  - Inference 1: The voting pattern her almost resembles the pattern in age group vs genre heat maps.
  - Inference 2: Although drama genre has the highest number of movies, the average number of top users who have rated it is less as compared to other genres which have lesser       number of movies in them.
