[Think Stats Chapter 8 Exercise 3](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77)

---

>> 
```

import numpy as np
import random
import thinkstats2
import thinkplot

def SimulateGame(lam):
    """Simulates a game and returns the estimated goal-scoring rate.

    lam: actual goal scoring rate in goals per game
    """
    goals = 0
    t = 0
    while True:
        time_between_goals = random.expovariate(lam)
        t += time_between_goals
        if t > 1:
            break
        goals += 1

    #estimated goal-scoring rate is the actual number of goals scored
    L = goals
    return L

def myRMSE(means, lam):
    square_mean = [(m-lam)**2 for m in means]
    return np.sqrt(np.mean(square_mean))

def Sim_many_games(lam, m=1000000):
    ls = [SimulateGame(lam) for _ in range(m)]
    mean_error = np.mean([l - lam for l in ls])
    lRMSE = myRMSE(ls, lam)
    print('mean error', mean_error)
    print('RMSE', lRMSE)
    pmf = thinkstats2.Pmf(ls)
    thinkplot.Hist(pmf)
    thinkplot.Config(xlabel='Goals Scored', ylabel='Pmf')
    cdf = thinkstats2.Cdf(ls)
    ci = cdf.Percentile(5), cdf.Percentile(95)
    print('90% confidence interval=', ci)

Sim_many_games(2, m=1000)

Sim_many_games(2, m=1000000)

Sim_many_games(7)
```

This way of making an estimate appears to be unbiased because the mean error is small and approaches 0 as m increases. The standard error for lambda = 2 is approximately 1.4. As lambda increases, the sampling error also increases. 
