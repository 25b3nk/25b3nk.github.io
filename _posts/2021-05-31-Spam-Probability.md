---
layout: post
title: Is this email a SPAM ?
description: Calculating the probability that an email is spam when it contains this particular word
tags: maths probability
last_modified: 2021-05-31 23:55:00 +0530
---

## Question
One way to design a `spam` filter is to look at the words in an email. In particular, some words are more frequent in spam emails. Suppose that we have the following information:

- $$50\%$$ of emails are spam
- $$1\%$$ of spam emails contain the word "refinance"
- $$0.001\%$$ of non-spam emails contain the word "refinance"

Suppose that an email is checked and found to contain the word "refinance". What is the probability that the email is spam?


## Answer

Let's chart down the data we know from the question:

$$S \Rightarrow \text{Event that the email is spam}$$

$$P(S) = 0.5 \implies P(S^c) = 0.5$$

$$P(R) \Rightarrow \text{Probability that email contains the word "refinance"}$$

Given,

$$P(R \cap S) = \frac{1}{100}$$

$$P(R \cap S^c) = \frac{0.001}{100}$$

So,

$$P(R) = P(R \cap S) + P(R \cap S^c) = \frac{1.001}{100}$$

To find,
$$P(S|R) \Rightarrow \text{Probability that email is spam given that it contains the word "refinance"}$$

$$P(S|R) = \frac{P(S \cap R)}{P(R)} = \frac{\frac{1}{100}}{\frac{1.001}{100}} = \frac{1}{1.001}$$

$$\therefore P(S|R) = 0.999000999$$

One important observation, we see that "refinance" word occurs only $$1\%$$ of the time in `spam` emails, but since this occurrence ($$P(R \cap S)$$) forms larger chunk of the total occurrence ($$P(R)$$), we see the probability of the email being `spam` is $$0.999$$ if it contains the word "refinance".

But this is not what we would have thought firstly, based on our intuition. Solving such problems will extend our common sense by `mathematical` means, this extends to lots of things happening around us. **_How Not To Be Wrong_** by __Jordan Ellenberg__ is a book encouraging such thinking.


### References
1. [Probability course chapter 1 problems](https://www.probabilitycourse.com/chapter1/1_5_0_chapter1_problems.php) (_Problem 31_)
1. [How Not To Be Wrong](https://www.goodreads.com/book/show/18693884-how-not-to-be-wrong)
