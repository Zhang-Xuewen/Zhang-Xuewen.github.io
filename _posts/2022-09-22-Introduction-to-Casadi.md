---
layout: post
title:  "Introduction to CasADi"
date:   2022-09-22 
categories: Learning-notes CasADi
---


> Notes on CasADi, especially the usage of variables in CasADi

CSDN notes link: [1][1] [2][2]

# Variables
## SX 
SX data type represent matrix: create a matrix $x \in R^{2 \times 2}$
```
x = SX.sym('x', 2, 2)  #  create a matrix $\in R^{2 \times 2}$

print(x)
output: [[x_0, x_2],
	 [x_1, x_3]]

y = x**2
print(y)
output: x^2
```

## MX
Suitable for NLP model
```
evalf(DM)    # MX to DM
```
## DM
DM mainly used to save matrix and used as function input and output
```
DM.full()    # show the DM value
```
> **DM return values, SX,MX return equation that contains variables** \
> **SX have all the elements of the matrix, MX only define the matrix itself**


[1]: https://blog.csdn.net/qq_16775293/article/details/117422579?ops_request_misc=&request_id=ae5cbd820ce4495d96d15f99738b7544&biz_id=&utm_medium=distribute.pc_search_result.none-task-blog-2~all~koosearch~default-2-117422579-null-null.142^v90^insert_down28v1,239^v3^control&utm_term=casadi&spm=1018.2226.3001.4187
[2]: https://blog.csdn.net/weixin_43879302/article/details/107370402?ops_request_misc=&request_id=&biz_id=102&utm_term=casadi&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-107370402.nonecase&spm=1018.2226.3001.4187
