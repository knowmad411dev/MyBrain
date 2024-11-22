---
tags: [math, calculus]
---

## **Gradient Descent

Gradient descent is an optimization technique used to find the local minimum of a differentiable function. In calculus, it leverages the concept of gradients to iteratively adjust variables, moving them in the direction that decreases the function's value most rapidly.

**Key Concepts:**

- **Gradient:** The gradient of a function is a vector composed of its partial derivatives with respect to each variable. It points in the direction of the steepest ascent of the function. Mathematically, for a function $$f(x1,x2,…,xn)f(x_1, x_2, \ldots, x_n)f(x1​,x2​,…,xn​), the gradient ∇f\nabla f∇f is: ∇f=(∂f∂x1,∂f∂x2,…,∂f∂xn)\nabla f = \left( \frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, \ldots, \frac{\partial f}{\partial x_n} \right)∇f=(∂x1​∂f​,∂x2​∂f​,…,∂xn​∂f​)$$
- **Descent Direction:** To minimize the function, we move in the opposite direction of the gradient, as this is where the function decreases most rapidly.
- **Learning Rate:** This is a positive scalar that determines the size of the steps taken in the direction of the negative gradient. Choosing an appropriate learning rate is crucial; too large a rate can lead to overshooting the minimum, while too small a rate can result in slow convergence.

**Gradient Descent Algorithm:**

1. **Initialization:** Start with an initial guess for the variables, denoted as x0\mathbf{x}_0x0​.
2. **Iteration:** Update the variables iteratively using the formula:
3. $$xk+1=xk−η∇f(xk)\mathbf{x}_{k+1} = \mathbf{x}_k - \eta \nabla f(\mathbf{x}_k)xk+1​=xk​−η∇f(xk​)$$ Here, xk\mathbf{x}_kxk​ represents the variables at the kkk-th iteration, η\etaη is the learning rate, and ∇f(xk)\nabla f(\mathbf{x}_k)∇f(xk​) is the gradient evaluated at xk\mathbf{x}_kxk​.
3. **Convergence Check:** Repeat the iteration until the change in the function's value or the variables is smaller than a predefined threshold, indicating that the algorithm has converged to a minimum.

**Applications:**

Gradient descent is widely used in various fields, including:

- **[[Machine Learning]]:** To minimize loss functions during model training.

    [Machine Learning Mastery](https://machinelearningmastery.com/gradient-descent-for-machine-learning/)

- **Economics:** For optimizing cost functions.
- **Physics:** In simulations to find equilibrium states.

**Considerations:**

- **Local vs. Global Minima:** Gradient descent may converge to a local minimum, which is not necessarily the global minimum, especially in functions with multiple minima.
- **Learning Rate Selection:** Choosing an appropriate learning rate is essential for efficient convergence.
- **Function Properties:** The algorithm performs best on convex functions, where any local minimum is also a global minimum.

For a more detailed exploration of gradient descent and its applications, you can refer to resources like the [Gradient Descent article on Khan Academy](https://www.khanacademy.org/math/multivariable-calculus/applications-of-multivariable-derivatives/optimizing-multivariable-functions/a/what-is-gradient-descent).