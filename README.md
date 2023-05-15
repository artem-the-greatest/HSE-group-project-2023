# HSE-group-project-2023
Hello! You are on our group project repository. Here you can find all the material of our project and useful links. 

We tried to build an optimal momentum trading strategy, laying down the rules under which we enter into one position or another.\
In our model, the expediency of actions is influenced by six parameters:
- Weights of currencies in the portfolio
- The threshold at which we consider a change in value to be significant
- Number of consecutive previous days in which the threshold was
crossed\

We assume exchange rate deviations to be symmetrical, so we set a
single threshold in both directions. Among all possible options, we tried to find the outcome with the highest Sharpe Ratio
