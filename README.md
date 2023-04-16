# Identifying Successful Movie Trends for Microsoft's New Movie Studio



## Project Overview

The project involves analyzing data from various sources to help Microsoft's new movie studio identify the most successful film genres, key factors that contribute to a movie's success, and audience demographics. The project aims to provide actionable insights and recommendations to create a movie portfolio and execute marketing strategies for the studio's success in the highly competitive movie industry.

## Business Problem

Microsoft sees all the big companies creating original video content and they want to get in on the fun. They have decided to create a new movie studio, but they don’t know anything about creating movies. You are charged with exploring what types of films are currently doing the best at the box office. You must then translate those findings into actionable insights that the head of Microsoft's new movie studio can use to help decide what type of films to create.

## Goals
1.Identify successful movie genres and their audience demographics
2.Determine key factors contributing to a movie's success
3.Develop a strategy for creating a movie portfolio and executing marketing campaigns based on the data analysis.

### The Data


* [Rotten Tomatoes](https://www.rottentomatoes.com/)
* [TheMovieDB](https://www.themoviedb.org/)
* [The Numbers](https://www.the-numbers.com/)

### Methods
This project uses exploratory analysis

First importing the packages we will use for analysis

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

%matplotlib inline

Loading the data sets

rt_movie_info = pd.read_csv("rt.movie_info.tsv.gz", sep='\t', encoding='unicode_escape')
movie_budgets = pd.read_csv("tn.movie_budgets.csv.gz")
tmdb_movies = pd.read_csv("tmdb.movies.csv.gz", index_col=0)

Cleaning the datasets to remove columns with too many missing values and unnecessary columns, changing the datatypes of some columns to floats for easier manipulation.

Merging the datasets

merged_data1 = pd.merge(movie_budgets, rt_movie_info, on='id', how='inner')
merged_data = pd.merge(merged_data1, tmdb_movies, left_on=['movie'], right_on=['title'], how='left')

### Results

Plot scatter plot of movie budget vs. worldwide gross revenue to see the correlation

sns.scatterplot(x='production_budget', y='worldwide_gross', data=movie_budgets)
plt.xlabel('Production Budget ($)')
plt.ylabel('Worldwide Gross Revenue ($)')
plt.title('Movie Budget vs. Worldwide Gross Revenue')
plt.show()
![My Graph](my_graph.png)


sorted_genres = merged_data.sort_values(by='worldwide_gross', ascending=False)

Plot top 10 genres by worldwide gross revenue

plt.bar(sorted_genres['genre'][:10], sorted_movies['worldwide_gross'][:10])
plt.xticks(rotation=90)
plt.ylabel('Worldwide Gross Revenue ($)')
plt.title('Top 10 Genres by Worldwide Gross Revenue')
plt.show()
![My Graph](my_graph.png)


plt.hist(merged_data['vote_average'], bins=20)
plt.xlabel('Votes')
plt.ylabel('Count')
plt.title('Distribution of Movie Votes')
plt.show()
![My Graph](my_graph.png)


plt.bar(genre_ratings.index, genre_ratings.values)
plt.xticks(rotation=90)
plt.xlabel('Genre')
plt.ylabel('Average Rating')
plt.title('Average Rating by Genre')
plt.show()
![My Graph](my_graph.png)


## Conclusion

From the analysis we have done from the datasets we can conclude that:

1. Adventure, Action, and Drama are the top three most profitable genres in the film industry.
2. Films with a higher worldwide gross revenue are likely to have a higher profit margin.
3. Films with a higher rating tend to have a higher profit margin.

## Next Steps

The next steps the Microsft film producer could take include:

1. Consider investing in the production of adventure, action, and drama films as they have proven to be the most profitable genres.
2. Invest in films with high potential for worldwide gross revenue can yield a higher profit margin.
3. Produc films with a high rating can lead to a higher profit margin, so Microsoft should strive to create high-quality films that appeal to audiences and critics alike.