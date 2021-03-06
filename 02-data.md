# Data sources

In order to aggregate a comprehensive list of movie titles, box office gross, and ratings, we turned to the following data sources and followed the following processes. 

The first observation we made is that the IMDB data set with aggregate movies, genres, and ratings was quite large. For movies alone, there were well over millions of titles from around the world. Therefore, we needed to make some strategic decisions about which movies to include, and what logic to include. Because of the sheer volume of titles, we aggregated the following: 

* We constrained our movies to be within movies released from 2011 to 2021 
* We constrained the movies included to be the top 200 total grossing movies from each year
  + Total gross includes both box office and streaming services 

Once we constrained our list, the first task was to get a working list of the movies we wanted to include. We first turned to box office mojo, https://www.boxofficemojo.com/, which is a product offered by IMDB. In box office mojo, IMDB aggregates the top 200 movies from each year by title, gross, total gross, and number of theaters the film was released in. Using this data source, we aggregated all movies from each year to create our first data frame and get our initial movie list we planned to scrape. 

## Rotten Tomatoes
Rotten Tomatoes is one of the most cited and well known movie ratings websites in the world. Rotten Tomatoes aggregates both an "audience score" and a "critics score". This distinction is important, as one of our focuses of our analysis is looking at how reviews impact box office scores, and so by having both of these perspectives we can see if one or the other drives box office performance more. 

In order to aggregate our Rotten Tomatoes data, we used a simple Rotten Tomatoes scraper package in python. The documentation can be found here: https://github.com/pdrm83/rotten_tomatoes_scraper 

To implement this scraper, we passed in our initial list of 2,200 movie titles that we had originally sorted by box office gross in our initial data collection. By iterating through each title in our list, we were able to successfully scrape both audience and critic ratings from Rotten Tomatoes, with only minor data loss (more on that in the missing values section).


## IMDB
As previously mentioned, the IMDB data set is quite large. Because IMDB traces movies, shorts, and TV shows back to the early days of film (the early 1900s), the data set was quite unweildy and took quite a bit of masnaging to wrangle. We will cover exactly how we cleaned this data in our cleaning section. 

The two files we pulled from the IMDB data were the "title.ratings.tsv.gz" and "title.basic.tsv.gz". The documentation can be found here: https://www.imdb.com/interfaces/ 

For the ratings file, there were 3 elements: 

* tconst (the unique title identifier; a string)
* averageRating (from 0-10)
* numVotes (the number of votes included)

For the titles file, there were 9 elements: 

* tconst (the unique title identifier; a string)
* titleType (the type of film it is - could be TV Show, Movie, Short, etc.)
* primaryTitle (the title used in promotional materials. This was the title we used in our filtering)
* originalTitle (the title originally used. Typically the two titles are the same, unless one is in a different language)
* isAdult (boolean operator for adult movies. We did not include any adult movies in our analysis)
* startYear (release year of the title)
* endYear (only used for TV series; if the series ended)
* runTimeMinutes (run time of the title)
* genres (the genre of the film. Can be 1 - 3 values in a string)

## Final Data Table

After aggregating the three data sources, we had the following data inputs: 



```
##  [1] "Rank - ranking of box office gross within the release year"
##  [2] "Movie Title"                                               
##  [3] "Gross"                                                     
##  [4] "Number of Theaters"                                        
##  [5] "Total Gross - includes streaming / DVD / etc."             
##  [6] "Release Date (D/M)"                                        
##  [7] "Primary Studio"                                            
##  [8] "Year Released"                                             
##  [9] "Critic score scraped from RT"                              
## [10] "Audience score scraped from RT"                            
## [11] "Genre - concatenated - max 3 elements"                     
## [12] "1st genre element"                                         
## [13] "2nd genre element"                                         
## [14] "3rd genre element"                                         
## [15] "Average IMDB rating"                                       
## [16] "Number of IMDB votes"                                      
## [17] "Year pulled from IMDB"
```

=======
* Scraped data from rotten tomatoes
* Downloaded from imdb
* Chosen because these are the biggest hubs for movie information
* Refer to sample column names above
* Started from 2300
  * Talk about how we picked the top 200 movies
  * Talk about why we picked the top 200 movies
* Issues: duplicate names, same movie multiple countries
