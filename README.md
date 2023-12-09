# Monte Carlo Simulator
This notebook runs Monte Carlo simulations in two dimensions. Try it live at
https://colab.research.google.com/github/controversy187/monte-carlo/blob/main/query-jira.ipynb

The first model forecasts how long it will take to complete a given backlog, given the historical amount of work completed.

The second model forecasts how many work items you can expect to complete in a given number of iterations.

The "work items" themselves are irrelevant. They could be User Stories, Features, Epics, Tasks, or any similar-sized bodies of work. Likewise, the iterations could be hours, days, weeks, sprints, quarters, or any other timebox, as long as it is consistent across the model.

## How does a Monte Carlo Simulation work?
Unlike averaging work, which tends to hide details and nuance, the Monte Carlo simulation actually runs sample events, based on historic data. Lets say that your team has gotten 14 tasks done this week, 12 the week before, 8 the week prior, and 22 the week prior to that. So your team's data looks like:
Week 1: 22
Week 2:  8
Week 3: 12
Week 4: 14

You can continue to gather as much data as you believe is relevant to the way your team is operating currently, whether that's the past 3 weeks or the past 50. Next, lets say you want to know how long it will take your team to complete a project that has 200 tasks in it, assuming that your team is dedicated to this project and they don't experience any abnormal dependencies or interruptions that they didn't experience during your past data set. We then randomly select one past week from our data set and grab the number of tasks we completed in that week, and subtract it from our total of 200 tasks. We keep doing that until the remaining tasks is 0, and then count how many times we had to pull a random week's completed task count. That total would be the number of weeks it took us to complete the project in a single trial.

Next, we repeat that process many times, like 1000 or more. Once we have that full data set, of 1000 trials of completing the project, we start to gather our data points across those trials. We can start to see thresholds of success, such as "89% of the trials completed in 16 or fewer weeks. 97% completed in 17 or fewer." This allows us to talk about risks around deadlines as opposed to estimated completions which hide the potential variances of work.

The second model in this notebook is similar, but instead of forecasting the time to complete a body of work, it forecasts how much work can be completed in a given timeframe.