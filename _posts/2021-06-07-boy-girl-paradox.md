---
layout: post
title: Probability that all the children are girls given a condition
description: Calculating the probability that all the children are girls given a condition
tags: maths probability
last_modified: 2021-06-07 23:55:00 +0530
---

## Question
A family has $$n$$ children, $$n \geq 2$$. What is the probability that all of their children are girls for the following cases:

a) We ask the father: "Do you have at least one daughter?" He responds "Yes!"

b) We pick one of them at random and find out that she is a girl

c) We ask the father, "Do you have at least one daughter named Lilia?" He replies, "Yes!"

>    Here you can assume that if a child is a girl, her name will be Lilia with probability $$\alpha \ll 1$$ independently from other children's names. If the child is a boy, his name will not be Lilia.


## Answer

Let us chart down what we know:

$$E_1 \Rightarrow \text{Event that atleast one of the children is daughter}$$
$$E_2 \Rightarrow \text{Event that the random child we picked was a girl}$$
$$E_3 \Rightarrow \text{Event that atleast one of the children is a daughter named Lilia}$$
$$G_n \Rightarrow \text{Event that all the } n \text{ children are girls}$$

To find,

$$P(G_n|E_1) \Rightarrow \text{Probability that all the children are girls given } E_1$$

$$P(G_n|E_2) \Rightarrow \text{Probability that all the children are girls given } E_2$$

Let,

$$G_i \Rightarrow \text{Event that all the } i \text{ children are girls}$$

### Part A
Let us calculate 
$$P(G_n|E_1)$$:

$$P(G_n|E_1) = \frac{P(G_n \cap E_1)}{P(E_1)}$$

$$P(E_1) = P(E_1 \cap G_0) + P(E_1 \cap G_1) + P(E_1 \cap G_2) + .... + P(E_1 \cap G_n)$$

$$P(E_1 \cap G_i) = P(E_1|G_i)P(G_i)$$

$$P(E_1 \cap G_0) = P(E_1|G_0)P(G_0) = 0$$

Then,

$$P(E_1 \cap G_1) = P(E_1|G_1)P(G_1)$$

As we know that atleast one of the children is a girl:

$$P(E_1|G_1) = 1$$


Probability of having a single girl child considering all the combinations possible:

$$P(G_1) = \frac{1}{2^n}*{}^n \mathrm{ C }_1$$

So,

$$P(E_1 \cap G_1) = \frac{1}{2^n}*{}^n \mathrm{ C }_1$$

The above can be generalized as following:

$$P(E_1 \cap G_i) = \frac{1}{2^n}*{}^n \mathrm{ C }_i$$

So,

$$P(E_1) = \frac{1}{2^n}*\sum_{i=1}^n {}^n \mathrm{ C }_i$$

Using binomial expansion for $$(1 + x)^n$$ we find that the summation is equal to $$2^{n} - 1$$

$$P(E_1) = \frac{2^n - 1}{2^n}$$

$$P(G_n|E_1) = \frac{P(G_n \cap E_1)}{P(E_1)}$$

$$
\begin{aligned}
P(G_n|E_1) &= \frac{\frac{1}{2^n}*{}^n \mathrm{ C }_n}{\frac{2^n - 1}{2^n}}
\end{aligned}
$$

$$\boxed{P(G_n|E_1) = \frac{1}{2^n - 1}}$$

### Part B

Let us calculate 
$$P(G_n|E_2)$$:

$$P(G_n|E_2) = \frac{P(G_n \cap E_2)}{P(E_2)}$$

$$P(E_2) = P(E_2 \cap G_0) + P(E_2 \cap G_1) + P(E_2 \cap G_2) + .... + P(E_2 \cap G_n)$$

$$P(E_2 \cap G_i) = P(E_2|G_i)P(G_i)$$

$$P(E_2 \cap G_0) = P(E_2|G_0)P(G_0) = 0$$

Then,

$$P(E_2 \cap G_1) = P(E_2|G_1)P(G_1)$$

As we pick the child randomly and turns out to be a girl:

$$P(E_2|G_1) = \frac{1}{n}$$


Probability of having a single girl child considering all the combinations possible:

$$P(G_1) = \frac{1}{2^n}*{}^n \mathrm{ C }_1$$

So,

$$P(E_2 \cap G_1) = \frac{1}{2^n}*\frac{1}{n}*{}^n \mathrm{ C }_1$$


The above can be generalized as following:

