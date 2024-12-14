---
tags:
- math
- calculus
---

## **Fundamental Theorem of Calculus

The **Fundamental Theorem of Calculus** is a central theorem in calculus that links the concept of differentiation with integration, establishing that they are inverse processes. It is divided into two main parts:

### Part 1: The Relationship Between Integration and Antiderivatives

The first part states that if fff is a continuous real-valued function on a closed interval [a,b][a, b][a,b], and FFF is an antiderivative of fff on that interval, then:

$$∫abf(x) dx=F(b)−F(a)\int_a^b f(x) \, dx = F(b) - F(a)∫ab​f(x)dx=F(b)−F(a)$$

This means that the definite integral of fff from aaa to bbb can be calculated by evaluating an antiderivative of fff at the endpoints and finding the difference. Essentially, this part shows that the integral can be computed using an antiderivative, which is an easier calculation than summing infinitely many tiny areas directly.

### Part 2: Differentiation of the Integral

The second part states that if fff is a continuous function on an interval [a,b][a, b][a,b], then the function F(x)F(x)F(x), defined by the integral from aaa to xxx:

$$F(x)=∫axf(t) dtF(x) = \int_a^x f(t) \, dtF(x)=∫ax​f(t)dt$$

is differentiable, and its derivative is the original function fff. In other words:

$$ddx(∫axf(t) dt)=f(x)\frac{d}{dx} \left( \int_a^x f(t) \, dt \right) = f(x)dxd​(∫ax​f(t)dt)=f(x)$$

This part shows that integrating a function and then differentiating it returns the original function, emphasizing the inverse nature of differentiation and integration.

### Summary

Together, the two parts of the Fundamental Theorem of Calculus show that:

1. The definite integral of a function over an interval can be calculated using antiderivatives.
2. The derivative of an integral of a function gives back the original function.

This theorem is foundational because it enables practical computation of areas under curves and relates two major branches of calculus.

[[Math]]   [[Calculus]]