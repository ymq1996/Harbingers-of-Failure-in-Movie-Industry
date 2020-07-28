# Harbingers-of-Failure-in-Movie-Industry
"Harbingers of Failure" refers to certain group of customers with peculiar tastes whose early adoption of a new product indicates it might be a flop. "Harbingers of Failure" effect, discovered by a group of MIT researchers, originally was an unconventional phenomenon in the retail industry. This project, using the online movie rating data, successfully proves that harbingers of failure also exist in the movie industry. <br />

The project consists of two parts: data collection and machine learning.
## 1. Movie_Websites_Scraping.ipynb
This code is used to collect data from two online sources: Box Office Mojo and Rotten Tomato. <br />
The required fields are listed as follows: <br />
Box Office Mojo: movie name, release date, opening weekend revenue, gross domestic revenue <br />
Rotten Tomato: movie name, critic name, pre-release movie rating <br />
Movie ratings before the movie release date are of interest to our analysis, because we want to examine if movie critics with peculiar tastes can have a predictive power of a failure of a movie.
## 2. Feature Engineering & Modelling Script.ipynb
This code performs the task of feature engineering and implemented logistic regression model to demonstrate the effect of harbingers of failures. <br />
The dependent variable is a binary variable indicating whether a movie is successful or not. A movie is defined as successful if its opening weekend revenue exceeds or equals to 30% of its gross domestic revenue. <br />
![equation](https://latex.codecogs.com/gif.latex?SuccessIndicator=\frac{OpeningWeekendRevenue}{GrossRevenue}\geq0.3) <br />


