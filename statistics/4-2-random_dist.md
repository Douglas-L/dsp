[Think Stats Chapter 4 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2005.html#toc41) (a random distribution)

>> 
```
%matplotlib inline

import numpy as np
import thinkstats2
import thinkplot
%matplotlib inline

rand_pmf = thinkstats2.Pmf(np.random.random(1000))
thinkplot.Pmf(rand_pmf)
thinkplot.Show(xlabel='random variate', ylabel='PMF', axis=[0,1,0,.0012])


thinkplot.Cdf(rand_pmf)
thinkplot.Config(xlabel='random variate', ylabel='CDF')
```

The slight bumps in the CDF reveal that the random function does not generate perfectly uniform numbers even though it samples from a uniform distribution because it is still a sample.