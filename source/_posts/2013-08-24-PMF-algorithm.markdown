---
layout: post
title: "source code of a PMF algorithm"
date: 2013-08-16 11:33
comments: true
categories: rs
---

Here is the code of basic PMF(probabilistic matrix factorization) source code. It is based on a article called <<Probabilistic Matrix Factorization>>. I will give some interpretations for that as well.

<!--more-->

PMF is one of the most popular approaches to collaborative filtering which is based on low-dimensional factor models. It uses a user feature vector(U) and a item feature vector(V)to compute the rating matrix(R), which is used for predicting unseen user propensities to items that they have not ranked before.

I will choose **batch learning of SVD with Momentum algorithm** to do this job.

Here I will a bref introduction to it.

Our goal is to minimize:

$$
E = \frac{1}{2}\sum_{i=1} ^n \sum_{j=1} ^m I_{ij}(V_{ij} - p(U_i,M_j))^2 + \frac{k_u}{2} \sum_{i=1} ^n \left \| U_i \right \|^2 + \frac{k_m}{2} \sum_{j=1} ^m \left \| M_j \right \|^2
$$

and our algorithm is here:

- Initialize matrices U, M
- Set the movement of matrices $\Delta U$ and $\Delta M$
- Repeat
- - Set $\Delta U \leftarrow \lambda\Delta U, \Delta M \leftarrow \lambda\Delta M.$
- - Compute gradients  $\nabla _{U}$ and $\nabla _{M}$.
- - Set $\Delta U \leftarrow \Delta U - \mu \nabla _{U}, \Delta M \leftarrow \Delta M - \mu \nabla _{M}$.
- - Set $U \leftarrow U + \Delta U, M \leftarrow M + \Delta M$

The source code is here:
- First we initialize the parameters we need in the algorithm: $\lambda, \epsilon$


