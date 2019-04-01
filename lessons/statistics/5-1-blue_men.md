[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

# Exercise 5.1

#### In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters μ = 178 cm and σ = 7.7 cm for men, and μ = 163 cm and σ = 7.3 cm for women. In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: use scipy.stats.norm.cdf.

Using the scipy normal distribution model and the mean and standard deviation given in the question we can calculate that the percentae of U.S. males eligible to perform in the blue man group is approximately 34.275%. This was done by fiding the percentage of males approximately under 5'10" and subtracting from the percentage of males approximately 6'10.

### Code used for calculating approximate percentage of U.S. males between 5'10" and 6'1"

```python
import scipy.stats

def inch_to_cm(inches):
    return inches * 2.54

mu = 178
sigma = 7.7
height_dist_model = scipy.stats.norm(loc = mu, scale = sigma)
short_prob = height_dist_model.cdf(inch_to_cm(70))
tall_prob = height_dist_model.cdf(inch_to_cm(73))

print ("Percentage of U.S. males eligible for blue man group: ",
        (tall_prob-short_prob) * 100, "%")
```