[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

>> 
```
%matplotlib inline

import numpy as np
import pandas as pd
import math

import thinkstats2
import thinkplot

#import data
import first
live, firsts, others = first.MakeFrames()
live = live.dropna(subset=['agepreg', 'totalwgt_lb'])

birth_weight = live['totalwgt_lb']
mom_age = live['agepreg']
thinkplot.Scatter(mom_age, birth_weight, alpha=0.15, s=10)
thinkplot.Config(xlabel="Mother's age (years)", ylabel='Birth weight(lbs)')
#The scatter plot shows no obvious correlation as the weights look relatively uniform across the different ages. 

#binning
bins = np.arange(10,48,3)
indices = np.digitize(live.agepreg, bins)
groups = live.groupby(indices)

#Trimmed off ends for nicer visualization
moms_age = [group.agepreg.mean() for i, group in groups][1:-1]
cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for i, group in groups][1:-1]

print(moms_age)
thinkplot.PrePlot(3)
for percent in [75,50,25]:
    birth_weight = [cdf.Percentile(percent) for cdf in cdfs]
    label = '%dth' % percent
    thinkplot.Plot(moms_age, birth_weight, label=label)
thinkplot.Config(xlabel="mother's age (years)", ylabel='Birth weight(lbs)',
                 xlim=[14,45])
#The percentile plot suggests a weak reationship between age and birth weight, especially when the mothers are young.                   
                
def Corr(xs,ys):
    xs = np.asarray(xs)
    ys = np.asarray(ys)
    meanx, varx = np.mean(xs), np.var(xs)
    meany, vary = np.mean(ys), np.var(ys)
    corr = np.dot(xs-meanx, ys-meany) / len(xs) / math.sqrt(varx * vary)
    return corr
print('Corr', Corr(mom_age, birth_weight))

def SpearmanCorr(xs, ys):
    xranks = pd.Series(xs).rank()
    yranks = pd.Series(ys).rank()
    return Corr(xranks, yranks)
print('SpearmanCorr', SpearmanCorr(mom_age, birth_weight))
```
Binning and the percentile plot revealed a weak positive relationship between mother's age and birth weight that was hard to see in the scatter plot. The Pearson's and Spearman's correlations of 0.07 and 0.09, respectively, support this observation of small positive correlations.
