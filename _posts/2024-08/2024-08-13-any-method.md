---
layout: post
title: "잡동사니 메서드들 모음"
date: 2024-08-13 +0900
categories: [python, pytorch]
tags: [python, pythorch]
published: true
author: jihwan
toc: true
---

## numpy

```python
import numpy as np

# 제곱근을 계산한다. 
# array_like_value => ndarray
no.sqrt([1,4,9])
# array[1,2,3]


```


## torch Tensor

```python
# 정규분포값을 주어진 shape로 반환한다. 
torch.randn([3,4])
```

```python
# 난수 정수를 주어진 shape로 반환한다. 
torch.randint(low=0, high=10, size=(10,))
```


