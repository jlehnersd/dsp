[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

The mean of the actual distribution of children under 18 in homes in the United States is 1.02 and the mean of the biased distribution is 2.40 - the code I wrote to determine the means is:

```python
import nsfg
import thinkstats2
import thinkplot

def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label = label)
    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
    new_pmf.Normalize()
    return new_pmf
    
df = nsfg.ReadFemResp()
under18 = df['numkdhh']

under_actual = thinkstats2.Pmf(under18, label = 'actual')
under_biased = BiasPmf(under_actual, label = 'biased')
    
thinkplot.PrePlot(2)
thinkplot.Pmfs([under_actual, under_biased])
thinkplot.Show(xlabel = 'Number of children under 18', ylabel = 'Probability')

mean_actual = under_actual.Mean()
mean_biased = under_biased.Mean()
print('actual mean: ', mean_actual)
print('biased mean: ', mean_biased)
```
