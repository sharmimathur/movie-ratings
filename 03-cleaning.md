# Data transformation

The data transofrmation process was relatively straightforward. For each source, we will go through how and in what platforms we aggregated the values.

## Box Office Mojo
The box office mojo data set is presented in a simple table that is easily scraped from the website. For each year we were evaluating, we filted by top 200 movies, and imported the data into a CSV by title. From there, we had an aggregate list of 2,200 movies from 2011-2021. 


## Rotten Tomatoes
Once we ran the scraper, we output the rotten tomatoes data from jupyter notebook into a CSV. The data was organized by movie title, and by critic / audience rating. 

## IMDB
This was one of the most cumbersome cleaning processes, because the data set was so large. In order to make it more managable, we did all of our maniuplation in python, and filtered on the following: 

* Release Year - we had to convert to a numeric string, and then filtered if release year was greater than 2010
* Title Type - we filtered only movies 

From there, we imported a new .dat file that was the aggregate list of 2,200 movies we had originally scraped from Box Office Mojo, and iterated through the remaining data values to pull the required IMDB data. We output the new IMDB data into a CSV file as well. 

## Aggregation
After our scraping from the 3 sources, we had 3 unique CSV files. We merged these files by title, to create our aggregate list of movies and the corresponding data points. 
* Scraping box office mojo
  *adding to a .csv
* Downloaded data from imdb
  * tsv
* Scraped rotten tomatoes
  * Excel spreadsheet to csv
* Brought together with python
  * Merge on movie title
