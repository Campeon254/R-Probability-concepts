# Probability-concept
# RMarkdown
```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## Load the necessary packages

```{r}
library(ggplot2)
library(dplyr)
```

A recent national study showed that approximately 44.7% of college students have used Wikipedia as a source in at least one of their term papers. Let X equal the number of students in a random sample of size n = 31 who have used Wikipedia as a source.

## Question 1

**How is X distributed?**

```         
X is a binomial distribution.
A binomial distribution is a disrete probability distribution that models the number of outcomes in a sequence of fixed independent experiments (the sample size of 31) where each experiment has only two possible outcomes: success and failure.
In this case, there are only two possible outcomes: success - the students using Wikipedia and failure - the students who fail to use Wikipedea as a source of information for their term papers.
next statement
```

## Question 2

**Generate and plot the probability mass function.**

```{r}
# parameters
n <- 31 #sample size 
p <- 0.447 # probability of success in decimal form

# generate sequence from 0 to 31
x <- 0:31
# calculate PMF values for x
pmf <- dbinom(x, n, p)

# Plot PMF
plot(x, pmf, type = 'l', xlab = 'Number of Students Using Wikipedia', ylab = 'Probability', main = 'PMF of Wikipedia Usage by College Students', col = 'blue', lwd = 2)



```

### Interpretation

*The plot shows the probabilities for each possible value of x, i.e the number of students using Wikipedia. The most frequent value corresponds with the peak of the PMF curve.*

## Question 3

**Generate and plot the cumulative distribution function**

```{r}
# Parameters
n <- 31  # Sample size
p <- 0.447  # Probability of success

# Generate sequence from 0 to 31
x <- 0:31
# Calculate the CDF values
cdf_values <- pbinom(x, n, p)

# Plot the CDF
plot(x, cdf_values, type = 'l', xlab = 'Number of Students Using Wikipedia',
     ylab = 'Cumulative Probability', main = 'CDF Wikipedia Usage by College Students',
     col = 'red', lwd = 2)

```

### Interpretation

*The cumulative density function(CDF) for the value x(the number of students who use Wikipedia) will take a value less than or equal to (x). The CDF plot shows an increase in the cumulative probability from left to right. The CDF curve helps us understand the likelihood of observing a certain number of students using Wikipedia.*

## Question 4

Find the probability that X is:

a\. **Equal to 17.**

```{r}
# p(x) = 17
n <- 31
p <- 0.447

# Calculate PMF for X = 17
pmf_17 <- dbinom(17, size = n, prob = p)
print(paste('pmf(x=17) = ', pmf_17))

```

*The PMF value for f(x) is given by nCx.p^x.(1-p)^(n-x) where: nCx = number of combination without repetition p = probability of a student using Wikipedia x = number of success(x = 17) n = sample space(31) Therefore, the probability that x = 17 is, (p(x) = 17) = 0.0753224*

b.  **At most 13.**

```{r}
# calculate the probability that x is at most 13
p_at_most_13 <- pbinom(13, size = n, prob = p)
print(paste('p(x<=13) = ', p_at_most_13))

# Generate 100,000 random variables each number representing the number of students who use Wikipedia(x)
set.seed(32)
# set seed to 32
# (x) <= 13
p_ran_sample <- mean(rbinom(100000, n, p)<= 13)
print(paste('random_sample, p(x<=13) = ', p_ran_sample))


```

*In the first part, the CDF value of x being at most 13 is approximately 0.45135. In the second part, we are generating 100,000 random variables to confirm the first answer using rbinom() function. We then specify the criteria(x \<= 13) and finally calculate the mean of the random variables than meet the criteria. The final answer is 0.45321 which is fairly close to 0.45135 with a difference of .002 hence confirming the first probability.*

c.  **Greater than 11.**
d.  **At least 15.**

```{r}
# Calculate CDF for X > 11 (complement of CDF)
cdf_greater_than_11 <- 1 - pbinom(11, size = n, prob = p)
print(paste("P(X > 11) =", cdf_greater_than_11))

# Calculate CDF for X ≥ 15 (complement of CDF)
cdf_at_least_15 <- 1 - pbinom(14, size = n, prob = p)
print(paste("P(X ≥ 15) =", cdf_at_least_15))
```

*The CDF is defined as F_x(x) = p(X\<=x) The CDF for X \> 11 is P(X \> 11) = 0.80203387250424 while the CDF for X ≥ 15 is: "P(X ≥ 15) = 0.40602400318711"*

This can also be confirmed by generating another 100,000 random observations, and specifying the needed criteria

```{r}
# set seed to 33
set.seed(33)
x_greater_than_11 <- mean(rbinom(100000, 31, .447)> 11)
print(paste('P(x > 11) = ', x_greater_than_11))

x_greater_than_or_equal_to_15 <- mean(rbinom(100000, 31, .447)>= 15)
print(paste('P(x >= 15) = ', x_greater_than_or_equal_to_15))
```

e.  **Between 16 and 19, inclusive.**

```{r}
# Calculate CDF for 16 ≤ X ≤ 19
x_greater_than_16_less_than_19 <- pbinom(19, n, p) - pbinom(15, n, p)
print(paste("P(16 ≤ X ≤ 19) =", x_greater_than_16_less_than_19))
```

*The probability that x will fall between 16 and 19 (inclusive) is 0.2544758.*

## Question 5

**Give the mean of X, denoted E(X).**

```{r}
n <- 31
p <- 0.447

# calculating the mean
expected_value <- n * p
expected_value
```

*The mean of X is 13.857 The mean is calculated by finding the product between size and probability.*

## Question 6

**Give the variance and standard deviation of X.**

```{r}
# calculating the variance of x

variance <- n * p * (1 - p)
print(paste('The variance of x is ', variance))

# calculating the standard deviation of x
sd <- sqrt(variance)
print(paste("The standard deviation of x is", sd))
```

*The variance is calculated by multiplying the mean(size \* probability) by 1 minus the probability. Therefore, the variance of x is 7.662921 The standard deviation is simply calculated by finding the square root of the variance : therefore, standard deviation of x is 2.76819815042204"*
