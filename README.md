# <center>Investigating-Data Project: Which Passengers on board of the Titanic Vessel were more likely to survive the Tragedy?</center><br><center>A walk-through of the Project</center>
### <center>by Karine Legrand, December 2021</center><br><br>


### Presentation of the Dataset and Challenges:

#### Introduction
I have chosen to conduct a Data Analysis on the infamous 'Titanic' Dataset which contains a subset list of the Passengers that were on board, with characteristic informations for each of them and wether they survived or not.

#### What is the structure of the dataset?
The Dataset contains 891 observations of persons embarked on the Titanic Vessel. There are 12 columns with  characteristics of each Person such as 'Age', 'Gender', 'Class of Travelling', 'Cabin', 'Embarkment', 'PassengerId' and so on.

#### What is/are the main feature(s) of interest in the dataset?
I want to investigate which of the characteristics, or features, possibly affected the chance of survival.<br>
In particular I want to focus on the variables describing the 'Age', 'Gender' and 'Travelling Class' of the passengers.<br>
Eventually my Challenge is to try and answer the core following Questions:<br><br>
"Were some Passengers more likely to survive than others, based on their:
- Age ?
- Gender ?
- The Class they travelled in ?"<br>





### Strategy followed to get to our Insights: 

#### 1.) Data Wrangling
In this section we first **gather, assess and clean** our Data, fixing Quality Issues found such as "Missing values".
We make extensive use of the usual <i>numpy</i> and <i>pandas</i> libraries to get a grap on our Data and to end up with a cleaned Dataset that we can conduct an Exploratory Data Analysis on.<br>
#### 2.) Exploratory Data Analysis
In this section I organize my Investigation in an ascending complexity Order:
- first as 'Univariate Exploration' where I look at each Distribution of the variables of Interest
- finally as 'Bivariate Exploration' where I focus on finding correlations between the three independent variables ('Age', 'Gender' and 'Class') and the dependent variable ('Survived')

### Encountered challenges and solutions:
#### 1) Adding a new categorical Variable:
In the Bivariate Exploratory Section, I wanted to make use of Seaborn's Barchart plotting functions which work with categorical variables. I needed to create a new categorical variable 'Fate', holding wether a Passenger survived or not as levels \['Died', 'Survived'\]. I used the following method:
```
df_eda['Fate']= np.where(df_eda.Survived == 1, 'Survived', 'Died')
```

#### 2) Computing Proportions instead of Counts:
Plotting different levels of a category (for example 'Gender') to show the Amount of People that survived in each group, can be less demonstrative, if the amount of People in the two groups are very different. In this case there are much more Men than Women in the Dataset, thus making our plot less intuitive than it could be.<br>
To solve this, I computed Proportions for each Group which could make the plot even clearer. I used the following method:
```
# get proportions for each Fate, for each Gender
fate_props_bygender = (df_eda.groupby(['Sex'])['Fate']
                     .value_counts(normalize=True)# get proportions instead of counts
                     .rename('Percentage')
                     .mul(100) # get percents
                     .reset_index())
```

### Conveying our Findings as answers to our questions:

The Bivariate Exploration helped us gain following Insights of Correlation between 'Gender', 'Class', 'Age' and 'Survived'and to find answers to our questions:
- Most of the Men died, about $80$%, whereas, as opposite, most of the Women survived, about $75$%
- Babies and young children until about $8$ years old seem to had more chances to survive
- A big proportion of People in the third class died, $75$%, whereas most people travelling first class did survive,  about $62$%<br>

<b>These characteristics of the passengers seem to have certainly affected wether they could survive the Tragedy.</b>
