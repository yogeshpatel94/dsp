[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

# Exercise 2.4  
#### Using the variable totalwgt_lb, investigate whether first babies are lighter or heavier than others. Compute Cohen’s d to quantify the difference between the groups. How does it compare to the difference in pregnancy length?

The effect of birth order on total_wgt at -0.0887 standard deviations is similarly marginal as the effect that birth order has on prglngth at 0.0289 standard deviations.

### Code used for outputting Cohen's Effect Size 

```python
import first
import thinkstats2
import thinkplot
import nsfg
import math

def CohenEffectSize(group1, group2):
    diff = group1.mean() - group2.mean()
    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)
    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / math.sqrt(pooled_var)
    return d

preg = nsfg.ReadFemPreg()
live = preg[preg.outcome == 1]
firsts = live[live.birthord == 1]
others = live[live.birthord != 1]

baby_order_total_wgt_effect = CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)
baby_order_prglngth_effect = CohenEffectSize(firsts.prglngth, others.prglngth)

print('Baby order effect on prglngth: ', baby_order_prglngth_effect)
print('Baby order effect on total_wgt: ', baby_order_total_wgt_effect)
```

