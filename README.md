[Playoff Championship Analysis.pdf](https://github.com/user-attachments/files/18272071/Playoff.Championship.Analysis.pdf)

The NBA blocks data scraping on their official website, and even with workarounds, we were not able to retrieve it. This prompted us to manually input – using copy-and-paste – this data into an Excel spreadsheet over a few days, a massive team effort. In addition to the NBA’s official data page, we utilized Basketball Reference (a branch of Pro Sports Reference family of websites) to determine the playoff field and ultimate champion every season. Homecourt advantage information was pulled from Wikipedia records, and then cross checked with Pro Basketball Reference, as not every top-four team in each conference was guaranteed home court advantage in the first round of the playoffs. As there are 16 playoff teams per season and our data runs for 27 seasons, we will have 432 subjects in our dataset – each playoff team over the 27-year span being a subject. Our data additionally features 18 independent variables, for a total of 7,776 individual units of data. In the table below, we discuss the meaning of the variables our dataset use, with each row representing a team during a specific year:

In the table below, we discuss the meaning of the variables our dataset use, with each row
representing a team during a specific year:
Variable Name Variable Type Variable Description
WonChampionship Categorical (Y/N)
(Dependent)
Did the team win the championship this year?
WasFirstSeed Categorical (Y/N) Was the team the first seed in its conference?
HadHomeCourt Categorical (Y/N) Did the team have home-court advantage in the first
round of the playoffs (i.e. was it a top-four team in its
conference)?
Win% Ratio Percentage of games won
PTS Ratio Points scored per game
PTSRank Interval Where the team ranked total points scored during the
season, in comparison to the whole league
FG% Ratio A team’s season-long field goal accuracy
3PARank Interval Where the team ranked total three-point shots scored
during the season, in comparison to the whole league
3P% Ratio A team’s season-long three-point shot accuracy
FTARank Interval Where the team ranked total free throw shots attempted
during the season, in comparison to the whole league
FT% Ratio A team’s season-long free throw accuracy
NetRTGRank Interval Where, in the league, does the team’s net rating (points
scored/possession - points allowed/possession) rank
that season?
REB Ratio Total rebounds per game
TOV Ratio Turnovers committed per game
BLK Ratio Blocks per game
PF Interval Personal fouls per game
PointDiff Interval The season long total of how many more points a team
scored than they had scored on them
Playoff Seeding Interval Which position the team is placed in the playoffs (from
1-8)
PTS*Win % Ratio Interaction term, does more points scored per game lead
to a higher win percentage?
To learn more about some of our variables, we conducted variation analysis. We first looked at
the ranking variables PTSRank and 3PARank, and the numerical variables of Win % and PTS. We
believe that a better understanding of these variables will allow us to decipher what makes a good playoff
team, and determine if these four variables might play a large role in answering our research questions.
We believe that these variables will shed light on the answer, as they stand out as measures of strong
offenses, and because offense is so critical to winning games, a championship-caliber team. Furthermore,
we decided to include PTS and PTSRank in this analysis to analyze the difference in offensive eras. The
table below demonstrates our findings from our variation analysis (see Excel spreadsheet, sheets
“Categorical” and “Numerical” for calculations):
Variable: Standard
Deviation
Variance Mean Coefficient of
Variation
Margin of
error for the
sample mean
PTSRank 8.047217685 64.75771247 14.61304167 0.550687384 4.210226243
3PARank 8.667182248 75.12004812 13.87037037 0.624870282 4.321472128
Win % 0.084086883 0.007070604 0.613310411 0.137103302 0.214742537
PTS 7.33148521 53.75067538 102.2219907 0.071721213 1.450273099
The frequency distribution of our categorical variables (pictured below) was another good way for us to
make sense of these variables:
Additionally, we used histograms to visualize the data on our numeric variables, as pictured below:
Conducting this analysis showed us that we might have set “all playoff teams” as too low of a bar
for our analysis. Many of the playoff teams “snuck” into the playoffs, with records at or below .500.
Looking further into this phenomenon revealed that many Eastern Conference playoff teams made the
playoffs with sub .500 records, from the 2000’s to the 2010’s. The nature of the playoffs demands that
eight teams from each conference be invited, and a weak Eastern Conference in this period contributed to
many sub .500 teams being represented in our dataset. We believe that this may have dragged down the
averages of many of our variables, explaining why they are all not extremely high, something that would
be expected of a championship-caliber team.
Our analysis also showed us that many of the teams showed signs of a low scoring offense,
something that surprised us. This could be accredited to the previous point, or the aforementioned
difference in eras – offensive output has skyrocketed over the last decade due to a higher volume of threepoint shots attempted, as is reflected in higher final scores of games. However, this means that our model
will not discredit teams who performed poorly early in the season, and “got hot” before the playoffs. We
believe that this is fair, as moving forward, no team who has qualified for the playoffs should be
discredited from being a title contender.
Lastly, we performed a correlation analysis on our entire dataset to check for multicollinearity
before building our regression equation. We have highlighted correlation that is greater than .75 in green,
and less than -.75 in red. We are operating on the notion that the magnitude of a correlation coefficient
equal to or greater than .75 demonstrates multicollinearity, and these variables will be removed. Below is
the correlation matrix:
Based on our previous assertions, we have removed the variables of PointDiff, PlayoffSeed,
PTS*WinPercent, and NetRTGRank due to high pairwise correlation, and demonstration of
multicollinearity.
Analysis:
We used a logistic regression to answer the question of: What is the probability that a playoff
team will win an NBA championship at the end of the regular season? We chose to use a logistic
regression model because of the nature of our binary dependent variable: a team either will or will not win
the championship. We are studying whether a team will win the championship (1) or they will not (0), and
a traditional linear regression model would allow for results to be beyond the range, falling short of 0 or
exceeding 1. Additionally, our aim was to generate a probability, making a logistic regression model even
more logical to help answer this question.
After removing the four variables that demonstrated multicollinearity, we ran our initial
regression model in python. This model had an LLR p-value of 4.096e-12, demonstrating that this model
was a significant improvement over the null model. However, the model also prompted a message in
Python noting that the model demonstrated the possibility of complete quasi-separation: 50% of
observations could be perfectly predicted by this regression equation. In other words, at least one outcome
in the dependent variable (WonChampionship) had no instances of at least one category of at least one
independent variable. We identified HadHomeCourt as the problematic variable, because no team in our
dataset that did not have home-court advantage in the first round has won the championship. However,
this is not true of the entire NBA history. This highlights the problem with using official data that was
only truly tracked starting in 1997. In terms of our variables, all instances in which the independent
variable HadHomeCourt was 0, the dependent variable WonChampionship was also 0. To resolve this
issue, we removed this variable and were left with our final regression equation of:
P(WonChampionship) = Sigmoid(Constant + WasFirstSeed + WinPercent – PTS +
FGPercent – 3PPercent – FTPercent – REB + TOV + BLK – PF + FTARank – PTSRank –
3PARank).
In this equation, the Sigmoid() function is the key to logistic regression. The sigmoid function is
as follows: �������(�) = !
!"#!". This function places bounds on P(WonChampionship), such that it
must be between 0 and 1, not inclusive.
Coefficients and p-values were:
Variable Regression Coefficients P-Value
Constant -9.8838 0.584
WasFirstSeed 0.4833 0.448
WinPercent 18.0926 0.001
PTS -.0282 .739
FGPercent 62.3266 .078
3PPercent -59.5069 .003
FTPercent -11.7131 .201
REB -.0183 .925
TOV .1069 .698
BLK .3182 .323
PF -.1827 .298
FTARank .0734 .042
PTSRank -.0244 .628
3PARank -.0296 .476
This equation had an LLR p-value of 6.416e-11, still well under the significance cutoff of .05.
Even though this model technically has a higher LLR p-value, we feel confident that the minimal increase
to offset the quasi separation was warranted. Additionally, we ran regression models with various other
variables removed to investigate whether or not we could further lower the LLR p-value. There was only
a significant decrease when we removed all independent variables besides WinPercent, FGPercent, and
3PPercent. The LLR p-value of this model was only 4.744e-14. After deliberation, we decided to not go
with this model, as we believe that having more variables will more accurately reflect real-world
scenarios, and that these additional variables do not come at a significant cost in LLR p-value. This
assumption is justified as well, due to the LLR p-values of both models being significantly lower than .05.
The results of this logistic regression model are very interesting, and at times even run contrary to
our expectations. We did not think many metrics based on points scored would result in a lesser
probability of winning the championship. This suggests that perhaps offense matters less to winning and
defense matters more to winning than we expected. Additionally, our data is not era-adjusted, giving a
massive negative weight to three-point shots that were relatively unpopular in the 1990s and 2000s
despite our knowing now in modern-day basketball, that those shots are incredibly valuable towards being
an efficient offense. Of course, these results could also be impacted by the nature of the sport: the best
statistical team, on-paper, does not always win the championship.
The massive weight on FGPercent makes sense, as teams generally need to shoot accurately and
score efficiently to win games. This same logic also holds true for the weight on the WinPercent variable.
Lastly, it is possible that there are confounding variables that are resulting in negative weights for some of
our variables. For example, a team trailing by a significant amount more often than not may be forced to
shoot more three-point shots to try and get themselves back into a competitive state. However, this is just
speculation, and with these results we have finalized a model that we can confidently say will predict a
team's percent chance of winning the NBA championship based on regular season data, to the best ability
of historical data.
Conclusion:
We set out on this project to attempt to answer the question: what is the chance an NBA team will
win the NBA championship, based on their regular season statistics? Through this research process, we
determined that a multitude of variables will increase a team's chances, including if they were a one seed,
their win percentage, the amount of field goals that they made per game, the amount of turnovers they
commit per game, the amounts of blocks they record per game, and where they rank in the league on free
throws taken per game. Conversely, the amount of points a team scores per game, the percentage of their
three point shots made, their rebounds per game, the percentage of their free throws made, the amount of
personal fouls they commit per game, where the team ranked in the league in points scored, and where the
team ranked in the league on three point shots decreases a team's odds of winning a championship.
Some of these coefficients were surprising, and we can accredit that to a variety of factors outside
of the control of someone using limited historical data. Using historical data opens our analysis to the
possibility of weighing some variables with greater significance, as they were important in the past, but
not the present. It is also important to note that sports are unpredictable, and miracle runs can happen,
subverting the expectations of the past. Additionally, players are also liable to get injured at various points
during the season, which can affect teams disproportionately. However, we can say that based on
statistical analysis of our results, we can be confident that this model is the best that an analysis on purely
historical factors can produce.
This has major implications for sports bettors, who can use this research to level the playing field
against major sports books. This can also be helpful for fans, who are angsty to see how far their team
will make it come the end of the regular season. Lastly, we can see this model being used by general
managers, to better understand what makes a team a true championship contender. In the world of sports,
everyone is always trying to predict who will be the next champion, and we believe that we have created a
model that will answer this question to the best of our ability.
