[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

>> 
```
#prep
%matplotlib inline

import numpy as np

import nsfg
import first
import thinkstats2
import thinkplot

resp = nsfg.ReadFemResp()

#actual distribution
actual_pmf = thinkstats2.Pmf(resp['numkdhh'], label='actual')
thinkplot.Pmf(actual_pmf)
thinkplot.Config(xlabel='number of kids', ylabel='pmf')

#Multiply probabilities by number of kids
biased_pmf = actual_pmf.Copy(label='biased')
for x, p in actual_pmf.Items():
    biased_pmf.Mult(x,x)
biased_pmf.Normalize()

#plot both distributions together
thinkplot.PrePlot(2)
thinkplot.Pmfs([actual_pmf, biased_pmf])
thinkplot.Config(xlabel='Number of kids', ylabel='PMF')

def pmf_mean(pmf):
    total = 0
    for x,p in pmf.Items():
        total += x * p
    return total
        
print(pmf_mean(actual_pmf))

print(pmf_mean(biased_pmf))
```

Children surveyed would answer a mean of 2.40 children per household, which is much higher than the actual mean of 1.02 per household.
