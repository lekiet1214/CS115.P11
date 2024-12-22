---
# You can also start simply with 'default'
theme: bricks
addons:
  - slidev-addon-python-runner
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: 
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
layout: cover
---

# Support Vector Machines

CS115 - Math for Computer Science

University of Information Technology - Vietnam National University

---
layout: center
background: https://cover.sli.dev
---

# Table of contents

<Toc columns="1" maxDepth="1"/>

---
transition: fade-out
layout: default
---

# Logistic Regression Review

In Logistic Regression, we have the loss function:

$$
\mathcal{L}(\mathbf{w}) = \sum_{i=1}^{n} -[y_i\log(\hat{y_i}) + (1-y_i)\log(1-\hat{y}_i)]
$$

The loss function is the relative entropy between the true distribution and the predicted distribution. In which, the $sigmoid$ function is used to predict the probability of the positive class:

$$
\hat{y} = \sigma(z) = \frac{1}{1+e^{-z}}
$$

We also know that the classficication boundary is a hyperplane:

$$
\mathbf{w}^T\mathbf{x} = 0
$$

$$
\begin{split}
\begin{split}
\hat{y} = \left\{
\begin{matrix}
1 \text{ if } \mathbf{w}^{\intercal}\mathbf{x} > 0 \\
0 \text{ if } \mathbf{w}^{\intercal}\mathbf{x} \leq 0
\end{matrix}
\right.\end{split}
\end{split}
$$



---
transition: slide-up
level: 2
---

# Logistic Regression Loss Function

![LR LOSS FUNCTION](./image.png)

We can see that the loss function shape in two cases are different. The loss function of Logistic Regression is convex, which means that it has only one global minimum. This is a good property for optimization.

---
title: From Logistic Regression to SVM
skip: true
layout: section
---

# From Logistic Regression to SVM

---
layout: default
image: https://cover.sli.dev
level: 2
title: The hinge loss function 
---

# The hinge loss function

In SVM, we modify the loss function of Logistic Regression to make it more robust to outliers. We do this by using a function that only penalizes the points that are far from the decision boundary.

$$
\begin{split}\begin{split}
\left\{
\begin{matrix}
\text{cost}_1(z) = \max(1+z, 0) ~ \text{if } y=0 \\
\text{cost}_2(z) = \max(0, 1-z) ~ \text{if } y=1
\end{matrix}
\right.\end{split}\end{split}
$$

The above functions are called the **hinge loss** functions. The hinge loss function is defined as:

$$
\mathcal{L}(\mathbf{w}) = \sum_{i=1}^{n} -[y_i\text{cost}_1(\hat{y_i}) + (1-y_i)\text{cost}_2(1-\hat{y}_i)]
$$

Which simplifies to:

$$
\mathcal{L}(\mathbf{w}) = \sum_{i=1}^{n} \max(0, 1-y_i\mathbf{w}^{\intercal}\mathbf{x}_i)
$$

---
layout: image-right
level: 2
image: ./image2.png
backgroundSize: contain
---

# Margin and Support Vectors

The margin is the distance between the decision boundary and the closest point of the training set. The support vectors are the points that lie on the margin.


---
title: Distance from the decision boundary
layout: default
level: 3
---

## Distance from the decision boundary

Let $\mathbf{w}^{\intercal}\mathbf{x} + b = 0$ be the equation of the decision boundary. The distance from a point $Z_i = (\mathbf{x}_i, \mathbf{y}_i)$ to the decision boundary is:

$$
d(Z_i, H) = \frac{|b+\mathbf{w}^{\intercal}\mathbf{x}_i|}{||\mathbf{w}||_2} = \frac{y_i(b+\mathbf{w}^{\intercal}\mathbf{x}_i)}{||\mathbf{w}||_2}
$$

$|b+\mathbf{w}^{\intercal}\mathbf{x}| = y_i(b+\mathbf{w}^{\intercal}\mathbf{x}_i)$ because:

- If $y_i = 1$, then $b+\mathbf{w}^{\intercal}\mathbf{x}_i \geq 0$ $\implies$ $y_i(b+\mathbf{w}^{\intercal}\mathbf{x}_i) \geq 0$

- If $y_i = -1$, then $b+\mathbf{w}^{\intercal}\mathbf{x}_i \leq 0$ $\implies$ $y_i(b+\mathbf{w}^{\intercal}\mathbf{x}_i) \geq 0$

In both cases, $|b+\mathbf{w}^{\intercal}\mathbf{x}| = y_i(b+\mathbf{w}^{\intercal}\mathbf{x}_i)$

---
title: Find the best decision boundary
layout: image-right
image: ./image2.png
backgroundSize: contain
level: 3
---

## Find the best decision boundary

The set of points that lie on the margin are the ***support vectors***. The best decision boundary is the one that maximizes the margin. This can be formulated as an optimization problem:

$$
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block">
  <mtable displaystyle="true">
    <mlabeledtr>
      <mtd id="mjx-eqn:1">
        <mtext>(1)</mtext>
      </mtd>
      <mtd>
        <mtable displaystyle="true" columnalign="right center left" columnspacing="0em 0.278em" rowspacing="3pt">
          <mtr>
            <mtd>
              <mrow data-mjx-texclass="ORD">
                <mover>
                  <mrow data-mjx-texclass="ORD">
                    <mi mathvariant="bold">w</mi>
                  </mrow>
                  <mo stretchy="false">^</mo>
                </mover>
              </mrow>
              <mo>,</mo>
              <mrow data-mjx-texclass="ORD">
                <mover>
                  <mi>b</mi>
                  <mo stretchy="false">^</mo>
                </mover>
              </mrow>
            </mtd>
            <mtd>
              <mi></mi>
              <mo>=</mo>
            </mtd>
            <mtd>
              <mi>arg</mi>
              <mo data-mjx-texclass="NONE">&#x2061;</mo>
              <mo data-mjx-texclass="OP" movablelimits="true">max</mo>
              <mo fence="false" stretchy="false">{</mo>
              <munder>
                <mo data-mjx-texclass="OP" movablelimits="true">min</mo>
                <mrow data-mjx-texclass="ORD">
                  <mo stretchy="false">(</mo>
                  <msub>
                    <mrow data-mjx-texclass="ORD">
                      <mi mathvariant="bold">x</mi>
                    </mrow>
                    <mi>i</mi>
                  </msub>
                  <mo>,</mo>
                  <msub>
                    <mi>y</mi>
                    <mi>i</mi>
                  </msub>
                  <mo stretchy="false">)</mo>
                  <mo>&#x2208;</mo>
                  <mrow data-mjx-texclass="ORD">
                    <mi data-mjx-variant="-tex-calligraphic" mathvariant="script">Z</mi>
                  </mrow>
                </mrow>
              </munder>
              <mfrac>
                <mrow>
                  <mi>b</mi>
                  <mo>+</mo>
                  <msub>
                    <mi>y</mi>
                    <mi>i</mi>
                  </msub>
                  <mo stretchy="false">(</mo>
                  <msup>
                    <mrow data-mjx-texclass="ORD">
                      <mi mathvariant="bold">w</mi>
                    </mrow>
                    <mrow data-mjx-texclass="ORD">
                      <mo>&#x22BA;</mo>
                    </mrow>
                  </msup>
                  <msub>
                    <mrow data-mjx-texclass="ORD">
                      <mi mathvariant="bold">x</mi>
                    </mrow>
                    <mi>i</mi>
                  </msub>
                  <mo stretchy="false">)</mo>
                </mrow>
                <mrow>
                  <mo stretchy="false">|</mo>
                  <mrow data-mjx-texclass="ORD">
                    <mo stretchy="false">|</mo>
                  </mrow>
                  <mrow data-mjx-texclass="ORD">
                    <mi mathvariant="bold">w</mi>
                  </mrow>
                  <mrow data-mjx-texclass="ORD">
                    <mo stretchy="false">|</mo>
                  </mrow>
                  <msub>
                    <mo stretchy="false">|</mo>
                    <mn>2</mn>
                  </msub>
                </mrow>
              </mfrac>
              <mo fence="false" stretchy="false">}</mo>
              <mtext>&#xA0;</mtext>
            </mtd>
          </mtr>
        </mtable>
      </mtd>
    </mlabeledtr>
  </mtable>
</math>
$$

---
title: Find the best decision boundary
hideInToc: true
---

Back to the equation of the decision boundary:

$$
\mathbf{w}^{\intercal}\mathbf{x} + b = 0
$$

If we scale $\mathbf{w}$ and $b$ by a factor $c$, the equation remains the same:

$$
(c\mathbf{w})^{\intercal}\mathbf{x} + cb = 0
$$

Which means that we can scale $\mathbf{w}$ and $b$ by any factor without changing the decision boundary. We can use this property to set the margin to 1:

$$
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block">
  <munder>
    <mo data-mjx-texclass="OP" movablelimits="true">min</mo>
    <mrow data-mjx-texclass="ORD">
      <mo stretchy="false">(</mo>
      <msub>
        <mrow data-mjx-texclass="ORD">
          <mi mathvariant="bold">x</mi>
        </mrow>
        <mi>i</mi>
      </msub>
      <mo>,</mo>
      <msub>
        <mi>y</mi>
        <mi>i</mi>
      </msub>
      <mo stretchy="false">)</mo>
      <mo>&#x2208;</mo>
      <mrow data-mjx-texclass="ORD">
        <mi data-mjx-variant="-tex-calligraphic" mathvariant="script">Z</mi>
      </mrow>
    </mrow>
  </munder>
  <mi>b</mi>
  <mo>+</mo>
  <msub>
    <mi>y</mi>
    <mi>i</mi>
  </msub>
  <mo stretchy="false">(</mo>
  <msup>
    <mrow data-mjx-texclass="ORD">
      <mi mathvariant="bold">w</mi>
    </mrow>
    <mrow data-mjx-texclass="ORD">
      <mo>&#x22BA;</mo>
    </mrow>
  </msup>
  <msub>
    <mrow data-mjx-texclass="ORD">
      <mi mathvariant="bold">x</mi>
    </mrow>
    <mi>i</mi>
  </msub>
  <mo stretchy="false">)</mo>
  <mo>=</mo>
  <mn>1</mn>
</math>
$$

Plugging this into the optimization problem $(1)$, we get:

$$
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block">
  <mtable displaystyle="true" columnalign="right" columnspacing="0em" rowspacing="3pt">
    <mtr>
      <mtd>
        <mtable displaystyle="true" columnalign="right center left" columnspacing="0em 0.278em" rowspacing="3pt">
          <mtr>
          <mtd id="mjx-eqn:2">
              <mtext>(2)</mtext>
            </mtd>
            <mtd>
            
              <mrow data-mjx-texclass="ORD">
                <mover>
                  <mrow data-mjx-texclass="ORD">
                    <mi mathvariant="bold">w</mi>
                  </mrow>
                  <mo stretchy="false">^</mo>
                </mover>
              </mrow>
              <mo>,</mo>
              <mrow data-mjx-texclass="ORD">
                <mover>
                  <mi>b</mi>
                  <mo stretchy="false">^</mo>
                </mover>
              </mrow>
            </mtd>
            <mtd>
              <mi></mi>
              <mo>=</mo>
            </mtd>
            <mtd>
              <mi>arg</mi>
              <mo data-mjx-texclass="NONE">&#x2061;</mo>
              <mo data-mjx-texclass="OP" movablelimits="true">max</mo>
              <mfrac>
                <mn>1</mn>
                <mrow>
                  <mo stretchy="false">|</mo>
                  <mrow data-mjx-texclass="ORD">
                    <mo stretchy="false">|</mo>
                  </mrow>
                  <mrow data-mjx-texclass="ORD">
                    <mi mathvariant="bold">w</mi>
                  </mrow>
                  <mrow data-mjx-texclass="ORD">
                    <mo stretchy="false">|</mo>
                  </mrow>
                  <msub>
                    <mo stretchy="false">|</mo>
                    <mn>2</mn>
                  </msub>
                </mrow>
              </mfrac>
            </mtd>
          </mtr>
        </mtable>
      </mtd>
    </mtr>
  </mtable>
</math>
$$

$$
subject : y_i(b+\mathbf{w}^{\intercal}\mathbf{x}_i) \geq 1, \forall i=\overline{1, N} 
$$

<!-- 
The subject is the constraint that the points lie on the margin or beyond.
 -->

---
title: Find the best decision boundary
hideInToc: true
layout: fact
---

Simplifying the optimization problem $(2)$, we get:

$$
\hat{\mathbf{w}}, \hat{b}  =  \arg \min ||\mathbf{w}||_2^2
$$

$$
\text{subject}  :  y_i(b+\mathbf{w}^{\intercal}\mathbf{x}_i) \geq 1, \forall i=\overline{1, N} \tag{3}
$$

The squared $L_2$ norm of $\mathbf{w}$ is used as the loss function. This is because the $L_2$ norm is differentiable, which makes it easier to optimize.

The optimization problem $(3)$ is a **quadratic programming** problem. This problem has a linear objective function and linear constraints, but the variables are squared. This makes it a **convex optimization** problem. We can solve this problem using the **Lagrange multipliers** method with the **KKT conditions**.

---
title: Optimal decision boundary
level: 1
layout: section
---

# Optimal decision boundary
## Optimize the loss function

---
title: The KKT conditions and the Lagrange multipliers method
level: 2
layout: two-cols-header
hideInToc: false
---

## The KKT conditions and the Lagrange multipliers method

The optimization problem $(2)$ can be solved using the **Lagrange multipliers** method with the **Karush-Kuhn-Tucker conditions** (KKT). The KKT conditions are:

::left::

1. **Stationarity**: The gradient of the Lagrangian with respect to the primal variables is zero:

$$
\nabla_{\mathbf{x}} f(\mathbf{x}) + \sum_{i=1}^{m}\lambda_i \nabla_{\mathbf{x}} h_i(\mathbf{x}) + \sum_{i=1}^{n} \nu_j \nabla_{\mathbf{x}} g_j(\mathbf{x}) = 0
$$

2. **Primal feasibility**: The primal variables satisfy the constraints:

$$
h_i(\mathbf{x}) = 0, g_j(\mathbf{x}) \leq 0, ~~\forall i, j
$$

::right::

3. **Dual feasibility**: The dual variables are non-negative:

$$
\nu_i \geq 0, ~~ \forall i
$$

4. **Complementary slackness**: The complementary slackness condition:

$$
\nu_j g_j(\mathbf{x}) = 0, ~~ \forall j
$$

---
title: The KKT conditions and the Lagrange multipliers method
hideInToc: true
---

## The KKT conditions and the Lagrange multipliers method

We have the Lagrangian Dual function:

$$
\mathcal{L}(\mathbf{x}, \lambda, \nu) = f(\mathbf{x}) + \sum_{i=1}^{m}\lambda_i h_i(\mathbf{x}) + \sum_{j=1}^{n}\nu_j g_j(\mathbf{x})
$$

Which we can use to derive the KKT conditions:

$
Stationary: \nabla_{\mathbf{x}} f(\mathbf{x}) + \sum_{i=1}^{m}\lambda_i \nabla_{\mathbf{x}} h_i(\mathbf{x}) + \sum_{i=1}^{n} \nu_j \nabla_{\mathbf{x}} g_j(\mathbf{x}) = 0
\\
Complenatery slackness: \nu_j g_j(\mathbf{x}) = 0, ~~ \forall j
\\
Primal feasibility: h_i(\mathbf{x}) = 0, g_j(\mathbf{x}) \leq 0, ~~\forall i, j
\\
Dual feasibility: \nu_i \geq 0, ~~ \forall i
$


---
layout: two-cols-header
title: The SVM optimization problem
level: 2
---

## The SVM optimization problem

The optimization problem $(3)$ can be formulated as follow:

$$
g(\lambda) = \min_{\mathbf{w}, b, \lambda} \mathcal{L}(\mathbf{w}, b, \lambda) = \frac{1}{2} ||\mathbf{w}||_2^2 + \sum_{i=1}^N \lambda_i(1 - y_i(\mathbf{w}^{\intercal}\mathbf{x}_i + b) ) \tag{4}
$$

The optimal solution of the Lagrangian Dual function $(4)$ can be solved using the first derivative of the Lagrangian Dual function with respect to $\mathbf{w}$, $b$ and $\lambda$:

$$
\frac{\partial \mathcal{L}(\mathbf{w}, b, \lambda)}{\partial \mathbf{w}} = \mathbf{w} - \sum_{i=1}^N \lambda_i y_i \mathbf{x}_i = 0 \Rightarrow \mathbf{w} = \sum_{i=1}^N \lambda_i y_i \mathbf{x}_i  \tag{6}
$$

$$
\frac{\partial \mathcal{L}(\mathbf{w}, b, \lambda)}{\partial b} = -\sum_{i=1}^N \lambda_iy_i = 0 \tag{7}
$$

$$
\frac{\partial \mathcal{L}(\mathbf{w}, b, \lambda)}{\partial \lambda}  =  \sum_{i=1}^N  1-y_i(\mathbf{w}^{\intercal}\mathbf{x}_i + b) = 0 \tag{8}
$$


---
title: The SVM optimization problem
hideInToc: true
---

## The SVM optimization problem

We get the optimal solution of the SVM optimization problem by solving the equations $(6)$, $(7)$ and $(8)$:

$
g(\lambda)  =  \frac{1}{2} ||\mathbf{w}||_2^2 + \sum_{i=1}^N\lambda_i - \mathbf{w}^{\intercal} \underbrace{\sum_{i=1}^{N} \lambda_iy_i \mathbf{x}_i}_{\mathbf{w}} - b \underbrace{\sum_{i=1}^N \lambda_i y_i}_{0}
\\
 =  \sum_{i=1}^N\lambda_i - \frac{1}{2} ||\mathbf{w}||_2^2 \\
 =  \sum_{i=1}^N\lambda_i - \frac{1}{2} \sum_{i=1}^N \lambda_i y_i \mathbf{x}_i^{\intercal} \sum_{i=1}^N \lambda_i y_i \mathbf{x}_i
$
$$
 =  \sum_{i=1}^N \lambda_i - \frac{1}{2} \sum_{i=1}^N \sum_{j=1}^N \lambda_i \lambda_j y_i y_j \mathbf{x}_i^{\intercal} \mathbf{x}_j
$$

---
title: The SVM optimization problem
hideInToc: true
---

## The SVM optimization problem

The minimum of the function $g(\lambda)$ is obtained when:

$$
\sum_{i=1}^N \lambda_i(1 - y_i(\mathbf{w}^{\intercal}\mathbf{x}_i + b) ) = 0
$$

At the optimal solution, the points that lie on the margin or beyond satisfy:

$$
\lambda_i = 0 \text{ or } 1-y_i(\mathbf{w}^{\intercal}\mathbf{x}_i + b) = 0, ~ \forall i=\overline{1,N}
$$

In practice, the points that lie on the margin are the support vectors. The optimal solution of the SVM optimization problem is the set of support vectors ${S}$.

---
title: The SVM optimization problem
hideInToc: true
---

## The SVM optimization problem

Function $(6)$ can be rewritten as:

$$
\mathbf{w} = \sum_{i=1}^{N} \lambda_iy_i\mathbf{x}_i = \sum_{i=1, \lambda_i \neq 0}^{N} \lambda_iy_i\mathbf{x}_i = \sum_{(\mathbf{x}_i, y_i) \in \mathcal{S}} \lambda_i y_i\mathbf{x}_i
$$

The decision boundary is the set of points that satisfy:

$$
1-y_i(\mathbf{w}^{\intercal}\mathbf{x}+b) = 0 \leftrightarrow y_i(y_i-\mathbf{w}^{\intercal}\mathbf{x}_i-b) = 0 \leftrightarrow y_i - \mathbf{w}^{\intercal}\mathbf{x}_i-b=0
$$

Let us have w, we can find b by:

$$
b = \frac{1}{|\mathcal{S}|}\sum_{(\mathbf{x}_i, y_i) \in \mathcal{S}}(y_i-\mathbf{w}^{\intercal}\mathbf{x}_i)
$$

---
title: SVM Classification
level: 1
layout: section
---

# SVM Classification

---
title: SVM Classification
hideInToc: true
---

## SVM Classification

The class of a new point $\mathbf{x}$ is determined by the sign of the decision function:

$
h_{\mathbf{w}, b}(\mathbf{x}_i)  =  b + \mathbf{w}^{\intercal}\mathbf{x}_i \\
=  b + (~ \sum_{(\mathbf{x}_j, y_j) \in \mathcal{S}}\lambda_jy_j \mathbf{x}_j^{\intercal} ~)\mathbf{x}_i \\
=  b + \sum_{(\mathbf{x}_j, y_j) \in \mathcal{S}} \lambda_j y_j \mathbf{x}_{j}^{\intercal} \mathbf{x}_i \\
$

The class of $\mathbf{x}$ is:

$
\hat{y} = \left\{
\begin{matrix}
1 \text{ if } h_{\mathbf{w}, b}(\mathbf{x}) > 0 \\
0 \text{ if } h_{\mathbf{w}, b}(\mathbf{x}) \leq 0
\end{matrix}
\right.
$

We can see that the decision function is a linear combination of the support vectors. This is why SVM is called a **sparse model**. Which mean that the decision function depends only on a few points of the training set.

---
title: Soft Margin SVM
level: 1
layout: section
---

# Soft Margin SVM

---
title: Soft Margin SVM
hideInToc: true
layout: image-right
image: ./image3.png
backgroundSize: 100%
---

## Soft Margin SVM

While the hard margin SVM tries to find the decision boundary that separates the classes perfectly, the soft margin SVM allows some points to lie on the wrong side of the decision boundary. This is done by introducing a slack variable $\xi_i$ for each point:

$$
d(Z_i, H) \triangleq \xi_i = |b+\mathbf{w}^{\intercal}\mathbf{x}_i-y_i|
$$

The optimization problem of the soft margin SVM is:

$$
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block">
  <mtable displaystyle="true" columnalign="right" columnspacing="0em" rowspacing="3pt">
    <mtr>
      <mtd>
        <mtable displaystyle="true" columnalign="right center left" columnspacing="0em 0.278em" rowspacing="3pt">
          <mtr>
            <mtd>
              <mrow data-mjx-texclass="ORD">
                <mover>
                  <mrow data-mjx-texclass="ORD">
                    <mi mathvariant="bold">w</mi>
                  </mrow>
                  <mo stretchy="false">^</mo>
                </mover>
              </mrow>
              <mo>,</mo>
              <mrow data-mjx-texclass="ORD">
                <mover>
                  <mi>b</mi>
                  <mo stretchy="false">^</mo>
                </mover>
              </mrow>
            </mtd>
            <mtd>
              <mi></mi>
              <mo>=</mo>
            </mtd>
            <mtd>
              <mi>arg</mi>
              <mo data-mjx-texclass="NONE">&#x2061;</mo>
              <mo data-mjx-texclass="OP" movablelimits="true">min</mo>
              <mtext>&#xA0;</mtext>
              <mo stretchy="false">[</mo>
              <mtext>&#xA0;</mtext>
              <mrow data-mjx-texclass="ORD">
                <mo stretchy="false">|</mo>
              </mrow>
              <mrow data-mjx-texclass="ORD">
                <mo stretchy="false">|</mo>
              </mrow>
              <mrow data-mjx-texclass="ORD">
                <mi mathvariant="bold">w</mi>
              </mrow>
              <mrow data-mjx-texclass="ORD">
                <mo stretchy="false">|</mo>
              </mrow>
              <msubsup>
                <mrow data-mjx-texclass="ORD">
                  <mo stretchy="false">|</mo>
                </mrow>
                <mn>2</mn>
                <mn>2</mn>
              </msubsup>
              <mo>+</mo>
              <mi>C</mi>
              <munderover>
                <mo data-mjx-texclass="OP">&#x2211;</mo>
                <mrow data-mjx-texclass="ORD">
                  <mi>i</mi>
                  <mo>=</mo>
                  <mn>1</mn>
                </mrow>
                <mrow data-mjx-texclass="ORD">
                  <mi>N</mi>
                </mrow>
              </munderover>
              <mrow data-mjx-texclass="ORD">
                <mo stretchy="false">|</mo>
              </mrow>
              <mi>b</mi>
              <mo>+</mo>
              <msup>
                <mrow data-mjx-texclass="ORD">
                  <mi mathvariant="bold">w</mi>
                </mrow>
                <mrow data-mjx-texclass="ORD">
                  <mo>&#x22BA;</mo>
                </mrow>
              </msup>
              <msub>
                <mrow data-mjx-texclass="ORD">
                  <mi mathvariant="bold">x</mi>
                </mrow>
                <mi>i</mi>
              </msub>
              <mo>&#x2212;</mo>
              <msub>
                <mi>y</mi>
                <mi>i</mi>
              </msub>
              <mrow data-mjx-texclass="ORD">
                <mo stretchy="false">|</mo>
              </mrow>
              <mtext>&#xA0;</mtext>
              <mo stretchy="false">]</mo>
            </mtd>
          </mtr>
          <mtr>
            <mtd></mtd>
            <mtd>
              <mi></mi>
              <mo>=</mo>
            </mtd>
            <mtd>
              <mi>arg</mi>
              <mo data-mjx-texclass="NONE">&#x2061;</mo>
              <mo data-mjx-texclass="OP" movablelimits="true">min</mo>
              <mtext>&#xA0;</mtext>
              <mo stretchy="false">[</mo>
              <mtext>&#xA0;</mtext>
              <mrow data-mjx-texclass="ORD">
                <mo stretchy="false">|</mo>
              </mrow>
              <mrow data-mjx-texclass="ORD">
                <mo stretchy="false">|</mo>
              </mrow>
              <mrow data-mjx-texclass="ORD">
                <mi mathvariant="bold">w</mi>
              </mrow>
              <mrow data-mjx-texclass="ORD">
                <mo stretchy="false">|</mo>
              </mrow>
              <msubsup>
                <mrow data-mjx-texclass="ORD">
                  <mo stretchy="false">|</mo>
                </mrow>
                <mn>2</mn>
                <mn>2</mn>
              </msubsup>
              <mo>+</mo>
              <mi>C</mi>
              <munderover>
                <mo data-mjx-texclass="OP">&#x2211;</mo>
                <mrow data-mjx-texclass="ORD">
                  <mi>i</mi>
                  <mo>=</mo>
                  <mn>1</mn>
                </mrow>
                <mrow data-mjx-texclass="ORD">
                  <mi>N</mi>
                </mrow>
              </munderover>
              <msub>
                <mi>&#x3BE;</mi>
                <mi>i</mi>
              </msub>
              <mtext>&#xA0;</mtext>
              <mo stretchy="false">]</mo>
            </mtd>
          </mtr>
        </mtable>
      </mtd>
    </mtr>
  </mtable>
</math>
$$
$$
\text{subject}  :  y_i(b+\mathbf{w}^{\intercal}\mathbf{x}_i) + \xi_i - 1 \geq 0, \xi_i \geq 0 ~ \forall i=\overline{1, N}
$$

<!-- Ràng buộc có ý nghĩa rằng chúng ta chỉ cho phép các điểm bị lấn sang vùng không an toàn một ngưỡng tối đa soft_margin. Ngoài ra trong bài toán tối ưu cần có thêm điều kiện ràng buộc soft >= 0
. -->

---
title: Soft Margin SVM
hideInToc: true
---

## Soft Margin SVM

The optimization problem of the soft margin SVM is:

$$
\mathcal{L}(\mathbf{w}, b, \xi, \lambda, \nu) = \frac{1}{2}{||\mathbf{w}||_2^2} + C \sum_{i=1}^N \xi_i + \sum_{i=1}^N \lambda_i ( 1 - \xi_i - y_i(\mathbf{w}^{\intercal}\mathbf{x}_i + b)) - \sum_{i=1}^N \nu_i \xi_i
$$

sastify $\lambda_i, \nu_i > 0, ~~ \forall i=\overline{1,N}$

THe solution of the optimization problem become:

$$
\frac{\partial \mathcal{L}(\mathbf{w}, b, \xi, \lambda, \nu)}{\partial \mathbf{w}} = \mathbf{w} - \sum_{i=1}^N \lambda_i y_i \mathbf{x}_i = 0 \Rightarrow \mathbf{w} = \sum_{i=1}^N \lambda_i y_i \mathbf{x}_i \tag{10}
$$

$$
\\ 
\frac{\partial \mathcal{L}(\mathbf{w}, b, \xi, \lambda, \nu)}{\partial b} = 
-\sum_{i=1}^N \lambda_iy_i = 0 \tag{11}
$$

$$
\frac{\partial \mathcal{L}(\mathbf{w}, b, \xi, \lambda, \nu)}{\partial \xi_i} = C - \lambda_i-\nu_i = 0 \tag{12}
$$

---
title: Soft Margin SVM
hideInToc: true
---

## Soft Margin SVM

From $(12)$, we have:

$$
\nu_i = C-\lambda_i \geq 0
$$

which mean that $\lambda_i \leq C$ and $\nu_i \geq 0$ for all $i=\overline{1,N}$

Plugging $(10)$, $(11)$ and $(12)$ into the Lagrangian Dual function, we get:

$$
g(\lambda, \nu) = \sum_{i=1}^N \lambda_i - \frac{1}{2} \sum_{i=1}^N \sum_{j=1}^N \lambda_i \lambda_j y_i y_j \mathbf{x}_i^{\intercal} \mathbf{x}_j
$$

Now, the optimization problem is to maximize $g(\lambda, \nu)$ subject to the constraints $\lambda_i \leq C$ and $\nu_i \geq 0$ for all $i=\overline{1,N}$

This problem is similar to the hard margin SVM optimization problem, but with an additional constraint that $\lambda_i \leq C$. At extreme values of $C$, the soft margin SVM behaves like the hard margin SVM.

---
title: Soft Margin SVM
hideInToc: true
---

## Soft Margin SVM

We perform the same steps as the hard margin SVM to find the optimal solution of the soft margin SVM:

$$
\mathbf{w} = \sum_{i \in S} \lambda_i y_i \mathbf{x}_i
$$

$$
\mathbf{w} = \sum_{i \in \mathcal{S}} \lambda_m y_i \mathbf{x}_i  \newline
b = \frac{1}{N_{\mathcal{M}}} \sum_{n \in \mathcal{M}} (y_n - \mathbf{w}^T\mathbf{x}_n) = \frac{1}{N_{\mathcal{M}}} \sum_{n \in \mathcal{M}} \left(y_n - \sum_{i \in \mathcal{S}} \lambda_i y_i \mathbf{x}_i^T\mathbf{x}_n\right)
$$

with $\mathcal{M} = \{n: 0 < \lambda_n < C \}$ and $\mathcal{S} = \{i: 0 < \lambda_i \leq C\}$


---
title: SVM Classification with Soft Margin
hideInToc: true
---

## SVM Classification with Soft Margin

The class of a new point $\mathbf{x}$ is determined by the sign of the decision function:

$$
h_{\mathbf{w}, b}(\mathbf{x}_i) = b + \mathbf{w}^{\intercal}\mathbf{x}_i
$$

$$
h_{\mathbf{w}, b}(\mathbf{x}_i) = b + \sum_{i=1}^{N} \alpha_i y_i \mathbf{x}_i^\top \mathbf{x}
$$

We can see the introduction of the slack variable $\xi_i$ in the optimization problem allows the soft margin SVM to handle noisy data and outliers.

However, the choice of the hyperparameter $C$ is crucial. A small value of $C$ allows more points to lie on the wrong side of the decision boundary, while a large value of $C$ forces more points to lie on the correct side of the decision boundary.

---
title: Kernel Trick in SVM
level: 1
layout: section
---

# Kernel Trick in SVM

---
title: Kernel in SVM
layout: fact
hideInToc: true
---

## Kernel in SVM

The main idea of the kernel trick is to map the input data into a higher-dimensional space where the classes are linearly separable. This is done by defining a kernel function $K(\mathbf{x}_i, \mathbf{x}_j)$ that computes the inner product of the mapped data points in the higher-dimensional space.

---
layout: image
image: /image5.png
backgroundSize: contain
---
---
layout: image
image: /image6.png
backgroundSize: contain
---
---
layout: image
image: /image4.png
backgroundSize: contain
---

---
title: Properties of the Kernel Function
level: 2
---

## Properties of the Kernel Function

 The kernel function $K(\mathbf{x}_i, \mathbf{x}_j)$ must satisfy the following properties:

1. **Symmetry**: $K(\mathbf{x}_i, \mathbf{x}_j) = K(\mathbf{x}_j, \mathbf{x}_i)$
2. **Positive definiteness**: For any set of points $\mathbf{x}_1, \mathbf{x}_2, ..., \mathbf{x}_n$, the matrix $K$ defined by $K_{ij} = K(\mathbf{x}_i, \mathbf{x}_j)$ is positive definite.


3. **Mercer's theorem**: If $K(\mathbf{x}_i, \mathbf{x}_j)$ is a continuous function, then it can be expressed as an inner product in a higher-dimensional space.

---
title: Kernel Functions
level: 2
---

## Kernel Functions

There are several types of kernel functions that are commonly used in SVM:

1. **Linear kernel**: $K(\mathbf{x}_i, \mathbf{x}_j) = \mathbf{x}_i^{\intercal}\mathbf{x}_j$

2. **Polynomial kernel**: $K(\mathbf{x}_i, \mathbf{x}_j) = (\mathbf{x}_i^{\intercal}\mathbf{x}_j + c)^d$

3. **Gaussian (RBF) kernel**: $K(\mathbf{x}_i, \mathbf{x}_j) = \exp\left(-\frac{||\mathbf{x}_i - \mathbf{x}_j||^2}{2\sigma^2}\right)$

4. **Sigmoid kernel**: $K(\mathbf{x}_i, \mathbf{x}_j) = \tanh(\alpha \mathbf{x}_i^{\intercal}\mathbf{x}_j + c)$

5. **Laplacian kernel**: $K(\mathbf{x}_i, \mathbf{x}_j) = \exp\left(-\frac{||\mathbf{x}_i - \mathbf{x}_j||}{\sigma}\right)$

---
title: Experiment
level: 1
layout: section
---

# Experiment
## Handwriting Recognition with SVM

---
title: Experiment setup
level: 2
---

# Experiment setup

## Dataset
EMNIST Dataset (Extended MNIST) contains 814,255 characters from 62 classes. Each character is represented as a 28x28 pixel image. This experiment uses a subset of the EMNIST dataset containing 62 classes.

## Preprocessing
The EMNIST ByClass dataset is extremely unbalanced, with some classes having very few samples. To balance the dataset, we merge uppercase and lowercase characters then perform undersampling to ensure that each class has an equal number of samples. Then augment data by rotating, scaling, and shifting the images.

Final dataset has 47 classes, 10 digits and 37 letters.

We then perform standard preprocessing steps such as normalization and splitting the dataset into training and testing sets.

---
title: Experiment setup
hideInToc: true
layout: default
---

# Experiment setup
## Model
This experiment ultilizes three models: CNN, SVM with linear kernel, and KNN for comparison.

### CNN

- A Convolutional Neural Network (CNN) with 3 convolutional layers and 2 fully connected layers.
- The CNN is trained using the Adam optimizer with a learning rate of 0.001.
- The CNN is trained for 10 epochs with a batch size of 64.

### SVM

We use GridSearchCV to find the best hyperparameters for the SVM model. The hyperparameters are:
- C: The regularization parameter.
- kernel: The kernel function used in the SVM model.

### KNN

- A K-Nearest Neighbors (KNN) model with k=7.
- The KNN model uses the Euclidean distance metric.

---
title: Experiment setup
hideInToc: true
layout: default
---

# Experiment setup
## Evaluation
We evaluate the models using the following metrics:
- Accuracy: The percentage of correctly classified samples.
- Precision: The ratio of correctly predicted positive observations to the total predicted positive observations.
- Recall: The ratio of correctly predicted positive observations to all observations in the actual class.
- F1 Score: The weighted average of Precision and Recall.

## Results
We compare the performance of the CNN, SVM, and KNN models on the EMNIST dataset through Accuracy, Recall, and Precision.

---
title: Results
hideInToc: true
layout: image
image: ./all_c.png
backgroundSize: contain
---



---
title: Results
level: 2
hideInToc: true
layout: none
# image: ./svm_c_r.png
# backgroundSize: contain
---

<style>
  .images {
    display: flex;
    justify-content: space-between;
  }
  .images img {
    max-width: 28%; /* Adjust size of images */
  }
</style>

<div class="images">
  <img src="./svm_c_r.png" alt="Image 1">
  <img src="./knn_c_r.png" alt="Image 2">
  <img src="./cnn_c_r.png" alt="Image 3">
</div>

---
title: end
level: 1
layout: end
---

# The End
## Thanks for your attention!


<div class="abs-br m-6 text-xl">
  <a href="https://github.com/lekiet1214/cs115.p11" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>