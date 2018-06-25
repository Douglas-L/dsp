[Think Stats Chapter 9 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2010.html#toc90) (resampling)

>> 
```

import numpy as np
import thinkstats2
import first

live, firsts, others = first.MakeFrames()


class DiffMeansPermute(thinkstats2.HypothesisTest):

    def TestStatistic(self, data):
        group1, group2 = data
        test_stat = abs(group1.mean() - group2.mean())
        return test_stat

    def MakeModel(self):
        group1, group2 = self.data
        self.n, self.m = len(group1), len(group2)
        self.pool = np.hstack((group1, group2))

    def RunModel(self):
        np.random.shuffle(self.pool)
        data = self.pool[:self.n], self.pool[self.n:]
        return data
    
class DiffMeansResample(DiffMeansPermute):
    
    def RunModel(self):
        group1 = np.random.choice(self.pool, self.n, replace=True)
        group2 = np.random.choice(self.pool, self.m, replace=True)
        data = group1, group2
        return data
        
def runResampletests(group1, group2):
    preg_lengths = firsts.prglngth.values, others.prglngth.values
    ht_preg_lngth = DiffMeansResample(preg_lengths)
    pv_preg_lngth = ht_preg_lngth.PValue(iters=10000)
    print('Resampled preg lengths p value=', pv_preg_lngth)
    print('Preg length actual=', ht_preg_lngth.actual)
    print('ts max=', ht_preg_lngth.MaxTestStat())
    
    birth_weights = (firsts.totalwgt_lb.dropna().values, 
                     others.totalwgt_lb.dropna().values)
    #need to drop na's since they are present
    ht_birth_wts = DiffMeansResample(birth_weights)
    pv_birth_wts = ht_birth_wts.PValue(iters=10000)
    print('Resampled birth weight p value=', pv_birth_wts)
    print('Preg length actual=', ht_birth_wts.actual)
    print('ts max=', ht_birth_wts.MaxTestStat())        
    
runResampletests(firsts,others)

def runDifftests(group1, group2):
    preg_lengths = firsts.prglngth.values, others.prglngth.values
    ht_preg_lngth = DiffMeansPermute(preg_lengths)
    pv_preg_lngth = ht_preg_lngth.PValue(iters=10000)
    print('Resampled preg lengths p value=', pv_preg_lngth)
    print('Preg length actual=', ht_preg_lngth.actual)
    print('ts max=', ht_preg_lngth.MaxTestStat())
    
    birth_weights = firsts.totalwgt_lb.dropna().values, others.totalwgt_lb.dropna().values
    #need to drop na's since they are present
    ht_birth_wts = DiffMeansPermute(birth_weights)
    pv_birth_wts = ht_birth_wts.PValue(iters=10000)
    print('Resampled birth weight p value=', pv_birth_wts)
    print('Preg length actual=', ht_birth_wts.actual)
    print('ts max=', ht_birth_wts.MaxTestStat())
runDifftests(firsts,others)
```
The model using resampling had nearly identical results as the permutation model. 
