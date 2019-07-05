[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

The value of Cohen's d for these two groups is -0.089

The code I wrote to determine this is:

import nsfg
import thinkstats2
import math

pregnancies = nsfg.ReadFemPreg()
livebirths  = pregnancies[pregnancies.outcome == 1]
firstborns  = livebirths[livebirths.birthord == 1]
nonfirsts   = livebirths[livebirths.birthord != 1]

first_weight = firstborns.totalwgt_lb
nonfirst_weight = nonfirsts.totalwgt_lb

def cohend(group1, group2):
    mean_difference = group1.mean() - group2.mean()
    
    var1 = group1.var()
    var2 = group2.var()
    
    n1 = len(group1)
    n2 = len(group2)
    
    s = (n1 * var1  + n2 * var2) / (n1 + n2)
    
    d = mean_difference / math.sqrt(s)
    return d

d = cohend(first_weight, nonfirst_weight)
print(d)
