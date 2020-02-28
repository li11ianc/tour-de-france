# STA 323 :: Exam 1

## Introduction

The Tour de France is a multi-stage bike race held annually in July. The race
has riders primarily cycle throughout French cities, countrysides, and 
mountains. It is considered one of the toughest endurance events in the world.
Participants will cover over 3,300 kilometers in a 23-day span.

Cycling is both a team and individual sport. Riders are members of teams, but
there are individual accolades up for grabs. Riders in first with regards
to these individual award categories wear special colored / patterned jerseys.


- Overall winner (as determined by time): yellow jersey
- Best sprinter (as determined by points): green jersey
- King of the mountains / best climber (as determined by points): polka dot jersey
- Best young rider (as determined by time): white jersey 

<center>
<img src="images/jerseys.jpg" width="350" height="300">
</center>


## Data

Data in your repository is from the 2019 Tour de France. To get started, read in 
`tdf_2019.rds` and create an object `tdf` with

```r
tdf <- readRDS(file = "data/tdf_2019.rds")
```

Most of the variables are self-explanatory. The data should be clean and
organized; maybe not in the form you want, but I did not add any issues as 
I did in Homework 4. Below are a few details on the data.

1. Time is expressed in hours:minutes.seconds.
2. Only the winning rider (team) in a stage has a real time, the time
   for others are relative to the winner's and formatted as "+hh:mm.ss".
3. `sprint` and `climber` are the number of points a rider earned in the stage
   for that respective category.

## Essential details

#### Deadline and submission

**The deadline to submit Exam 1 is 5:00pm on Friday, March 6.** 
Only the code in the master branch will be graded.

#### Rules

**Phase I**: Data understanding, Friday, Feb 28 at 5:00pm - Monday, Mar 
             2 at 5:00pm

**Phase II**: Tasks, Monday, Mar 2 at 5:00pm - Friday, Mar 6 at 5:00pm

- This is an individual assignment.

- Everything in your repository is for your eyes only except for the 
  instructor and TAs.

- You may not communicate anything about this exam to anyone.

- You may use any online, book, and note resources. As always, you must cite 
  any code you use as inspiration.

- During Phase I, post any questions about the data to channel #exam1 on Slack. 
  During Phase II, only send direct messages to the instructor on Slack. 
  Questions should only be about understanding the data or the exam's 
  instructions.

#### git / GitHub

You will only have one branch to start with in your repository - master. 
You may create other branches as needed, but only your work in the master 
branch will be graded. Be sure to push your work before the deadline.

#### Academic integrity

This is an individual assignment. See the Rules section above.
As a reminder, any code you use directly or as inspiration must be cited.

To uphold the Duke Community Standard:

- I will not lie, cheat, or steal in my academic endeavors;
- I will conduct myself honorably in all my endeavors; and
- I will act if the Standard is compromised.

