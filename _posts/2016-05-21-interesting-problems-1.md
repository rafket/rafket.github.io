---
layout: post
title: "Interesting Problems and Puzzles 1: Emptying the box"
description: "Three boxes with at least one marble in each are given. In a step we choose two of the boxes, doubling the number of marbles in one of the boxes by taking the required number of marbles from the other box. Is it always possible to empty one of the boxes after a finite number of steps?"
---

Three boxes with at least one marble in each are given. In a step we choose two of the boxes, doubling the number of marbles in one of the boxes by taking the required number of marbles from the other box. Is it always possible to empty one of the boxes after a finite number of steps?

*This problem, as well as the solution, was taken from Andreescu and Andrica's "Number Theory: Structures, Examples, and Problems" where it is indexed as problem 1.7.11. Its original source is the 1999 Slovenian Mathematical Olympiad.*


## Initial thoughts


Instinctively, the answer seems to be negative. The most basic way to prove this is to find a counterexample. This prompts us to try some cases:


|Initial state         |3    |5    |7    |
|:--------------------:|:---:|:---:|:---:|
|Pour second into first|6    |2    |7    |
|Pour first into second|4    |4    |7    |
|Pour first into second|0    |8    |7    |

|Initial state         |11   |21   |23   |
|:--------------------:|:---:|:---:|:---:|
|Pour second into first|22   |10   |23   |
|Pour third into second|22   |20   |13   |
|Pour first into second|2    |40   |13   |
|Pour second into first|4    |38   |13   |
|Pour third into first |8    |38   |9    |
|Pour third into first |16   |38   |1    |
|Pour second into third|16   |37   |2    |
|Pour second into third|16   |35   |4    |
|Pour second into third|16   |31   |8    |
|Pour second into third|16   |23   |16   |
|Pour first into third |0    |23   |32   | 


You could go on and try a few more cases, but we should be suspicious that it is always possible to empty one of the boxes in a finite number of steps. To prove this, we will propose an algorithm that solves this problem, and prove that it has a finite number of steps. Each step will consist of several (again, finite) operations in which we will select two boxes and pour marbles from the one that has the most marbles to the other, until the latter's marbles have doubled in number.


To ensure that this algorithm will have a finite number of steps, even if we do not know their exact number, we will make sure that, after each step, the number of marbles in the box that contains the least marbles is strictly decreasing. Let's move onto the algorithm itself.


## Solution

Denote $$a, b, c$$ the number of marbles in each box initially. Without loss of generality, assume that $$a \leq b \leq c$$. $$b$$ can be written as $$b=q*a+r$$, where $$q, r$$ are natural numbers, with $$r<a$$. We plan on constructing a series of operations which will decrease the marbles in the second box by $$q*a$$.

Obviously, if $$q=1$$, all we need to do is apply the operation on $$a$$ and $$b$$, which will decrease the marbles in the second box by $$a$$, and double the marbles in the first one. If $$q=2$$, we first need to double $$a$$, while leaving $$b$$ unchanged. This can be done by pouring the marbles in the third box into the first one. Then, we can pour $$2*a$$ marbles from the second box into the first (by applying the operation on the first two boxes), effectively decreasing $$b$$ by $$2*a$$. Let's try to generalize this procedure.

We know that every natural number can be written as a sum of powers of two (since they can be written in [base 2](https://en.wikipedia.org/wiki/Binary_number)). Write $$q$$ as a sum of powers of 2 as $$q=2^{k_1} + 2^{k_2} + 2^{k_3} + 2^{k_4} + \ldots$$ ($$k_1 < k_2 < k_3 < \ldots$$). Then we have that $$b=2^{k_1}*a + 2^{k_2}*a + 2^{k_3}*a + 2^{k_4}*a + \ldots + r$$. By pouring the third box into the first $$k_1$$ times, we will have doubled the marbles in the first box $$k_1$$ times, increasing them to $$2^{k_1}*a$$. Then, we pour the second box into the first one, subtracting $$2^{k_1}*a$$ marbles from the second box, and increasing the marbles in the first box to $$2^{k_1+1}*a$$. Since $$k_1<k_2$$, we have that $$k_1+1 \leq k_2$$. Therefore, by pouring the third box into the first one $$k_2-k_1-1$$ times, we increase the marbles in the first box to $$2^{k_2}*a$$.

We continue this process until the marbles left on the second box are $$r$$. Since $$r < a$$, we have effectively decreased the number of marbles in the box with the least marbles. If we do this process in each step, there can only be a finite number of steps until the number of marbles in the box with the least marbles reaches zero. Each step will have a finite number of operations (equal to $$\lceil log_2(q) \rceil$$).


And that's it! The solution provided by Andreescu and Andrica is written in an even shorter way. While small, this solution by no means simple, since the problem does not lead us into this direction.
