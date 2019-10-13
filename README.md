## USF MSDS 601: Linear Regression Analysis
Project: NBA Player of the Week

###### Team Members
* Shirley Li ([@Shirleyiscool](https://github.com/Shirleyiscool))
* Charles Siu ([@chunheisiu](https://github.com/chunheisiu))


### Description of Dataset
Our dataset is a combination of the following datasets with regards to NBA:

- NBA Player of the Week (1985 - 2019)<br>
https://www.kaggle.com/jacobbaruch/nba-player-of-the-week<br>
1,187 Rows, 14 Columns

- NBA Player Salary from basketball-reference.com (1991 - 2017)<br>
https://www.kaggle.com/whitefero/nba-player-salary-19902017<br>
11,837 Rows, 7 Columns

- NBA Player Salary from basketball-reference.com (2018 - 2019)<br>
https://web.archive.org/web/20181002194236/www.basketball-reference.com/contracts/players.html<br>
578 Rows, 11 Columns

- NBA Player Statistics (1985 - 2019)<br>
https://www.basketball-reference.com/leagues/<br>
18,480 Rows, 30 Columns

- NBA Yearly Summary (1985 - 2019)<br>
https://www.basketball-reference.com/leagues/<br>
35 Rows, 8 Columns

Combining the aforementioned datasets, we created a dataset in which, each row is an NBA player per season, and each column is a statistic of the player. We filtered the rows so that only the players who have both statistics and salary data for that particular season are included.

There are 9,003 Rows and 38 Columns in the dataset.

#### Index of the Dataset
| Variable | Definition | Type |
|---|---|---|
| `Year` | (e.g. `1991` means the NBA 1990 - 1991 Season) | Numerical |
| `Player` | Player name | Categorical |

#### Variables of the Dataset
| Variable | Definition | Type |
|---|---|---|
| `Pos` | Player Position | Categorical |
| `Age` | Age of Player at the start of February 1st of that season | Numerical |
| `Tm` | Team of Player | Categorical |
| `G` | Number of games played | Numerical |
| `GS` | Number of games played when the game started | Numerical |
| `MP` | Minutes played per game | Numerical |
| `FG` | Field Goals per game | Numerical |
| `FGA` | Field Goal attempts per game | Numerical |
| `FG_Prct` | Field Goal percentage | Numerical |
| `Three_P` | 3-Point Field Goals per game | Numerical |
| `Three_PA` | 3-Point Field Goal attempts per game | Numerical |
| `Three_P_Prct` | 3-Point Field Goal percentage | Numerical |
| `Two_P` | 2-Point Field Goals per game | Numerical |
| `Two_PA` | 2-Point Field Goal attempts per game | Numerical |
| `Two_P_Prct` | 2-Point Field Goal percentage | Numerical |
| `ePF_Prct` | Effective Field Goal percentage<br>_This statistic adjusts for the fact that a 3-point field goal is worth one more point than a 2-point field goal._ | Numerical |
| `FT` | Free Throws per game | Numerical |
| `FTA` | Free Throw attempts per game | Numerical |
| `FTA_Prct` | Free Throw percentage | Numerical |
| `ORB` | Offensive Rebounds per game | Numerical |
| `DRB` | Defensive Rebounds per game | Numerical |
| `TRB` | Total Rebounds per game | Numerical |
| `AST` | Assists per game | Numerical |
| `STL` | Steals per game | Numerical |
| `BLK` | Blocks per game | Numerical |
| `TOV` | Turnovers per game | Numerical |
| `PF` | Personal Fouls per game | Numerical |
| `PTS` | Points per game | Numerical |
| `Potw` | Was the player named _Player of the Week_ during the season? | Binary |
| `APG_Leader` | Was the player named _Assists Per Game Leader_ during the season? | Binary |
| `MVP` | Was the player named _Most Valuable Player_ during the season? | Binary |
| `PPG_Leader` | Was the player named _Points Per Game Leader_ during the season? | Binary |
| `RPG_Leader` | Was the player named _Rebounds Per Game Leader_ during the season? | Binary |
| `Rookie` | Was the player named _Rookie of the Year_ during the season? | Binary |
| `WS Leader` | Was the player named _Win Shares Leader_ during the season? | Binary |
| `Salary` | Player Salary | Numerical |


### Statement of Research Problems and Methods
Using the dataset, we stemmed two main research problems:
- **What player statistic contributes the most to the event that the player is named Player of the Week?**<br>
Since whether a player is named Player of the Week is a binary variable, we decided to approach this problem using the logistic regression model.

- **What NBA title, including Player of the Week, has the most weight on the salary of the player?**<br>
Since the salary of a player is a numerical variable, we decided to approach this problem using the multiple linear regression model.

For both problems, model selection was performed to find the optimal model, and model diagnosis was performed to mitigate the possible issues of heteroscedasticity, multicollinearity and autocorrelation.


### Problem 1: Relationship between Player Statistics and Player of the Week

#### Explanatory Analysis

After extracting the relevant player statistics and Player of the Week from the dataset, we plotted the relationship between the statistics and Player of the Week using a scatter plot.

![Problem 1 Scatter Plot](plot/eda_1_scatter.png)

Observing the scatter plot, since `Potw` is a binary variable, the scatter plot did not give us a lot of useful information, apart from the differences in range of statistic values between the `Potw = 0` and `Potw = 1`. For every statistic, the range of values seems to be smaller for `Potw = 1`, with the most significant variable being `eFG_Prct`.

This discrepancy in range is also evident in the difference in frequency between `Potw = 0` and `Potw = 1`.

| `POTW` | Count | Prct |
|---|---|---|
| 0 | 8505 | 0.944685 |
| 1 | 498 | 0.055315 |

The frequency table shows that `Potw = 0` accounts for 94% of the data, which is to be expected since the number of players receiving an award would always be significantly smaller than those who did not. However, we are not sure if this would effect the reliability of the models we would build in regression analysis.

We also plotted the correlation using a heatmap.

![Problem 1 Heatmap Plot](plot/eda_1_heatmap.png)

Observing the heatmap, there are evidence that multicollinearity might exist. For example, The most correlated variables are `Two_P_Prct` and `FG_Prct`, but this is to be expected since `FG_Prct` is derived from `Two_P_Prct`. Similarly, `eFG_Prct` is derived from `FG_Prct`, so the correlation is high between them. Hence, some of these variables, specifically those that have direct relationships, will need to be removed prior to regression analysis.

Meanwhile, `TOV`, `AST` and `STL` are highly correlated between one another. However, turnovers, assists and steals are basketball moves often performed by point guards, so there might be indirect relationships between these variables. Nonetheless, these correlations would need to be addressed in regression analysis.


### Problem 2: Relationship between NBA Titles and Player Salary

#### Explanatory Analysis

After extracting the relevant player titles and salary from the dataset, we plotted the relationship between the titles and salary using a scatter plot.

![Problem 2 Scatter Plot](plot/eda_2_scatter.png)

Observing the scatter plot, since all of the variables are binary except for `Year`, it is difficult to interpret the relationships using the scatter plot. Looking at the `Year` plot, there is evidently a positive linear relationship between `Year` and `Salary`. What is also interesting about the `Year` graph is that, despite having a positive relationship, the range of values also increased for every season.

This change in range may have been affected by the increase in observations over the years.

| Decade | Count |
|---|---|
| 1990 | 2416 |
| 2000 | 2998 |
| 2010 | 3589 |

From the frequency table, we can clearly see the increase in observations over the seasons. The cause of this is unknown; either there is a steady increase in players, or there is a steady increase in data collected. Nonetheless, this might be worth looking into and be cautious about during regression analysis.

We also plotted the correlation using a heatmap.

![Problem 2 Heatmap Plot](plot/eda_2_heatmap.png)

Observing the heatmap, the overall correlation seems pretty low, except for `WS_Leader` and `MVP`. This means that, except for MVP and Win Shares Leader, having one NBA title does not automatically entitled you to another. It also meant that multicollinearity is likely not an issue in regression analysis.
