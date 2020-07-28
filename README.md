# Harbingers-of-Failure-in-Movie-Industry
"Harbingers of Failure" refers to certain group of customers with peculiar tastes whose early adoption of a new product indicates it might be a flop. "Harbingers of Failure" effect, discovered by a group of MIT researchers, originally was an unconventional phenomenon in the retail industry. This project, using the online movie rating data, successfully proves that harbingers of failure also exist in the movie industry. <br />

To help you understand harbingers of failure effect, the article published by MIT News is recommended to you. <br />
http://news.mit.edu/2015/harbinger-failure-consumers-unpopular-products-1223 <br />

The project consists of two parts: data collection and machine learning.
## 1. Data Collection
Code: Movie_Websites_Scraping.ipynb <br />
This code is used to collect the following data from two online sources: Box Office Mojo and Rotten Tomato. <br />
* Box Office Mojo: movie name, movie release date, opening weekend revenue, gross domestic revenue <br />
* Rotten Tomato: movie name, critic name, pre-release movie rating <br />
Movie ratings before the movie release date are of interest to our analysis, because we want to examine if movie critics with peculiar tastes can have a predictive power of a failure of a movie.
## 2. Machine Learning
Code: Feature Engineering & Modelling Script.ipynb <br />
This code runs on PySpark and performs the task of feature engineering and implements logistic regression model to demonstrate the effect of harbingers of failures. <br />
### Calculate important metrics
* Success Indicator. <br />
![equation](https://latex.codecogs.com/gif.latex?SuccessIndicator=\frac{OpeningWeekendRevenue}{GrossRevenue}) <br />
A movie is defined as successful if its opening weekend revenue exceeds or equals to 30% of its gross domestic revenue. If the success indicator < 0.3, then the movie is a flop. <br />
* Flop Affinity. <br />
![equation](https://latex.codecogs.com/gif.latex?FlopAffinity=\frac{NumFlopsRecommended}{NumNewMoviesRecommended}) <br />
The pre-release movie ratings are grouped by critic to calculate the flop affinity ratio for each critic. The ratio measures how likely a critic will recommend a flop movie out of all the new movies he or she recommends. Specifically, a fresh tomato sign given by the critic indicate that he or she favors the movie. For example, if I recommend 10 new movies in total, however 4 of them are financially unsuccessful, then my flop affinity ratio is 40%. <br />
### Group critics according to their tastes
Based on the flop affinity ratio, we group the critics into five groups using the 25%, 50% and 75% percentile of the ratio, which are flop rates of 40%, 60% and 75% respectively. <br />
Group1: critics with FlopAffinity  [0, 40%] <br />
Group2: critics with FlopAffinity  (40%, 60%] <br />
Group3: critics with FlopAffinity (60%, 75%] <br />
Group4: critics with FlopAffinity > 75% <br />
Other: critics who recommended no more than 2 movies <br />
### Estimate two logitic regression models
In this step, we estimate two logistic regression models.
* Model 1: <br />
![equation](https://latex.codecogs.com/gif.latex?ln(\frac{p_i}{1-p_i})=\alpha&plus;\beta_0TotalRecommendation_i) <br />
p_i is the probability of the movie i being successful. The independent variable is the total number of fresh reviews (likes) for the movie i. <br />
* Model 2: <br />
![equation](https://latex.codecogs.com/gif.latex?ln(\frac{p_i}{1-p_i})=\alpha&plus;\beta_1Group1Recommendation_i&plus;\beta_2Group2Recommendation_i&plus;\beta_3Group3Recommendation_i&plus;\beta_4Group4Recommendation_i&plus;\beta_5OtherRecommendation_i) <br />
Model 2 extends beyond Model 1 and considers the tastes of the critics. For example, ![equation](https://latex.codecogs.com/gif.latex?\beta_1Recommendation_1) is the number of fresh reviews for the movie i give by Group 1 critics whose flop affinity ratios are no more than 40%.
### Compare the likelihood ratio of the two models
We use the chi-squared test to compare the likelihood ratio of two logistic regression models. The test result shows that compared to Model 1, Model 2 has a signiciant improvement of model fitness, after we take the critics' tastes into account. Harbingers of failures do exist in the movie industry, and particularly, Group 4 critics with the most "wierd" tastes has very signficant predictive power of flop movies.



