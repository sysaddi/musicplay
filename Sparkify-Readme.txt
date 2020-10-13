Description
This Project is based on a task by Udacity. It's about a fictional music streaming plattform called sparkify. The dataset 
is a medium dump that is also available on IBMs plattform and contains 19 features. The goal of the task is to predict churn 
of the user(s) based on this features. 

Approach: 

The approach can be clustered in 2 bigger parts that contain smaller subtasks. 
The bigger parts are:
1) Data exploartion and preperation 
2) Building and comparing different approaches for prediction of user churn. 

First, let's have a closer look at part one: 

After loading all necessary components and the data a first look into the dataset is used to think and describe the possible 
churn indicators and which features could be useful:
 
Theory: possible churn indicators based on dataset

1) Ration thumbs up vs down or count e.g. to identify if he liked the music available or not
2) Hours logged in e.g. did he listened to all songs already?
3) Songs played & author e.g. does he enjoy a lot of music or just one album
4) Gender differences

Indicators that could be beneficial:

1) Thumbs up
2) Thumbs down
3) Songs played
4) Gender
5) Artists
6) Total length
7) Level

After loading the data and talking about the theory this first part has 5 subparts:

1) Data exploration and handling NaNs

Afterwards some data exploration is done to understand the data and the missing data better. 
For the missing data I decided to delete this data instead of using e.g. forward-fill because a lot of this data is 
created by guests or user that are not logged in and that are therefore not relevant for churn. 


2) Check some more features for unique values to understand the sample even better

Some basic data exploration to continue with step 3. 


3) Define what is churn in our dataset based on the understanding we have now

For this task churn will be defined based on the feature "page". Page has the value 'Cancellation Confirmation' that will be used as the identifier. 
I'm aware that there are multiple ways here to define churn in a different way but for this task this featture seems to be sufficient. 
(I don't use the Submit Downgrade because I would have to control for reupgrade and users that first downgrade and later cancle.) 
Using this marker in the dataset 99 users out of 449 churned (22,098%). This number seems to be high enough to really identify paterns 
but low enough that it could be true. 
Of course using this definition means that we have a inbalanced sample but I think this could be a good approximation of the true underlying 
business case even if 22% still seem to be worrying high. But that's the reason why they asked for our help :) 


4) Drop unnecessary data columns (based on what defined so far and on what the goal is and the described indicators at the top

Based on the features in the theory-part in the beginning unnecessary columns will be dropped. 

5) Checking the remaining data and visualize it (especially the important features to figure out if there are differences between churned users and not churned users

The remaining data will be visualized to understand differences and explored e.g. unique values. In addition the six indicators are created based on the remaining 
features and will be the factors and features used for the prediction. 



Part 2:

Part 2 beginns with the overlapping part of creating one dataframe based on the new feature (Preparation for the model).  
After the new dataframe is created 3 approaches will be tested and compared. 
1. A regression model
2. A random forest model 
3. A gradient boosting approach

Of course other approaches and models could be possible too but these would be still kind of easy explainable to the business side 
without diving to deep into data (because after all this is this a project that had a business case of prediction churn 
to later on reducing it - even if part 2 is not included in this project it could be a logical follow up). 
As already mentioned the dataset is unbalanced having less churn customers (22%). Therefore the in this project the F1 score 
is used to measure the performance of the 3 approaches. 

The F1 scores of the different models are:

1) 0.67471737675971322

2) 0.65291005291005277

3) 0.69744346116027522



Result:
Using the regression model as a base line we can see that the other two models are performing (+/- 2%-points better or worse). 
While the Random Forest values all features (0-4 really high) it performes worse. The gradient boost model performs better usinging 
especially feature 0 and 4 but also it looks like features 5 & 6 are valued lower. 
Overall features 5 & 6 seem to be outlier.  

Software used:
Jupyter Notebook
Python 3.6+
including e.g.: NumPy, SciPy, Pandas, Sciki-Learn, NLTK, SQLalchemy, Pickle, Flask, Plotly


Author
Sören Karnstädt












Idea - Appendix:
Having a look on the correlation matrix this becomes more clear. Feature 5&6 are compared to the other features "uncorrelated" 
(compared to the other) while feature 2,3,4 are perfectly correlated. This explains why the Random Forest with equal weights does not 
have any advantages because the data of feature 2,3,4 are fully correlated.  
