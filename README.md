[Playoff Championship Analysis.pdf](https://github.com/user-attachments/files/18272071/Playoff.Championship.Analysis.pdf)

This project focuses on building a logistic regression model in Python to predict the probability of an NBA playoff team winning the championship based on their regular season statistics. Using historical NBA data from 27 seasons (spanning 432 playoff teams), we explored how various metrics influence championship outcomes, which can help aim to provide insights for sports analytics, betting strategies, and team management.  Our data additionally features 18 independent variables, for a total of 7,776 individual units of data.

In the table below, we discuss the meaning of the variables our dataset use, with each row
representing a team during a specific year:

| Variable Name   | Variable Type  | Variable Description                                                                                             |
|-----------------|----------------|-------------------------------------------------------------------------------------------------------------------|
| WonChampionship | Categorical (Y/N) | Did the team win the championship this year?                                                                      |
| WasFirstSeed    | Categorical (Y/N) | Was the team the first seed in its conference?                                                                    |
| HadHomeCourt    | Categorical (Y/N) | Did the team have home-court advantage in the first round of the playoffs (i.e. was it a top-four team in its conference)? |
| Win%            | Ratio          | Percentage of games won                                                                                           |
| PTS             | Ratio          | Points scored per game                                                                                             |
| PTSRank         | Interval       | Where the team ranked total points scored during the season, in comparison to the whole league                    |
| FG%             | Ratio          | A team’s season-long field goal accuracy                                                                            |
| 3PARank         | Interval       | Where the team ranked total three-point shots scored during the season, in comparison to the whole league         |
| 3P%             | Ratio          | A team’s season-long three-point shot accuracy                                                                     |
| FTARank         | Interval       | Where the team ranked total free throw shots attempted during the season, in comparison to the whole league       |
| FT%             | Ratio          | A team’s season-long free throw accuracy                                                                           |
| NetRTGRank      | Interval       | Where, in the league, does the team’s net rating (points scored/possession - points allowed/possession) rank that season? |
| REB             | Ratio          | Total rebounds per game                                                                                            |
| TOV             | Ratio          | Turnovers committed per game                                                                                        |
| BLK             | Ratio          | Blocks per game                                                                                                    |
| PF              | Interval       | Personal fouls per game                                                                                             |
| PointDiff       | Interval       | The season long total of how many more points a team scored than they had scored on them                          |
| Playoff Seeding | Interval       | Which position the team is placed in the playoffs (from 1-8)                                                        |
| PTS*Win %       | Ratio          | Interaction term, does more points scored per game lead to a higher win percentage?                               |

To learn more about some of our variables, we conducted variation analysis. We first looked at the ranking variables PTSRank and 3PARank, and the numerical variables of Win % and PTS. We believe that a better understanding of these variables will allow us to decipher what makes a good playoff team, and determine if these four variables might play a large role in answering our research questions. We believe that these variables will shed light on the answer, as they stand out as measures of strong offenses, and because offense is so critical to winning games, a championship-caliber team. Furthermore, we decided to include PTS and PTSRank in this analysis to analyze the difference in offensive eras. The table below demonstrates our findings from our variation analysis (see Excel spreadsheet FINAL PROJECT DATA, sheets “Categorical” and “Numerical” for calculations):

| Variable          | Standard Deviation | Variance       | Mean        | Coefficient of Variation | Margin of error for the sample mean |
|-------------------|--------------------|----------------|-------------|--------------------------|-------------------------------------|
| PTSRank           | 8.047217685        | 64.75771247    | 14.61304167 | 0.550687384              | 4.210226243                        |
| 3PARank           | 8.667182248        | 75.12004812    | 13.87037037 | 0.624870282              | 4.321472128                        |
| Win %             | 0.084086883        | 0.007070604    | 0.613310411 | 0.137103302              | 0.214742537                        |
| PTS               | 7.33148521         | 53.75067538    | 102.2219907 | 0.071721213              | 1.450273099                        |

The frequency distribution of our categorical variables (pictured below) was another good way for us to make sense of these variables:

![image](https://github.com/user-attachments/assets/70325436-8e0a-4cfd-b18a-ac382f670663)

Additionally, we used histograms to visualize the data on our numeric variables, as pictured below: 

![image](https://github.com/user-attachments/assets/fb764535-4b0c-4924-ab8b-81a65132f871)
![image](https://github.com/user-attachments/assets/50c3bc7b-b663-4abc-b466-abd2259e5ffa)



