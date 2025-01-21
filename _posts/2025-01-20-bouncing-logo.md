---
layout: post
title: The Bouncing DVD Logo
subtitle: How group theory explains when the screensaver hits a corner
gh-repo: davidthemathman/the-limit-does-not-exist
tags: [Group Theory, The Office, Billiards Problem]
comments: true
mathjax: true
author: David Kyle
---

In a cold open for the show The Office, the cast watches the bouncing DVD logo on a TV screen while their boss, uaware of the screensaver behind him, rambles on at a team meeting. 
The character, Pam, is convinced that she once saw the logo perfectly slot into the corner of the screen. After a few near misses, the logo finally hits the corner and the cast cheers in excitement. 

![office]({{'/assets/img/office_bouncing_logo.gif' | relative_url}}){: .mx-auto.d-block :}


This cast is not the first to be mesmerized by the DVD screensaver. The question about the path of a bouncing object in a rectangle first came up in the context of billiards. 
Knowing what angle to cue the ball to get it into a corner pocket. Mathematicians took this concept and ran with it creating a bunch of problems around idealized billiards tables 
with perfect elasticity and no friction so that the ball could bounce indefinitely. There is a wealth of literature on the subject, considering all kinds of pool tables, including 
triangles, regular polygons, circles, ellipses, or arbitrary smooth boundaries. 

Given the extensive research on this fun problem, I know I won't be adding anything new to the topic, but I am excited to think about it all the same. I was particularly interested 
if the movement of the bouncing screensaver in a rectangular screen could be represented as an algebraic group. 

## Motivating Questions

In particular, there are a few questions I want to answer. Given the starting position and slope of of the moving logo:

1. Will the logo every hit a corner exactly? Which corners?
2. How many bounces are between each corner hit?
3. Which corner will the logo hit next and how many bounces until it does?

![office](/assets/img/DVD_logo_bouncing.gif){: .mx-auto.d-block :}

### Horizontal Case

