---
layout: blog
title:  "DeePC for WWTPs"
date:   2024-04-05 
categories: DeePC WWTPs
comments: true
---


> Notes on DeePC applied to Wasterwate treatment process
 
---



# WWTPs_DeePC Sample Code

Method: Date-enabled Predictive Control (DeePC)

Application case: waste-water treatment process

---


# I. Wastewater treatment process  

## 1. System parameters 

- Sampling period: $t_s = 15 \ min = 15/(60*24) \ day = 0.0104 \ day$   

- Control inputs: $u = [Q_a, K_L a_5]^T \in \mathbb{R}^{2}$

  > $0 \leq Q_a \leq 5*Q_{0, stab} = 5 * 18446 =518446$
  > 
  > $0 \leq K_L a_5 \leq 240$

- Controlled outputs: $y = [x_{sno}, x_{so}]^T \in \mathbb{R}^{2}$

  $x_{sno}$ is the $22^{th}$ variables of state $x$	

  $x_{so}$ is the $60^{th}$ variables of state $x$

  > $0 \leq x_{sno} \leq 3$
  > 
  > $0 \leq x_{so} \leq 4$

- State variables: $x \in \mathbb{R}^{145}$

## 2. Set-point 

- Set-point of controlled outputs $y^r$

  > $y^r = [x_{sno}^r, x_{so}^r]^T  =  [1, 2]^T$



---

# II. Robust DeePC for simulator

> run “main_rain_DeePC.m”
> 
> Apply the DeePC to the nonlinear system
> 
> Robust DeePC with slack variables and regularization on operator g


## 1. Control configuration

Entire control length: $t_{f} = 14 \ days$   (DeePC starts from the $T_{ini}$ steps)



---

# III. Robust DeePC for Koopman model

> run “main_rain_DeePC_v2.m”
> 
> Lift the control input u and output y to lifted state and then apply DeePC 
> 
> Robust DeePC with slack variables and regularization on operator g

## 1. Koopman lifting model 

> Lifted $u$: $\tilde{u} = [u(1), u(2), u(1)^2, u(2)^2, u(1)*u(2), u(1)^3, u(2)^3]^T$
>
> Lifted $y$: $\tilde{y} = [y(1), y(2), y(1)^2, y(2)^2, y(1)*y(2)]^T$


## 2. DeePC configuration

- $T_{ini} = 4 * 24 = 96 $
- $N = 30 $
- $T = 1625 $
- $n_{length} = T - T_{ini} - N + 1 = 1500 $

## 3. Control configuration

- Entire control length: $t_{f} = 14 \ days$   (DeePC starts from the $T_{ini}$ steps)

- Weighting matrices

  > $Q = \text{diag}([40, 40]) $
  > 
  > $R = \text{diag}([10^{-10}, 10^{-10}])$
  > 
  > $\lambda_g = 10 $
  > 
  > $\lambda_y = 5 \times 10^3 $



