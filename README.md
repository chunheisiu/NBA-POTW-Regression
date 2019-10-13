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

There are 9,003 Rows and 38 Variables in the dataset.

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
