[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

    import numpy as np
    import math
    import thinkstats2
    import thinkplot

    import nsfg

    #prep data
    preg = nsfg.ReadFemPreg()
    live = preg[preg.outcome == 1]
    firsts = live[live.birthord == 1]
    others = live[live.birthord != 1]
    
    def CohenEffectSize(group1, group2):
        diff = group1.mean() - group2.mean()
    
        var1 = group1.var()
        var2 = group2.var()
        n1, n2 = len(group1), len(group2)
        pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
        d = diff / math.sqrt(pooled_var)
        return d

    print("birth weight Cohen's d:", CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb))
    print("pregnancy length Cohen's d:", CohenEffectSize(firsts.prglngth, others.prglngth))
    
birth weight Cohen's d: -0.088672927072602
pregnancy length Cohen's d: 0.028879044654449883

Cohen's *d* for the two variables indicates that first babies tend to be lighter in weight and require a longer pregnancy than other babies. The magnitude of Cohen's *d* suggests a three-fold difference in the size of the effect of a first baby. 
