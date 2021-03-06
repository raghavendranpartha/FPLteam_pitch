---
title       : Build your Fantasy Premier League football team
subtitle    : Developing Data Products
author      : Raghavendran Partha
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Fantasy Premier League

1. Based on the Barclays Premier League/English Premier League (EPL)

2. Over 3.5 million fantasy managers/users every season

3. Each manager is given a fixed amount of money (100 million pounds) to build a squad consisting of
     
     a. 2 Goalkeepers     
     b. 5 Defenders     
     c. 5 Midfielders     
     d. 3 Forwards
     
     with a maximum of 3 players from a single EPL team
     
4. Winner at the end of the season gets to take home 25,000 pounds

--- .class #id 

## Basics of the game

1. In each gameweek the fantasy football players will earn points based on their performance in the Barclays Premier League
2. Additional rules that allow managers to transfer players in and out of their team every week
3. Objective of a manager is thus to create a team that scores the highest points over the course of the season

Sample Player data: (available for free at http://fantasy.premierleague.com/stats/elements/)




|Player  |Team |Pos |Price |Total |
|:-------|:----|:---|:-----|:-----|
|Payet   |WHU  |MID |�8.2  |71    |
|Mahrez  |LEI  |MID |�6.5  |70    |
|Vardy   |LEI  |FWD |�7.1  |70    |
|S�nchez |ARS  |MID |�11.5 |65    |
|Ayew    |SWA  |MID |�7.2  |57    |
|Myhill  |WBA  |GKP |�4.7  |57    |
|Pell�   |SOU  |FWD |�8.4  |56    |

--- .class #id 

## Choosing the initial squad

- Objective: Select 15 players from a pool of 700

- Current season underway with 8 of the 38 gameweeks completed

- Constraint-based optimization problem: Select players who have scored the highest points in aggregate over the past gameweeks subject to the following constraints

     * There are exactly 2 goalkeepers     
     * There are exactly 5 defenders     
     * There are exactly 5 midfielders     
     * There are exactly 3 forwards     
     * There are no more than 3 players belonging to the same EPL team     
     * Their combined cost is at most 100 million pounds
     


--- .class #id

## Linear Programming Solution to the problem

- Implemented using lpSolveAPI package in R

- Optimization over 26 variables associated with each player: 

     * Total Points scored by the player (Pts)     
     * Price of the player (Cost)     
     * Value of 0 or 1 for the 4 different positions: if the player belongs to a position, that value is set to 1, and rest are 0     
     * Value 0 or 1 for the 20 different teams: if the player belongs to a team, that value is set to 1, and rest are 0     

- The optimization problem tries to maximize sum of Pts for 15 players under the condition that the 

     - Sum of the variable Cost is at most 100
     - Sum of the position variables is equal to the desired number of players in each position
     - Sum of each of the team variables is at most 3 

