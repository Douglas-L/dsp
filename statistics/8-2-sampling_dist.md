[Think Stats Chapter 8 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77) (scoring)

>> 
```

import numpy as np

import thinkstats2
import thinkplot

def myRMSE(means, lam):
    square_mean = [(m-lam)**2 for m in means]
    return np.sqrt(np.mean(square_mean))
def expo_estimate(n=10, m=1000):
    lam = 2
    
    means = []
    for _ in range(m):
        xs = np.random.exponential(1/lam, n)
        L = 1 / np.mean(xs)
        means.append(L)
    print('standard error:', myRMSE(means, lam))
    
    cdf = thinkstats2.Cdf(means)
    ci = cdf.Percentile(5), cdf.Percentile(95)
    print('90% confidence internval', ci)
    thinkplot.Cdf(cdf, label=('n=%s' % n))
    thinkplot.Config(xlabel='random variate', ylabel='CDF')
expo_estimate()
#n=10 

#Plot other values of n
thinkplot.PrePlot(3)
expo_estimate(n=100)
expo_estimate(n=1000)
expo_estimate(n=100000)
thinkplot.Config(xlabel='Random variate', ylabel='CDF')
```

As sample size increases, the standard error decreases and the sampling distribution of the estimate L gets narrower.