$$P(E_2 \cap G_i) = \frac{1}{2^n}*\frac{i}{n}*{}^n \mathrm{ C }_i$$

So,

$$P(E_2) = \frac{1}{2^n}*\frac{1}{n}*\sum_{i=1}^n i*{}^n \mathrm{ C }_i$$

Using binomial expansion for $$(1 + x)^n$$ we find that the summation is equal to $$n*2^{n-1}$$

$$P(E_2) = \frac{1}{2}$$

$$P(G_n|E_2) = \frac{P(G_n \cap E_2)}{P(E_2)}$$

$$
\begin{aligned}
P(G_n|E_2) &= \frac{\frac{1}{2^n}*\frac{n}{n}*{}^n \mathrm{ C }_n}{\frac{1}{2}}
\end{aligned}
$$

$$\boxed{P(G_n|E_2) = \frac{1}{2^{n-1}}}$$

### Part C

Let us calculate 
$$P(G_n|E_3)$$:

$$P(G_n|E_3) = \frac{P(G_n \cap E_3)}{P(E_3)}$$

$$P(E_3) = P(E_3 \cap G_0) + P(E_3 \cap G_1) + P(E_3 \cap G_2) + .... + P(E_3 \cap G_n)$$

$$P(E_3 \cap G_i) = P(E_3|G_i)P(G_i)$$

$$P(E_3 \cap G_0) = P(E_3|G_0)P(G_0) = 0$$

Then,

$$P(E_3 \cap G_1) = P(E_3|G_1)P(G_1)$$

To calculate 
$$P(E_3|G_1)$$ 
we know that the probability that atleast one girl is named $$Lilia$$ is same is the complement of the probability that no girl is named $$Lilia$$.

$$P(E_3|G_1) = 1 - P({E_3}^c|G_1)$$

$$P({E_3}^c|G_1) = (1 - \alpha)^1$$

$$P(E_3|G_1) = 1 - (1 - \alpha)^1$$


Probability of having a single girl child considering all the combinations possible:

$$P(G_1) = \frac{1}{2^n}*{}^n \mathrm{ C }_1$$

So,

$$P(E_3 \cap G_1) = \big[1 - (1 - \alpha)\big]*\frac{1}{2^n}*{}^n \mathrm{ C }_1$$


The above can be generalized as following:

$$P(E_3 \cap G_i) = \big[1 - (1 - \alpha)^i\big]*\frac{1}{2^n}*{}^n \mathrm{ C }_i$$

So,

$$P(E_3) = \frac{1}{2^n}*\sum_{i=1}^n \big[1 - (1 - \alpha)^i\big]*{}^n \mathrm{ C }_i$$

$$P(E_3) = \frac{1}{2^n}* \Big[ \sum_{i=1}^n  {}^n \mathrm{ C }_i -  \sum_{i=1}^n (1 - \alpha)^i*{}^n \mathrm{ C }_i \Big]$$

Using binomial expansion for $$(1 + x)^n$$ we find that:

$$\sum_{i=1}^n  {}^n \mathrm{ C }_i = 2^n - 1$$

$$\sum_{i=1}^n (1 - \alpha)^i*{}^n \mathrm{ C }_i = (2 - \alpha)^n - 1$$

$$P(E_3) = \frac{1}{2^n}*\big[ 2^n - 1 - ((2 - \alpha)^n - 1) \big]$$

$$P(E_3) = \frac{1}{2^n}*\big[ 2^n - (2 - \alpha)^n \big]$$


$$P(G_n|E_3) = \frac{P(G_n \cap E_3)}{P(E_3)}$$

$$P(G_n \cap E_3) = \big[1 - (1 - \alpha)^n\big]*\frac{1}{2^n}*{}^n \mathrm{ C }_n$$

$$
\begin{aligned}
P(G_n|E_3) &= \frac{\big[1 - (1 - \alpha)^n\big]*\frac{1}{2^n}*{}^n \mathrm{ C }_n}{\frac{1}{2^n}*\big[ 2^n - (2 - \alpha)^n \big]}
\end{aligned}
$$

$$\boxed{P(G_n|E_3) = \frac{1 - (1 - \alpha)^n}{2^n - (2 - \alpha)^n}}$$


### References
1. [Probability course chapter 1 problems](https://www.probabilitycourse.com/chapter1/1_5_0_chapter1_problems.php) (_Problem 37 & 39 & 38_)
1. [Finding the sum: $$\sum_{i=1}^n i*{}^n \mathrm{ C }_i$$](https://qr.ae/pGYUNo)
