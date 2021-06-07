---
layout: post
title: Will it be HEADS ?
description: Calculating the probability of (n+1)th toss of one of the given coins
tags: maths probability
last_modified: 2021-06-02 23:55:00 +0530
---

## Question
A box contains two coins: a regular coin and one fake two-headed coin ($$P(H)=1$$). I choose a coin at random and toss it $$n$$ times. If the first $$n$$ coin tosses result in `heads`, what is the probability that the $$(n+1)^{th}$$ coin toss will also result in `heads`?


## Answer

Let us chart down what we know:

$$A \Rightarrow \text{Event that first 'n' tosses are heads}$$

$$C_1 \Rightarrow \text{Event that regular coin is chosen}$$

$$\text{Probability of heads given regular coin, } P(H|C_1) = \frac{1}{2}$$

$$C_2 \Rightarrow \text{Event that two-headed coin is chosen}$$

$$\text{Probability of heads given two-headed coin, } P(H|C_2) = 1$$

To find,

$$B \Rightarrow \text{Event that } (n + 1)^{th} \text{ toss is heads}$$

Now, let's calculate the probability of event $$A$$ happening for each of the coins:

$$P(A|C_1) = \frac{1}{2}*\frac{1}{2}*\frac{1}{2}*\text{...n times} = \frac{1}{2^n}$$

$$P(A|C_2) = 1*1*1*\text{...n times} = 1$$

$$P(A) = P(A \cap C_1) + P(A \cap C_2)$$
$$P(A) = P(A|C_1)P(C_1) + P(A|C_2)P(C_2)$$
$$P(A) = \Big[\frac{1}{2^n}*\frac{1}{2}\Big] + \Big[1*\frac{1}{2} \Big] = \frac{1}{2}*\Big[\frac{1}{2^n} + 1\Big]$$

Now, before we calculate $$P(B)$$, we first need to know the probability of the coin based on $$n$$ observations of heads. Also, one needs to note that $$(n+1)^{th}$$ toss is independent of other tosses, so we have:

$$P(B) = P(C_1|A)P(H|C_1) + P(C_2|A)P(H|C_2)$$

where, 

$$P(C_1|A) \rightarrow \text{Probability that regular coin is chosen given the event A}$$

$$P(C_2|A) \rightarrow \text{Probability that two-headed coin is chosen given the event A}$$

Now, let's calculate,
$$P(C_1|A) \text{ & } P(C_2|A)$$


$$P(C_1|A) = \frac{P(A \cap C_1)}{P(A)}$$

$$P(C_1|A) = \frac{\frac{1}{2^n}*\frac{1}{2}}{\frac{1}{2}*\Big[\frac{1}{2^n} + 1\Big]} = \frac{1}{2^n + 1}$$

$$P(C_2|A) = \frac{P(A \cap C_2)}{P(A)}$$

$$P(C_2|A) = \frac{\Big[1*\frac{1}{2} \Big]}{\frac{1}{2}*\Big[\frac{1}{2^n} + 1\Big]} = \frac{2^n}{2^n + 1}$$

_$$P(C_2|A)$$
 shows us that, higher the $$n$$, closer will be probability that two-headed coin is chosen to $$1$$._

Now plugging the above values will give,

$$P(B) = \frac{1}{2^n + 1}*\frac{1}{2} + \frac{2^n}{2^n + 1}*1$$

$$\boxed{P(B) = \frac{2^{n+1} + 1}{2^{n+1} + 2}}$$

So, the probability $$P(B)$$ tends to $$1$$ as $$n$$ tends to $$\infty$$.


### References
1. [Probability course chapter 1 problems](https://www.probabilitycourse.com/chapter1/1_5_0_chapter1_problems.php) (_Problem 36_)
