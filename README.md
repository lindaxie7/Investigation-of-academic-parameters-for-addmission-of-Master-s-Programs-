# Investigation-of-academic-parameters-for-addmission-of-Master-Programs

[R Code](https://github.com/lindaxie7/PyBer-analysis/blob/main/PyBer_Challenge_starter_code.ipynb)

## Overview of Project
The purpose of this project is to analyze the factors considered in Graduate admission applications, to predict factors resulting in high chances of getting admitted into graduate programs. The parameters are: 

1.	GRE Scores (out of 340)

2.	TOEFL Scores (out of 120)

3.	Undergraduate Degree University Rating (out of 5)

4.	Statement of Purpose (out of 5)

5.	Letter of Recommendation Strength (out of 5)

6.	Undergraduate GPA (out of 10)

7.	Research Experience (either 0 or 1)

8.	Chance of Admit (ranging from 0 to 1)

## Methods

### Initial evaluation
We generated a scatterplot to evaluate if predictors are linearly related with response variable ‘Chance.of.Admit’, and to identify if there is a problem of multicollinearity between predictors. As there are many predictors, we also created various graphs to visualize the data amongst all the predictors. 

### Analyze linear regression model
We began our analysis by fitting a linear regression model to the data. We then evaluated the following linear regression assumptions 
a)	Linearity: By calculating Pearson’s correlation between predictors and response variable
b)	Independence: Using DurbinWatson test.
c)	Homoscedasticity: Using Breusch-Pagan test
d)	Normality: Using Shapiro-Wilk test
In an attempt to normalize the linear regression model, we utilized several techniques to transform the data and used diagnostic tests (stated above) to evaluate our transformed models. 

### Random forest regression 
Using randomForest(), we created a variable importance plot that ranks the variables for how important it is in classifying the data. We used this information to help us choose variables to test with the likelihood ratio test. 

### Regression tree
After splitting the data into training and testing sets, we used the training data to construct a regression decision tree. We created another factor to index the admission chances as high or low using the mean chance of admission. Anything above the mean received a “high” rating, and anything below the mean received a “low” rating. Then, using the test data set, we were able to calculate the accuracy of the decision tree method deciding whether a student has a high or low chance of being admitted. We created a confusion matrix and calculated sensitivity and specificity to evaluate the predictive power of the regression tree.

### Analyze Beta regression model
Using betareg(), we fit the initial beta regression model using all available predictors (GRE and TOEFL scores, university ranking, SOP, LOR, CGPA and Research) and determined multicollinearity using vif(). Predictors with values greater than 5 would be problematic to our model. Using the p-values from that initial model, we removed insignificant predictors. 

We also compared the function with the logit link vs. loglog to determine which link function improves the model fit better. To further account for heteroscedasticity, we tested our model with variable dispersion and compared the logit, loglog and variable dispersion models using AIC. 

In our final analysis of this model, we created a confusion matrix and calculated sensitivity and specificity to evaluate the predictive power of the variable dispersion model. 

### Hypothesis tests
#### Test equivalence of contributions of GRE and TOEFL scores
Given that the two exams have strong positive correlations and test similar skills, we want to test if the two scores have equivalent contributions to the chance of admit. We used the linearHypothesis() function to test this hypothesis.

#### Test pairwise comparisons for all 8 levels of letters of recommendation ratings 
We utilized tukey comparisons in the function lsmeans() to compare all levels of letters of recommendation ratings. 

#### Test significance of research binary predictor 
We determined the significance of the research predictor in multiple ways: pairwise comparison using lsmeans(), confidence interval analysis, likelihood ratio test to compare the model with and without research, and the regression summary p-value.

#### Test pairwise comparisons for all 5 levels of university ratings 
Similar to the letters of recommendation ratings, we used tukey comparisons in the function lsmeans() to compare all levels of university ratings. 


## Results

Through analysis and aggregation of PyBers ride sharing data, I have created a summary DataFrame of the ride-sharing data by city type:
![Untitled](https://user-images.githubusercontent.com/38533045/128641850-3e21c8ba-169f-410f-8c04-e9a6437caa65.png)

A multiple-line graph that shows the total weekly fares for each city type as below:
![Untitled](https://user-images.githubusercontent.com/38533045/128641892-b614f4d6-46d7-4ca9-a94b-7aa490565583.png)

By reviewing the summary we can see that there are several key findings including:

Urban cities have the highest ridership demand while rural cities have the least.

Urban cities have 4x+ more drivers than suburban cities, suburban cities have 6x + drivers than rural with almost 4.5x the revenue.

Rural cities have the highest average fare per ride and driver.

The summary data shows a relationship in which fare revenue is higher by city type when there is a larger ratio of drivers to rides.


## Summary

The variable dispersion model using beta regression was determined to be the most appropriate fit to the data, with a predictive power accuracy rate of 92.3%. We conclude that the statement of purpose is not necessary to explain variances in and to predict the chance of admissions. Research plays an important role in improving admission chances and is found to be associated with high scorers in GRE and TOEFL exams and high CGPA scores.

GRE and TOEFL scores have equal contributions to the chance of admit. Based on the results from the Likelihood Ratio Tests comparing models with and without the test scores, we recommend both GRE and TOEFL scores be included in the model to most accurately predict the chance of admission. 

If we were to repeat the project, it would be interesting to obtain data from other universities to analyze the differences between universities. Another interesting aspect would be to obtain the program type (i.e. STEM, liberal arts, etc. programs) to determine if there are differences between types of programs. This information would be useful to students so they know how competitive different types of programs are, and how to best improve their chances of admission depending on their choice of program.



 



