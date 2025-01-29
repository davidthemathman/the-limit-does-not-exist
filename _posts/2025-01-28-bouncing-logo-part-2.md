---
layout: post
title: Bouncing DVD Logo Part 2
subtitle: Answering more questions using group theory
gh-repo: davidthemathman/the-limit-does-not-exist
tags: [Group Theory, The Office, Billiards Problem]
comments: true
mathjax: true
author: David Kyle
---

In my last post, I showed that you can determine if the logo will hit a corner with the starting position and slope of the path. If it does hit a corner and the slope is rational, it will alternate
between hitting exactly two corners and any two corners are possible candidates. Reviewing the motivating questions, I've answered the first one, and will move one to questions 2 and 3. 

### How many bounces are between each corner hit?

The number of bounces between each corner is a result from Martin Gardner's *Sixth Book of Mathematical Games* where he shows that on a billiards table with integer length sides $$m$$ and $$k$$, 
a 45° hit from a corner will hit another corner after exactly $$\gcd(m, k) - 2$$ bounces. Although he is only considering a 45° hit, it's possible to rescale 
the pool table to consider any rational slope hit. I could use this result to prove the number of bounces between corner hits in the DVD logo example, but I'll rederive it using
the group theory approach I have already established for this problem. 

Assuming that the logo hits a corner, we can reorient the screen to put this corner in the bottom left so that the origin is in the screensaver path. 

![]({{'/assets/img/reorient_screen.png' | relative_url}}){: .mx-auto.d-block :}

*Example: Suppose you calculate that the trajectory of the DVD logo will hit the top left and bottom right corner. You can rotate the picture so that one of the corners
is in the bottom left.*


The logo lauching at an outward diagonal with slope $$n/d$$ in reduced form will first hit the right side of the screen at the point $$(1, n/d \text{ mod } 2)$$. 

![]({{'/assets/img/first_bounce.png' | relative_url}}){: .mx-auto.d-block :}

Continuing this trajectory forms
the subgroup $$\langle(1, n/d \text{ mod } 2)\rangle$$ with order $$2d$$. 

Proof. Since $$n$$ and $$d$$ are relatively prime $$k (n /d \text{ mod } 2) = k n/d \text{ mod } 2$$ is only 
an integer when $$k$$ is a multiple of $$d$$. If $$d$$ is odd, then 

$$d (1, n/d \text{ mod }2) = ( d \text{ mod } 2, n \text{ mod } 2) = (1, n \text{ mod } 2) \ne (0, 0), $$ 

and if $$d$$ is even, then $$n$$ is odd and

$$d (1, n/d \text{ mod }2) = (d \text{ mod } 2, n \text{ mod } 2) = (0, 1) \ne (0, 0). $$ 

However, in either case, 

$$2d (1, n \text{ mod } 2) = (0, 0).$$ 

So, $$\lvert(1, n/d \text{ mod } 2)\rvert = 2d.$$ 

The trajectory of the points where the logo hits the top or bottom of the screen is given by subgroup $$\langle(d/n \text{ mod } 2, 1) \rangle$$ with order $$2n$$ by a similar proof.

The previous proof also shows that $$k = d$$ is the smallest positive integer such that $$k (1, n/d \text{ mod } 2)$$ is the other, non-origin, corner. Therefore there are $$d - 1$$
left/right wall bounches between corners. Similarly, there are $$n - 1$$ top/bottom wall bounces making a total of $$n + d - 2$$ bounces which matches the result from Gardner since $$n$$ and $$d$$ 
are relatively prime.


### Calculating the slope

So far, I've assumed that the starting position and slope are known. However, estimating the slope visually in real life would be prone to enormous error since the number of bounces between corners
depends on precise integer values of the slope. For example, a slope of $$1/2$$ would only have 1 bounce between corners, but a very similar slope of $$101/200$$ would have 299 bounces between corners.

A more achievable calculation would be to do the reverse.
That is, count how many top/bottom wall bounces are between corner hits and how many left/right wall bounces and use that to calculate the slope.

$$\text{ slope} = \frac{\text{top bottom wall hits} + 1}{\text{left right wall hits} + 1}$$

![]({{'/assets/img/subgroup_lattice.png' | relative_url}}){: .mx-auto.d-block :}

### Which corner is next and how many bounces?

In part 1, I showed that, given the location of the logo at a moment in time and the slope, one can figure out which two corners the logo 
will alternate between.

Without loss of generality, I can assume that one of the two corners is the origin by reorinting the board. Assuming that 
the slope is not exactly vertical or horizontal, I can also place the starting location
in the quadrant of my choice so that the logo is moving up and to the right.

![]({{'/assets/img/correct_quadrant.png' | relative_url}}){: .mx-auto.d-block :}

The question is given the starting location of $$(x_0, y_0)$$, will it hit the origin or the other
corner first? and how many bounces until it hits that corner?

One can backtrack the location of the last left-right wall bounce fairly easily by using the trajectory slope. Specifically, I'm looking for the last
time that the $$x$$-coordinate was an integer. These new coordinates $$(x_1, y_1)$$ are given by

$$x_1 = \lfloor x_0 \rfloor$$

$$y_1 = \left(y_0 - (x_0 - \lfloor x_0\rfloor ) \frac nd \right) \text{ mod } 2 $$

Since there are no left-right wall bounces or corners between $$(x_1, y_1)$$ and $$(x_0, y_0)$$, it's sufficient to find the number of left-right wall bounces between 
$$(x_1, y_1)$$ and the next corner. 

This new point $$(x_1, y_1)$$ will be somewhere in the subgroup generated by $$\langle(1, n/d \text{ mod }2) \rangle$$ as discussed earlier. So, by iterating on the
generator $$(1, n/d \text{ mod }2)$$, we can solve for $$0 \le k_1 < 2d$$ such that 

$$k_1\left(1, \frac nd \text{ mod }2 \right) = (x_1, y_1).$$

If $$k < d$$, then $$(x_1, x_2)$$ is still in the first half of it's $$2d$$ cycle and will hit the non-origin corner after $$d - k_1 - 1$$ left/right wall bounces. 
If $$k \ge d$$, then it will hit the origin next after $$2d - k_1 - 1$$ bounces. In both cases, the number of left-right wall bounces until the next corner is $$(-k_1 - 1) \text{ mod } d$$.

A similar analysis shows that finding the last top-bottom wall bounce is given by

$$x_2 = \left(x_0 - (y_0 - \lfloor y_0\rfloor ) \frac dn \right) \text{ mod } 2 $$

$$y_2 = \lfloor y_0\rfloor$$

and when you solve for $$0 \le k_2 < 2n$$ in 

$$k_2 \left( \frac dn \text{ mod } 2, 1 \right) = (x_2, y_2),$$

one finds that there are $$(-k_2 - 1) \text{ mod } n$$ top bottom wall bounces until the next corner for a total of 

$$(-k_1 - 1) \text{ mod } d + (-k_2 - 1) \text{ mod } n$$

wall bounces until the next corner. 

The answer to this last question is a little less satisfying than the others since it involves iterating over the subgroup generators. I would be
delighted to find a closed form solution to this problem. 


### Remaining Problems

Here are a few unanswered questions I still have on this topic. Some of these problems may already be solved. 
Unfortunately, I have not taken the time to do a deep dive into the literature on billiards problems. 

1. Is there a closed form solution for how many bounces it takes to get to the next corner?
2. Show that when the slope is irrational, no point is visited twice, and that the path can only hit at most one corner. 
3. Given a starting position and irrational slope, is it possible to determine which corner will be hit and how many bounces it will take to get there?

