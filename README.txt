

##### SC1015 SC20 PROJECT GROUP 1 ######
----------------------------------------

# Members:
1. Hashil Jugjivan (U2120599F)
2. Ryan Teo Cher Kean (U2122540D)
3. Tiew Yen Huei (U2121588J)



This README file is intended to help readers to understand the intention and methodology of our project.


# Project introduction
----------------------

Basketball is a widely known sport played all around the world. The most popular basketball league in the
world is the NBA, and it has a rich history and many decorated players, such as the legendary LeBron James
and Kobe Bryant. 

Representing a team in the NBA as a professional basketball player warrants a salary. As some of us may
already know, popular and high performing players, such as the aforementioned LeBron James, tend to
receive exorbitant salaries. Stephen Curry currently receives a salary of $45,780,966 per year.

This led our group to question what constitutes to a player's salary in the NBA, eventually leading up to
our question:

<<< How does a player's performance in the NBA affect their salary? >>>



# Collecting data
-----------------

For this project, we will be using 2 data sets:

1. "20 Years of NBA Draft Data" (will be referred to as "Draft data"), taken from kaggle.com. 

	This data set includes numerous statistics for over 1800 basketball players. Statistics range 	
	from things like the team they played for to the average amount of time played per match.
	Relevant metrics will be chosen to assess a player's performance.


2. "Salary data", scraped from basketball-reference.com.

	The salary data of currently active NBA players. Some players have contracts that extend far 
	into the future, but we won't be considering those.

For the purposes of this project, the data will be cleaned, merged and then analysed using regression 
techniques. Upon doing the actual data analysis, we found that the regression did not output satisfactory 
results, so we decided to try classification instead.



# Data cleaning
---------------

1. Salary data
	There were several problems we had to clean up for salary data:

		1. The player names had unnecessary information (e.g. Stephen Curry\curryst01)
		2. Team column is irrelevant (not indicative of individual performance)
		3. Salaries had non-numeric characters inside (e.g. '$')
		4. Future salary column were unnecessary
	
	After cleaning, salary data was reduced from 617 entries to 452 entries

2. Valid Salary data set
	Next, we decide to create a new data set called "Valid Salary". This data set includes the
	players who have both valid entries in the Draft Data set and a salary data point from the
	Salary data set.

	First, Salary Data was merged with Draft Data to create Combined Data. Then, from Combined Data,
	any rows with a column containing "NA" was dropped to create Valid Salary. Valid Salary has
	372 entries.

	A heat map was plotted to assess the best metrics to use from the data set. In the end, we
	decided to use these metrics:

		1. WS (Win shares in the NBA)
		2. MPG (Average minutes per game)
		3. PPG (Average points per game)
		4. RPG (Average number of rebounds grabbed per game)
		5. APG (Average assists per game)
	
	The rest of the columns were dropped from Valid Salary.


# Exploratory Data Analysis
---------------------------


Since the data types we were using were all continuous variables, the obvious first choice for modelling 
our data was to use regression. Our group first tried out using linear regression, ridge and lasso regression. 
We found that the ridge and lasso regressions produced highly similar results as the linear regression model,
possibly due to the lack of irrelevant variables to be minimised or eliminated in the equations.

Upon plotting our regression lines, we found that the regression models did not output satisfactory
results (R^2 ≈ 0.6 / higher MSE). Removing outliers from the mix also did not help to improve the models'
scores for train and test datasets. 

As a result, we decided to shift our focus from only predicting the exact salary of a player to also predicting 
a range of salaries for the player using multi-class classification. We split a players' salary into 
4 pay grades where grade 4 represents the lower quartile and grade 1 representing the upper quartile of the salaries
from the salary dataset. We also split the players' salary into 4 classes where class 'D' is salary less than 100k,
class 'C' is salary between 100k to 1million, class 'B' is between 1million to 10million and class 'A' is between 10million
to 50million. We have used a cap of 50million as no player currently earns 50million or more. We then ran a simple decision tree 
classifier, then a randomforest classifier on the data.

Using classification yielded much better results than regression, where the random forest classifier had the highest accuracy compared
to the simple decision tree.



# Outcomes
----------

At the end of the day, basketball salaries are based on many factors alongside a player's performance
on the court. For example, players like Stephen Curry receive higher pay due to their popularity among
fans, which makes them able to rake in more money for teams through merchandise and whatnot.

As a result, predicting exact salaries solely based on performance may be difficult for a considerably
small sample size. Furthermore, even based solely on performance, it is unlikely that all players could 
realistically be judged by the same metrics. It is clear that some players are better at certain things,
while others are not. Players also take up different positions on the court and it may be unfair to judge
them based on the same metrics

Classification likely offers a better result since we are able to assign a class to a player rather than
an exact salary. Multi-variate classification allows for all player's statistics to be analysed as a 
group, leading to more accurate classes.

While we are uncertain about predicting a player's exact salary, a pay grade is indicative of a player's performance and what they can expect moving forward.