First, consider the case where DVD logo moves horizontally side-to-side. I'm going to try to represent the movement with modular arithmetic. To do so, let's assume that the logo is moving 
(it's not stationary), then the logo could be anywhere along the width of the screen, $$w$$. However, the logo also has two modes of movement, either moving to the left or moving to the right. 
So, rather than considering only the location of the point, I'll consider the distance of the point along the path out and back starting from the left edge. So, while a point at $$w/2$$ moving 
to the right is at the same position as a point at $$w/2$$ moving to the left, they are at different points along their journey. The first one being in the first half, having gone distance $$w/2$$ 
and the second one already in the second half of the trip being distance $$\frac {3w}2$$ from the starting point. The addition operator modulo $$2w$$ represents the location of the point with the 
sum of the two distances. 

<img src="/assets/img/back_and_forth.png" alt="drawing" width="300" style="display: block; margin: 0 auto"/>

The horizontal movement case is simple. If the logo starts along the top edge, it will alternate between the top two corners. If it's along the bottom edge, it will alternate between the bottom two corners. 
Otherwise, it never hits any corners. The vertical case is similar. 

### Diagonal Case

Now, let's think about when the movement is some diagonal (not vertical, horizontal, or stationary). First, I note that when moving on a diagonal, the horizontal and vertical components of the moving logo 
operate independently. Whenever, the logo hits a left or right wall, the horizontal component of it's trajectory flips, but the vertical component remains constant and vice versa for the top and bottom walls 
of the screen. When the logo hist a corner exactly, screensavers typically reverse their path in a 180 degree turn (which is the same as a horizontal and vertical flip). Since the physics of the path of the 
ball has independent components, I can represent it's position as the external direct product of two cyclic groups $$[0, 2w) \oplus [0, 2h)$$ where $$w, h$$ are the width and height of the screen and 
the operation is modular addition of real numbers. You can think of the $$x$$ component representing the horizontal out-and-back distance and the $$y$$ component as the vertical out-and-back distance. 
It may be helpful to think of the topology of this group as a torus.

![torus](/assets/img/modular_2d.png){: .mx-auto.d-block :}

The rectangular group $$[0, 2w) \oplus [0, 2h)$$ is isomorphic to the group $$[0, 2) \oplus [0, 2)$$ and for convenience, I'll be using this group. This is essentially normalizing the screen height 
and width to create a unit square screen. Also, I'll be referring to a points location $$(x, y) \in [0, 2) \oplus [0, 2)$$ in terms of the group, not the physical location on the screen. So, a point 
at $$(0.5, 0.5)$$ and one at $$(1.5, 1.5)$$ both are located in the middle of the screen, but are at different points in their cyclic paths and so are considered distinct points. I'll refer to $$[0, 2) 
\oplus [0, 2)$$ simply as $$[0, 2)^2$$ assuming it's clear that it's an external direct product under real modular addition.

Suppose the path of the logo goes through point $$(x_0, y_0)$$ with rational slope $$n/d$$ where $$n, d$$ are nonzero integers and $$|n|$$ and $$|d|$$ are relatively prime (i.e. the fraction is simplified).
 The equation of this line is

$$n(x - x_0) = d(y - y_0)$$

where the operation is real addition modulo 2. It's important that the coefficients $$n, d$$ in this equation are integers because in general scalar multiplication is not well-defined for 
modular addition. So, $$n$$ and $$d$$ are interpreted in the typical group theory context as a $$n$$ and $$d$$ summand with negatives representing inverses. 

<img src="/assets/img/line_in_torus.png" alt="drawing" width="300" style="display: block; margin: 0 auto"/>

Rearranging this formula, I get 

$$nx - dy = nx_0 - dy_0.$$

### The Homomorphism

The function $$\phi((x, y)) = nx - dy$$ is a homomorphism from $$[0, 2)^2$$ to $$[0, 2)$$. Proof: Let $$(x, y)$$ and $$(x', y')$$ be in $$[0, 2)^2$$. Then,

$$\phi((x, y) + (x', y'))$$

$$ = \phi(x + x', y + y')$$

$$ = n(x + x') - d(y + y')$$

$$ = nx - dy + nx' - dy'$$

$$ = \phi((x, y)) + \phi((x', y')).$$

The kernel, a normal subgroup of $$[0, 2)^2$$ represents the set of points in the path of the bouncing logo with slope $$n/d$$ in the situation when the starting position $$(x_0, y_0)$$ 
satisfies $$nx_0 - dy_0 = 0$$. 

$$\ker(\phi) = \{(x, y) : nx - dy = 0\} \triangleleft [0, 2)^2$$

For other starting positions where $$nx_0 - dy_0$$ is not necessarily zero, the set of points in the path of the bouncing logo is a coset of $$\ker(\phi)$$ given by the isomorphism 
$$\phi((x_0, y_0)) \rightarrow (x_0, y_0) + \ker(\phi)$$ from $$\phi([0, 2)^2)$$ to $$[0, 2)^2 / \ker(\phi)$$. Also, $$\phi([0, 2)^2) = [0, 2)$$. Proof: Let $$z \in [0, 2)$$. Since $$n \ne 0$$,

$$\phi((z/n, 0)) = n (z/n) + d(0) = z.$$

This means the bouncing paths can be uniquely characterized by the slope $$n/d$$ and a value $$c \in [0, 2)$$. Starting values with the same value under $$\phi$$ result in the same path. 
So, it's sufficient to know just the $$c = \phi((x_0, y_0))$$ value instead of the exact starting position $$(x_0, y_0)$$.

### Which Corners?

The four corners of the screen are represented by the integer values in $$[0, 2)^2$$. If $$c$$ is not an integer notice that $$nx - dy = c$$ will have no integer solutions because if $$x$$ 
and $$y$$ were integers, $$c$$ would be also. 

If $$c = 0$$, this corresponds to the case where the set of values in the path is a subgroup. It contains the identity $$n(0) - d(0) = 0$$, but it will also hit the corner 
$$(d \mod 2, n \mod 2)$$. Proof: 

$$n (d \mod 2) - d (n \mod 2) = nd \mod 2 - dn \mod 2 = 0.$$

$$(d \mod 2, n \mod 2) \ne (0, 0)$$ because at least one of $$n$$ and $$d$$ must be odd. Otherwise, they would not be relatively prime. 

The corner solutions correspond exactly to the kernel of the same mapping we used earlier except applied to the integer subgroup $$\mathbb{Z}_2^2 < [0, 2)^2$$.

$$\ker(\phi) = \{(0, 0), (d \mod 2, n \mod 2) \}$$

There is only one other coset to $$\ker(\phi)$$ corresponding to when $$c = 1$$ which will result in the other two corners. 

Amazingly, knowing if the logo will hit a corner is just a matter of checking if $$nx_0 - dy_0$$ is an integer. If it is an integer, it will hit a pair of corners. However, any two
 corners are possible and it just depends on the parity of $$n$$ and $$d$$ and whether $$nx_0 - dy_0$$ is 0 or 1. 

So far, I've answered the first question: knowing the conditions in which the logo will hit a corner and which corners it will hit. I will save the next two questions for a future post. 

