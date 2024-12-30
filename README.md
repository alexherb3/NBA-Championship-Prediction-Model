# NBA-Championship-Prediction-Model

[Playoff Championship Analysis.pdf](https://github.com/user-attachments/files/18272071/Playoff.Championship.Analysis.pdf)

This project focuses on building a logistic regression model in Python to predict the probability of an NBA playoff team winning the championship based on their regular season statistics. Using historical NBA data from 27 seasons (spanning 432 playoff teams), we explored how various metrics influence championship outcomes, which can help aim to provide insights for sports analytics, betting strategies, and team management.  Our data additionally features 18 independent variables, for a total of 7,776 individual units of data. The full-in depth analysis is featured in the PDF file.

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
