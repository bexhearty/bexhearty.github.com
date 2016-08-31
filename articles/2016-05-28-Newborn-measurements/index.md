# Newborn percentiles

How did the nurse know that my son was born in the 96th percentile?

When my son was born earlier this month, the nurse measured his length, head circumference, and weight. She then informed us that 96% of male babies were born below his height. How did she know that? 

The concept of a normal distribution is helpful for understanding this percentage. In a normal distribution, most observations are grouped around the middle; more precisely, 34% fall between the mean and +1 standard deviation, and the other 34% -1 standard deviation. Also, in a normal distribution, 50% of the observations fall below the mean, and the other half above the mean. 

![](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a9/Empirical_Rule.PNG/675px-Empirical_Rule.PNG)

This is useful when calculating other interesting statistics, like how many individuals do we expect to fall below or above a particular point.  If a baby is 1 standard deviation above the mean, then we know that such baby is at the 84th percentile (50% which correspond to all the individuals below the mean + 34% which correspond to all the individuals between the mean and 1 standard deviation).

In statistcs, a z-score is equivalent to how many standard deviations your observation is from the mean. A positive score means that your observation lays above the mean, and a negative score means below the mean. If we have the following input:

* My child measures 53.34 cm of length at birth
* The mean of length in newborn boys is [49.9 cm](http://www.who.int/childgrowth/standards/LFA_boys_0_13_zscores.pdf?ua=1)
* The standard deviation of length in newborn boys is [1.89 cm](http://www.who.int/childgrowth/standards/LFA_boys_0_13_zscores.pdf?ua=1)
 
Then we can calculate the z-score, like so:

[My Measure - Mean] / Standard Deviation = z-score

So for us, we get a z-score of 1.82 ( [53.34 - 49.9] / 1.89 = 1.82). Looking at a [z-score chart](http://math.arizona.edu/~rsims/ma464/standardnormaltable.pdf), we gather that 1.82 corresponds to 0.9641, which means that 96.41% of the population fall at or below this measure.

So they'll tell you that your baby is in the 34% in weight, 96% of height, and 90% of brain circumpherence. So what? Does it all mean that my baby is tall, dark, handsome and wicked smart and because of that he is going to be accepted into daycare and then into Harvard, and the become POTUS? Sure mom. Especially if you weigh him after feeding him a big meal and before changing that dirty diaper. 
