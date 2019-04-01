[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

# Exercise 3.1

#### Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample. Use the NSFG respondent variable NUMKDHH to construct the actual distribution for the number of children under 18 in the household.Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household. Plot the actual and biased distributions, and compute their means. As a starting place, you can use chap03ex.ipynb.

The bias that would have been reflected by surveying only children under 18 to gather data for number of kids in a household is immense and is reflected by the means of the two distributions. The unbiased mean is 1.024 while the biased mean is 2.403. That is a major difference of almost 1.5 children! This shows how careful you have to be when considering how to collect data and the origins of your data.

### Code used for outputting PMF plots and distribution data 

```python
import thinkstats2
import thinkplot
import nsfg

def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)
    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
    new_pmf.Normalize()
    return new_pmf

data = nsfg.ReadFemResp()
nsfg.CleanFemResp(data)

kids_pmf = thinkstats2.Pmf(data.numkdhh, label = 'actual')
biased_kids_pmf = BiasPmf(kids_pmf, label = 'observed')

thinkplot.PrePlot(2)
thinkplot.Pmfs([kids_pmf, biased_kids_pmf])
thinkplot.Show(xlabel='Number of Kids', ylabel='PMF')
print ('Unbiased Mean: ', kids_pmf.Mean())
print ('Biased Mean: ', biased_kids_pmf.Mean())
```

