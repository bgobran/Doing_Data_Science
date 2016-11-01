# BGobran_HomeworkAssignment4
Brian Gobran Section 403  
11/1/2016  


##Code Description
##### There are two parts to the Central Limit Theorem that this program will prove:

#####   1. The mean of the means of the samples is the mean of the population
#####   2. The standard deviation of the means of the samples is the standard deviation of the population divided by the square root of the sample size

##### The first step is to create very large arrays of the normal and exponential distributions that we will extract our samples from.

#####  For the normal distributions, we will use a mean of 10 and a standard deviation of 2.

#####  For the exponential distributions, we will use a rate of 0.1 which yields a mean and a standard deviation of 10.

##### Then we will sample from these large distributions.

##### We will test this with normal and exponential distributions with two different sample sizes each (i.e., four cases)

#####  The sample sizes we will take are 10 and 50

#####  In all cases, we will take the same number (5,000) of samples of means

##### All of these numbers are set at the top of the program and may be changed easily.

#
#


### Initialize the parameters


```r
pop      <- 500000  # population size that we will create and sample from
mu       <- 10      # mean of the distributions (populations)
sigma    <- 2       # standard deviation of the distributions (populations)
erate    <- 0.1     # exponential distribution rate
sample1  <- 10      # first sample size
sample2  <- 50      # second sample size
numsamp  <- 5000    # number of samples

normpop  <- numeric(pop)        # normal distribution population we will sample from
exppop   <- numeric(pop)        # exponential distribution population we will sample from

meanns1  <- numeric(numsamp)    # means for the normal distribution of sample1 samples
meanns2  <- numeric(numsamp)    # means for the normal distribution of sample2 samples
meanes1  <- numeric(numsamp)    # means for the exponential distribution of sample1 samples
meanes2  <- numeric(numsamp)    # means for the exponential distribution of sample2 samples
```
### Define the vectors of samples


#### xns1     - vector of sample1 samples from the normal distribution
#### xns2     - vector of sample2 samples from the normal distribution
#### xes1     - vector of sample1 samples from the exponential distribution
#### xes2     - vector of sample2 samples from the exponential distribution

#
### Define the properties of the sets of numsamp samples
#

#### yns1     - mean of the numsamp means from the normal distribution of sample1 samples
#### yns2     - mean of the numsamp means from the normal distribution of sample2 samples
#### yes1     - mean of the numsamp means from the exponential distribution of sample1 samples
#### yes2     - mean of the numsamp means from the exponential distribution of sample2 samples

#### sns1     - standard dev. of the numsamp means from the normal distribution of sample1 samples
#### sns2     - standard dev. of the numsamp means from the normal distribution of sample2 samples
#### ses1     - standard dev. of the numsamp means from the exponential distribution of sample1 samples
#### ses2     - standard dev. of the numsamp means from the exponential distribution of sample2 samples

#

#### Create the normal distribution population
#### Create the exponential distribution population



```r
normpop <- rnorm(pop, mu, sigma)
exppop  <- rexp(pop, erate)
```

### Loop over the number of samples from the populations
####     ----Determine the vector for each sample
####     ----Determine the mean for each vector


```r
for (i in 1:numsamp) {
  xns1 <- sample(normpop, sample1, replace=TRUE)
  xns2 <- sample(normpop, sample2, replace=TRUE)
  xes1 <- sample(exppop,  sample1, replace=TRUE)
  xes2 <- sample(exppop,  sample2, replace=TRUE)
  
  meanns1[i] <- mean(xns1)
  meanns2[i] <- mean(xns2)
  meanes1[i] <- mean(xes1)
  meanes2[i] <- mean(xes2)
}
```

### Determine the properties (means and standard deviations) of the numsamp means


```r
yns1 <- mean(meanns1)
yns2 <- mean(meanns2)
yes1 <- mean(meanes1)
yes2 <- mean(meanes2)

sns1 <- sd(meanns1)
sns2 <- sd(meanns2)
ses1 <- sd(meanes1)
ses2 <- sd(meanes2)
```

### Print the means compared to what we expected


```r
message ("These two normal distribution means should be ", mu)
```

```
## These two normal distribution means should be 10
```

```r
message ("The normal distribution means for the two sample sizes are ", round(yns1,4), " and ", round(yns2,4))
```

```
## The normal distribution means for the two sample sizes are 10.0051 and 10.0021
```

```r
message ("These two exponential distribution means should be ", round(1/erate,4))
```

```
## These two exponential distribution means should be 10
```

```r
message ("The exponential distribution means for the two sample sizes are ", round(yes1,4), " and ", round(yes2,4))
```

```
## The exponential distribution means for the two sample sizes are 9.989 and 10.0039
```

### Print the standard deviations compared to what we expected


```r
message ("These two normal distribution standard deviations should be ", round(sigma/sqrt(sample1),4), " and ", round(sigma/sqrt(sample2),4))
```

```
## These two normal distribution standard deviations should be 0.6325 and 0.2828
```

```r
message ("The normal distribution standard deviations for the two sample sizes are ", round(sns1,4), " and ", round(sns2,4))
```

```
## The normal distribution standard deviations for the two sample sizes are 0.6256 and 0.2824
```

```r
message ("These two exponential distribution standard deviations should be ", round(1/(erate*sqrt(sample1)),4), " and ", round(1/(erate*sqrt(sample2)),4))
```

```
## These two exponential distribution standard deviations should be 3.1623 and 1.4142
```

```r
message ("The exponential distribution standard deviations for the two sample sizes are ", round(ses1,4), " and ", round(ses2,4))
```

```
## The exponential distribution standard deviations for the two sample sizes are 3.1878 and 1.425
```


##
## With the means matching the population mean, we validated the first part of the Central Limit Theorem.
##
## With the standard deviations matching the prediction, we validated the second part of the Central Limit Theorem.
#







