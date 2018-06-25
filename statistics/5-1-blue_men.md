[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

>> 
```
import scipy.stats

mu = 178 #cm
sigma = 7.7 #cm
male_heights = scipy.stats.norm(loc=mu, scale=sigma)

#convert inches to cm
low = 70 * 2.54
high = 73 * 2.54

male_heights.cdf(high) - male_heights.cdf(low)
```

34.3% of the US male populaton is between 5'10" and 6'11".