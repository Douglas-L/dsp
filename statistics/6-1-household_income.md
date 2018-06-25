[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)


```
import numpy as np
import hinc
income_df = hinc.ReadData()

def InterpolateSample(df, log_upper=6.0):
    """Makes a sample of log10 household income.

    Assumes that log10 income is uniform in each range.

    df: DataFrame with columns income and freq
    log_upper: log10 of the assumed upper bound for the highest range

    returns: NumPy array of log10 household income
    """
    #compute the log10 of the upper bound for each range
    df['log_upper'] = np.log10(df.income)

    #get the lower bounds by shifting the upper bound and filling in
    #the first element
    df['log_lower'] = df.log_upper.shift(1)
    df.loc[0, 'log_lower'] = 3.0

    #plug in a value for the unknown upper bound of the highest range
    df.loc[41, 'log_upper'] = log_upper
    
    #use the freq column to generate the right number of values in
    #each range
    arrays = []
    for _, row in df.iterrows():
        vals = np.linspace(row.log_lower, row.log_upper, row.freq)
        arrays.append(vals)

    #collect the arrays into a single sample
    log_sample = np.concatenate(arrays)
    return log_sample
    
def CentralMoment(xs, k):
    mean = np.mean(xs)
    return sum((x - mean)**k for x in xs) / len(xs)
def StandardizedMoment(xs, k):
    var = CentralMoment(xs, 2)
    std = np.sqrt(var)
    return CentralMoment(xs, k) / std**k

def Skewness(xs):
    return StandardizedMoment(xs, 3)

def PearsonMedianSkewness(xs):
    median = np.median(xs)
    mean = np.mean(xs)
    var = CentralMoment(xs, 2)
    std = np.sqrt(var)
    gp = 3 * (mean - median) / std
    return gp
    
log_sample = InterpolateSample(income_df, log_upper=6.0)
#np.linspace makes up a new even spaced sample based on frequency in bins in real sample

#turn pseudo sample back into normal scale
sample = np.power(10, log_sample)

print('Skewness=', Skewness(sample))
print("pearson's skewness=", PearsonMedianSkewness(sample))
def frac(xs, below_which):
    return len(xs[xs < below_which]) / len(xs)
print('frac=',frac(sample,np.mean(sample)))

log_sample2 = InterpolateSample(income_df, log_upper=7.0)
sample2 = np.power(10, log_sample2)

print('Skewness=', Skewness(sample2))
print("pearson's skewness=", PearsonMedianSkewness(sample2))
print('frac=',frac(sample2,np.mean(sample2)))


```

66% of households report a taxable income below the mean when the upper bound is one million. The results depend strongly on the assumed upper bound as the fraction jumps up to 86% after increasing the upper bound to 10 million. The skewness more than doubles from 5 to 11,demonstrating the strong effect of outliers. In contrast, the Pearson's median skewness coefficient is more robust since there are no exponents to amplify the weight of outliers.